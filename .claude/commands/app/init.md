---
argument-hint: <app-description>
description: Initialize a new application with collaborative decisions from all specialized agents
---

# Initialize Application - Collaborative Multi-Agent Workflow

Initialize a new application with coordinated guidance from Product Owner, Design System Manager, Rails Architect, Tailwind Specialist, and Hotwire Specialist agents working collaboratively.

**Usage**: `/app:init <app-description>`

**Example**: `/app:init "CRM system for managing sales leads with kanban board and email integration"`

## What This Command Does

This command orchestrates a comprehensive application initialization process where five specialized agents collaborate to make informed decisions about your application:

1. **Product Owner** - Validates the product idea with JTBD analysis
2. **Design System Manager** - Establishes visual guidelines and design tokens
3. **Rails Architect** - Designs the application architecture
4. **Tailwind Specialist** - Sets up utility-first CSS configuration
5. **Hotwire Specialist** - Plans interactive features and real-time updates

## Implementation

### Phase 1: Product Discovery (Product Owner)

Launch the Product Owner agent to analyze the application idea:

```
Application description: $ARGUMENTS

Task for Product Owner agent:
- Perform Jobs To Be Done (JTBD) analysis
- Identify core user problems this app solves
- Define key features (must-have vs nice-to-have)
- Create lean PRD with success metrics
- Recommend MVP scope

Output: JTBD document and lean PRD saved to .product/features/initialization/
```

**Wait for Product Owner agent to complete before proceeding.**

### Phase 2: Design System Planning (Design System Manager)

Launch the Design System Manager agent to establish visual foundation:

```
Based on the application: $ARGUMENTS
And the PRD from Phase 1

Task for Design System Manager agent:
- Define color palette (primary, secondary, accent, semantic colors)
- Establish typography scale and font families
- Define spacing system (margins, padding, gaps)
- Specify component styles (buttons, forms, cards, navigation)
- Create design tokens for consistency
- Document visual guidelines

Output: Design system specification saved to .design-system/
```

**Wait for Design System Manager agent to complete before proceeding.**

### Phase 3: Architecture Design (Rails Architect)

Launch the Rails Architect agent to design the application structure:

```
Based on the application: $ARGUMENTS
PRD from Phase 1
Design system from Phase 2

Task for Rails Architect agent:
- Design database schema (models, associations, validations)
- Plan REST resources and routes
- Identify Service Objects for complex operations
- Design authentication/authorization strategy
- Recommend gem dependencies
- Define folder structure and namespaces
- Apply SOLID principles to architecture
- Plan testing strategy

Output: Architecture document with models, routes, and technical decisions
```

**Wait for Rails Architect agent to complete before proceeding.**

### Phase 4: CSS Framework Setup (Tailwind Specialist)

Launch the Tailwind Specialist agent to configure Tailwind:

```
Based on the application: $ARGUMENTS
Design system from Phase 2
Architecture from Phase 3

Task for Tailwind Specialist agent:
- Configure tailwind.config.js with design tokens
- Map design system colors to Tailwind palette
- Set up custom spacing scale if needed
- Configure content paths for Rails
- Recommend Tailwind plugins (@tailwindcss/forms, typography, etc.)
- Set up dark mode configuration if needed
- Define component utilities for reusable patterns
- Plan responsive breakpoints

Output: Complete tailwind.config.js and setup instructions
```

**Wait for Tailwind Specialist agent to complete before proceeding.**

### Phase 5: Interactive Features Planning (Hotwire Specialist)

Launch the Hotwire Specialist agent to plan interactivity:

```
Based on the application: $ARGUMENTS
PRD features from Phase 1
Architecture from Phase 3
Tailwind setup from Phase 4

Task for Hotwire Specialist agent:
- Identify features requiring Turbo Frames (inline editing, modals)
- Identify features requiring Turbo Streams (real-time updates)
- Plan Stimulus controllers for client-side interactions
- Design ActionCable broadcasts if needed
- Plan page navigation with Turbo Drive
- Recommend Hotwire patterns for each feature
- Plan progressive enhancement strategy

Output: Hotwire implementation plan with specific patterns for each feature
```

**Wait for Hotwire Specialist agent to complete before proceeding.**

### Phase 6: Consolidation and Initialization

After all agents have completed their analysis:

1. **Create comprehensive initialization document** combining all agent outputs:
   - Executive Summary (from Product Owner)
   - Design System Specification (from Design System Manager)
   - Technical Architecture (from Rails Architect)
   - Tailwind Configuration (from Tailwind Specialist)
   - Interactivity Plan (from Hotwire Specialist)

2. **Generate initialization checklist**:
   ```markdown
   ## Application Initialization Checklist

   ### Setup
   - [ ] Create new Rails app: `rails new app-name --css=tailwind`
   - [ ] Configure database (PostgreSQL recommended)
   - [ ] Set up Git repository

   ### Dependencies
   - [ ] Add recommended gems to Gemfile
   - [ ] Bundle install
   - [ ] Install Tailwind plugins: npm install <plugins>

   ### Design System
   - [ ] Configure tailwind.config.js with design tokens
   - [ ] Create design system helper in app/helpers/
   - [ ] Set up base component styles

   ### Database & Models
   - [ ] Generate models: rails g model <ModelName>
   - [ ] Run migrations: rails db:migrate
   - [ ] Set up seed data

   ### Routes & Controllers
   - [ ] Configure routes.rb with REST resources
   - [ ] Generate controllers
   - [ ] Set up authentication (Devise/custom)

   ### Views & Components
   - [ ] Create layout with design system
   - [ ] Set up Turbo Frame wrappers
   - [ ] Implement Stimulus controllers

   ### Testing
   - [ ] Set up RSpec/Minitest
   - [ ] Write model tests
   - [ ] Write feature tests

   ### Deployment Preparation
   - [ ] Configure production database
   - [ ] Set up environment variables
   - [ ] Configure asset compilation
   ```

