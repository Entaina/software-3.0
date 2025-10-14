# /organize-plan

*Reorganizes technical implementation plan from infrastructure-focused to feature-capability-focused structure.*

## Auto-Loaded Project Context:
@/CLAUDE.md
@/docs/ai-context/project-structure.md
@/docs/ai-context/docs-overview.md
@.claude/commands/feature/_state-management.md

## Command Overview

You are a Software Engineer tasked with reorganizing a technical implementation plan. Your goal is to restructure the current implementation checklist from infrastructure-component organization into feature-capability groupings that consider dependencies and enable more logical development flow.

User provided context: "$ARGUMENTS"

## Step 1: Load Current State and Validate Prerequisites

### Load State (Use State Management Protocol)
1. Read `docs/product-development/current-feature` file to get active feature name
2. Read `docs/product-development/.feature-state.json` for feature metadata
3. Validate current feature is set and active
4. If current_feature is empty:
   - Error: "No current feature set"
   - Guidance: "Run /feature-switch [name] to set active feature"
   - List available features and exit

### Determine Feature Paths
5. Once feature name is confirmed, construct paths:
   - Feature directory: `docs/product-development/features/active/[feature-name]/`
   - plan.md: `docs/product-development/features/active/[feature-name]/plan.md`
   - plan-organized.md: `docs/product-development/features/active/[feature-name]/plan-organized.md` (will be created)

### Required Resources
6. **Product context**: `docs/product-development/resources/product.md` (recommended)

### Prerequisite Validation
7. **Required documents** (must exist):
   - plan.md: If missing, inform user to run `/create-plan` first

8. **Recommended documents** (should exist):
   - PRD.md: Warn if missing, for user-context perspective
   - JTBD.md: Warn if missing, for workflow understanding

### Error Handling for Missing Prerequisites
If any required documents are missing:
- **Current feature not set**: "No current feature set. Run: /feature-switch [name]"
- **Feature not active**: "Feature '[name]' is {status}. Run: /feature-restore [name]"
- **Plan missing**: "plan.md not found. Run: /create-plan first (required for organizing)"
- **Context incomplete**: Display feature status and suggest completing plan stage

## Step 2: Analyze Current Implementation Structure

### Extract Current Task Organization
From the existing plan.md, identify:
- **Backend Implementation tasks**: Rails-specific backend work
- **Frontend Implementation tasks**: Hotwire/Stimulus and UI work
- **Integration Implementation tasks**: External service connections
- **Testing Implementation tasks**: RSpec and quality assurance
- **Documentation tasks**: Documentation and deployment work

### Identify Infrastructure-Component Groupings
Current organization typically groups by:
- **Technology layer**: Backend vs Frontend vs Integration
- **System component**: Database vs API vs UI vs Jobs
- **Development phase**: Foundation vs Logic vs Interface vs Testing

### Assess Current Dependencies
Analyze existing task structure for:
- **Sequential dependencies**: Tasks that must be completed before others
- **Parallel opportunities**: Tasks that can be worked on simultaneously
- **Cross-component dependencies**: How different system parts interact
- **Risk dependencies**: Tasks that might block others if they fail

## Step 3: Feature-Capability Analysis

### Define User-Facing Capabilities
Using JTBD and PRD context, identify:
- **Primary user workflows**: Main user journeys and interactions
- **Core feature capabilities**: Distinct functional areas users will experience
- **Supporting capabilities**: Technical features that enable user-facing functionality
- **Integration capabilities**: External service interactions that deliver user value

### Map Technical Tasks to User Capabilities
For each user-facing capability, identify:
- **Required backend tasks**: Models, services, APIs needed
- **Required frontend tasks**: Controllers, views, JavaScript needed
- **Required integration tasks**: External service connections needed
- **Required testing tasks**: Test coverage for the capability
- **Required documentation**: Documentation updates for the capability

### Consider Rails-Specific Dependency Patterns
Account for Rails architecture dependencies:
- **Model-first dependencies**: Database and model creation before service logic
- **Service-before-controller**: Business logic before API endpoints
- **API-before-frontend**: Backend endpoints before frontend integration
- **Integration sequencing**: OAuth setup before API calls
- **Multi-tenant considerations**: Account-level setup before user features

## Step 4: Create Feature-Capability Structure

### Reorganization Framework

Restructure tasks into logical feature groupings:

```markdown
# [Feature Name] - Organized Implementation Plan

## Implementation Overview
[Brief summary of reorganization approach and capability groupings]

## Feature Capability 1: [Primary User Workflow]

### User Value
[What user capability this enables, referencing JTBD]

### Implementation Tasks
#### Foundation (Must Complete First)
- [ ] [Database/model tasks that other tasks depend on]
- [ ] [Core service setup that enables functionality]

#### Core Functionality
- [ ] [Business logic implementation]
- [ ] [API endpoint creation]
- [ ] [Background job setup if needed]

#### User Interface
- [ ] [Frontend controller and view creation]
- [ ] [Hotwire/Stimulus interactive features]
- [ ] [CSS styling and responsive design]

#### Testing & Validation
- [ ] [Unit tests for models and services]
- [ ] [Integration tests for full workflow]
- [ ] [Multi-tenant test coverage]

### Dependencies
- **Internal**: [Other capabilities this depends on]
- **External**: [Third-party services or setup required]

### Risk Factors
- [Potential blockers or challenges for this capability]

## Feature Capability 2: [Secondary User Workflow]
[Continue same structure]

## Supporting Infrastructure

### Cross-Capability Requirements
- [ ] [Tasks that support multiple capabilities]
- [ ] [Infrastructure setup needed across features]
- [ ] [Security and permission framework]

### Integration Framework
- [ ] [OAuth and authentication setup]
- [ ] [Webhook infrastructure]
- [ ] [External service configuration]

### Documentation and Deployment
- [ ] [CLAUDE.md updates for new patterns]
- [ ] [API documentation updates]
- [ ] [Environment configuration]
- [ ] [Migration deployment plans]

## Implementation Sequence Recommendation

### Phase 1: Foundation
[Which capabilities to implement first and why]

### Phase 2: Core Features
[Primary user workflows and their dependencies]

### Phase 3: Enhanced Capabilities
[Secondary features and optimizations]

### Parallel Development Opportunities
[Tasks that can be worked on simultaneously by different developers]
```

