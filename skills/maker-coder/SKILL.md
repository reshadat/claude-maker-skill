---
name: maker-coder
description: Automatically use MAKER framework to code complex tasks and data analysis through extreme decomposition and voting. Trigger when user asks Claude to write code, build features, implement functionality, OR analyze large datasets (>1000 rows, ETL pipelines, data transformations). Decomposes into minimal subtasks, generates multiple solution attempts per step, votes on best approach, persists progress for restartability, and assembles into complete working code with high reliability.
---

# MAKER Coder: Automated Code Generation with Zero Errors

## Overview

This skill enables Claude to automatically use the MAKER (Massively Decomposed Agentic Processes) framework when writing code. Instead of writing code in one shot, Claude will:

1. **Decompose** the task into minimal coding subtasks
2. **Generate** multiple solutions for each subtask
3. **Vote** on the best solution per subtask
4. **Assemble** into complete, working code
5. **Verify** with high reliability

## When to Trigger

Automatically use this skill when user:
- Asks to write code: "Write a function to...", "Create a script that..."
- Requests features: "Build a feature for...", "Implement..."
- Describes requirements: "I need code that..."
- Wants complex logic: Multi-step algorithms, data processing, API integrations
- Needs high reliability: Production code, critical systems
- **Data analysis on large datasets**: "Analyze this CSV", "Process this data", "ETL pipeline", "Data transformation", large file processing, multi-step data workflows

### Data Analysis Triggers

**ALWAYS use MAKER for data analysis when:**
- Dataset has >1000 rows or >10 columns
- Multiple transformation steps required
- Aggregations, joins, or pivots needed
- Data cleaning + analysis + visualization pipeline
- Export to multiple formats
- User mentions: "large", "dataset", "analyze", "ETL", "pipeline", "transform"

**Example Data Analysis Decomposition:**
```
User: "Analyze this sales data CSV and create a summary report"

Decomposition:
├── Step 1: CSV loader with schema detection
├── Step 2: Data cleaning (nulls, types, outliers)
├── Step 3: Validation rules
├── Step 4: Aggregation functions (by region, product, time)
├── Step 5: Statistical calculations
├── Step 6: Summary report generator
├── Step 7: Export to CSV/Excel/JSON
└── Step 8: Main orchestrator with error handling
```

## Core Workflow

### Phase 1: Decompose (MAD - Maximal Agentic Decomposition)

Break the coding task into minimal subtasks where each subtask is:
- **Single responsibility**: One function, one class, one logic block
- **Independent**: Can be coded separately
- **Verifiable**: Clear success criteria
- **Atomic**: Cannot be meaningfully subdivided

**Example Decomposition:**
```
User: "Build a CSV data validator with email checking and export"

Decomposition:
├── Step 1: CSV file reader function
├── Step 2: Email validation regex function  
├── Step 3: Row validation logic
├── Step 4: Error collection structure
├── Step 5: Valid data filter function
├── Step 6: Export to CSV function
└── Step 7: Main orchestration function
```

### Phase 2: Generate Multiple Solutions (Voting)

For each subtask, generate K=3 different solution attempts:

**Solution 1**: Most straightforward approach
**Solution 2**: Alternative implementation
**Solution 3**: Different technique/library

Each solution must:
- Solve the exact subtask
- Be syntactically correct
- Include docstring/comments
- Have consistent interfaces

### Phase 3: Vote and Select

Compare solutions based on:
1. **Correctness**: Does it solve the problem?
2. **Simplicity**: Is it clear and maintainable?
3. **Robustness**: Does it handle edge cases?
4. **Performance**: Is it reasonably efficient?

Select the winning solution that scores highest across criteria.

### Phase 4: Assemble and Verify

1. Combine winning solutions in correct order
2. Add integration code if needed
3. Add imports and setup
4. Verify interfaces match between components
5. Add error handling at integration points
6. Create complete working program

### Phase 5: Present Results

