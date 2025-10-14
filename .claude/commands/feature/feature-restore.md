# /feature-restore

*Restores a previously archived or trashed feature back to active development.*

## Auto-Loaded Project Context:
@/docs/product-development/.feature-state.json
@/docs/product-development/current-feature

## Command Overview

You are tasked with restoring a feature from archived or trashed state back to active development. This command reverses the effects of feature-archive or feature-trash operations.

User provided input: "$ARGUMENTS"

## Step 1: Parse and Identify Feature

### Extract Feature Name
- Parse arguments for feature name
- Require explicit feature name
- No default behavior without arguments

### Feature Search
Look for feature in:
1. `features/archived/` directory
2. `features/trashed/` directory
3. State file with archived/trashed status

## Step 2: Locate and Analyze Feature

### Find Feature Location
Search order:
```python
locations = [
    "features/archived/{feature_name}",
    "features/trashed/{feature_name}"
]
```

### Load Feature Information
From found location, analyze:
- Current status (archived vs trashed)
- Archive/trash metadata if available
- Progress state from last active period
- File structure integrity

### Display Feature Summary
```
Feature Found: [feature-name]
==========================
Current Status: [archived|trashed]
Location: features/[archived|trashed]/[feature-name]/
Last Active: [date]
Progress When Removed: [X]%

Files Present:
✓ feature.md
✓ JTBD.md
✓ PRD.md
✗ plan.md
✗ plan-organized.md

[If archived]
Archive Reason: [completed|paused|abandoned]
Archived Date: [date]

[If trashed]
Trash Date: [date]
Auto-Delete In: [X days]
Trash Reason: [reason]
```

## Step 3: Verify Restoration Viability

### Check for Conflicts
Before restoring:
1. Ensure no active feature with same name
2. Check name availability
3. Verify directory structure intact
4. Confirm no missing critical files

### Conflict Resolution
If name conflict exists:
```
Error: Active feature with name "[feature-name]" already exists.

Options:
1. Choose different name for restored feature
2. Archive/trash the existing feature first
3. Merge features (manual process)

Cannot proceed with restoration.
```

### File Integrity Check
Verify feature has minimum files:
- `feature.md` must exist
- Directory structure intact
- No corruption detected

## Step 4: Restoration Process

### Directory Operations
1. Move feature from archived/trashed to active:
   ```
   features/[archived|trashed]/[feature-name]/ → features/active/[feature-name]/
   ```
2. Preserve all files and structure
3. Remove any archive/trash metadata files

### State File Updates
Update `.feature-state.json`:
```json
{
  "features": {
    "feature-name": {
      "status": "active",
      "restored_at": "YYYY-MM-DD",
      "restored_from": "archived|trashed",
      "updated_at": "YYYY-MM-DD",
      // Original progress preserved
      "progress": {
        "jtbd": true,
        "prd": true,
        "plan": false,
        "plan_organized": false,
        "implementation": false
      }
    }
  }
}
```

### Restoration Metadata
Track restoration in feature history:
- Restoration date
- Restored from (archived/trashed)
- Previous removal reason
- Restoration context

## Step 5: Post-Restoration Actions

### Feature Activation Options
After successful restoration:
```
✓ Feature Successfully Restored

Feature: [feature-name]
Restored to: features/active/[feature-name]/
Status: Active (not current)
Progress: [X]% complete

Next Steps:
1. Switch to feature: /feature-switch [feature-name]
2. Review status: /feature-status [feature-name]
3. Continue work: [suggested command based on progress]

The feature is now active but not set as current.
```

### Automatic Activation
Optionally ask user:
```
Would you like to:
1. Switch to this feature now? (/feature-switch)
2. Keep current feature? (no change)
3. View detailed status? (/feature-status)

Choice: [await user input or skip]
```

## Step 6: Handle Special Cases

### Restoring from Trash
Additional considerations:
- Remove `.trash-info` metadata file
- Cancel auto-deletion timer
- Note if close to deletion date
- Preserve trash history

### Restoring Completed Features
If restoring archived "completed" feature:
```
Note: This feature was archived as "completed".
Restoring suggests additional work needed.
Consider:
- Creating new feature for enhancements
- Documenting why restoration needed
- Updating status to reflect new work
```

### Old Features
For features archived/trashed long ago:
```
⚠️ Warning: Feature was removed [X months] ago.
- Technology may have changed
- Dependencies might be outdated
- Review thoroughly before continuing

Proceed with restoration? [confirm]
```

## Step 7: Update Related Information

### Dependency Updates
If other features referenced this one:
1. Scan for references in other features
2. Note that feature is now restored
3. Update dependency status if needed

### Documentation Updates
In restored feature's documentation:
1. Add restoration note to feature.md
2. Update status checklist
3. Note any new context since removal

### Example Update to feature.md
```markdown
## Restoration Note
- Restored: [YYYY-MM-DD]
- Restored from: [archived|trashed]
- Reason: [why restored]
- Previous state: [X]% complete
```

## Error Handling

### Feature Not Found
```
Error: Feature "[feature-name]" not found in archives or trash.

Available archived features:
- feature-1
- feature-2

Available trashed features:
- feature-3
- feature-4

Use exact feature name for restoration.
```

### Corrupted Feature
If feature structure damaged:
```
Error: Feature structure corrupted
Missing required files or invalid structure.
Cannot restore automatically.

Manual recovery needed:
1. Check features/[archived|trashed]/[feature-name]/
2. Verify file integrity
3. Move manually if structure intact
```

### State Conflicts
If state file shows different status:
```
Warning: State mismatch detected
- File location: [archived|trashed]
- State file shows: [different status]

Proceeding with restoration based on actual location.
State file will be updated.
```

## Integration Considerations

### Workflow Continuity
Restored features:
- Resume from last progress point
- Maintain all historical documentation
- Continue with normal workflow commands
- Preserve relationships and dependencies

### History Preservation
Restoration history tracked:
- Original creation date preserved
- Archive/trash/restore events logged
- Progress history maintained
- Document timestamps kept

### Command Integration
After restoration:
- Feature appears in `/feature-list active`
- Can be selected with `/feature-switch`
- Works with all workflow commands
- Status shows restoration info

## Best Practices

### Restoration Guidelines
- Document why feature was restored
- Review old documentation for relevance
- Update outdated information
- Consider if new feature more appropriate

### Post-Restoration Review
After restoring:
1. Review all existing documentation
2. Update technical dependencies
3. Reassess user needs (JTBD)
4. Revise timeline estimates

### Restoration vs New Feature
Consider creating new feature if:
- Original heavily outdated
- Requirements changed significantly
- Better to start fresh
- Only need small part of original

Now proceed to restore the specified feature: $ARGUMENTS