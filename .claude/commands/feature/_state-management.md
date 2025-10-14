# Feature State Management Protocol

*Shared state management functions for all feature commands. Include this file in command prerequisites.*

## Purpose

This module defines the unified state management paradigm that all feature commands must follow to ensure consistency across filesystem, state file, and current context.

## Core Principles

1. **Filesystem is Source of Truth**: Directories and files are the authoritative state
2. **State File is Materialized View**: `.feature-state.json` is a cache for query optimization
3. **Current Context is Pointer**: `current-feature` file points to the active working feature
4. **Consistency is Maintained**: Every command updates all three layers synchronously

## State File Structure

Location: `docs/product-development/.feature-state.json`

```json
{
  "version": "1.0",
  "current_feature": "feature-name-or-empty",
  "last_updated": "2025-10-14T10:30:00Z",
  "features": {
    "feature-name": {
      "name": "feature-name",
      "description": "Brief description",
      "status": "active|archived|trashed",
      "created_at": "2025-10-14",
      "updated_at": "2025-10-14",
      "archived_at": null,
      "trashed_at": null,

      "workflow": {
        "current_stage": "definition|design|planning|development|complete",
        "stages_completed": ["definition"],
        "next_recommended_command": "/feature-switch [name]"
      },

      "documents": {
        "feature_md": {"exists": true, "last_modified": "2025-10-14"},
        "jtbd_md": {"exists": false, "last_modified": null},
        "prd_md": {"exists": false, "last_modified": null},
        "plan_md": {"exists": false, "last_modified": null},
        "plan_organized_md": {"exists": false, "last_modified": null}
      },

      "implementation": {
        "total_tasks": 0,
        "completed_tasks": 0,
        "in_progress_task": null,
        "last_implementation": null
      }
    }
  }
}
```

## Workflow Stages

```
definition → design → planning → development → complete
    ↓          ↓         ↓           ↓            ↓
feature.md  JTBD.md   plan.md   code commits   archived
           PRD.md   plan-org.md
```

### Stage Completion Criteria

- **definition**: feature.md exists
- **design**: JTBD.md and PRD.md exist
- **planning**: plan.md and plan-organized.md exist
- **development**: implementation in progress (tasks being completed)
- **complete**: all tasks in plan-organized.md are done

## Standard Functions (Use in Every Command)

### Function 1: Load Current State

**When to use**: At the beginning of every command (Step 1)

```markdown
## Step 1: Load Current State

### Read Current Context
1. Read `docs/product-development/current-feature` file
   - If file doesn't exist: current_feature = ""
   - If file is empty: current_feature = ""
   - Otherwise: current_feature = file contents (trimmed)

### Load State File
2. Read `docs/product-development/.feature-state.json`
   - If file doesn't exist: Initialize empty state structure
   - If file is corrupted: Attempt recovery or initialize empty
   - Parse JSON into state object

### Validate Current Feature
3. If current_feature is set:
   - Check if feature exists in state.features
   - Verify directory exists at expected location:
     - `features/active/[name]/` OR
     - `features/archived/[name]/` OR
     - `features/trashed/[name]/`
   - If inconsistency found: Sync state (see Function 3)

### Return Context Object
4. Return: {
     current_feature: "name-or-empty",
     state: state_object,
     feature_exists: boolean,
     feature_status: "active|archived|trashed|not_found"
   }
```

### Function 2: Update State After Action

**When to use**: After any command that modifies features (Step 4+)

```markdown
## Step N: Update State Consistently

### Execute Filesystem Operations First
1. Perform all file/directory operations
   - Create/modify/move files
   - Create/move/delete directories
   - Verify operations succeeded

### Update State Object
2. Load current state (if not already loaded)
3. Update relevant fields in state.features[feature_name]:
   - Update timestamps (updated_at, etc.)
   - Update workflow.current_stage if changed
   - Update workflow.stages_completed if stage added
   - Update workflow.next_recommended_command
   - Update documents.*.exists and last_modified
   - Update implementation.* if relevant

### Write State File
4. Write updated state to `.feature-state.json`
   - Use pretty-printed JSON (indent: 2)
   - Validate write succeeded
   - Handle write errors gracefully

### Update Current Feature File (if needed)
5. If command changes current feature:
   - Write new feature name to `current-feature` file
   - Or clear file if no current feature

### Verify Consistency
6. Re-read state file to confirm changes
7. If verification fails: Log error and attempt retry
```