3. **Save all artifacts**:
   - `.product/features/initialization/jtbd.md`
   - `.product/features/initialization/prd.md`
   - `.design-system/visual-guidelines.md`
   - `.product/features/initialization/architecture.md`
   - `.product/features/initialization/tailwind-setup.md`
   - `.product/features/initialization/hotwire-plan.md`
   - `.product/features/initialization/INITIALIZATION_PLAN.md` (consolidated)
   - `.product/features/initialization/CHECKLIST.md`

4. **Present summary to user**:
   ```markdown
   # Application Initialization Complete

   Your application "$ARGUMENTS" has been analyzed by all specialized agents.

   ## Key Decisions Made:

   ### Product (Product Owner)
   - Core JTBD: [summary]
   - MVP Features: [list]
   - Success Metrics: [metrics]

   ### Design (Design System Manager)
   - Primary Color: [color]
   - Typography: [fonts]
   - Component Style: [description]

   ### Architecture (Rails Architect)
   - Core Models: [list]
   - Key Patterns: [Service Objects/etc]
   - Authentication: [strategy]

   ### Styling (Tailwind Specialist)
   - Tailwind Config: Ready
   - Plugins: [list]
   - Custom Utilities: [if any]

   ### Interactivity (Hotwire Specialist)
   - Turbo Frames: [features using]
   - Turbo Streams: [features using]
   - Stimulus: [controllers needed]

   ## Next Steps:

   1. Review the initialization plan: `.product/features/initialization/INITIALIZATION_PLAN.md`
   2. Follow the checklist: `.product/features/initialization/CHECKLIST.md`
   3. Start implementing with: `/feature-switch initialization`
   4. Begin coding with: `/implement-code`

   All agents are aligned and ready to assist with implementation!
   ```

## Agent Coordination Strategy

### Sequential vs Parallel Execution

Agents run **sequentially** in the order specified because each agent's decisions inform the next:

- Product Owner → defines what to build
- Design System Manager → defines how it should look (informs Tailwind)
- Rails Architect → defines technical structure (informs Hotwire patterns)
- Tailwind Specialist → configures styling (uses design tokens)
- Hotwire Specialist → plans interactivity (uses architecture knowledge)

### Inter-Agent Dependencies

```mermaid
Product Owner (JTBD, PRD)
    ↓
Design System Manager (Colors, Typography, Components)
    ↓
Rails Architect (Models, Routes, Architecture)
    ↓ ↘
Tailwind Specialist          Hotwire Specialist
(Config, Utilities)         (Frames, Streams, Stimulus)
    ↓ ↙
Consolidated Plan
```

### Communication Between Agents

Each agent receives:
- Original application description
- Output from all previous agents
- Specific questions to answer based on their expertise

This ensures:
- No duplicate work
- Consistent decisions
- Comprehensive coverage
- Aligned recommendations

## Examples

### Example 1: Simple CRUD Application
```bash
/app:init "Todo list app with categories and due dates"
```

**Expected Flow**:
1. Product Owner: Identifies JTBD as "organize tasks by category and deadline"
2. Design System: Suggests clean, minimal design with color-coded categories
3. Rails Architect: Models: Todo, Category; Simple REST; No Service Objects needed
4. Tailwind: Basic config with category colors, form styling
5. Hotwire: Turbo Frames for inline editing, Stimulus for date pickers

### Example 2: Complex Application
```bash
/app:init "CRM system for managing sales leads with kanban board, email integration, and real-time notifications"
```

**Expected Flow**:
1. Product Owner: Multiple JTBDs, prioritizes features, defines MVP
2. Design System: Professional design with status colors, card-based UI
3. Rails Architect: Models: Lead, User, Email, Activity; Service Objects for email sending; Background jobs
4. Tailwind: Drag-and-drop styling, card components, responsive grid
5. Hotwire: Turbo Frames for kanban cards, Streams for notifications, Stimulus for drag-drop

### Example 3: API-First Application
```bash
/app:init "REST API for inventory management with admin dashboard"
```

**Expected Flow**:
1. Product Owner: Defines API consumers, admin use cases
2. Design System: Admin-focused design system (tables, filters, charts)
3. Rails Architect: API namespacing, serializers, admin authentication
4. Tailwind: Data-dense layout, table utilities, dashboard components
5. Hotwire: Turbo Frames for CRUD operations, real-time inventory updates

## Success Criteria

- All 5 agents complete their analysis successfully
- No conflicting recommendations between agents
- Consolidated plan is comprehensive and actionable
- Checklist covers all necessary steps
- User can immediately start implementation with clear guidance
- All artifacts are properly saved and organized

## Error Handling

- If any agent fails, report which phase failed and why
- Allow user to retry individual phases
- Provide partial results if some agents succeed
- Suggest manual completion for failed phases

## Post-Initialization

After running `/app:init`, users should:

1. Review all generated documents
2. Ask questions to any agent for clarification
3. Use `/feature-switch initialization` to activate the feature
4. Use `/implement-code` to start building
5. Iterate with agents as implementation progresses

The agents remain available throughout development to answer questions and provide guidance specific to their domains.
