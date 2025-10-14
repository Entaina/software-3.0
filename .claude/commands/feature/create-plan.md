# /create-plan

*Creates a comprehensive technical implementation plan enhanced with full codebase context analysis.*

## Auto-Loaded Project Context:
@/CLAUDE.md
@/docs/ai-context/project-structure.md
@/docs/ai-context/docs-overview.md

## Command Overview

You are a Technical Lead tasked with creating a comprehensive technical implementation plan for a new feature. Your goal is to translate product requirements into specific, actionable technical tasks while leveraging deep codebase understanding.

User provided feature context: "$ARGUMENTS"

## Step 1: Prerequisites and Context Gathering

### Required Input Documents
1. **Product context**: `docs/product-development/resources/product.md`
2. **Current feature**: Read `docs/product-development/current-feature` file for active feature name
3. **JTBD analysis**: `docs/product-development/features/active/[feature-name]/JTBD.md`
4. **PRD requirements**: `docs/product-development/features/active/[feature-name]/PRD.md`
5. **Feature background**: `docs/product-development/features/active/[feature-name]/feature.md`

### Validate Prerequisites
- **Check current feature**: If `current-feature` file is missing/empty, prompt user to specify feature
- **Confirm PRD exists**: If missing, inform user to run `/create-prd` first
- **Read product requirements**: Extract technical requirements from PRD
- **Understand user context**: Reference JTBD for user workflow understanding
- **Load project context**: Use auto-loaded files for Rails architecture understanding

### Error Handling for Missing Prerequisites
If any required documents are missing:
- **Current feature not set**: "Please specify the current feature name or update the current-feature file"
- **PRD missing**: "Please run `/create-prd` first to define product requirements"
- **JTBD missing**: "Please run `/create-jtbd` first to understand user needs"
- **Feature.md missing**: "Please ensure feature documentation exists in features/active/[feature-name] directory"

## Step 2: Enhanced Context Analysis with Full-Context Integration

### Intelligent Analysis Strategy Decision

Think deeply about the optimal technical analysis approach based on the PRD requirements and auto-loaded project context. Based on the feature requirements from the PRD AND the auto-loaded project context, intelligently decide the optimal approach:

#### Strategy Options:

**Direct Planning** (0-1 sub-agents):
- Simple features with clear Rails patterns (CRUD operations, basic integrations)
- Features with minimal cross-system dependencies
- Standard patterns already well-established in the codebase
- Low architectural complexity and risk

**Focused Analysis** (2-3 sub-agents):
- Moderate complexity features affecting multiple Rails components
- Features requiring new integrations or extending existing patterns
- Changes that span 2-3 architectural areas (frontend, backend, external services)
- Novel implementations that need careful architectural consideration

**Comprehensive Analysis** (3+ sub-agents):
- Complex features affecting multiple system areas and integrations
- Major architectural changes or new system capabilities
- Features requiring extensive Rails ecosystem integration
- High-risk implementations needing thorough dependency analysis

### For Sub-Agent Approaches: Autonomous Architecture Analysis

You have complete autonomy to design sub-agents based on the specific feature requirements. Consider these investigation areas and design custom agents to cover what's most relevant:

**Core Investigation Areas to Consider:**
- **Rails Architecture Analysis**: How this fits with existing Rails 8.0 + Jumpstart Pro patterns
- **Multi-Tenant Implementation**: Account isolation, user roles, data segregation strategies
- **Integration Points Mapping**: External services, APIs, webhooks, existing system connections
- **Database Design Analysis**: Schema changes, migrations, performance implications
- **AI/LLM Integration Planning**: LangChain.rb usage, content processing pipeline integration
- **Frontend Architecture Planning**: Hotwire/Stimulus implementation, UI component design
- **Background Processing Design**: Solid Queue integration, async operation patterns
- **Security and Performance Analysis**: Authentication, authorization, scalability considerations

**Autonomous Sub-Agent Design Principles:**
- **Custom Specialization**: Define agents based on the specific feature's technical complexity
- **Flexible Agent Count**: Use as many agents as needed - scale based on actual architectural scope
- **Adaptive Coverage**: Ensure all critical technical aspects are covered without unnecessary overlap
- **Implementation-Focused Analysis**: Prioritize investigation that directly supports actionable technical planning

