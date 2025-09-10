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
3. Show what changes will be lost (current uncommitted changes)
4. Display the target commit information (hash, message, date, author)
5. Ask for confirmation if there are uncommitted changes
6. Run `git reset --hard <resolved-reference>`
7. Show confirmation of the reset operation with details

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
- Reset the repository to that commit
- Discard any uncommitted changes
- Show confirmation with detailed commit information

**Reference Types Supported**:
- **Commit hashes**: `abc123f`, `a1b2c3d4e5f6`
- **Tags**: `version-1-0`, `2024-03-15_14-30` (created by vcs:tag)
- **Branches**: `main`, `develop`, `feature-branch`
- **Relative**: `HEAD~1`, `HEAD~2`, `HEAD^`
- **Descriptions**: Search commit messages for matches

**Warning**: This command will permanently discard uncommitted changes. Users should be warned and asked for confirmation.