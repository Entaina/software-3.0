# VCS Help - Version Control System Help

Display helpful information about all available VCS commands.

**Usage**: `/vcs/help`

## Implementation

Show a comprehensive help guide for all VCS commands, designed for non-developers to understand version control concepts and usage.

Steps to execute:
1. Display an overview of what version control is
2. List all available VCS commands with descriptions
3. Provide common workflow examples
4. Include troubleshooting tips
5. Show git concepts explained in simple terms

## Examples

```bash
/vcs/help
```

This will display:

### Version Control System (VCS) Commands

Version control helps you track changes to your files over time, like having a save history for your entire project.

#### Available Commands:

- **`/vcs/init`** - Start version control in this folder
- **`/vcs/save [message]`** - Save current changes with a description (auto-generates message if not provided)
- **`/vcs/load <commit>`** - Go back to a previous saved version  
- **`/vcs/history [number]`** - See all previous saves
- **`/vcs/diff`** - See what changes you've made since last save
- **`/vcs/help`** - Show this help information

#### Common Workflow:

1. **Start a new project**: `/vcs/init`
2. **Make changes to your files**
3. **Save your progress**: `/vcs/save "Added new feature"` or simply `/vcs/save` for auto-generated message
4. **Continue working and saving**: `/vcs/save "Fixed bug"` or `/vcs/save`
5. **Check your history**: `/vcs/history`
6. **Go back if needed**: `/vcs/load abc123f`

#### Tips:

- Save often with descriptive messages, or let the system auto-generate them
- Use `/vcs/diff` before saving to see what changed
- Manual commit messages should describe what you did
- Auto-generated messages analyze your changes and create appropriate descriptions
- You can always go back to any previous save

#### Auto-Generated Commit Messages:

When you use `/vcs/save` without a message, the system will:
- Analyze what files you've changed
- Understand the type of work you've done
- Generate a professional commit message like:
  - `feat: add user login functionality`
  - `fix: resolve database connection issue`
  - `docs: update installation guide`
  - `config: setup development environment`