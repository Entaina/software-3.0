# VCS Load - Restore Previous Commit

Restore the repository to a previous commit state.

**Usage**: `/vcs/load <commit-hash-or-reference>`

## Implementation

Reset the repository to a specific commit using `git reset --hard`. This command allows users to restore their project to any previous state.

Steps to execute:
1. Check if we're in a git repository
2. Validate the provided commit hash or reference exists
3. Show what changes will be lost (current uncommitted changes)
4. Ask for confirmation if there are uncommitted changes
5. Run `git reset --hard <commit-hash-or-reference>`
6. Show confirmation of the reset operation

## Examples

```bash
/vcs/load abc123f
/vcs/load HEAD~1
/vcs/load main
```

This will:
- Reset the repository to the specified commit
- Discard any uncommitted changes
- Show confirmation of the operation

**Warning**: This command will permanently discard uncommitted changes. Users should be warned and asked for confirmation.