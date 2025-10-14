# /feature-status

*Shows detailed status and information about a specific feature.*

## Auto-Loaded Project Context:
@/docs/product-development/.feature-state.json
@/docs/product-development/current-feature

## Command Overview

You are tasked with providing detailed status information about a specific feature, including its progress, history, and current state of all associated documents.

User provided input: "$ARGUMENTS"

## Step 1: Determine Target Feature

### Parse Arguments
- If arguments provided: Use as feature name
- If no arguments: Use current feature from `current-feature` file
- If "." provided: Explicitly use current feature

### Feature Resolution
1. Load current feature from `current-feature` file
2. Parse user arguments for specific feature name
3. Default to current feature if no arguments

## Step 2: Load Feature Information

### State File Data
From `.feature-state.json`, extract:
- Basic metadata (name, description, status)
- Creation and update timestamps
- Progress tracking flags
- Lifecycle status (active/archived/trashed)

### Directory Inspection
Scan feature directory for:
```
features/[status]/[feature-name]/
├── feature.md          # Original request and notes
├── JTBD.md            # User needs analysis
├── PRD.md             # Product requirements
├── plan.md            # Technical plan
└── plan-organized.md  # Structured implementation
```

### File Analysis
For each existing file:
1. Check file size and last modified date
2. Extract key sections or summary
3. Count lines of content
4. Note completion status

## Step 3: Generate Comprehensive Status Report

### Report Structure
```
Feature Status: [feature-name]
==============================

Basic Information
-----------------
Name: [feature-name]
Description: [description]
Status: [active|archived|trashed]
Created: [YYYY-MM-DD]
Last Updated: [YYYY-MM-DD]
Current: [Yes/No] ⚡

Progress Overview
-----------------
[████████░░] 80% Complete

✓ Feature Definition (feature.md)
  - Created: [date]
  - Size: [X lines]
  
✓ JTBD Analysis (JTBD.md)
  - Created: [date]
  - Size: [X lines]
  - Jobs Identified: [count]
  
✓ Product Requirements (PRD.md)
  - Created: [date]
  - Size: [X lines]
  - Requirements: [count]
  
✓ Technical Plan (plan.md)
  - Created: [date]
  - Size: [X lines]
  - Tasks: [count]
  
✗ Organized Plan (plan-organized.md)
  - Status: Not created
  - Next Step: Run /organize-plan

Document Summaries
------------------
[For each existing document, provide key highlights]

Implementation Status
--------------------
[Check for any implementation artifacts or code]

Related Information
-------------------
- Related Features: [if any mentioned in feature.md]
- Dependencies: [if identified in plans]
- Blockers: [if noted anywhere]

Next Recommended Action
-----------------------
[Based on progress, suggest the next workflow command]
```

## Step 4: Extract Document Insights

### feature.md Analysis
Extract and summarize:
- Original request
- Status checklist progress
- Any noted blockers or concerns
- Related features mentioned

### JTBD.md Analysis
If exists, extract:
- Number of user jobs identified
- Primary user personas
- Key pain points addressed
- Success criteria defined

### PRD.md Analysis
If exists, extract:
- Number of requirements
- Technical constraints identified
- Acceptance criteria count
- Priority indicators

### plan.md Analysis
If exists, extract:
- Number of implementation tasks
- Estimated complexity
- Technical approach summary
- Identified risks

### plan-organized.md Analysis
If exists, extract:
- Task organization structure
- Sprint/phase breakdown
- Dependency mapping
- Timeline estimates

## Step 5: Provide Actionable Insights

### Progress Analysis
Based on completion status:

**0% Complete** (Only feature.md):
```
Status: Initial Definition Only
This feature has been defined but no analysis has begun.
Recommended: Start with `/create-jtbd` to analyze user needs.
```

**25% Complete** (Has JTBD):
```
Status: User Needs Analyzed
User jobs have been identified and documented.
Recommended: Create product requirements with `/create-prd`.
```

**50% Complete** (Has PRD):
```
Status: Requirements Defined
Product requirements are complete.
Recommended: Create technical plan with `/create-plan`.
```

**75% Complete** (Has plan):
```
Status: Planning Complete
Technical approach has been defined.
Recommended: Organize implementation with `/organize-plan`.
```

**100% Complete** (All docs):
```
Status: Ready for Implementation
All planning documents are complete.
Recommended: Begin coding with `/implement-code` or archive if done.
```

### Health Indicators
Identify potential issues:

**Stale Feature**:
```
⚠️ Warning: This feature hasn't been updated in 30+ days.
Consider archiving or resuming work.
```

**Missing Dependencies**:
```
⚠️ Warning: PRD created without JTBD analysis.
Consider creating JTBD for better user alignment.
```

**Incomplete Workflow**:
```
⚠️ Warning: Plan created but PRD missing.
Requirements may not be fully defined.
```

## Step 6: Historical Context

### Timeline Generation
Create activity timeline:
```
Feature Timeline
----------------
2024-01-15: Feature created
2024-01-16: JTBD analysis completed
2024-01-18: PRD document created
2024-01-20: Technical plan drafted
2024-01-20: Last activity
```

### Change Detection
If tracking detailed history:
- Major document updates
- Status transitions
- Significant revisions

## Step 7: Format Output

### Visual Elements
Use consistent formatting:
- ✓ for completed items
- ✗ for missing items
- ⚡ for current feature
- ⚠️ for warnings
- 📊 for statistics
- 📁 for file info

### Information Hierarchy
1. Essential status at top
2. Progress visualization
3. Detailed document status
4. Insights and warnings
5. Recommendations at bottom

### Responsive Detail
- Default: Comprehensive view
- With `--summary` flag: Brief overview
- With `--docs` flag: Document contents included

## Error Handling

### Feature Not Found
```
Error: Feature '[name]' not found.

Available features:
- feature-1 (active)
- feature-2 (active)
- feature-3 (archived)

Use exact feature name or check /feature-list.
```

### State Inconsistency
If files don't match state:
```
Warning: Inconsistency detected
- State file shows: 50% complete
- Actual files show: 75% complete

Updating state file to match reality...
```

### Access Issues
If can't read feature files:
```
Error: Cannot access feature directory
Path: features/active/[feature-name]/
Reason: [Permission/Missing/Error]

Showing information from state file only.
```

## Integration Notes

### Command Relationships
- Complements `/feature-list` with detailed view
- Helps decide when to `/feature-switch`
- Guides workflow command sequence
- Informs `/feature-archive` decisions

### State Synchronization
- Update state file if discrepancies found
- Maintain consistency across commands
- Log any automatic corrections

Now provide detailed status for the requested feature: $ARGUMENTS