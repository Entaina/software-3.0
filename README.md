# Software 3.0 Configuration for Claude Code

A **Software 3.0** configuration repository that extends Claude Code with powerful development workflows, specialized agents, and simplified commands designed for both developers and non-developers.

## What This Is

This repository provides a comprehensive development environment for Claude Code with five major systems:

1. **VCS Commands** - Simplified version control operations in plain language
2. **Feature Management** - Complete product development lifecycle from idea to implementation
3. **Specialized Agents** - Expert AI agents for Rails, Hotwire, Tailwind, Product Management, and Design Systems
4. **Context Management** - Save and restore development contexts across sessions
5. **Learning System** - Automatic documentation updates from conversation analysis

## Features

### VCS (Version Control System)
✨ **Plain Language Commands** - No technical jargon required
🤖 **Auto-Generated Commit Messages** - Intelligent analysis of your changes
🎯 **Selective File Operations** - Save specific files using natural descriptions
🔄 **Interactive History** - Browse and choose versions visually
📊 **Smart Change Analysis** - Understand the impact of your modifications
🏷️ **Easy Version Tagging** - Mark important milestones effortlessly
🧹 **Safe Cleanup Operations** - Discard unwanted changes with confirmation

### Feature Management
🎯 **Jobs To Be Done (JTBD)** - Define customer problems before building solutions
📋 **Product Requirements (PRD)** - Create comprehensive feature specifications
📐 **Technical Planning** - Organize implementation with architectural decisions
🔄 **Lifecycle Management** - Track features from creation to archive
💾 **State Persistence** - Maintain feature context across sessions
🗂️ **Feature Organization** - List, switch, archive, and restore features

### Specialized AI Agents
🏗️ **Rails Architect** - SOLID principles, architecture patterns, and best practices
⚡ **Hotwire Specialist** - Turbo Frames, Turbo Streams, and Stimulus controllers
🎨 **Tailwind Specialist** - Utility-first CSS, responsive design, and optimization
📊 **Product Owner** - Lean product management and prioritization

### Context Management
💾 **Save Contexts** - Preserve development state and conversation context
🔄 **Load Contexts** - Restore previous sessions with full context
📝 **Update Contexts** - Modify existing saved contexts
🔍 **Initialize Projects** - Set up new project contexts

### Learning System
🧠 **Conversation Analysis** - Extract insights from development sessions
📚 **Auto-Documentation** - Update CLAUDE.md with learned patterns
🔄 **Continuous Learning** - Keep documentation synchronized with project evolution
🎯 **Selective Updates** - Target specific sections for focused documentation
📊 **Pattern Recognition** - Identify architectural decisions and best practices

## Quick Start

### Version Control System (VCS)

#### 1. Initialize Version Control
```bash
/vcs:init
```
Start tracking changes in your project.

#### 2. Save Your Work
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

#### 3. Check Your Progress
```bash
# See what you've changed
/vcs:diff

# View your save history
/vcs:history

# View last 5 saves
/vcs:history 5
```

#### 4. Go Back to Previous Versions
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

#### 5. Mark Important Milestones
```bash
# Create timestamped tag
/vcs:tag

# Create named tag
/vcs:tag "version 1.0"
/vcs:tag "stable release"
```

#### 6. Clean Up Unwanted Changes
```bash
# Discard all uncommitted changes
/vcs:clean

# Clean specific files only
/vcs:clean src/auth.js README.md
/vcs:clean "*.js"
```

### Feature Management Workflow

#### 1. Create a New Feature
```bash
# Start a new feature with guided workflow
/feature-create

# The system will guide you through:
# - Feature name and description
# - Creating JTBD (Jobs To Be Done) document
# - Creating PRD (Product Requirements Document)
# - Creating technical implementation plan
```

#### 2. Work on Features
```bash
# Switch between features
/feature-switch feature-name

# Check current feature status
/feature-status

# List all features
/feature-list

# Implement code from plan
/implement-code
```

#### 3. Organize and Plan
```bash
# Create standalone planning documents
/create-jtbd    # Jobs To Be Done analysis
/create-prd     # Product Requirements Document
/create-plan    # Technical implementation plan
/organize-plan  # Organize existing plan
```

