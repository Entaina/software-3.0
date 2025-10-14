# /implement-code

*Implements the next uncompleted task from the organized technical implementation plan with full codebase context.*

## Auto-Loaded Project Context:
@/CLAUDE.md
@/docs/ai-context/project-structure.md
@/docs/ai-context/docs-overview.md

## Command Overview

You are an experienced Software Engineer tasked with building a new feature. Your goal is to implement the next uncompleted task in the organized technical implementation plan while leveraging deep codebase understanding and following established Rails patterns.

User provided implementation context: "$ARGUMENTS"

## Step 1: Prerequisites and Context Loading

### Required Input Documents
1. **Product context**: `docs/product-development/resources/product.md`
2. **JTBD analysis**: `docs/product-development/current-feature/JTBD.md`
3. **PRD requirements**: `docs/product-development/current-feature/PRD.md`
4. **Organized Implementation Plan**: `docs/product-development/current-feature/plan-organized.md`

### Validate Prerequisites
- **Confirm plan-organized.md exists**: If missing, inform user to run `/organize-plan` first
- **Read organized implementation plan**: Identify next uncompleted task
- **Understand feature context**: Use JTBD and PRD for user workflow understanding
- **Load Rails architecture context**: Use auto-loaded files for implementation patterns

### Error Handling for Missing Prerequisites
If any required documents are missing:
- **Organized plan missing**: "Please run `/organize-plan` first to structure implementation tasks"
- **PRD missing**: "Please run `/create-prd` first to define product requirements"
- **Context missing**: "Please ensure complete product development documentation exists"

## Step 2: Identify Next Implementation Task

### Parse Implementation Progress
From plan-organized.md, identify:
- **Completed tasks**: Tasks marked as done with checkboxes [x]
- **Next uncompleted task**: First task marked as todo [ ] in logical sequence
- **Task context**: Which feature capability the task belongs to
- **Task dependencies**: Whether prerequisites are completed

### Validate Task Readiness
Before implementing, ensure:
- **Dependencies completed**: All prerequisite tasks are marked as done
- **Context is clear**: Task description provides sufficient implementation guidance
- **Rails patterns understood**: Implementation approach aligns with existing codebase

### Handle Task Selection Edge Cases
- **No uncompleted tasks**: Inform user that implementation is complete
- **Dependencies not met**: Identify which prerequisite tasks need completion first
- **Ambiguous task**: Request clarification on implementation approach
- **Multiple parallel options**: Suggest logical next task based on feature capability flow

## Step 3: Enhanced Context Analysis for Implementation

### Intelligent Implementation Strategy Decision

Think deeply about the optimal implementation approach based on the specific task and auto-loaded project context. Based on the identified task AND the auto-loaded project context, intelligently decide the optimal approach:

#### Strategy Options:

**Direct Implementation** (0-1 sub-agents):
- Standard Rails CRUD operations following established patterns
- Simple service implementations using existing Service Actor patterns
- Straightforward frontend additions using established Hotwire patterns
- Minor modifications to existing features with clear precedents

**Focused Analysis** (2-3 sub-agents):
- Complex business logic requiring careful architecture decisions
- New integration patterns not yet established in the codebase
- Frontend features requiring novel Stimulus controller patterns
- Database changes with performance or migration complexity

**Comprehensive Analysis** (3+ sub-agents):
- Major architectural additions affecting multiple system areas
- Complex integrations with external services requiring OAuth/webhook setup
- Advanced AI/LLM features requiring LangChain.rb pattern extensions
- Multi-tenant features requiring careful permission and isolation design

### For Sub-Agent Approaches: Autonomous Implementation Analysis

You have complete autonomy to design sub-agents based on the specific implementation task. Consider these investigation areas and design custom agents to cover what's most relevant:

**Core Investigation Areas to Consider:**
- **Existing Pattern Analysis**: How similar features are implemented in the current codebase
- **Rails Convention Research**: Best practices for the specific type of implementation
- **Integration Point Investigation**: How this connects with existing system components
- **Multi-Tenant Implementation Analysis**: Account isolation and permission patterns for this feature
- **Testing Strategy Development**: RSpec patterns and test coverage approach
- **Performance and Security Analysis**: Optimization and security considerations for implementation

**Autonomous Sub-Agent Design Principles:**
- **Implementation-Focused**: Agents should provide actionable code and pattern guidance
- **Context-Aware**: Leverage understanding of existing Rails application patterns
- **Quality-Oriented**: Ensure implementation follows established coding standards
- **Risk-Conscious**: Identify potential issues before they become problems

**Sub-Agent Task Template:**
```
Task: "Analyze [SPECIFIC_IMPLEMENTATION_AREA] for implementing [TASK_DESCRIPTION] in the Rails application"

Standard Investigation Workflow:
1. Read /CLAUDE.md - **CRITICAL:** AI instructions, coding standards, and development protocols
2. Read /docs/ai-context/project-structure.md - **CRITICAL:** Technology stack and architecture patterns
3. Read /docs/ai-context/docs-overview.md - **CRITICAL:** Documentation architecture understanding
4. Search existing codebase for similar implementation patterns
5. [CUSTOM_ANALYSIS_STEPS] - Investigate the specific implementation area thoroughly
6. Return actionable implementation guidance with code examples and file paths

Return comprehensive implementation guidance for this specific area."
```

**CRITICAL: When launching sub-agents, always use parallel execution with a single message containing multiple Task tool invocations.**

## Step 4: Implementation Execution

### For Sub-Agent Approaches:
Think deeply about integrating findings from all sub-agent investigations for optimal implementation. Combine findings from all agents to execute optimal implementation:

**Integration Analysis:**
- **Pattern Guidance**: Use Pattern Analysis Agent's existing implementation examples
- **Rails Conventions**: Apply Rails Convention Agent's best practice recommendations
- **Integration Strategy**: Implement Integration Point Agent's connection approaches
- **Multi-Tenant Design**: Execute Multi-Tenant Agent's isolation and permission patterns
- **Testing Approach**: Follow Testing Strategy Agent's RSpec and coverage guidelines
- **Quality Assurance**: Implement Performance/Security Agent's optimization recommendations

### For Direct Implementation:
Use the task description and auto-loaded project context to implement directly.

### Implementation Execution Process

1. **Create/Modify Files**: Follow Rails conventions and existing patterns
2. **Implement Business Logic**: Use Service Actor patterns for complex operations
3. **Add Frontend Features**: Follow Hotwire/Stimulus patterns for interactive elements
4. **Create Database Changes**: Generate migrations following multi-tenant patterns
5. **Add Test Coverage**: Create RSpec tests following project testing patterns
6. **Update Documentation**: Update relevant CLAUDE.md files if patterns change

### Rails-Specific Implementation Guidelines

**Backend Implementation:**
- **Models**: Follow multi-tenant patterns with `acts_as_tenant`
- **Services**: Use Service Actor gem for business logic organization
- **Controllers**: Follow Rails RESTful conventions and authentication patterns
- **Jobs**: Use Solid Queue for background processing
- **APIs**: Follow established API patterns and serialization

**Frontend Implementation:**
- **Views**: Use Rails helpers and Hotwire Turbo patterns
- **Stimulus**: Create controllers following existing naming and organization
- **Styling**: Use TailwindCSS following the established design system
- **JavaScript**: Minimize custom JavaScript, prefer Stimulus patterns

**Integration Implementation:**
- **OAuth**: Follow existing OAuth integration patterns
- **Webhooks**: Use established webhook processing patterns
- **External APIs**: Follow HTTP client patterns and error handling
- **Email**: Use Action Mailbox patterns for inbound email processing

## Step 5: Code Quality and Testing

### Implementation Quality Standards
Ensure implementation follows:
- **Coding standards**: Follow Standard Ruby and project-specific conventions
- **Security practices**: Implement proper authentication, authorization, and data protection
- **Performance optimization**: Use efficient queries and caching where appropriate
- **Error handling**: Provide proper error handling and user feedback
- **Accessibility**: Follow web accessibility standards in frontend implementation

### Testing Implementation
Create comprehensive test coverage:
- **Unit tests**: RSpec tests for models, services, and business logic
- **Integration tests**: Request tests for controllers and API endpoints
- **System tests**: Feature tests for complete user workflows
- **Multi-tenant tests**: Verify account isolation and permission enforcement

### Code Review Preparation
Before marking task complete:
- **Self-review**: Check implementation against Rails conventions and project patterns
- **Test execution**: Run test suite to ensure no regressions
- **Manual testing**: Verify functionality works as expected in development
- **Documentation updates**: Update relevant documentation for any new patterns

## Step 6: Progress Tracking and Documentation

### Update Implementation Plan
1. **Mark current task as completed**: Update checkbox in plan-organized.md
2. **Add implementation notes**: Include any important decisions or deviations
3. **Update dependencies**: Mark any downstream tasks as ready if applicable
4. **Document issues**: Note any blockers or issues encountered

### Documentation Updates
If implementation introduces new patterns:
- **Update CLAUDE.md files**: Document new patterns in appropriate tier
- **Update API documentation**: Add new endpoints or modify existing ones
- **Update README**: Add any new setup or configuration requirements

### Prepare for Code Review
Set up for quality assurance:
- **Commit changes**: Create clear, descriptive commit messages
- **Prepare review context**: Summarize what was implemented and why
- **Identify review focus**: Highlight areas needing particular attention
- **Document testing approach**: Explain how the implementation was validated

## Step 7: Next Steps and Handoff

### Implementation Completion Summary
Provide clear summary:
- **Task completed**: Specific task that was implemented
- **Files modified**: List of files created or changed
- **Testing added**: Test coverage created
- **Next recommended task**: Suggested next implementation task

### Integration with Quality Workflow
After implementation, recommend:
- **commit-review**: For code quality validation
- **architecture-review**: For complex implementations affecting multiple components
- **refactor**: If technical debt was identified during implementation
- **update-docs**: If broader documentation updates are needed

### Continuous Improvement
Track implementation learnings:
- **Pattern refinements**: Improvements to existing implementation patterns
- **Tooling gaps**: Areas where better tooling could improve efficiency
- **Documentation gaps**: Areas where better documentation would help future implementation

## Error Handling and Edge Cases

**If task description is insufficient:**
- Request clarification on implementation requirements
- Suggest breaking complex tasks into smaller, more specific subtasks
- Provide implementation alternatives and ask for direction

**If implementation reveals design issues:**
- Document the design concern clearly
- Propose alternative approaches
- Suggest updating the organized plan to address the issue

**If testing reveals integration problems:**
- Identify the root cause of integration issues
- Propose fixes for both current implementation and affected systems
- Update documentation to prevent similar issues

## Integration with Development Workflow

This implementation approach ensures:
1. **Systematic progress**: Logical advancement through organized implementation plan
2. **Quality implementation**: Following Rails conventions and project patterns
3. **Comprehensive testing**: Proper test coverage and validation
4. **Documentation maintenance**: Keeping project documentation current
5. **Team coordination**: Clear progress tracking and handoff preparation

The implementation maintains alignment with user needs (JTBD/PRD) while ensuring technical quality and system integration.

Now proceed to implement the next task from the organized plan: $ARGUMENTS