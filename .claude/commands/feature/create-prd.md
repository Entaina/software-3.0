# /create-prd

*Creates a Product Requirements Document (PRD) based on JTBD analysis using standardized templates.*

## Auto-Loaded Project Context:
@/CLAUDE.md
@/docs/ai-context/project-structure.md
@/docs/ai-context/docs-overview.md
@.claude/commands/feature/_state-management.md

## Command Overview

You are a Product Manager tasked with creating a Product Requirements Document (PRD) for a new feature. Your goal is to translate user needs from the JTBD analysis into specific, actionable product requirements using the established PRD template.

User provided feature context: "$ARGUMENTS"

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
   - feature.md: `docs/product-development/features/active/[feature-name]/feature.md`
   - JTBD.md: `docs/product-development/features/active/[feature-name]/JTBD.md`
   - PRD.md: `docs/product-development/features/active/[feature-name]/PRD.md` (will be created)

### Required Resources
6. **Product context**: `docs/product-development/resources/product.md`
7. **PRD template**: `docs/product-development/resources/PRD-template.md`
   - If template missing: Warn user but continue with inline template

### Prerequisite Validation
8. **Required documents** (must exist):
   - feature.md: If missing, warn but allow proceeding

9. **Strongly recommended** (should exist):
   - JTBD.md: If missing, warn strongly and suggest running `/create-jtbd` first
   - Allow proceeding but note that PRD quality will be lower without JTBD

### Error Handling for Missing Prerequisites
If any required documents are missing:
- **Current feature not set**: "No current feature set. Run: /feature-switch [name]"
- **Feature not active**: "Feature '[name]' is {status}. Run: /feature-restore [name]"
- **JTBD strongly recommended**: "JTBD.md not found. Run: /create-jtbd first (strongly recommended for quality PRD)"
- **Context incomplete**: Display feature status and suggest completing JTBD stage

## Step 2: Analyze User Needs from JTBD

### Extract Key Insights
From the JTBD analysis, identify:
- **Primary user jobs**: The main tasks users are trying to accomplish
- **User personas**: Who will use this feature
- **Pain points**: Current frustrations and limitations
- **Success criteria**: How users will measure success
- **Priority levels**: Which jobs are most critical

### Connect to Product Strategy
Using product.md context:
- **Align with target audience**: Ensure feature serves primary/secondary users
- **Support product vision**: Connect feature to overall Brainsome mission
- **Leverage existing capabilities**: Build on current content processing and AI features
- **Consider success metrics**: How this impacts product KPIs

## Step 3: Technical Context Research

### Understand Current System
Before defining requirements, research the existing Rails application:

1. **Read auto-loaded project context** to understand:
   - Rails 8.0 + Jumpstart Pro architecture patterns
   - Multi-tenant structure with accounts and users
   - Existing integrations (Basecamp, Telegram, Discord, email)
   - AI/LLM processing capabilities with LangChain.rb

2. **Search for related functionality**:
   - Look for similar features that already exist
   - Identify reusable patterns and components
   - Understand integration points and dependencies
   - Review current user workflows and pain points

### Technical Integration Points
Consider how this feature integrates with:
- **Authentication & Authorization**: User roles and account-level permissions
- **Multi-tenancy**: Account isolation and data segregation
- **Content Processing**: Integration with resource processing pipeline
- **AI/LLM Systems**: Leveraging existing LlmActor patterns
- **External Services**: OAuth integrations, webhooks, API connections
- **UI Framework**: Hotwire/Stimulus patterns and TailwindCSS styling

## Step 4: Create PRD Using Template

### Use Standardized Template
1. **Copy PRD template** from `docs/product-development/resources/PRD-template.md`
2. **Populate each section** with feature-specific content
3. **Maintain template structure** for consistency across all PRDs
4. **Reference JTBD insights** throughout the document

### PRD Population Guidelines

**TL;DR Section:**
- Summarize the feature in 2-3 sentences
- Reference primary user need from JTBD
- State expected business impact

**Goals Section:**
- **Business Goals**: Connect to Brainsome's success metrics
- **User Goals**: Directly from JTBD analysis
- **Non-Goals**: Clear boundaries and scope limitations

**User Stories Section:**
- Translate JTBD job statements into user stories
- Use Brainsome user personas (knowledge workers, organizations)
- Include edge cases and error scenarios

**Functional Requirements Section:**
- Break down into specific, testable features
- Include acceptance criteria for each feature
- Consider Rails architecture implications

