# /feature-switch

*Switches the current active feature context for development workflow.*

## Auto-Loaded Project Context:
@/docs/product-development/.feature-state.json
@/docs/product-development/current-feature

## Command Overview

You are tasked with switching the current feature context, which updates tracking files so that subsequent development commands (create-jtbd, create-prd, etc.) operate on the selected feature.

User provided input: "$ARGUMENTS"

## Step 1: Parse and Validate Input

### Extract Feature Name
- Parse user arguments for feature name
- Feature name should be in kebab-case format
- Handle various input formats gracefully

### Input Validation
- If no feature name provided: Show current feature and prompt for selection
- If invalid format: Suggest correct format
- If multiple arguments: Use first as feature name

## Step 2: Verify Feature Exists

### Load Current State
1. Read `.feature-state.json` from `docs/product-development/`
2. Read current feature from `current-feature` file
3. Get list of all features and their status

### Feature Verification
Check if requested feature:
1. Exists in the state file
2. Has status "active" (not archived or trashed)
3. Has corresponding directory in `features/active/`

### Error Cases
- **Feature not found**: List available features and suggest alternatives
- **Feature archived**: Ask if user wants to restore it first
- **Feature trashed**: Inform user to restore before switching

## Step 3: Update Current Feature

### State Updates
1. Update `current_feature` field in `.feature-state.json`
2. Update `updated_at` timestamp for the feature
3. Write feature name to `current-feature` file

### File Operations
```python
# Pseudo-code for clarity
state = load_json('.feature-state.json')
old_feature = read_file('current-feature').strip()
state['current_feature'] = new_feature_name
state['features'][new_feature_name]['updated_at'] = current_date
save_json('.feature-state.json', state)
write_file('current-feature', new_feature_name)
```

## Step 4: Verify Switch Success

### Validation Checks
1. Confirm `.feature-state.json` updated correctly
2. Confirm `current-feature` file contains new feature name
3. Verify feature directory exists and is accessible

### Directory Structure Check
Ensure the feature directory contains expected structure:
```
features/active/[feature-name]/
├── feature.md     # Should exist
├── JTBD.md       # May or may not exist
├── PRD.md        # May or may not exist
├── plan.md       # May or may not exist
└── plan-organized.md  # May or may not exist
```

## Step 5: Provide Context and Status

### Feature Summary
Display information about the newly selected feature:

```
Switched to Feature: [feature-name]
=================================

Description: [Feature description from state file]
Created: [Creation date]
Last Updated: [Update date]

Progress Status:
✓ Feature Definition (feature.md)
[✓/✗] JTBD Analysis (JTBD.md)
[✓/✗] Product Requirements (PRD.md)
[✓/✗] Technical Plan (plan.md)
[✓/✗] Organized Plan (plan-organized.md)

Overall Progress: [X]% complete

Previous Feature: [old-feature-name]
```

### Next Steps Guidance
Based on feature progress, suggest next actions:

**If JTBD missing:**
```
Next Step: Run `/create-jtbd` to analyze user needs for this feature.
```

**If JTBD done but PRD missing:**
```
Next Step: Run `/create-prd` to create product requirements based on JTBD analysis.
```

**If PRD done but plan missing:**
```
Next Step: Run `/create-plan` to create technical implementation plan.
```

**If plan done but not organized:**
```
Next Step: Run `/organize-plan` to structure the implementation plan.
```

**If all documents complete:**
```
Ready for Implementation: Use `/implement-code` to begin coding.
```

## Step 6: Handle Special Cases

### Switching to Same Feature
If user tries to switch to current feature:
- Inform that feature is already current
- Show feature status anyway
- Don't update timestamps

### Quick Switch Syntax
Support convenient shortcuts:
- `/feature-switch -` : Switch to previous feature
- `/feature-switch .` : Show current feature status
- `/feature-switch ?` : List all active features

### Feature History
Optionally maintain a history of feature switches:
```json
{
  "switch_history": [
    {
      "from": "old-feature",
      "to": "new-feature",
      "timestamp": "ISO-8601"
    }
  ]
}
```

## Step 7: Error Recovery

### State File Issues
If state file is corrupted or missing:
1. Attempt to rebuild from directory structure
2. Preserve current-feature file content
3. Warn user about reconstruction

### Permission Issues
If can't write to files:
1. Report which files failed
2. Show what would have been changed
3. Suggest permission fixes

### Rollback on Failure
If switch fails partway:
1. Revert any partial changes
2. Ensure consistent state
3. Report failure clearly

## Integration Considerations

### Workflow Commands
After successful switch, these commands will operate on new feature:
- `/create-jtbd` - Creates in new feature directory
- `/create-prd` - Reads JTBD from new feature
- `/create-plan` - Uses PRD from new feature
- `/organize-plan` - Organizes plan in new feature
- `/implement-code` - Implements new feature

### Backward Compatibility
- `current-feature` file ensures existing commands work
- No changes needed to workflow commands
- Seamless integration with current system

### Multi-Session Support
- Multiple AI sessions can work on different features
- State file acts as coordination point
- Clear indication of which feature is current

## Output Format

### Success Message
```
✓ Successfully switched to feature: [feature-name]

Current Feature: [feature-name]
Status: [X]% complete
Next Action: [Suggested command based on progress]

All subsequent commands will now operate on this feature.
```

### Error Message
```
✗ Failed to switch feature: [reason]

Current Feature: [remains unchanged]
Available Features:
- feature-1 (75% complete)
- feature-2 (25% complete)
- feature-3 (100% complete)

To switch, use: /feature-switch [feature-name]
```

Now proceed to switch the current feature based on: $ARGUMENTS