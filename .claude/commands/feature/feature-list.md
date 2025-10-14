# /feature-list

*Lists all features with their current status/state.*

## Auto-Loaded Project Context:
@/docs/product-development/.feature-state.json
@/docs/product-development/current-feature

## Command Overview

You are tasked with displaying a simple list of all features showing only their name and current state. The state is determined by which folder they live in (active, archived, or trashed).

User provided input: "$ARGUMENTS"

## Step 1: Parse Arguments

### Filter Options
Support these argument formats:
- `--active` or `active` - Show only active features
- `--archived` or `archived` - Show only archived features  
- `--trashed` or `trashed` - Show only trashed features
- No arguments - Show all features (default)

### Argument Processing
```
Examples:
/feature-list --active
/feature-list archived
/feature-list --trashed
/feature-list
```

## Step 2: Scan Feature Directories

### Directory Structure
Check these directories for features:
```
docs/product-development/features/
├── active/      # State: active
├── archived/    # State: archived
└── trashed/     # State: trashed
```

### Feature Discovery
For each directory:
1. List all subdirectories (these are feature names)
2. Determine state based on parent directory
3. Don't read file contents or check progress

## Step 3: Filter Results

### Apply Filters
Based on arguments:
- `--active`: Only show features from `active/` folder
- `--archived`: Only show features from `archived/` folder
- `--trashed`: Only show features from `trashed/` folder
- No filter: Show all features from all folders

## Step 4: Format Output

### Simple List Format
```
# All features
feature-name-1 (active)
feature-name-2 (active)  
feature-name-3 (archived)
feature-name-4 (trashed)

# Filtered examples
# /feature-list --active
feature-name-1 (active)
feature-name-2 (active)

# /feature-list --archived
feature-name-3 (archived)
```

### Output Rules
- One feature per line
- Format: `feature-name (state)`
- State is: `active`, `archived`, or `trashed`
- No additional information (no progress, dates, descriptions)
- No headers or summaries unless helpful for context

## Step 5: Handle Edge Cases

### No Features Found
If no features exist or match filter:
```
No features found.
```

### Empty Directories
If feature directories don't exist:
```
No feature directories found.
```

### Invalid Filter
If user provides invalid filter argument:
```
Invalid filter. Use: --active, --archived, --trashed, or no argument for all.
```

## Implementation Notes

### Keep It Simple
- Don't read `.feature-state.json` unless needed for validation
- Don't read individual feature files
- Don't calculate progress or check completion
- Focus only on: name + state (based on folder location)

### State Determination
State is determined by folder location:
- `docs/product-development/features/active/[name]/` → `active`
- `docs/product-development/features/archived/[name]/` → `archived`  
- `docs/product-development/features/trashed/[name]/` → `trashed`

### Performance
- Use directory listing only
- Don't traverse into feature subdirectories
- Don't read file contents
- Quick response for all cases

Now provide the simple feature list based on: $ARGUMENTS