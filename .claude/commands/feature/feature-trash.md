# /feature-trash

*Moves a feature to trash for soft deletion, with ability to restore later.*

## Auto-Loaded Project Context:
@/docs/product-development/.feature-state.json
@/docs/product-development/current-feature

## Command Overview

You are tasked with moving a feature to trash, which soft-deletes it while preserving the ability to restore. Trashed features are removed from active workflow but retained for potential recovery.

User provided input: "$ARGUMENTS"

## Step 1: Parse and Validate Input

### Extract Feature Name
- Parse arguments for feature name to trash
- Require explicit feature name (no defaults)
- Reject if no feature specified

### Safety Checks
- Cannot trash current feature without confirmation
- Warn if feature has recent updates
- Suggest archive instead of trash for completed features

## Step 2: Verify Feature State

### Load Feature Information
1. Read `.feature-state.json`
2. Check feature exists
3. Verify current status (active or archived)
4. Cannot trash already trashed features

### Pre-Trash Analysis
Display feature information:
```
Feature to Trash: [feature-name]
=================================
Status: [active|archived]
Progress: [X]% complete
Last Updated: [X days ago]
Size: [X files, X KB]

⚠️ Warning: Trashing will remove this feature from workflow.
Consider archiving instead if you might need it later.
```

### Trash vs Archive Guidance
Recommend based on state:
- **Completed features**: Suggest `/feature-archive` instead
- **Active development**: Confirm abandonment
- **Experimental/Failed**: Proceed with trash
- **Superseded**: Add reference to replacement

## Step 3: Require Confirmation

### Confirmation Prompt
For safety, require explicit confirmation:
```
⚠️ CONFIRM TRASH OPERATION ⚠️

This will move "[feature-name]" to trash.
- Feature will be removed from active/archived lists
- Can be restored with /feature-restore
- Will be permanently deleted after 30 days

Type the feature name to confirm: [awaiting confirmation]
```

### Handle Current Feature
If trashing current feature:
```
⚠️ This is your current feature!

Trashing will:
1. Switch to another active feature (or none)
2. Move this feature to trash
3. Update your working context

Proceed? [requires confirmation]
```

## Step 4: Perform Trash Operation

### Directory Operations
1. Create trash directory: `features/trashed/`
2. Move feature from current location to trash
3. Preserve complete directory structure
4. Add trash metadata file

### Create Trash Metadata
Add `.trash-info` to moved feature:
```json
{
  "trashed_at": "YYYY-MM-DD HH:MM:SS",
  "trashed_from": "active|archived",
  "original_path": "features/active/feature-name",
  "trash_reason": "user provided reason or 'manual'",
  "auto_delete_after": "YYYY-MM-DD",
  "feature_state_snapshot": { ... }
}
```

### State File Updates
Update `.feature-state.json`:
```json
{
  "features": {
    "feature-name": {
      "status": "trashed",
      "trashed_at": "YYYY-MM-DD",
      "trash_reason": "abandoned|failed|superseded|other",
      "previous_status": "active|archived",
      "updated_at": "YYYY-MM-DD"
    }
  }
}
```

## Step 5: Handle Current Feature Update

### Switch Logic
If trashing current feature:
1. Find most recently updated active feature
2. Update `current-feature` file
3. If no active features, set to empty
4. Notify user of switch

### Post-Trash State
Ensure consistent state:
- Current feature is valid or empty
- State file reflects all changes
- No broken references remain

## Step 6: Provide Trash Summary

### Success Message
```
✓ Feature Moved to Trash

Feature: [feature-name]
Previous Status: [active|archived]
Trash Location: features/trashed/[feature-name]/
Auto-Delete Date: [30 days from now]

Summary:
- Files preserved: X
- Can restore with: /feature-restore [feature-name]
- Will auto-delete on: [date]

[If was current]
Current feature switched to: [new-feature]
```

### Trash Information
Explain trash behavior:
```
Trash Behavior:
- Feature hidden from all lists except trash view
- Fully recoverable for 30 days
- Auto-deleted after 30 days
- Use /feature-list trashed to view all trashed features
```

## Step 7: Auto-Cleanup Considerations

### Trash Retention Policy
Implement 30-day retention:
- Track trash date in metadata
- Check expiration on feature operations
- Auto-clean expired items
- Warn before permanent deletion

### Trash Maintenance
During feature operations:
```python
def check_trash_expiration():
    for feature in trashed_features:
        if days_since_trashed(feature) > 30:
            permanently_delete(feature)
```

## Error Handling

### Operation Failures
If move fails:
1. No partial state changes
2. Original location preserved
3. Clear error message
4. Manual recovery steps

### State Inconsistencies
If state update fails:
- Rollback file operations
- Preserve original state
- Log error details
- Provide recovery command

### Permission Issues
Handle access problems:
- Check write permissions
- Suggest permission fixes
- Provide manual instructions

## Integration with Other Commands

### Command Interactions
- `/feature-list trashed`: Shows trashed features
- `/feature-restore`: Recovers from trash
- `/feature-create`: Checks trash for name conflicts
- Status commands ignore trashed features

### Workflow Protection
Trashed features are excluded from:
- Active feature lists
- Switch targets
- Workflow commands
- Dependency checks

## Best Practices

### When to Trash
Appropriate for:
- Failed experiments
- Abandoned approaches
- Duplicate features
- Test features

### When NOT to Trash
Avoid trashing:
- Completed features (use archive)
- Features with valuable history
- Features referenced by others
- Anything you might need later

### Trash Hygiene
- Add meaningful trash reasons
- Review trash periodically
- Restore or permanently delete
- Don't use trash as archive

Now proceed to trash the specified feature: $ARGUMENTS