Show user:
- ✅ Complete working code
- 📊 Decomposition tree (what was built)
- 🎯 Key decisions made per subtask
- 🧪 How to test/run the code
- 💡 Alternative approaches considered

## Implementation Pattern

### Step-by-Step Process

**1. Acknowledge and Decompose**
```
"I'll use the MAKER framework to build this reliably.

Breaking down into minimal subtasks:
1. [Subtask 1 description]
2. [Subtask 2 description]
...

Let me generate and vote on solutions for each."
```

**2. For Each Subtask (Internal - Don't Show All Details)**

Generate 3 solutions silently, evaluate, select winner.

**3. Show Progress (Optional)**
```
✓ Step 1/7: CSV reader - Selected pandas approach
✓ Step 2/7: Email validator - Selected regex with RFC compliance
✓ Step 3/7: Row validation - Selected functional approach
...
```

**4. Present Final Code**
```python
"""
Complete implementation using MAKER framework
- 7 subtasks decomposed and solved
- 3 solutions evaluated per step
- Best solution selected for each component
"""

# [Complete working code here]
```

**5. Explain Key Decisions**
```
Key implementation choices:
- Step 2: Chose regex over email library for better control
- Step 4: Used dict over class for flexibility
- Step 6: Selected csv.DictWriter for header preservation
```

## Decomposition Guidelines

### Good Decomposition (Do This)

**✅ Single Function/Class**
```
Step 1: Parse JSON input
Step 2: Validate schema
Step 3: Transform data structure
Step 4: Generate output format
```

**✅ Clear Boundaries**
```
Step 1: Database connection function
Step 2: Query builder function  
Step 3: Result parser function
Step 4: Error handler function
```

**✅ Testable Units**
```
Step 1: Input validator (can test independently)
Step 2: Data processor (can test independently)
Step 3: Output formatter (can test independently)
```

### Bad Decomposition (Avoid This)

**❌ Too Large**
```
Step 1: Build entire REST API
Step 2: Add frontend
```

**❌ Too Small**
```
Step 1: Import pandas
Step 2: Create variable
Step 3: Assign value
```

**❌ Interdependent**
```
Step 1: Start function definition
Step 2: Add middle logic
Step 3: Close function
```

## Voting Criteria

### Solution Evaluation Matrix

For each solution, score 0-10 on:

1. **Correctness** (30% weight)
   - Solves the exact problem?
   - Handles requirements?
   - Syntactically valid?

2. **Clarity** (25% weight)
   - Easy to understand?
   - Well-commented?
   - Good naming?

3. **Robustness** (25% weight)
   - Handles edge cases?
   - Error handling?
   - Input validation?

4. **Efficiency** (20% weight)
   - Reasonable performance?
   - No obvious bottlenecks?
   - Appropriate data structures?

**Selection**: Choose highest total score

### Example Voting

**Subtask: Email validation function**

**Solution A: Simple regex**
```python
def validate_email(email):
    return re.match(r'^[\w\.-]+@[\w\.-]+\.\w+$', email) is not None
```
- Correctness: 7/10 (basic validation only)
- Clarity: 10/10 (very simple)
- Robustness: 5/10 (misses edge cases)
- Efficiency: 10/10 (fast)
- **Total: 7.35/10**

**Solution B: Comprehensive regex**
```python
def validate_email(email):
    """Validate email per RFC 5322"""
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return re.match(pattern, email) is not None
```
- Correctness: 9/10 (RFC compliant)
- Clarity: 9/10 (documented)
- Robustness: 9/10 (handles most cases)
- Efficiency: 10/10 (fast)
- **Total: 9.1/10** ✅ **WINNER**

**Solution C: Library-based**
```python
from email_validator import validate_email as lib_validate

def validate_email(email):
    try:
        lib_validate(email)
        return True
    except:
        return False
```
- Correctness: 10/10 (library handles all)
- Clarity: 8/10 (external dependency)
- Robustness: 10/10 (comprehensive)
- Efficiency: 8/10 (slower)
- **Total: 9.0/10**

**Decision**: Select Solution B (9.1) - best balance

## Red-Flagging (Quality Gates)

Reject a solution if it has:

**🚩 Syntax Errors**
- Code doesn't parse
- Invalid Python/language syntax

**🚩 Import Errors**
- Uses undefined modules
- Missing dependencies

**🚩 Logic Errors**
- Infinite loops
- Unreachable code
- Wrong algorithm

**🚩 Security Issues**
- SQL injection vulnerable
- Unsafe eval/exec
- Hardcoded secrets

**🚩 Interface Mismatches**
- Function signature doesn't match spec
- Wrong return type
- Missing required parameters

If solution is red-flagged, generate replacement immediately.

## Example: Complete Workflow

### User Request
```
"Write a Python script that reads a CSV file, validates email addresses in the 'email' column, filters out invalid rows, and exports valid rows to a new CSV file."
```

### Claude's Response (Using MAKER)

```
I'll use the MAKER framework to build this reliably by decomposing into minimal subtasks and selecting the best solution for each.

**Decomposition:**
1. CSV file reader
2. Email validation
3. Row validator
4. Data filter
5. CSV writer
6. Main orchestrator
7. CLI interface

Building with voting (3 solutions per step)...

✓ All 7 steps completed with best solutions selected

Here's the complete, verified code:
```

```python
#!/usr/bin/env python3
"""
CSV Email Validator
Built using MAKER framework - 7 decomposed steps, 3 solutions per step
"""

import csv
import re
import sys
from pathlib import Path

# Step 1 Winner: pandas-free approach for minimal dependencies
def read_csv(filepath):
    """Read CSV file and return list of dicts"""
    with open(filepath, 'r', encoding='utf-8') as f:
        reader = csv.DictReader(f)
        return list(reader)

# Step 2 Winner: RFC 5322 compliant regex (balance of correctness & speed)
def validate_email(email):
    """Validate email per RFC 5322 basic requirements"""
    if not email or not isinstance(email, str):
        return False
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return re.match(pattern, email.strip()) is not None

# Step 3 Winner: Functional approach with detailed error info
def validate_row(row, row_num):
    """Validate single row, return (is_valid, error_msg)"""
    if 'email' not in row:
        return False, f"Row {row_num}: Missing 'email' column"
    
    if not validate_email(row['email']):
        return False, f"Row {row_num}: Invalid email '{row['email']}'"
    
    return True, None

# Step 4 Winner: Generator pattern for memory efficiency
def filter_valid_rows(rows):
    """Filter rows, return (valid_rows, errors)"""
    valid = []
    errors = []
    
    for i, row in enumerate(rows, start=1):
        is_valid, error = validate_row(row, i)
        if is_valid:
            valid.append(row)
        else:
            errors.append(error)
    
    return valid, errors

# Step 5 Winner: Context manager with proper header handling
def write_csv(filepath, rows, fieldnames):
    """Write rows to CSV file"""
    with open(filepath, 'w', encoding='utf-8', newline='') as f:
        writer = csv.DictWriter(f, fieldnames=fieldnames)
        writer.writeheader()
        writer.writerows(rows)

# Step 6 Winner: Pipeline pattern with comprehensive error handling
def process_csv(input_file, output_file):
    """Main processing pipeline"""
    try:
        # Read
        rows = read_csv(input_file)
        print(f"Read {len(rows)} rows from {input_file}")
        
        # Validate and filter
        valid_rows, errors = filter_valid_rows(rows)
        
        # Report errors
        if errors:
            print(f"\nFound {len(errors)} invalid rows:")
            for error in errors[:5]:  # Show first 5
                print(f"  - {error}")
            if len(errors) > 5:
                print(f"  ... and {len(errors) - 5} more")
        
        # Write valid rows
        if valid_rows:
            fieldnames = rows[0].keys()
            write_csv(output_file, valid_rows, fieldnames)
            print(f"\nWrote {len(valid_rows)} valid rows to {output_file}")
        else:
            print("\nNo valid rows to write")
        
        return len(valid_rows), len(errors)
        
    except FileNotFoundError:
        print(f"Error: File '{input_file}' not found")
        sys.exit(1)
    except Exception as e:
        print(f"Error: {e}")
        sys.exit(1)

# Step 7 Winner: argparse for professional CLI
def main():
    """CLI entry point"""
    import argparse
    
    parser = argparse.ArgumentParser(
        description='Validate emails in CSV and export valid rows'
    )
    parser.add_argument('input', help='Input CSV file')
    parser.add_argument('output', help='Output CSV file')
    
    args = parser.parse_args()
    
    valid, invalid = process_csv(args.input, args.output)
    
    print(f"\n✓ Complete: {valid} valid, {invalid} invalid")

if __name__ == '__main__':
    main()
```

```
**How to use:**
```bash
python validator.py input.csv output.csv
```

**Key decisions made:**
- Step 1: CSV library over pandas (no heavy dependencies)
- Step 2: Regex over email-validator library (better control/performance balance)
- Step 3: Functional validation (easier to test/extend)
- Step 4: Generator pattern considered but list chosen for error reporting
- Step 5: DictWriter for automatic header preservation
- Step 6: Pipeline pattern for clear data flow
- Step 7: argparse over sys.argv for better UX

**Reliability:** 7 steps × 3 solutions = 21 implementations evaluated. Best solution selected for each step.
```

## Complexity Scaling

### Simple Tasks (< 5 steps)
- Quick decomposition
- Show solutions briefly
- Focus on final code

### Medium Tasks (5-15 steps)
- Show progress checkmarks
- Highlight key decisions
- Explain trade-offs

### Complex Tasks (15+ steps)
- Group into phases
- Show milestone completion
- Detailed decision log
- Consider breaking into multiple interactions

## Optimization Tips

### When to Show Voting
- **Simple tasks**: Don't show, just deliver code
- **Medium tasks**: Show key decisions only
- **Complex tasks**: Show decision tree for main components
- **User asks**: Always show voting details if requested

### When to Decompose More
- User requests high reliability
- Production/critical code
- Complex business logic
- Many edge cases

### When to Decompose Less
- Simple CRUD operations
- Boilerplate code
- Prototypes/MVPs
- User wants speed over perfection

## Example Triggers

### Automatic MAKER Usage

**✅ Use MAKER for:**
```
"Build a REST API with authentication"
"Create a data processing pipeline"
"Write a web scraper with rate limiting"
"Implement a caching layer with TTL"
"Build a CLI tool with subcommands"
```

**❌ Don't use MAKER for:**
```
"Write a hello world program"
"Create a simple for loop"
"Print a string"
"Define a variable"
```

## Red Flags to Watch

During voting, reject solutions with:

1. **Hardcoded values** that should be configurable
2. **No error handling** in critical sections
3. **SQL injection** vulnerabilities
4. **Unbounded loops** without exit conditions
5. **Memory leaks** (e.g., unclosed files)
6. **Race conditions** in concurrent code
7. **Insecure secrets** management

## Integration Checklist

After assembling all subtasks:

- [ ] All imports at top
- [ ] Constants defined
- [ ] Functions in logical order
- [ ] Main entry point present
- [ ] Error handling added
- [ ] Documentation complete
- [ ] Example usage provided
- [ ] Dependencies listed

## Output Format

### Standard Response Structure

```markdown
I'll use MAKER to build this with high reliability.

**Decomposition:** [X steps]
1. [Step description]
2. [Step description]
...

[Optional: Progress indicators]

**Complete Code:**
[Full working implementation]

**Key Decisions:**
- Step X: [Decision and reasoning]
- Step Y: [Decision and reasoning]

**Usage:**
[How to run/test]

**Reliability:** [X] steps, 3 solutions per step, best selected.
```

## Advanced Features

### Adaptive Decomposition

For user feedback like:
- "Too complex" → Reduce decomposition
- "Too simple" → Increase decomposition
- "Show me alternatives" → Display voting details
- "Explain your choice" → Show evaluation matrix

### Iterative Refinement

If user reports issues:
1. Identify failing subtask
2. Regenerate 3 new solutions
3. Re-vote with failure context
4. Replace in final code
5. Verify integration

### Code Review Mode

User can ask:
```
"Review this code using MAKER principles"
```

Claude will:
1. Decompose existing code
2. Generate alternative solutions
3. Compare approaches
4. Suggest improvements

## Batch Execution & Task Persistence

### Core Principle: Restartable Tasks

All MAKER tasks MUST be:
- **Batchable**: Process subtasks in configurable batches (default: 3-5 steps per batch)
- **Persistent**: Store progress in a task-specific folder
- **Restartable**: Resume from last checkpoint if interrupted

### Task Folder Structure

For every MAKER task, create a folder in the project:

```
.maker-tasks/
└── [task-id]/                    # e.g., csv-validator-20241223
    ├── task-manifest.json        # Task metadata and status
    ├── decomposition.md          # Full decomposition tree
    ├── progress.json             # What's done, what's remaining
    ├── batch-001/                # First batch of subtasks
    │   ├── step-01-solution.md   # Winning solution + alternatives considered
    │   ├── step-02-solution.md
    │   └── step-03-solution.md
    ├── batch-002/                # Second batch
    │   └── ...
    ├── assembled-code/           # Final assembled code per batch
    │   ├── partial-001.py        # Code after batch 1
    │   └── partial-002.py        # Code after batch 2
    └── final/
        └── complete.py           # Final assembled code
```

### Task Manifest (task-manifest.json)

```json
{
  "task_id": "csv-validator-20241223-143052",
  "created": "2024-12-23T14:30:52Z",
  "updated": "2024-12-23T14:45:30Z",
  "description": "CSV email validator with export",
  "status": "in_progress",
  "total_steps": 7,
  "completed_steps": 4,
  "current_batch": 2,
  "batch_size": 3,
  "can_resume": true,
  "last_checkpoint": "batch-001 complete"
}
```

### Progress Tracking (progress.json)

```json
{
  "steps": [
    {"id": 1, "name": "CSV file reader", "status": "completed", "batch": 1},
    {"id": 2, "name": "Email validation", "status": "completed", "batch": 1},
    {"id": 3, "name": "Row validator", "status": "completed", "batch": 1},
    {"id": 4, "name": "Data filter", "status": "in_progress", "batch": 2},
    {"id": 5, "name": "CSV writer", "status": "pending", "batch": 2},
    {"id": 6, "name": "Main orchestrator", "status": "pending", "batch": 3},
    {"id": 7, "name": "CLI interface", "status": "pending", "batch": 3}
  ],
  "batches": {
    "1": {"status": "completed", "steps": [1, 2, 3]},
    "2": {"status": "in_progress", "steps": [4, 5]},
    "3": {"status": "pending", "steps": [6, 7]}
  },
  "resume_point": {
    "batch": 2,
    "step": 4,
    "instruction": "Continue with data filter function"
  }
}
```

### Batch Execution Workflow

**Phase 0: Initialize Task Folder**
```
1. Create .maker-tasks/[task-id]/ folder
2. Write task-manifest.json with initial state
3. Write decomposition.md with full task breakdown
4. Initialize progress.json with all steps as "pending"
5. Determine batch groupings based on dependencies
```

**Phase 1-N: Process Batches**
```
For each batch:
  1. Update progress.json: batch status = "in_progress"
  2. For each step in batch:
     a. Generate 3 solutions
     b. Vote and select winner
     c. Write step-XX-solution.md with decision
     d. Update progress.json: step status = "completed"
  3. Assemble batch code → assembled-code/partial-XXX.py
  4. Update progress.json: batch status = "completed"
  5. Update task-manifest.json with checkpoint
  6. CHECKPOINT: Task can be safely interrupted here
```

**Phase Final: Assembly**
```
1. Combine all partial assemblies
2. Write final/complete.py
3. Update task-manifest.json: status = "completed"
4. Optionally clean up intermediate files
```

### Restart Protocol

When resuming a task:

```
1. Check for existing .maker-tasks/[task-id]/ folder
2. Read progress.json for resume_point
3. Announce: "Resuming MAKER task from [checkpoint]"
4. Skip completed batches
5. Continue from resume_point.step
6. Follow normal batch workflow from there
```

**Resume Command Pattern:**
```
User: "Continue the CSV validator task"
Claude: "Found existing task 'csv-validator-20241223' at batch 2, step 4.
        Resuming from: Data filter function
        Remaining: 4 steps across 2 batches"
```

### Batch Size Guidelines

| Task Complexity | Recommended Batch Size |
|-----------------|------------------------|
| Simple (< 7 steps) | 3-4 steps per batch |
| Medium (7-15 steps) | 4-5 steps per batch |
| Complex (15+ steps) | 5-7 steps per batch |

### Checkpoint Triggers

Create checkpoint (safe interrupt point) after:
- ✅ Each batch completion
- ✅ Every 3 completed steps
- ✅ Any user interruption
- ✅ Error recovery points

### Example: Batch Execution Output

```
I'll use MAKER with batch execution for restartability.

📁 Created task folder: .maker-tasks/csv-validator-20241223/

**Decomposition:** 7 steps in 3 batches
Batch 1 (steps 1-3): Core reading and validation
Batch 2 (steps 4-5): Filtering and writing
Batch 3 (steps 6-7): Orchestration and CLI

━━━ BATCH 1/3 ━━━
✓ Step 1/7: CSV reader - Selected DictReader approach
✓ Step 2/7: Email validator - Selected RFC regex
✓ Step 3/7: Row validation - Selected functional approach
💾 Checkpoint saved. Task can be safely interrupted.

━━━ BATCH 2/3 ━━━
✓ Step 4/7: Data filter - Selected list comprehension
✓ Step 5/7: CSV writer - Selected DictWriter
💾 Checkpoint saved. Task can be safely interrupted.

━━━ BATCH 3/3 ━━━
✓ Step 6/7: Orchestrator - Selected pipeline pattern
✓ Step 7/7: CLI - Selected argparse
💾 Task complete!

📄 Final code: .maker-tasks/csv-validator-20241223/final/complete.py
```

### Mandatory Behaviors

**ALWAYS:**
- Create .maker-tasks/ folder before starting any MAKER task
- Update progress.json after EVERY step completion
- Save checkpoint after EVERY batch
- Check for existing task folder before starting new task

**NEVER:**
- Process all steps without batching
- Skip progress tracking for "simple" tasks
- Delete task folder until user confirms task is complete
- Lose progress on interruption

### Integration with TodoWrite

For complex MAKER tasks, also create TodoWrite entries:
```
TodoWrite:
- [completed] MAKER: Initialize task folder
- [completed] MAKER: Batch 1 - Core functions
- [in_progress] MAKER: Batch 2 - Processing logic
- [pending] MAKER: Batch 3 - CLI interface
- [pending] MAKER: Final assembly and verification
```

## Summary

This skill enables Claude to:
- ✅ Automatically decompose coding tasks
- ✅ Generate multiple solutions per subtask
- ✅ Vote on best implementation
- ✅ Assemble reliable, complete code
- ✅ Explain key decisions
- ✅ Scale to complex requirements
- ✅ **Execute in batches for manageability**
- ✅ **Persist progress for restartability**
- ✅ **Resume interrupted tasks from checkpoints**

**Result:** Higher quality, more reliable code through systematic decomposition, voting, and robust task persistence.
