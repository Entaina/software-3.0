# VCS History - Show Commit History

Display the commit history of the repository in a user-friendly format.

**Usage**: `/vcs/history [number-of-commits]`

## Implementation

Show the commit history using `git log` with formatting optimized for non-developers. Display commits in a clear, readable format with essential information.

Steps to execute:
1. Check if we're in a git repository
2. Use `git log` with custom formatting to show:
   - Commit hash (short version)
   - Commit date
   - Author name
   - Commit message
3. Limit to specified number of commits (default: 10)
4. Format output in a clean, readable way

## Examples

```bash
/vcs/history
/vcs/history 5
/vcs/history 20
```

This will:
- Show the last 10 commits (or specified number)
- Display each commit with hash, date, author, and message
- Format the output for easy reading