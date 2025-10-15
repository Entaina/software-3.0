---
argument-hint: <task-description>
description: Load relevant context before starting a task
---

# Load Context

Retrieve relevant architectural knowledge and context before starting implementation, refactoring, or planning tasks.

**Usage**: `/contexts:load <task-description>`

**Example**: `/contexts:load "Implement user authentication with JWT tokens"`

## What This Command Does

This command delegates to the @context-engineer agent to retrieve relevant context documentation for your task. The agent will search and provide appropriate ADRs, specs, conventions, and related contexts from `.contexts/`.

## Implementation

Launch the context-engineer agent with the user's task:

**Task**: "Retrieve relevant context for: $ARGUMENTS"

The context-engineer agent will autonomously:
- Identify what context is relevant to the task
- Search through `.contexts/` for applicable documentation
- Provide context packages with ADRs, specs, conventions, etc.
- Prioritize current/active contexts over historical ones

## Success Criteria

- Context-engineer completes retrieval successfully
- User receives relevant context package for their task
- Context provided is current and actionable