**Technical Considerations Section:**
- Performance requirements for multi-tenant architecture
- Security and privacy considerations
- Integration requirements with existing systems
- Technical constraints and dependencies

## Step 5: Rails-Specific Requirements Integration

### Multi-Tenant Considerations
- **Account-level features**: What operates at the tenant level
- **User-level features**: What operates at individual user level
- **Permission structure**: How this works with existing user roles
- **Data isolation**: How account separation is maintained

### Architecture Alignment
- **Service Actor Pattern**: How business logic will be organized
- **Resource Processing Pipeline**: Integration with existing content processing
- **Background Jobs**: Async operations using Solid Queue
- **API Design**: RESTful endpoints following Rails conventions
- **Database Design**: Schema changes and migration considerations

### Integration Requirements
- **Hotwire/Stimulus**: Frontend interaction patterns
- **LangChain.rb**: AI/LLM processing integration
- **External Services**: OAuth, webhooks, third-party APIs
- **Email Processing**: Action Mailbox integration if relevant
- **Real-time Features**: WebSocket/ActionCable considerations

## Step 6: Quality Assurance and Validation

### PRD Quality Checklist
- [ ] All requirements trace back to JTBD user needs
- [ ] Requirements are specific, measurable, and testable
- [ ] Technical considerations address Rails architecture
- [ ] Multi-tenancy implications are clearly defined
- [ ] Integration points with existing features are identified
- [ ] Success metrics align with product KPIs
- [ ] Template structure is followed consistently
- [ ] Acceptance criteria are clear and actionable

### Stakeholder Alignment
Ensure the PRD addresses:
- **Product-market fit**: Solves real user problems identified in JTBD
- **Technical feasibility**: Can be implemented with current Rails stack
- **Business viability**: Benefits justify development investment
- **User experience**: Creates seamless integration with existing features

## Step 7: Documentation Output and Integration

### File Creation
1. **Save PRD** to `docs/product-development/features/active/[feature-name]/PRD.md`
2. **Use template structure** with feature-specific content
3. **Include cross-references** to JTBD.md and product.md

### Update Feature State (Use State Management Protocol)
4. Load current `.feature-state.json`
5. Update the feature's state:
   ```
   state.features[current_feature].workflow.stages_completed += ["prd"]
   state.features[current_feature].workflow.current_stage = "design"
   state.features[current_feature].workflow.next_recommended_command = "/create-plan"
   state.features[current_feature].documents.prd_md = {
     "exists": true,
     "last_modified": current_date
   }
   state.features[current_feature].updated_at = current_date
   ```
6. Write updated state to `.feature-state.json`

### Display Progress (Use State Management Protocol)
7. Show progress visualization:
   ```
   Feature: [feature-name]
   Status: active
   Progress: [█████░░░░░] 50% (2.5/5 stages)

   Workflow Stage: Design
   ✓ Definition (feature.md)
   ✓ Design - JTBD Analysis (JTBD.md)
   ✓ Design - Product Requirements (PRD.md)
   ▶ Planning - Technical Plan (next)

   Next Recommended: /create-plan
   ```

### Preparation for Next Steps
The completed PRD will be used by:
- **create-plan command**: For technical architecture planning
- **Technical team**: For implementation guidance and sprint planning
- **QA/Testing**: For test case development and acceptance criteria
- **Stakeholders**: For feature validation and go/no-go decisions

## Error Handling and Edge Cases

**If JTBD analysis is incomplete:**
- Request completion of JTBD analysis first
- Identify specific gaps in user need understanding
- Do not proceed without clear user requirements

**If technical constraints conflict with user needs:**
- Document the conflict clearly in technical considerations
- Propose alternative approaches or phased implementation
- Flag for technical review and stakeholder discussion

**If feature scope is too large:**
- Break into multiple phases with separate PRDs
- Prioritize core functionality for initial implementation
- Create clear dependencies between phases

## Integration with Development Workflow

This PRD serves as the bridge between user needs (JTBD) and technical implementation:
1. **User needs validation**: Stakeholders confirm PRD addresses JTBD
2. **Technical planning**: Engineering team uses PRD for architecture decisions
3. **Implementation tracking**: Development work references PRD requirements
4. **Quality assurance**: Testing validates PRD acceptance criteria

The PRD ensures that technical implementation remains aligned with user needs while fitting within Brainsome's Rails architecture and product strategy.

Now proceed to create the PRD for: $ARGUMENTS