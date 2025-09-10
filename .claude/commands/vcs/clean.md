# VCS Clean - Reset to Clean State

Discard all modifications and untracked files to return the repository to a clean state matching the current commit. This removes all uncommitted changes and new files.

**Usage**: `/vcs/clean`

## Implementation

Clean the working directory by discarding all modifications and removing untracked files using `git reset --hard` and `git clean -fd`. This command restores the repository to exactly match the current commit state.

Steps to execute:
1. Check if we're in a git repository
2. Check current repository status to see what will be cleaned:
   - Modified files that will be discarded
   - Untracked files that will be deleted
   - Staged changes that will be lost
3. If there are no changes to clean:
   - Inform user that repository is already clean
   - Exit without taking action
4. If there are changes to clean:
   - Display detailed summary of what will be lost:
     - List modified files with change descriptions
     - List untracked files that will be deleted
     - Show total count of affected files
   - **Ask for explicit confirmation** with clear warning about data loss
   - Require user to type "yes" or "y" to confirm (case-insensitive)
5. After confirmation:
   - Run `git reset --hard HEAD` to discard all modifications
   - Run `git clean -fd` to remove untracked files and directories
   - Show confirmation of cleaning operation with summary
6. Handle edge cases:
   - Repository with no commits (newly initialized)
   - Permission issues with untracked files
   - Files that cannot be removed

## Safety Features

- **Multiple confirmations**: Clear warnings about permanent data loss
- **Detailed preview**: Shows exactly what will be lost before cleaning
- **Explicit consent**: Requires typing confirmation, not just pressing Enter
- **No action on clean repo**: Skips operation if nothing to clean
- **Error handling**: Gracefully handles files that cannot be removed

## Examples

```bash
/vcs/clean
```

This will:
- Analyze current repository state
- Show what files will be affected
- Ask for confirmation before proceeding
- Discard all modifications and remove untracked files
- Return repository to clean state matching current commit

Example interaction:
```
🧹 **Repository Cleanup Analysis**

**Current Status**: Your repository has uncommitted changes

**Files that will be discarded** (3 modified):
- `src/main.js` - 15 lines changed
- `README.md` - 3 lines added
- `config.json` - Modified settings

**Files that will be deleted** (2 untracked):
- `temp_notes.txt` - New file (142 bytes)
- `debug.log` - New file (1.2 KB)

---

⚠️  **WARNING: This action cannot be undone!**
All uncommitted changes will be permanently lost.

**Total impact**: 5 files will be affected

Type "yes" to proceed with cleaning: _
```

After confirmation:
```
✅ **Repository Cleaned Successfully!**

**Actions taken**:
- Discarded modifications in 3 files
- Removed 2 untracked files
- Repository now matches commit: abc123d - "feat: add user authentication"

Your working directory is now clean and matches the current commit exactly.
```

**Warning**: This command permanently destroys uncommitted work. Use with extreme caution and only when you're certain you want to lose all current changes.