#### 4. Feature Lifecycle
```bash
# Archive completed features
/feature-archive feature-name

# Move to trash (soft delete)
/feature-trash feature-name

# Restore from trash
/feature-restore feature-name
```

### Context Management

```bash
# Save current development context
/contexts:save "Working on authentication feature"

# Load a saved context
/contexts:load context-name

# Update existing context
/contexts:update context-name

# Initialize new project context
/contexts:init
```

### Learning and Documentation

```bash
# Analyze conversation and update CLAUDE.md
/learn

# Update specific section only
/learn architecture
/learn principles
```

The `/learn` command analyzes your current conversation to extract:
- Technical decisions made
- New patterns discovered
- Architecture changes
- Best practices learned
- Feature additions

It then automatically updates the CLAUDE.md file to keep documentation in sync with the project's evolution.

### Using Specialized Agents

The specialized agents are automatically available and can be invoked directly in your conversations:

```
"I need to implement user authentication in Rails"
→ Rails Architect agent provides SOLID architecture guidance

"How do I add inline editing with Hotwire?"
→ Hotwire Specialist provides Turbo Frame implementation

"Style this form with Tailwind"
→ Tailwind Specialist provides utility-first CSS implementation

"Should we build this feature?"
→ Product Owner helps with JTBD analysis and prioritization
```

## Available Commands

### VCS Commands

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

### Feature Management Commands

| Command | Description |
|---------|-------------|
| `/feature-create` | Create new feature with guided workflow |
| `/feature-switch [name]` | Switch to a different feature |
| `/feature-status` | Show current feature status |
| `/feature-list` | List all features (active/archived/trash) |
| `/feature-archive [name]` | Archive completed feature |
| `/feature-trash [name]` | Move feature to trash |
| `/feature-restore [name]` | Restore feature from trash |
| `/create-jtbd` | Create Jobs To Be Done document |
| `/create-prd` | Create Product Requirements Document |
| `/create-plan` | Create technical implementation plan |
| `/organize-plan` | Organize existing plan |
| `/implement-code` | Implement code from plan |

### Context Management Commands

| Command | Description |
|---------|-------------|
| `/contexts:init` | Initialize new project context |
| `/contexts:save [description]` | Save current development context |
| `/contexts:load [name]` | Load saved context |
| `/contexts:update [name]` | Update existing context |

### Utility Commands

| Command | Description |
|---------|-------------|
| `/commands-manager` | Manage slash commands (create, edit, delete) |
| `/learn [section]` | Analyze conversation and update CLAUDE.md with insights |

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

## Specialized AI Agents

This configuration includes four expert AI agents with deep domain knowledge:

### 🏗️ Rails Architect
**Expertise**: Rails architecture, SOLID principles, design patterns
- Architectural decision making (Service Objects, STI vs polymorphism)
- Code review against SOLID/KISS/YAGNI principles
- Refactoring strategies and migration patterns
- REST-compliant design
- **Lines of code**: 55,278 lines of structured expertise

### ⚡ Hotwire Specialist
**Expertise**: Turbo Drive, Turbo Frames, Turbo Streams, Stimulus
- Deciding which Hotwire technique for specific features
- Implementing inline editing, modals, real-time updates
- Debugging Turbo Frame mismatches
- ActionCable broadcast setup
- **Lines of code**: 35,940 lines of Hotwire patterns

### 🎨 Tailwind Specialist
**Expertise**: Utility-first CSS, responsive design, performance
- Implementing UI components with Tailwind utilities
- Configuration and theme customization
- Bundle size optimization and PurgeCSS
- Dark mode implementation
- Accessibility with Tailwind
- **Lines of code**: 38,519 lines of CSS expertise

### 📊 Product Owner (Lean)
**Expertise**: Jobs To Be Done, product prioritization, lean methodology
- JTBD discovery before building features
- Creating Product Requirements Documents
- Prioritization frameworks (RICE, Kano)
- Scope management and saying "no"
- Post-launch metrics analysis
- **Lines of code**: 46,326 lines of product knowledge

**Total Agent Knowledge**: Over 176,000 lines of structured, expert knowledge

## Perfect For

