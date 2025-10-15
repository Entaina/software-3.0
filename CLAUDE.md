# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a "Software 3.0" configuration repository that defines custom VCS (Version Control System) commands for Claude Code. The project extends Claude Code's functionality with user-friendly git operations designed for non-developers.

## Architecture

### Command System Structure
- `.claude/commands/vcs/` - Contains custom slash command definitions
- Each vcs/*.md file defines a VCS command with implementation steps
- Commands wrap git operations with simplified, non-technical interfaces

### Available VCS Commands
The repository defines eight custom VCS commands:

1. **`vcs:iniciar`** - Initialize git repository with basic .gitignore
2. **`vcs:guardar [file-description] [-m "message"]`** - Stage all changes or specific files and commit with message (auto-generates message if not provided, supports natural language file selection)
3. **`vcs:cargar [commit]`** - Reset repository to specific commit (with warnings and interactive history display when no commit specified)
4. **`vcs:historial [count]`** - Display commit history in readable format with enhanced formatting
5. **`vcs:diferencias`** - Show pending changes with intelligent summaries and project impact analysis
6. **`vcs:etiquetar [message]`** - Create tags for important commits (auto-timestamps if no message)
7. **`vcs:limpiar [files...]`** - Discard modifications and untracked files to return to clean state (can target specific files or clean everything)
8. **`vcs:ayuda`** - Display comprehensive VCS help for non-developers

### Configuration Files
- `.claude/settings.local.json` - Claude Code permissions and output style settings
- `.gitignore` - Standard exclusions for OS files, IDE settings, build outputs
- Git repository with standard initialization

## Key Design Principles

### User Experience Focus
- Commands use plain language instead of git terminology
- Error messages and outputs are designed for non-technical users
- Complex git operations are simplified into single commands
- Confirmations and warnings protect users from data loss

### Command Implementation Pattern
Each VCS command follows a consistent structure:
1. Parameter validation and repository checks
2. Clear explanations of what will happen
3. User confirmations for destructive operations
4. Execution of underlying git commands
5. User-friendly success/error reporting

### Safety Features
- `vcs:cargar` includes warnings about losing uncommitted changes
- Commands check for git repository existence before execution
- Descriptive commit messages are required for `vcs:guardar`
- All outputs avoid technical jargon

## Development Notes

### No Traditional Build System
This repository doesn't contain traditional build, test, or lint commands as it's purely configuration-based. The "code" consists of markdown command definitions that are interpreted by Claude Code's command system.

### Testing Approach
Testing these commands requires:
1. Using Claude Code with this configuration loaded
2. Manual testing of each VCS command in a git repository
3. Verifying non-technical user experience and error handling

### File Structure
```
.claude/
├── commands/vcs/    # VCS command definitions
│   ├── iniciar.md     # vcs:iniciar command
│   ├── guardar.md     # vcs:guardar command
│   ├── cargar.md      # vcs:cargar command
│   ├── historial.md   # vcs:historial command
│   ├── diferencias.md # vcs:diferencias command
│   ├── etiquetar.md   # vcs:etiquetar command
│   ├── limpiar.md     # vcs:limpiar command
│   └── ayuda.md       # vcs:ayuda command
├── settings.local.json  # Claude Code configuration
.gitignore          # Standard git exclusions
```

The repository intentionally keeps a minimal structure focused on the command definitions and configuration needed for the VCS command system to function.