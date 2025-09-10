# VCS Load - Restore Previous Version

Restore the repository to a previous commit, tag, or branch state.

**Usage**: `/vcs/load <commit-hash-or-tag-or-reference>`

## Implementation

Reset the repository to a specific commit, tag, or branch using `git reset --hard`. This command allows users to restore their project to any previous state using various reference types.

Steps to execute:
1. Check if we're in a git repository
2. Resolve and validate the provided reference (commit hash, tag name, branch, or description):
   - If it looks like a commit hash (starts with alphanumeric), use directly
   - If it matches a tag name, resolve to the tagged commit
   - If it matches a branch name, resolve to the branch head
   - If it's a relative reference (HEAD~1, HEAD^), resolve it
   - If it's a description, search recent commits for matching messages
3. Check current repository status to analyze what will be lost:
   - Modified files that will be discarded
   - Untracked files (these will remain but may conflict with target state)
   - Staged changes that will be lost
4. Display the target commit information (hash, message, date, author)
5. Show detailed impact analysis:
   - List modified files with change descriptions
   - Show total count of affected files
   - Compare current state with target commit
6. **Ask for explicit confirmation** with clear warning about data loss:
   - Display clear warning about permanent data loss
   - Require user to type "yes" or "y" to confirm (case-insensitive)
   - Show exactly what commit they're loading
7. After confirmation:
   - Run `git reset --hard <resolved-reference>`
   - Show confirmation of the reset operation with details

## Examples

```bash
/vcs/load abc123f
```
Load specific commit by hash.

```bash
/vcs/load version-1-0
```
Load tagged version (created with vcs:tag).

```bash
/vcs/load HEAD~1
```
Load previous commit (relative reference).

```bash
/vcs/load main
```
Load specific branch head.

```bash
/vcs/load "add user authentication"
```
Load commit by searching for description match.

This will:
- Resolve the reference to a specific commit (hash, tag, branch, or description)
- Analyze what changes will be lost
- Show detailed impact preview
- Ask for explicit confirmation before proceeding
- Reset the repository to that commit
- Show confirmation with detailed operation summary

**Reference Types Supported**:
- **Commit hashes**: `abc123f`, `a1b2c3d4e5f6`
- **Tags**: `version-1-0`, `2024-03-15_14-30` (created by vcs:tag)
- **Branches**: `main`, `develop`, `feature-branch`
- **Relative**: `HEAD~1`, `HEAD~2`, `HEAD^`
- **Descriptions**: Search commit messages for matches

## Safety Features

- **Detailed preview**: Shows exactly what will be lost before loading
- **Explicit confirmation**: Requires typing "yes" to proceed, not just pressing Enter
- **Clear warnings**: Multiple warnings about permanent data loss
- **Impact analysis**: Compares current state with target commit
- **Target validation**: Confirms the target commit exists and is accessible

Example interaction:
```
🔄 **Repository Load Analysis**

**Target**: Loading commit abc123d - "feat: add user authentication system"
**Author**: John Doe (2 days ago)

**Current Status**: Your repository has uncommitted changes

**Files that will be discarded** (2 modified):
- `src/main.js` - 8 lines changed
- `config.json` - Modified settings

**Files that will be staged/unstaged**:
- Currently staged changes will be lost

---

⚠️  **WARNING: This action cannot be undone!**
All uncommitted changes will be permanently lost.
You will be moved to commit: abc123d - "feat: add user authentication system"

**Total impact**: 2 files will be affected

Type "yes" to proceed with loading: _
```

After confirmation:
```
✅ **Repository Loaded Successfully!**

**Target reached**: abc123d - "feat: add user authentication system"
**Actions taken**:
- Discarded modifications in 2 files
- Reset HEAD to target commit
- Working directory now matches target exactly

Your repository is now at the requested state.
```

**Warning**: This command permanently destroys uncommitted work. Use with extreme caution and ensure you want to lose all current changes.