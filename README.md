# Software 3.0 VCS Configuration

A **Software 3.0** configuration repository that extends Claude Code with simplified version control commands designed for non-developers.

## What This Is

This repository provides custom VCS (Version Control System) commands that make git operations accessible through plain language. Instead of learning complex git commands, users can save, load, and manage their project versions using simple, intuitive commands.

## Features

✨ **Plain Language Commands** - No technical jargon required  
🤖 **Auto-Generated Commit Messages** - Intelligent analysis of your changes  
🎯 **Selective File Operations** - Save specific files using natural descriptions  
🔄 **Interactive History** - Browse and choose versions visually  
📊 **Smart Change Analysis** - Understand the impact of your modifications  
🏷️ **Easy Version Tagging** - Mark important milestones effortlessly  
🧹 **Safe Cleanup Operations** - Discard unwanted changes with confirmation

## Quick Start

### 1. Initialize Version Control
```bash
/vcs:init
```
Start tracking changes in your project.

### 2. Save Your Work
```bash
# Save all changes with auto-generated message
/vcs:save

# Save with custom message
/vcs:save -m "Added user authentication"

# Save specific files using natural language
/vcs:save "all JavaScript files" -m "Fixed login bugs"
/vcs:save "files in src folder"
/vcs:save "configuration files"
```

### 3. Check Your Progress
```bash
# See what you've changed
/vcs:diff

# View your save history
/vcs:history

# View last 5 saves
/vcs:history 5
```

### 4. Go Back to Previous Versions
```bash
# Show history and choose interactively
/vcs:load

# Load specific version by hash
/vcs:load abc123f

# Load tagged version
/vcs:load version-1-0

# Go back one save
/vcs:load HEAD~1
```

### 5. Mark Important Milestones
```bash
# Create timestamped tag
/vcs:tag

# Create named tag
/vcs:tag "version 1.0"
/vcs:tag "stable release"
```

### 6. Clean Up Unwanted Changes
```bash
# Discard all uncommitted changes
/vcs:clean

# Clean specific files only
/vcs:clean src/auth.js README.md
/vcs:clean "*.js"
```

## Available Commands

| Command | Description |
|---------|-------------|
| `/vcs:init` | Initialize version control in current directory |
| `/vcs:save [files] [-m "message"]` | Save changes with smart commit messages |
| `/vcs:load [commit]` | Restore to previous version |
| `/vcs:history [count]` | View save history |
| `/vcs:diff` | Show pending changes with analysis |
| `/vcs:tag [message]` | Create version tags |
| `/vcs:clean [files]` | Discard changes safely |
| `/vcs:help` | Show detailed help |

## Natural Language File Selection

The `vcs:save` and `vcs:clean` commands understand natural descriptions:

- **File types**: `"JavaScript files"`, `"Python scripts"`, `"configuration files"`
- **Folders**: `"files in src folder"`, `"everything in docs directory"`
- **Patterns**: `"test files"`, `"documentation"`, `"build scripts"`
- **Specific files**: `"package.json yarn.lock"`, `"README.md src/main.js"`

## Smart Features

### Auto-Generated Commit Messages
When you use `/vcs:save` without a message, the system analyzes your changes and creates professional commit messages like:
- `feat: add user authentication system`
- `fix: resolve database connection issue`
- `docs: update installation guide`
- `config: setup development environment`

### Intelligent Change Analysis
The `/vcs:diff` command provides:
- **Project Impact Summary** - What your changes mean
- **Work Summary** - Type of work being done
- **File Analysis** - Detailed explanation of each change
- **Readiness Assessment** - Whether changes are ready to save

### Interactive History
Using `/vcs:load` without parameters shows your commit history and lets you choose which version to restore interactively.

## Safety Features

- **Explicit Confirmations** - Destructive operations require typing "yes"
- **Detailed Previews** - See exactly what will change before proceeding
- **Impact Analysis** - Understand what you'll lose before cleaning/loading
- **Selective Operations** - Target specific files without affecting others

## Installation

1. **Load this configuration in Claude Code**:
   - Open your project in Claude Code
   - Ensure this configuration repository is accessible
   - The VCS commands will be available as slash commands

2. **Start using VCS commands**:
   ```bash
   /vcs:init    # Initialize your project
   /vcs:help    # See all available commands
   ```

## Example Workflow

```bash
# Start a new project
/vcs:init

# Work on your files...
# Add features, fix bugs, update docs

# Check what you've done
/vcs:diff

# Save your work
/vcs:save "Added authentication and improved docs"

# Continue working...

# Save only specific changes
/vcs:save "test files" -m "Added unit tests"

# Mark a milestone
/vcs:tag "beta release"

# View your progress
/vcs:history

# Need to go back?
/vcs:load

# Clean up experimental changes
/vcs:clean "experimental-feature.js"
```

## Perfect For

- **Non-developers** managing project files
- **Content creators** tracking document versions  
- **Designers** versioning creative assets
- **Anyone** who wants simple version control
- **Teams** collaborating without git complexity

## Technical Details

This configuration extends Claude Code with custom slash commands that wrap git operations in user-friendly interfaces. Each command is implemented as a markdown file in `.claude/commands/vcs/` that defines the command behavior and implementation steps.

**No traditional build/test commands** - This is a pure configuration repository focused on command definitions.

## Support

For help with commands, use `/vcs:help` or refer to the comprehensive command documentation in the `.claude/commands/vcs/` directory.

---

**Software 3.0** - Where AI understands your intent and handles the technical complexity.