## Step 5: Dependency and Risk Analysis

### Cross-Capability Dependencies
Identify dependencies between feature capabilities:
- **Shared models**: Which capabilities depend on the same data structures
- **Shared services**: Which capabilities use common business logic
- **Integration dependencies**: Which capabilities require the same external services
- **User permission dependencies**: Which capabilities share authentication/authorization

### Internal Package Dependencies
Consider Rails application internal dependencies:
- **Gem dependencies**: New gems needed and their impact
- **Configuration dependencies**: Settings and environment variables
- **Database dependencies**: Migration sequencing and schema changes
- **Asset dependencies**: JavaScript, CSS, and image requirements

### Risk Mitigation Planning
For each identified risk:
- **Dependency risk**: What happens if dependent tasks are delayed
- **Integration risk**: Fallback plans for external service issues
- **Complexity risk**: Simplified alternatives for complex implementations
- **Performance risk**: Monitoring and optimization strategies

## Step 6: Enhanced Task Specification

### Detailed Task Enhancement
For each reorganized task, provide:
- **Specific file paths**: Exact Rails files to create or modify
- **Acceptance criteria**: Clear definition of task completion
- **Testing requirements**: How to verify the task works correctly
- **Integration points**: How this task connects with others

### Rails Pattern Alignment
Ensure reorganized tasks follow:
- **Service Actor patterns**: Proper business logic organization
- **Multi-tenant patterns**: Account isolation and user roles
- **Hotwire patterns**: Turbo and Stimulus integration approaches
- **Testing patterns**: RSpec and factory patterns used in the project

### Quality Assurance Integration
Include quality checkpoints:
- **Code review points**: When to pause for architectural review
- **Integration testing milestones**: When to test cross-capability functionality
- **Performance validation**: When to check scalability and optimization
- **Security review**: When to validate authentication and authorization

## Step 7: Documentation Output

### File Creation
1. **Save organized plan** to `docs/product-development/features/active/[feature-name]/plan-organized.md`
2. **Maintain traceability** to original plan.md and PRD requirements
3. **Include implementation sequence** and dependency rationale
4. **Count total tasks** in the organized plan for progress tracking

### Update Feature State (Use State Management Protocol)
5. Load current `.feature-state.json`
6. Count total tasks from plan-organized.md (count [ ] checkboxes)
7. Update the feature's state:
   ```
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
8. Write updated state to `.feature-state.json`

### Display Progress (Use State Management Protocol)
9. Show progress visualization:
   ```
   Feature: [feature-name]
   Status: active
   Progress: [████████░░] 85% (4.25/5 stages)

   Workflow Stage: Planning Complete
   ✓ Definition (feature.md)
   ✓ Design - JTBD Analysis (JTBD.md)
   ✓ Design - Product Requirements (PRD.md)
   ✓ Planning - Technical Plan (plan.md)
   ✓ Planning - Organized Plan (plan-organized.md)
   ▶ Development - Implementation (next)

   Implementation Ready:
   - Total Tasks: [X]
   - Ready to implement: /implement-code

   Next Recommended: /implement-code
   ```

### Reorganization Summary
Provide summary of changes:
- **Capability groupings**: How tasks were regrouped by user value
- **Dependency improvements**: How new structure improves development flow
- **Risk mitigation**: How organization reduces implementation risk
- **Parallel opportunities**: How multiple developers can work efficiently

## Step 8: Preparation for Implementation

### Implementation Readiness
The organized plan prepares for:
- **implement-code command**: Clear next-step guidance for development
- **Team coordination**: Parallel development opportunities
- **Progress tracking**: Feature-capability milestone tracking
- **Risk management**: Early identification and mitigation of blockers

### Quality Integration Points
Identify integration points with existing quality commands:
- **architecture-review**: When to conduct comprehensive reviews
- **commit-review**: Regular code quality checkpoints
- **refactor**: Opportunities for code improvement
- **update-docs**: Documentation maintenance triggers

## Error Handling and Edge Cases

**If current plan lacks sufficient detail:**
- Request additional technical planning before reorganization
- Identify specific areas needing more detailed task breakdown
- Suggest iterative refinement of implementation approach

**If dependency analysis reveals circular dependencies:**
- Restructure to break circular dependencies
- Identify minimal viable implementation approaches
- Suggest architectural changes if needed

**If feature scope is too large for single reorganization:**
- Break into multiple feature capability sets
- Create phased implementation with clear milestones
- Ensure each phase delivers user value independently

## Integration with Development Workflow

This organized plan enables efficient implementation:
1. **Clear development sequence**: Logical order of implementation
2. **Parallel development**: Multiple team members can work simultaneously
3. **Risk mitigation**: Early identification and resolution of blockers
4. **User value delivery**: Each capability delivers measurable user benefit

The reorganization transforms infrastructure-focused tasks into user-centered implementation that maintains technical quality while optimizing for development efficiency and user value delivery.

Now proceed to organize the implementation plan for: $ARGUMENTS