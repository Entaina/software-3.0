---
argument-hint: [session-summary]
description: Save session context and document decisions made
---

# Save Context

Document the work completed in the current session, capturing architectural decisions, patterns, and learnings.

**Usage**: `/contexts:save [session-summary]`

**Examples**:
- `/contexts:save "Implemented payment processing with Stripe"`
- `/contexts:save` (auto-detect from session)

## What This Command Does

This command delegates to the @context-engineer agent to capture session context. The agent will analyze what was accomplished and document relevant decisions, patterns, and learnings in `.contexts/`.

## Implementation

Launch the context-engineer agent with session information:

**Task**: "Document session context: $ARGUMENTS"

The context-engineer agent will autonomously:
- Analyze the session to identify significant work
- Create or update ADRs for architectural decisions made
- Update specs and conventions if new patterns were established
- Document learnings and important context for future sessions

## Success Criteria

- Context-engineer completes documentation successfully
- User receives summary of created/updated context documents
- Session decisions are properly captured in `.contexts/`
