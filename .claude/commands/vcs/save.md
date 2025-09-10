# VCS Save - Add and Commit Changes

Save current changes to the version control system with a commit message. If no message is provided, the command will automatically analyze the changes and generate an appropriate commit message.

**Usage**: `/vcs/save [commit-message]`

## Implementation

Add all current changes and create a commit with the provided message, or auto-generate one by analyzing the changes. This command combines `git add .` and `git commit -m` into a single, user-friendly operation with intelligent commit message generation.

Steps to execute:
1. Check if we're in a git repository
2. Run `git add .` to stage all changes
3. If no commit message provided:
   a. Run `git status --porcelain` to get overview of changed files
   b. Run `git diff` and `git diff --cached` to analyze actual changes
   c. Analyze the changes to determine:
      - Type of work (new features, bug fixes, configuration, documentation, etc.)
      - Scope of changes (which parts of project affected)
      - Key modifications made
   d. Generate a descriptive commit message in format: "action: brief description"
      - Use action verbs like: add, update, fix, remove, refactor, docs, config, feat
      - Keep message concise but descriptive (50 characters or less for first line)
      - Include additional details in body if changes are complex
4. Run `git commit -m "<commit-message>"` with provided or generated message
5. Show confirmation of the commit with hash and summary
6. Handle cases where there are no changes to commit

## Auto-Generated Commit Message Examples

The command analyzes changes and creates messages like:
- `feat: add user authentication system`
- `fix: resolve login validation bug`
- `docs: update API documentation`
- `config: setup project build tools`
- `refactor: improve database connection handling`

## Examples

```bash
/vcs/save "Added new feature for user authentication"
```
Manual commit message - stages all changes and commits with provided message.

```bash
/vcs/save
```
Auto-generated commit message - analyzes changes and creates appropriate commit message automatically.

This will:
- Stage all current changes
- Analyze changes if no message provided and generate intelligent commit message
- Create commit with provided or generated message
- Show confirmation with commit details and explain the generated message if auto-created