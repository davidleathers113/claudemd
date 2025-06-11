# Research: /agent Command

## Status: Does Not Exist

### Research Date: June 11, 2025

## Summary
The `/agent` command is **completely fictional**. It does not exist in Claude Code and appears to be part of the conceptual infinite agent loop pattern that demonstrates desired functionality rather than actual features.

## Evidence

### 1. GitHub Repository Analysis
- Examined https://github.com/disler/infinite-agentic-loop
- Empty `.claude/commands/` directory
- No implementation files found
- Conceptual documentation only

### 2. Official Documentation
- No mention in Claude Code docs
- Not listed in CLI usage guide
- Absent from command references
- No hidden command evidence

### 3. Community Research
- No usage examples found
- No error reports about `/agent`
- No discussions of the command
- Only appears in infinite loop context

### 4. Technical Analysis
- Would require implementation in `.claude/commands/agent.md`
- No such file exists in any repository
- Command syntax doesn't match Claude Code patterns
- Uses non-existent flags like `--prompt-file`

## What It Was Supposed to Do

According to the infinite loop documentation:
```bash
/agent --prompt-file infinite.md --spec_file spec.md --output_dir output --count 50
```

This would theoretically:
- Spawn autonomous agents
- Use orchestration file (`infinite.md`)
- Read specifications (`spec.md`)
- Manage output directory
- Control iteration count

## Reality

To achieve similar functionality, you would need:

1. **External Orchestration Script**
```python
import subprocess
import os

def run_agent(iteration, spec_file, output_dir):
    prompt = f"Act as agent {iteration}, implement {spec_file}"
    subprocess.run(['claude', '-p', prompt])
```

2. **Git Worktrees for Parallelism**
```bash
# Create parallel environments
git worktree add ../agent-1
cd ../agent-1 && claude
```

3. **Custom Commands**
```markdown
# .claude/commands/simulate-agent.md
Simulate agent behavior for: $ARGUMENTS
```

## Conclusion

The `/agent` command is a conceptual placeholder in the infinite agent loop pattern, not a real Claude Code feature. It represents the desired functionality of spawning and managing multiple AI agents, which must be implemented through external tooling and orchestration.