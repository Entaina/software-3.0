---
argument-hint: [change-description]
description: Update context based on code changes
---

# Update Context

Automatically update architectural context based on changes made to the codebase.

**Usage**: `/contexts:update [change-description]`

**Examples**:
- `/contexts:update "Migrated from PayPal to Stripe for payments"`
- `/contexts:update` (auto-detect from recent changes)

## What This Command Does

This command delegates to the @context-engineer agent to update context documentation based on code changes. The agent will analyze changes and update or supersede relevant contexts in `.contexts/`.

## Implementation

Launch the context-engineer agent with change information:

**Task**: "Update context based on changes: $ARGUMENTS"

The context-engineer agent will autonomously:
- Analyze what changed in the codebase
- Identify which contexts need updates
- Update or supersede ADRs when decisions change
- Archive obsolete documentation
- Maintain context accuracy and currency

## Success Criteria

- Context-engineer completes updates successfully
- User receives summary of updated/superseded context documents
- All contexts accurately reflect current state