**Sub-Agent Task Template:**
```
Task: "Analyze [SPECIFIC_TECHNICAL_AREA] for comprehensive technical planning of [FEATURE] based on PRD requirements: [PRD_SUMMARY]"

Standard Investigation Workflow:
1. Read /CLAUDE.md - **CRITICAL:** AI instructions, coding standards, and development protocols
2. Read /docs/ai-context/project-structure.md - **CRITICAL:** Technology stack and architecture patterns
3. Read /docs/ai-context/docs-overview.md - **CRITICAL:** Documentation architecture understanding
4. Read the PRD requirements to understand technical scope
5. [CUSTOM_ANALYSIS_STEPS] - Investigate the specific technical area thoroughly
6. Return actionable findings that support comprehensive technical planning

Return comprehensive findings addressing this technical area for implementation planning."
```

**CRITICAL: When launching sub-agents, always use parallel execution with a single message containing multiple Task tool invocations.**

## Step 3: Synthesize Technical Architecture

### For Sub-Agent Approaches:
Think deeply about integrating findings from all sub-agent investigations for optimal technical implementation planning. Combine findings from all agents to create comprehensive technical architecture:

**Integration Analysis:**
- **Rails Architecture**: Use Architecture Analysis Agent's patterns and conventions
- **Multi-Tenancy**: Apply Multi-Tenant Agent's isolation and permission strategies
- **Integrations**: Implement Integration Points Agent's external service connections
- **Data Design**: Execute Database Analysis Agent's schema and migration plans
- **AI/LLM Systems**: Leverage AI Integration Agent's LangChain.rb patterns
- **Frontend Implementation**: Apply Frontend Agent's Hotwire/Stimulus designs
- **Background Processing**: Implement Async Processing Agent's job queue strategies

**Technical Decision Framework:**
Based on synthesized analysis, determine:
- **Architecture patterns**: Which Rails patterns and conventions to follow
- **Implementation approach**: Phased rollout vs. complete implementation
- **Integration strategy**: How to connect with existing systems
- **Data modeling**: Database changes and migration approach
- **Performance considerations**: Scalability and optimization requirements

### For Direct Planning:
Use the PRD requirements and auto-loaded project context to create technical architecture directly.

## Step 4: Create Comprehensive Technical Plan

### Technical Implementation Plan Structure

```markdown
# [Feature Name] - Technical Implementation Plan

## Feature Summary
[Brief overview connecting PRD requirements to technical approach]

## Architecture Overview

### System Integration Points
[How this feature integrates with existing Rails architecture]

### Multi-Tenant Considerations
[Account isolation, user permissions, data segregation approach]

### Technology Stack Usage
[How this leverages Rails 8.0, Jumpstart Pro, and existing integrations]

## Key Technical Decisions

### Framework and Pattern Choices
[Service Actor patterns, resource processing integration, AI/LLM usage]

### Database Design
[Schema changes, migrations, indexing, performance considerations]

### Frontend Implementation
[Hotwire/Stimulus patterns, UI components, user experience implementation]

### Background Processing
[Solid Queue integration, async operations, job scheduling]

### External Service Integration
[API connections, OAuth flows, webhook handling]

### Security Implementation
[Authentication, authorization, data protection, compliance]

## Dependencies & Assumptions

### Internal Dependencies
[Existing Rails features, components, and services this depends on]

### External Dependencies
[Third-party services, APIs, libraries, infrastructure requirements]

### Technical Assumptions
[Assumptions about system capacity, user load, data volume]

## Implementation Checklist

### Backend Implementation
- [ ] [Specific Rails backend task with file references]
- [ ] [Database migration and model changes]
- [ ] [Service Actor implementation for business logic]
- [ ] [API endpoint creation following Rails conventions]
- [ ] [Background job implementation with Solid Queue]
- [ ] [Integration with existing LLM/AI processing pipeline]

### Frontend Implementation
- [ ] [Hotwire/Stimulus controller creation]
- [ ] [View template implementation with Rails helpers]
- [ ] [TailwindCSS styling following design system]
- [ ] [JavaScript interactions and real-time features]
- [ ] [Mobile responsiveness and accessibility]

### Integration Implementation
- [ ] [External service OAuth/API integration]
- [ ] [Webhook endpoint creation and processing]
- [ ] [Email/notification system integration]
- [ ] [Multi-channel support (web, Telegram, Discord)]

### Testing Implementation
- [ ] [RSpec test suite creation following project patterns]
- [ ] [Factory creation for test data]
- [ ] [Integration test implementation]
- [ ] [Multi-tenant test coverage]
- [ ] [Security and permission testing]

### Documentation and Deployment
- [ ] [Update relevant CLAUDE.md files in 3-tier system]
- [ ] [API documentation updates]
- [ ] [Environment variable configuration]
- [ ] [Database migration deployment plan]
- [ ] [Feature flag implementation if needed]

## Risk Assessment and Mitigation

### Technical Risks
[Potential implementation challenges and mitigation strategies]

### Performance Risks
[Scalability concerns and optimization approaches]

### Security Risks
[Security considerations and protection strategies]

### Integration Risks
[External service dependencies and fallback plans]

## Implementation Phases

### Phase 1: Core Foundation
[Database, models, basic service implementation]

### Phase 2: Business Logic
[Service Actor implementation, core feature functionality]

### Phase 3: User Interface
[Frontend implementation, user experience]

### Phase 4: Integration and Polish
[External integrations, testing, documentation]

---

*This technical plan was created based on PRD requirements and comprehensive Rails architecture analysis.*
```

