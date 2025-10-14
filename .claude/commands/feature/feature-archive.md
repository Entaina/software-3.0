# /feature-archive

*Archives a completed or paused feature, moving it out of active development.*

## Auto-Loaded Project Context:
@/docs/product-development/.feature-state.json
@/docs/product-development/current-feature

## Command Overview

You are tasked with archiving a feature, which moves it from active development to the archived state. This preserves the feature's documentation and history while removing it from active workflow.

User provided input: "$ARGUMENTS"

## Step 1: Parse and Validate Input

### Extract Feature Name
- Parse arguments for feature name to archive
- If no arguments: Ask user to specify feature
- Handle special cases like "." for current feature

### Initial Validation
- Feature name must be provided
- Warn if trying to archive current feature
- Confirm action for features with recent activity

## Step 2: Verify Feature State

### Load Current State
1. Read `.feature-state.json`
2. Read `current-feature` file
3. Verify feature exists and is active

### Pre-Archive Checks
Verify the feature:
- Exists in state file
- Has status "active"
- Has directory in `features/active/`
- Is not the current feature (or handle appropriately)

### Feature Analysis
Check feature completion:
```
Progress Check:
- JTBD: [✓/✗]
- PRD: [✓/✗]
- Plan: [✓/✗]
- Organized Plan: [✓/✗]
- Last Updated: [date]
```

## Step 3: Confirm Archive Action

### Display Feature Summary
Show what will be archived:
```
Feature to Archive: [feature-name]
==================================
Description: [description]
Status: [X]% complete
Created: [date]
Last Updated: [date]
Size: [total files, total size]

Documents:
✓ feature.md (X lines)
✓ JTBD.md (X lines)
✓ PRD.md (X lines)
✗ plan.md (not created)
✗ plan-organized.md (not created)

Archive Reason: [completed|paused|abandoned]
```

### Get Archive Reason
Determine or ask for archive reason:
- **Completed**: Feature fully implemented
- **Paused**: Temporarily on hold
- **Abandoned**: No longer needed
- **Superseded**: Replaced by another feature

## Step 4: Handle Current Feature

### If Archiving Current Feature
Special handling required:
1. Inform user that current feature will be archived
2. Suggest switching to another feature first
3. Or automatically switch to most recent active feature
4. Update `current-feature` file if needed

### Current Feature Logic
```python
if feature_name == current_feature:
    active_features = get_active_features()
    if len(active_features) > 1:
        # Switch to most recent other feature
        new_current = most_recent_active_feature()
        update_current_feature(new_current)
    else:
        # No other active features
        update_current_feature("")
```

## Step 5: Perform Archive Operation

### Directory Move
1. Create archived directory if needed: `features/archived/`
2. Move feature directory from `active/` to `archived/`
3. Preserve all files and structure
4. Verify move completed successfully

### State File Updates
Update `.feature-state.json`:
```json
{
  "features": {
    "feature-name": {
      "status": "archived",
      "archived_at": "YYYY-MM-DD",
      "archive_reason": "completed|paused|abandoned",
      "updated_at": "YYYY-MM-DD"
      // ... other fields remain
    }
  }
}
```

### Archive Metadata
Add archive-specific information:
- Archive timestamp
- Archive reason
- Final progress state
- Any archive notes

## Step 6: Create Archive Summary

### Generate Archive Report
Create `ARCHIVE_SUMMARY.md` in archived feature:
```markdown
# Archive Summary: [feature-name]

## Archive Information
- Archived Date: [YYYY-MM-DD]
- Archive Reason: [reason]
- Final Status: [X]% complete
- Archived By: AI Assistant

## Feature Overview
[Original description]

## Final State
- ✓ Feature Definition
- ✓ JTBD Analysis (X user jobs identified)
- ✓ PRD Document (X requirements defined)
- ✗ Technical Plan (not created)
- ✗ Implementation (not started)

## Key Outcomes
[Summary of what was accomplished]

## Archive Notes
[Any additional context about why archived]

## Restoration
To restore this feature to active development:
`/feature-restore [feature-name]`
```

## Step 7: Post-Archive Actions

### Update References
If other features reference this one:
1. Scan other features for references
2. Note in their documentation that referenced feature is archived
3. Suggest updates if dependencies affected

### Success Confirmation
Display confirmation:
```
✓ Feature Successfully Archived

Feature: [feature-name]
Moved to: features/archived/[feature-name]/
Archive Reason: [reason]
Archive Date: [YYYY-MM-DD]

Summary:
- Files preserved: X
- Total size: X KB
- Progress at archive: X%
- Current feature: [updated if changed]

To view archived features: /feature-list archived
To restore this feature: /feature-restore [feature-name]
```

## Step 8: Handle Edge Cases

### Incomplete Features
For features with low completion:
```
Warning: Feature is only X% complete.
Are you sure you want to archive?
Consider:
- Completing planning documents first
- Using 'paused' as archive reason
- Adding notes about future work
```

### Recently Active Features
For features updated recently:
```
Warning: Feature was updated X days ago.
Recent activity detected. Confirm archive?
```

### Dependencies
If other features depend on this:
```
Warning: Other features reference this one:
- feature-xyz mentions this in PRD
- feature-abc lists as dependency

Archive anyway? Dependencies should be updated.
```

## Error Handling

### Move Failures
If directory move fails:
1. Attempt to rollback any changes
2. Check permissions and disk space
3. Provide manual move instructions
4. Keep state file unchanged

### State Corruption
If state file update fails:
1. Preserve original state file
2. Report what changes were attempted
3. Provide recovery instructions

### Current Feature Issues
If can't update current feature:
1. Complete archive anyway
2. Warn user about current feature state
3. Provide manual fix instructions

## Integration Considerations

### Workflow Impact
After archiving:
- Feature no longer appears in active lists
- Can't be switched to without restoring
- Workflow commands won't operate on it
- History and documentation preserved

### Restoration Path
Archived features can be restored:
- `/feature-restore` reverses the process
- All documents remain intact
- Progress tracking continues
- History includes archive/restore events

### Archive Organization
Consider archive organization:
```
features/archived/
├── 2024-01-completed/
│   └── feature-1/
├── 2024-01-paused/
│   └── feature-2/
└── feature-name/  # Default flat structure
```

## Best Practices

### Archive Timing
Recommend archiving when:
- Feature is fully implemented and deployed
- Feature is abandoned and won't be continued
- Feature is paused for extended period
- Feature is superseded by new approach

### Archive Hygiene
- Add meaningful archive notes
- Update related documentation
- Clean up any temporary files
- Document lessons learned

### Archive vs Trash
Guide users on when to:
- **Archive**: Completed or might resume later
- **Trash**: Definitely won't need again
- Archive preserves history better than trash

Now proceed to archive the specified feature: $ARGUMENTS