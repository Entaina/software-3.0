# VCS Diff - Show Pending Changes

Display all current changes that are pending to be committed, with an intelligent summary of what the changes mean for your project.

**Usage**: `/vcs/diff`

## Implementation

Show all changes in the working directory and staging area with a meaningful summary for non-developer users. This command analyzes changes and explains their impact in plain language.

Steps to execute:
1. Check if we're in a git repository
2. Run `git status --porcelain` to get an overview of changed files
3. Run `git diff` and `git diff --cached` to analyze actual changes
4. Analyze the changes to understand:
   - What type of work is being done (new features, bug fixes, configuration changes, etc.)
   - Which parts of the project are affected
   - The scope and impact of the changes
5. Present a user-friendly summary including:
   - **Project Impact Summary**: What these changes mean for the project in plain language
   - **Work Summary**: What kind of work has been done
   - **Files Affected**: List of changed files with brief explanations
   - **Readiness Assessment**: Whether changes are ready to be saved
6. Avoid technical jargon and focus on the practical meaning of changes

## Examples

```bash
/vcs/diff
```

This will show:
- **"You've been working on..."** - A summary of what the changes accomplish
- **"These changes affect..."** - Which parts of your project are impacted  
- **"Ready to save?"** - Whether the changes form a complete unit of work
- Clear, non-technical explanations of what each file change does

Example output:
```
📋 **Project Changes Summary**

You've been working on: Setting up project configuration and development tools
These changes affect: Project foundation and development workflow

**Work Summary:**
- Added configuration files for better project management
- Set up development tools and editor settings
- Created project structure for team collaboration

**Files Ready to Save:**
- `.gitignore` - Prevents unwanted files from being tracked
- `package.json` - Defines project dependencies and scripts
- `.vscode/settings.json` - Configures editor for consistent formatting

✅ **Ready to save**: These changes form a complete setup that's ready to commit
```