### Function 3: Sync State with Filesystem

**When to use**: When inconsistencies detected, or in status/list commands

```markdown
## Sync State with Filesystem Reality

### Scan Filesystem Directories
1. Scan `docs/product-development/features/active/`
   - List all subdirectories (feature names)
   - For each feature: status = "active"

2. Scan `docs/product-development/features/archived/`
   - List all subdirectories
   - For each feature: status = "archived"

3. Scan `docs/product-development/features/trashed/`
   - List all subdirectories
   - For each feature: status = "trashed"

### Update State for Each Found Feature
4. For each feature found in filesystem:
   - If not in state.features: Add new entry
   - If in state.features: Update/verify fields
   - Check which documents exist:
     - feature.md
     - JTBD.md
     - PRD.md
     - plan.md
     - plan-organized.md
   - Update documents.*.exists = true/false
   - Update documents.*.last_modified from filesystem
   - Verify status matches directory location

### Remove Orphaned State Entries
5. For each entry in state.features:
   - If directory doesn't exist in any location: Remove entry
   - Log removed entries for user awareness

### Update Workflow Stage
6. For each feature, infer workflow.current_stage:
   - If plan-organized.md exists: "development" or "complete"
   - Else if plan.md exists: "planning"
   - Else if PRD.md or JTBD.md exist: "design"
   - Else: "definition"

### Write Synchronized State
7. Save updated state to `.feature-state.json`
8. Return sync report: {
     features_added: count,
     features_removed: count,
     features_updated: count
   }
```

## Prerequisite Validation Patterns

### For Commands Requiring Current Feature

```markdown
## Prerequisite Validation

### Check Current Feature Set
1. Load current state (Function 1)
2. If current_feature is empty:
   - Error: "No current feature set"
   - Guidance: "Run /feature-switch [name] to set active feature"
   - Show available features: Run feature-list logic
   - Exit command

### Verify Feature is Active
3. Check state.features[current_feature].status
4. If status != "active":
   - Error: "Feature '[name]' is {status}, not active"
   - If archived: "Run /feature-restore [name] to reactivate"
   - If trashed: "Run /feature-restore [name] to recover"
   - Exit command

### Verify Feature Directory Exists
5. Check filesystem for `features/active/[current_feature]/`
6. If directory missing:
   - Error: "Feature directory not found"
   - Suggest: "State may be corrupted. Run /feature-status to diagnose"
   - Offer: "Sync state with /feature-list to rebuild"
   - Exit command
```

### For Commands with Document Prerequisites

```markdown
## Document Prerequisite Validation

### Required Documents (Hard Prerequisite)
For documents that MUST exist:
1. Check if file exists in filesystem
2. If missing:
   - Error: "[Document] is required but not found"
   - Guidance: "Run [command] to create it first"
   - Example: "PRD.md is required. Run /create-prd first"
   - Exit command

### Recommended Documents (Soft Prerequisite)
For documents that SHOULD exist:
1. Check if file exists in filesystem
2. If missing:
   - Warning: "[Document] not found (recommended for better results)"
   - Guidance: "Consider running [command] first"
   - Prompt: "Continue anyway? (not recommended)"
   - Allow user to proceed or exit
```

## Progress Visualization Standard

Use this format consistently across all commands:

```markdown
## Display Progress

Feature: [feature-name]
Status: [active|archived|trashed]
Progress: [████████░░] 80% (4/5 stages)

Workflow Stage: Development
✓ Definition (feature.md)
✓ Design (JTBD.md, PRD.md)
✓ Planning (plan.md, plan-organized.md)
▶ Development (3/10 tasks completed)
  Implementation: Last activity [X days ago]

Next Recommended: /implement-code
```

### Progress Calculation Formula

