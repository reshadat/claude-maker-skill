# MAKER Skill for Claude Code

A Claude Code skill that enables systematic code generation through extreme decomposition, voting, and restartable batch execution.

## What is MAKER?

**MAKER** (Massively Decomposed Agentic Processes) is a framework that transforms how Claude writes code:

1. **Decompose** - Break tasks into minimal, atomic subtasks
2. **Generate** - Create 3 different solutions for each subtask
3. **Vote** - Evaluate and select the best solution
4. **Assemble** - Combine winning solutions into complete code
5. **Persist** - Save progress for restartability

## Why Use MAKER?

| Traditional Approach | MAKER Approach |
|---------------------|----------------|
| One-shot code generation | Systematic decomposition |
| Single implementation | 3 solutions per step, best selected |
| Lost progress on interruption | Checkpointed, restartable batches |
| Variable quality | Consistent, evaluated quality |

## Installation

### Option 1: Copy to Claude Config

Copy the files to your Claude configuration:

```bash
# Create directories if they don't exist
mkdir -p ~/.claude/skills/maker-coder
mkdir -p ~/.claude/commands

# Copy skill and command
cp skills/maker-coder/SKILL.md ~/.claude/skills/maker-coder/
cp commands/maker.md ~/.claude/commands/
```

### Option 2: Symlink (for development)

```bash
ln -s "$(pwd)/skills/maker-coder/SKILL.md" ~/.claude/skills/maker-coder/SKILL.md
ln -s "$(pwd)/commands/maker.md" ~/.claude/commands/maker.md
```

## Usage

### Slash Command

```
/maker Build a REST API with authentication
```

### Automatic Triggering

The skill auto-activates for:
- Complex coding tasks (>5 steps)
- Multi-file implementations
- Data analysis on large datasets (>1000 rows)
- ETL pipelines and data transformations
- Production/critical code

### Example Session

```
User: /maker Create a CSV email validator with export

Claude: I'll use MAKER with batch execution for restartability.

📁 Created task folder: .maker-tasks/csv-validator-20241225/

**Decomposition:** 7 steps in 3 batches
Batch 1 (steps 1-3): Core reading and validation
Batch 2 (steps 4-5): Filtering and writing
Batch 3 (steps 6-7): Orchestration and CLI

━━━ BATCH 1/3 ━━━
✓ Step 1/7: CSV reader - Selected DictReader approach
✓ Step 2/7: Email validator - Selected RFC regex
✓ Step 3/7: Row validation - Selected functional approach
💾 Checkpoint saved. Task can be safely interrupted.

[continues...]
```

## Task Persistence

MAKER creates a `.maker-tasks/` folder to track progress:

```
.maker-tasks/
└── csv-validator-20241225/
    ├── task-manifest.json      # Task metadata
    ├── decomposition.md        # Full breakdown
    ├── progress.json           # Step completion status
    ├── batch-001/              # Solutions per batch
    │   ├── step-01-solution.md
    │   └── ...
    └── final/
        └── complete.py         # Assembled code
```

### Resuming Interrupted Tasks

```
User: Continue the CSV validator task

Claude: Found existing task 'csv-validator-20241225' at batch 2, step 4.
        Resuming from: Data filter function
        Remaining: 4 steps across 2 batches
```

## Voting Criteria

Each solution is scored on:

| Criterion | Weight | Description |
|-----------|--------|-------------|
| Correctness | 30% | Solves the problem correctly |
| Clarity | 25% | Readable, well-documented |
| Robustness | 25% | Handles edge cases |
| Efficiency | 20% | Reasonable performance |

## When MAKER is Used

### Automatic Triggers
- "Build a REST API with..."
- "Create a data processing pipeline"
- "Write a web scraper with..."
- "Implement a caching layer"
- Multi-step algorithms
- Production code requirements

### Skip MAKER For
- Simple single-function tasks
- Quick fixes and typos
- Explanations or questions
- Tasks with <3 steps

## File Structure

```
maker-skill/
├── README.md                           # This file
├── skills/
│   └── maker-coder/
│       └── SKILL.md                    # Main skill definition
└── commands/
    └── maker.md                        # Slash command definition
```

## Configuration

The skill uses these defaults:
- **Batch size**: 3-5 steps per batch (scales with complexity)
- **Solutions per step**: 3
- **Checkpoint frequency**: After each batch

## License

MIT License - Feel free to use and modify.

## Contributing

Contributions welcome! Please open an issue or PR.
