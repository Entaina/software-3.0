# Create JTBD - Job-to-be-Done Analysis

Generate comprehensive Job-to-be-Done analysis for product features within the multi-feature development system.

**Usage**: `/project:create-jtbd [feature-name]`

## Implementation

Execute JTBD analysis for the specified feature or current active feature. The directory path should be already created using the create-feature command. This folder might or might not include a feature.md already. If it exists, this can be updated by this command.

User provided feature context: "$ARGUMENTS"

## Step 1: Prerequisites and Setup

### Required Resources
1. **Read product context**: `docs/product-development/resources/product.md`
2. **Read JTBD template**: `docs/product-development/resources/JTBD-template.md`
3. **Understand current product**: Use product.md to understand Brainsome's vision, users, and positioning

### Parse Feature Request
Analyze the user's input to determine:
- **Feature name**: Extract or create a descriptive kebab-case name
- **Feature scope**: Understand what functionality is being requested
- **User context**: Identify who would use this feature

### Determine Current Feature Directory
Read the current feature name from the already created feature directory:

1. **Read current feature**: Check `docs/product-development/current-feature` file for the active feature name
2. **Validate feature directory**: Ensure the feature directory exists in `docs/product-development/features/active/[feature-name]/`
3. **Use existing directory**: The directory should already be created by the create-feature command

```
docs/product-development/features/active/[feature-name]/
├── feature.md          # Original feature idea/request
├── JTBD.md            # This document (Jobs to be Done)
├── PRD.md             # Product Requirements (created later)
├── plan.md            # Technical implementation plan (created later)
└── plan-organized.md  # Organized implementation plan (created later)
```

**Important**: Use the feature name from `current-feature` file to construct the correct directory path.

## Step 2: Research and Context Gathering

### Product Context Analysis
Using the product.md file, understand:
- **Target audience**: Primary and secondary user types
- **Product positioning**: How this feature fits Brainsome's vision
- **Existing capabilities**: What features already exist
- **Success metrics**: How this aligns with product KPIs

### Feature Context Research
1. **Search existing codebase** for similar functionality
2. **Understand user workflows** related to this feature area
3. **Identify integration points** with existing Brainsome features
4. **Research user pain points** in the current system

## Step 3: Create Feature Documentation

### Update feature.md (if needed)
If feature.md exists, read it for context. If it needs updates based on the JTBD analysis, update it accordingly. The feature.md structure should maintain the original feature request for traceability.

## Step 4: Apply JTBD Template Framework

### Use Standardized Template
1. **Copy the JTBD template** from `docs/product-development/resources/JTBD-template.md`
2. **Adapt the template** to the specific feature context
3. **Follow the established structure** for consistency

### JTBD Analysis Process

**For each relevant JTBD item identified:**

1. **Job Statement**: Use format "As a [type of user], I want to [achieve a goal], so that I can [realize a benefit]"

2. **Context**: Specify when and where this job occurs in the Brainsome user journey

3. **Motivation**: Connect to user pain points identified in product research

4. **Current Alternatives**: Describe how users currently solve this problem (within Brainsome or external tools)

5. **Desired Outcome**: Define what success looks like from the user's perspective

6. **Priority Level**: Assess based on product strategy and user impact

### Integration with Brainsome Context
- **Account-level vs User-level**: Consider multi-tenant implications
- **Integration channels**: How this affects web, Telegram, Discord, email channels
- **Content processing**: How this relates to Brainsome's AI processing pipeline
- **User roles**: Consider different user types (account admins, team members, end users)

## Step 5: Quality and Validation

### JTBD Quality Standards
- **User-focused**: Written from user perspective, not technical perspective
- **Specific**: Concrete situations and outcomes, not generic statements
- **Measurable**: Clear success criteria that can be observed/measured
- **Grounded**: Based on actual user research and product context
- **Prioritized**: Clear indication of which jobs are most important

### Validation Checklist
Before finalizing the JTBD:
- [ ] Connects to Brainsome's target audience from product.md
- [ ] Addresses real user pain points in content processing/AI interaction
- [ ] Avoids technical implementation details
- [ ] Includes measurable success criteria
- [ ] Follows the established template structure
- [ ] Is understandable by non-technical stakeholders

## Step 6: Documentation Output

### File Creation
1. **Save JTBD analysis** to `docs/product-development/features/active/[feature-name]/JTBD.md`
2. **Use template structure** but populate with feature-specific content
3. **Include cross-references** to product.md where relevant

### Next Steps Preparation
The completed JTBD will be used by:
- **create-prd command**: To generate detailed product requirements
- **create-plan command**: To inform technical architecture decisions
- **Implementation team**: To maintain user focus during development

## Error Handling

**If templates are missing:**
- Inform user that template files need to be created first
- Provide guidance on setting up the product-development resources

**If feature context is insufficient:**
- Ask specific questions about user needs and pain points
- Research similar functionality in existing Brainsome features
- Focus on understanding the underlying user problem

**If feature scope is too broad:**
- Break down into multiple, focused JTBD analyses
- Prioritize based on product strategy and user impact
- Create separate feature documents if necessary

## Integration with Product Development Workflow

This JTBD analysis ensures that subsequent development work remains grounded in user needs:
1. **Product validation**: Stakeholders can validate user need
2. **Requirements definition**: PRD will be based on these user insights
3. **Technical planning**: Architecture decisions will consider user workflows
4. **Implementation tracking**: Development can reference user outcomes

Now proceed to create the JTBD analysis for: $ARGUMENTS