## Step 5: Technical Quality Assurance

### Implementation Plan Quality Checklist
- [ ] All PRD requirements are addressed with specific technical tasks
- [ ] Rails architecture patterns are followed consistently
- [ ] Multi-tenancy implications are properly handled
- [ ] Integration points with existing systems are identified
- [ ] Security and performance considerations are addressed
- [ ] Implementation tasks are specific and actionable
- [ ] Dependencies and risks are clearly identified
- [ ] Testing strategy covers all critical functionality

### Technical Feasibility Validation
Ensure the plan addresses:
- **Rails compatibility**: Works with Rails 8.0 and Jumpstart Pro patterns
- **System integration**: Properly integrates with existing architecture
- **Scalability**: Can handle expected load and growth
- **Maintainability**: Follows established coding standards and patterns
- **Security**: Implements proper authentication, authorization, and data protection

## Step 6: Documentation Output and Integration

### File Creation
1. **Save technical plan** to `docs/product-development/features/active/[feature-name]/plan.md`
2. **Reference PRD requirements** throughout the implementation plan
3. **Include specific file paths** and Rails conventions
4. **Update feature.md** to mark technical planning as completed

### Preparation for Next Steps
The completed technical plan will be used by:
- **organize-plan command**: To restructure tasks by feature capability
- **implement-code command**: For step-by-step implementation guidance
- **Development team**: For sprint planning and task assignment
- **Architecture review**: For technical validation and approval

## Error Handling and Edge Cases

**If PRD requirements are insufficient:**
- Request clarification on specific technical requirements
- Identify gaps in product requirements that affect technical implementation
- Flag areas needing product stakeholder input

**If technical complexity exceeds expected scope:**
- Break implementation into smaller, manageable phases
- Identify areas requiring additional research or prototyping
- Suggest alternative approaches or simplified implementations

**If integration conflicts are identified:**
- Document conflicts clearly with existing systems
- Propose resolution strategies or architectural changes
- Flag for technical review and architectural decision

## Integration with Development Workflow

This technical plan serves as the foundation for implementation:
1. **Architecture validation**: Technical review of approach and decisions
2. **Task organization**: organize-plan will restructure for optimal implementation
3. **Implementation execution**: implement-code will reference specific tasks
4. **Progress tracking**: Development work will follow the structured checklist

The plan ensures that feature implementation follows Rails best practices while meeting all PRD requirements and integrating seamlessly with existing Brainsome architecture.

Now proceed to create the technical implementation plan for: $ARGUMENTS