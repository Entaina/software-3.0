# /feature-create

*Creates a new feature workspace with proper structure and tracking.*

## Auto-Loaded Project Context:
@/CLAUDE.md
@/docs/ai-context/project-structure.md
@.claude/commands/feature/_state-management.md

## Command Overview

You are tasked with creating a new feature workspace for product development. This command initializes the feature structure, updates tracking files, and prepares the workspace for the development workflow.

User provided input: "$ARGUMENTS"

## Step 1: Parse and Validate Input

### Extract Feature Information
Parse the user arguments to determine:
- **Feature name**: Extract or generate a kebab-case name (e.g., "user-notifications")
- **Description**: Brief description of the feature purpose
- **Initial context**: Any additional details provided

### Validation Rules
- Feature name must be kebab-case (lowercase, hyphen-separated)
- Feature name must be unique (not already exist in active/archived/trashed)
- Description should be concise (under 100 characters)

### Error Handling
If input is invalid:
- Missing name: Request feature name in kebab-case format
- Invalid format: Convert to kebab-case and confirm with user
- Duplicate name: Inform user and suggest alternatives

## Step 2: Load and Update Feature State

### Read Current State
1. Load `.feature-state.json` from `docs/product-development/`
2. Check for existing features with same name
3. Determine next available feature slot

### State Structure (Use Enhanced Schema from State Management Protocol)
```json
{
  "version": "1.0",
  "current_feature": "current-feature-name",
  "last_updated": "2025-10-14T10:30:00Z",
  "features": {
    "feature-name": {
      "name": "feature-name",
      "description": "Feature description",
      "status": "active|archived|trashed",
      "created_at": "YYYY-MM-DD",
      "updated_at": "YYYY-MM-DD",
      "archived_at": null,
      "trashed_at": null,

      "workflow": {
        "current_stage": "definition",
        "stages_completed": ["definition"],
        "next_recommended_command": "/feature-switch feature-name"
      },

      "documents": {
        "feature_md": {"exists": true, "last_modified": "YYYY-MM-DD"},
        "jtbd_md": {"exists": false, "last_modified": null},
        "prd_md": {"exists": false, "last_modified": null},
        "plan_md": {"exists": false, "last_modified": null},
        "plan_organized_md": {"exists": false, "last_modified": null}
      },

      "implementation": {
        "total_tasks": 0,
        "completed_tasks": 0,
        "in_progress_task": null,
        "last_implementation": null
      }
    }
  }
}
```

## Step 3: Create Feature Directory Structure

### Directory Creation
Create the feature directory in `docs/product-development/features/active/[feature-name]/`:

```
features/active/[feature-name]/
├── feature.md          # Feature overview and request
├── JTBD.md            # Jobs to be Done (created by create-jtbd)
├── PRD.md             # Product Requirements (created by create-prd)
├── plan.md            # Technical plan (created by create-plan)
└── plan-organized.md  # Organized plan (created by organize-plan)
```

### Initial feature.md Content
```markdown
# [Feature Name] - Feature Overview

## Description
[Feature description from user input]

## Original Request
[User's original feature request from $ARGUMENTS]

## Creation Date
[Current date in YYYY-MM-DD format]

## Status Tracking
- [ ] JTBD Analysis (use `/create-jtbd`)
- [ ] PRD Creation (use `/create-prd`)
- [ ] Technical Planning (use `/create-plan`)
- [ ] Plan Organization (use `/organize-plan`)
- [ ] Implementation (use `/implement-code`)

## Notes
[Any additional context or considerations]

## Related Features
[List any related or dependent features]
```

## Step 4: Update Tracking Files

### Update .feature-state.json
1. Add new feature entry with initial progress state
2. Keep current_feature unchanged (user must explicitly switch)
3. Set all progress indicators to false

### Update Log
Consider creating a feature creation log entry:
```json
{
  "action": "created",
  "feature": "feature-name",
  "timestamp": "ISO-8601 timestamp",
  "user_context": "original request"
}
```

## Step 5: Provide User Guidance

### Success Output
Inform the user about:
1. Feature created successfully at: `features/active/[feature-name]/`
2. Current feature remains: `[current-feature-name]`
3. To switch to new feature: `/feature-switch [feature-name]`
4. Next steps in workflow:
   - `/feature-switch [feature-name]` - Make it current
   - `/create-jtbd` - Start JTBD analysis
   - `/feature-list` - See all features

### Feature Workflow Reminder
```
Standard Feature Development Flow:
1. /feature-create [name] [description]  ← You are here
2. /feature-switch [name]
3. /create-jtbd [context]
4. /create-prd [context]
5. /create-plan [context]
6. /organize-plan
7. /implement-code
8. /feature-archive [name]
```

## Step 6: Integration Considerations

### Backward Compatibility
- Don't modify `current-feature` file unless explicitly switching
- Existing commands will continue to work with current feature
- Feature creation doesn't disrupt ongoing work

### Multi-Feature Support
- Users can create multiple features before switching
- Each feature maintains independent progress tracking
- Features can be worked on in parallel by different sessions

## Error Recovery

### Rollback on Failure
If any step fails:
1. Remove created directories
2. Revert .feature-state.json changes
3. Provide clear error message
4. Suggest corrective actions

### Common Issues
- **Disk space**: Check before creating directories
- **Permissions**: Ensure write access to directories
- **State corruption**: Validate JSON before writing

## Quality Checklist
- [ ] Feature name is valid kebab-case
- [ ] Feature doesn't already exist
- [ ] Directory structure created correctly
- [ ] feature.md contains all required sections
- [ ] .feature-state.json updated accurately
- [ ] User received clear next steps
- [ ] Current feature unchanged

Now proceed to create the new feature based on: $ARGUMENTS