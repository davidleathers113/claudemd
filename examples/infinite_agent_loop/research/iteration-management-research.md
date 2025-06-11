# Research: Iteration Management

## Status: Basic Session Storage

### Research Date: June 11, 2025

## Summary
Claude Code has **basic session management** stored in `~/.claude/projects/` with encoded directory paths. There is **no built-in iteration tracking** or automatic state management for the infinite loop pattern. Each directory maintains independent conversation history.

## Research Findings

### Actual Session Storage

1. **Directory Structure**
```
~/.claude/
├── projects/
│   └── [encoded-directory-paths]/
│       ├── [session-uuid].jsonl     # Full conversation history
│       └── [summary-uuid].jsonl     # Conversation summaries
├── settings.json                     # Global preferences
├── .credentials.json                 # Authentication
└── statsig/                          # Analytics
```

2. **Path Encoding**
   - Directories encoded by replacing `/` with `-`
   - Example: `/home/user/project` → `-home-user-project`
   - Each directory has independent sessions

3. **No Migration Support**
   - Moving directories breaks continuity
   - Manual workaround required
   - No automatic state transfer

### Session Management Features

1. **Continue Previous Session**
```bash
# Continue most recent conversation
claude --continue

# Resume with prompt
claude --continue --print "Show progress"

# Show conversation picker
claude --resume
```

2. **Local Storage Only**
   - All data stored locally
   - No cloud sync
   - No cross-machine access

3. **JSONL Format**
   - Each message stored as JSON line
   - Full conversation history
   - Can be manually parsed

### What Doesn't Exist

The infinite loop pattern assumes features that **don't exist**:
- Automatic iteration number tracking
- Directory structure per iteration
- State files for progress
- Cross-iteration context sharing
- Automatic file naming conventions

### Manual Implementation

To achieve iteration management:

1. **Directory Structure**
```bash
#!/bin/bash
OUTPUT_DIR="output"
ITERATION=1

# Create iteration directory
mkdir -p "$OUTPUT_DIR/generation_$ITERATION"

# Track state manually
echo "$ITERATION" > "$OUTPUT_DIR/.current_iteration"

# Run Claude with context
claude -p "Generate iteration $ITERATION in $OUTPUT_DIR/generation_$ITERATION"
```

2. **State Tracking File**
```json
// state.json (manual)
{
  "current_iteration": 5,
  "completed_iterations": [1, 2, 3, 4],
  "output_directory": "output",
  "spec_file": "spec.md",
  "started": "2025-06-11T10:00:00Z"
}
```

3. **Progress Management**
```python
import json
import os
from datetime import datetime

class IterationManager:
    def __init__(self, output_dir="output"):
        self.output_dir = output_dir
        self.state_file = f"{output_dir}/.state.json"
        self.load_state()
    
    def load_state(self):
        if os.path.exists(self.state_file):
            with open(self.state_file) as f:
                self.state = json.load(f)
        else:
            self.state = {
                "current_iteration": 0,
                "completed": [],
                "started": datetime.now().isoformat()
            }
    
    def next_iteration(self):
        self.state["current_iteration"] += 1
        iter_dir = f"{self.output_dir}/generation_{self.state['current_iteration']}"
        os.makedirs(iter_dir, exist_ok=True)
        return iter_dir
    
    def complete_iteration(self):
        self.state["completed"].append(self.state["current_iteration"])
        self.save_state()
    
    def save_state(self):
        with open(self.state_file, 'w') as f:
            json.dump(self.state, f, indent=2)
```

### File Naming Patterns

1. **No Automatic Conventions**
   - Claude doesn't enforce naming
   - Manual specification required
   - No iteration variables in filenames

2. **Manual Naming**
```bash
# In prompt
claude -p "Save as ui_hybrid_${ITERATION}.html"

# Or in custom command
# File: .claude/commands/generate-ui.md
Generate UI component and save as:
ui_hybrid_$ARGUMENTS.html
```

### Context Window Management

1. **Per-Session Context**
   - Each Claude instance has own limit
   - No sharing between iterations
   - Manual summary required

2. **CLAUDE.md for Persistence**
   - Project-level context
   - Shared across sessions
   - Manual updates needed

### Community Workarounds

1. **Harper Reed's Approach**
   - Uses `prompt_plan.md` for tracking
   - Manual "completed" markers
   - Commits after each step

2. **Basic Memory Project**
   - External knowledge graph
   - Markdown-based persistence
   - MCP server for access

3. **Custom Scripts**
   - External state management
   - Progress tracking
   - Automated directory creation

## Conclusion
Claude Code provides basic session persistence per directory but lacks the sophisticated iteration management described in the infinite loop pattern. Any iteration tracking, directory structure management, or state persistence must be implemented externally through scripts and manual processes.

## References
- [Claude Code Tutorials - Resuming Sessions](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/tutorials)
- [Claude Code Continue After Directory Move (Gist)](https://gist.github.com/gwpl/e0b78a711b4a6b2fc4b594c9b9fa2c4c)
- [Feature Request: Session Context Persistence](https://github.com/anthropics/claude-code/issues/1741)
- [Basic Claude Code - Harper Reed](https://harper.blog/2025/05/08/basic-claude-code/)
- [Basic Memory CLAUDE.md](https://github.com/basicmachines-co/basic-memory/blob/main/CLAUDE.md)