```
Total Stages: 5 (definition, design, planning, development, complete)

Stage Weights:
- definition: 10%
- design: 25% (JTBD + PRD)
- planning: 25% (plan + plan-organized)
- development: 35% (implementation tasks)
- complete: 5% (archiving)

Progress % = Sum of completed stage weights
```

## Error Recovery Guidance Pattern

When commands fail, provide actionable recovery:

```markdown
## Error Recovery Guidance

Error: [Specific error message]

What Happened:
[Clear explanation of what went wrong]

Recovery Options:
1. [Primary recommended action with command]
2. [Alternative action if applicable]
3. [Diagnostic action to understand issue]

Current State:
- Feature: [name]
- Stage: [current_stage]
- Completed: [list of completed documents]
- Missing: [list of missing prerequisites]

Need Help?
- Check feature status: /feature-status
- List all features: /feature-list
- Review this document: @.claude/commands/feature/_state-management.md
```

## State Update Examples by Command Type

### Lifecycle Command Example (feature-create)

```markdown
After creating feature directory and feature.md:

state.features[feature_name] = {
  "name": feature_name,
  "description": user_provided_description,
  "status": "active",
  "created_at": current_date,
  "updated_at": current_date,
  "archived_at": null,
  "trashed_at": null,
  "workflow": {
    "current_stage": "definition",
    "stages_completed": ["definition"],
    "next_recommended_command": "/feature-switch " + feature_name
  },
  "documents": {
    "feature_md": {"exists": true, "last_modified": current_date},
    "jtbd_md": {"exists": false, "last_modified": null},
    "prd_md": {"exists": false, "last_modified": null},
    "plan_md": {"exists": false, "last_modified": null},
    "plan_organized_md": {"exists": false, "last_modified": null}
  },
  "implementation": {
    "total_tasks": 0,
    "completed_tasks": 0,
    "in_progress_task": null,
    "last_implementation": null
  }
}
```

### Design Command Example (create-jtbd)

```markdown
After creating JTBD.md:

state.features[current_feature].workflow.stages_completed += ["jtbd"]
state.features[current_feature].workflow.current_stage = "design"
state.features[current_feature].workflow.next_recommended_command = "/create-prd"
state.features[current_feature].documents.jtbd_md = {
  "exists": true,
  "last_modified": current_date
}
state.features[current_feature].updated_at = current_date
```

### Planning Command Example (organize-plan)

```markdown
After creating plan-organized.md and counting tasks:

state.features[current_feature].workflow.stages_completed += ["plan_organized"]
state.features[current_feature].workflow.current_stage = "planning"
state.features[current_feature].workflow.next_recommended_command = "/implement-code"
state.features[current_feature].documents.plan_organized_md = {
  "exists": true,
  "last_modified": current_date
}
state.features[current_feature].implementation.total_tasks = task_count
state.features[current_feature].implementation.completed_tasks = 0
state.features[current_feature].updated_at = current_date
```

### Execution Command Example (implement-code)

```markdown
After completing one task:

state.features[current_feature].workflow.current_stage = "development"
state.features[current_feature].implementation.completed_tasks += 1
state.features[current_feature].implementation.last_implementation = current_timestamp
state.features[current_feature].documents.plan_organized_md.last_modified = current_date
state.features[current_feature].updated_at = current_date

If all tasks complete:
  state.features[current_feature].workflow.current_stage = "complete"
  state.features[current_feature].workflow.next_recommended_command = "/feature-archive " + feature_name
Else:
  state.features[current_feature].workflow.next_recommended_command = "/implement-code"
```

## Integration Instructions for Command Authors

To integrate this state management into your command:

1. **Add to prerequisites**: `@.claude/commands/feature/_state-management.md`
2. **Step 1**: Use "Load Current State" function
3. **Step 2+**: Add prerequisite validation as appropriate
4. **After main action**: Use "Update State After Action" function
5. **Before output**: Use "Progress Visualization Standard"
6. **On error**: Use "Error Recovery Guidance Pattern"

## Maintenance Notes

This state management protocol should be updated when:
- New workflow stages are added
- State structure changes
- New document types are introduced
- Error patterns need refinement

All feature commands should reference the latest version of this protocol to ensure consistency.