### Non-Technical Users
- **Content creators** tracking document versions
- **Designers** versioning creative assets
- **Project managers** organizing feature development
- **Anyone** who wants simple version control

### Developers
- **Rails developers** building maintainable applications
- **Full-stack developers** using Hotwire and Tailwind
- **Solo developers** needing architecture guidance
- **Teams** wanting consistent design patterns

### Product Teams
- **Product managers** defining features with JTBD
- **Designers** maintaining design systems
- **Stakeholders** understanding development lifecycle

## Technical Details

### Architecture

This configuration extends Claude Code through three main components:

#### 1. Slash Commands
Custom commands defined as markdown files in `.claude/commands/`:
- **VCS commands** (`vcs/`) - 8 commands for version control
- **Feature commands** (`feature/`) - 12 commands for feature lifecycle management
- **Context commands** (`contexts/`) - 4 commands for context management
- **Utility commands** - Command manager and learning system for self-improvement

#### 2. Specialized Agents
AI agents with domain expertise in `.claude/agents/`:
- Each agent contains 30,000+ lines of structured knowledge
- Uses 6-context framework (c₁-c₆) for consistent responses
- Automatically invoked based on conversation context
- Provides expert guidance in specific domains

#### 3. State Management
Persistent state tracking for features and contexts:
- `.features/active/` - Active feature development
- `.features/archive/` - Completed features
- `.features/trash/` - Soft-deleted features
- `.features/state.json` - Current feature and metadata
- `.contexts/` - Saved development contexts

### File Structure
```
.claude/
├── commands/
│   ├── vcs/           # 8 VCS commands
│   ├── feature/       # 12 feature management commands
│   ├── contexts/      # 4 context commands
│   ├── commands-manager.md
│   └── learn.md       # Learning system command
├── agents/
│   ├── rails-architect.md        # 55,278 lines
│   ├── hotwire-specialist.md     # 35,940 lines
│   ├── tailwind-specialist.md    # 38,519 lines
│   └── product-owner.md          # 46,326 lines
└── settings.local.json

.features/
├── active/           # Active features
├── archive/          # Archived features
├── trash/            # Soft-deleted features
└── state.json        # Current feature state

.contexts/            # Saved contexts
```

**No traditional build/test commands** - This is a configuration repository that extends Claude Code's capabilities.

## Key Innovations

### 1. Product-Driven Development
Instead of just writing code, start with customer problems:
- **JTBD First**: Understand the job customers are trying to do
- **PRD Documentation**: Define requirements before implementation
- **Technical Planning**: Organize architecture before coding
- **Lifecycle Tracking**: Manage features from idea to archive

### 2. Expert AI Collaboration
Four specialized agents provide deep domain expertise:
- **176,000+ lines** of structured knowledge
- **6-context framework** ensures consistent, high-quality responses
- **Automatic invocation** based on conversation context
- **Complementary expertise** across product and engineering

### 3. Context Preservation
Never lose your place in complex development work:
- **Save entire conversations** with full context
- **Restore development state** across sessions
- **Feature-specific context** keeps work organized
- **Persistent metadata** tracks progress and decisions

### 4. Simplified Workflows
Complex operations made simple:
- **Natural language** instead of technical commands
- **Guided workflows** for feature creation
- **Auto-generated artifacts** (commit messages, PRDs, plans)
- **Safety confirmations** for destructive operations

### 5. Self-Documenting System
A learning configuration that improves itself:
- **Conversation analysis** extracts patterns and decisions automatically
- **CLAUDE.md updates** keep documentation synchronized with reality
- **Continuous learning** from every development session
- **Pattern recognition** identifies architectural best practices
- **Knowledge accumulation** builds better context for future work

## Support

### Getting Help
- Use `/vcs:help` for VCS command documentation
- Use `/feature-list` to see all feature management commands
- Check `.claude/commands/` for detailed command specifications
- Agents automatically provide guidance in their domains

### Command Discovery
- Type `/` in Claude Code to see all available commands
- Use `/commands-manager` to create custom commands
- Explore `.claude/commands/` directory for examples

---

**Software 3.0** - Where AI understands your intent, provides expert guidance, and handles the technical complexity while you focus on building great products.