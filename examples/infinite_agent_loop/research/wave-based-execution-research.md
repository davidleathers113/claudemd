# Research: Wave-Based Execution

## Status: Not a Native Feature

### Research Date: June 11, 2025

## Summary
"Wave-based execution" (groups of parallel agents executing in waves) is **not an official Claude Code feature**. While parallel execution is supported through git worktrees and Claude 4 has parallel tool capabilities, the specific concept of coordinated waves is a conceptual pattern requiring external orchestration.

## Research Findings

### What Actually Exists

1. **Git Worktrees for Parallel Instances**
   - Official best practice for running multiple Claude instances
   - Each worktree provides isolated execution environment
   - Can run 3-10 instances simultaneously
   - Manual management required

2. **Claude 4 Parallel Tool Use**
   - Claude 4 models can "use tools in parallel"
   - Built-in capability for concurrent operations
   - Applies to API-level tool usage, not agent orchestration

3. **Sub-Agent Research Tasks**
   - Can request Claude to "research 3-5 ideas in parallel"
   - Limited to exploration/research, not full implementation
   - Results are synthesized by main Claude instance

### Community Implementations

1. **Claude-SPARC's BatchTool**
   - Community-created concept, not official
   - Described as enabling "parallel batch operations"
   - Part of a larger orchestration system
   - Requires external implementation

2. **async-code Project**
   - Web UI for managing multiple agents
   - Supports parallel execution
   - External tool, not built into Claude Code

3. **claude-squad**
   - CLI tool for managing multiple AI agents
   - External orchestration layer

### Wave Execution Reality

The "waves of 5 agents" pattern described in the infinite loop documentation:
- **Does not exist** as a built-in feature
- Would require external scripting
- No automatic wave management
- No built-in synchronization between waves

### Practical Parallel Execution

**Manual Approach with Git Worktrees:**
```bash
# Create multiple worktrees
for i in {1..5}; do
  git worktree add ../feature-$i main
done

# Run Claude in each (manually)
cd ../feature-1 && claude
# In new terminal: cd ../feature-2 && claude
# etc.
```

**Scripted Parallel Execution:**
```bash
#!/bin/bash
# Run 5 Claude instances in parallel
for i in {1..5}; do
  (
    cd worktree-$i
    claude -p "Generate variation $i" > output-$i.log
  ) &
done
wait # Wait for all background jobs
```

**GitHub Actions Parallel Execution:**
- Multiple Claude agents can run in parallel workflows
- Managed by GitHub Actions, not Claude Code itself
- Example from research: "Multiple Claude Code agents work on your codebase in parallel"

### Key Insights from Research

1. **10x Engineer Concept**: One developer managing up to 10 Claude instances
2. **Practical Limit**: Most users report managing 3 agents effectively
3. **Manual Orchestration**: All parallel execution requires human or script coordination
4. **No Wave Synchronization**: No built-in mechanism for wave-based coordination

### Implementation Requirements

To create wave-based execution:
1. **External Orchestrator**: Script to manage waves
2. **Process Management**: Track running instances
3. **Synchronization Logic**: Wait for wave completion
4. **Result Collection**: Gather outputs from each wave
5. **Context Management**: Share information between waves

Example implementation concept:
```python
def run_wave(wave_number, agents_per_wave=5):
    processes = []
    for i in range(agents_per_wave):
        agent_id = (wave_number - 1) * agents_per_wave + i
        cmd = f"claude -p 'Generate variation {agent_id}'"
        process = subprocess.Popen(cmd, shell=True)
        processes.append(process)
    
    # Wait for wave to complete
    for p in processes:
        p.wait()
    
    print(f"Wave {wave_number} completed")
```

## Conclusion
Wave-based execution is a **conceptual pattern** not implemented in Claude Code. While parallel execution is possible through git worktrees and external tools, the specific concept of coordinated waves executing groups of agents requires custom orchestration built on top of Claude Code's actual capabilities.

## References
- [Claude Code Best Practices - Git Worktrees](https://www.anthropic.com/engineering/claude-code-best-practices)
- [How To Use Claude Code To Wield Coding Agent Clusters](https://www.pulsemcp.com/posts/how-to-use-claude-code-to-wield-coding-agent-clusters)
- [Claude 4 Announcement - Parallel Tool Use](https://www.anthropic.com/news/claude-4)
- [Claude-SPARC System](https://gist.github.com/ruvnet/e8bb444c6149e6e060a785d1a693a194)
- [Faster Claude Code agents in GitHub Actions](https://depot.dev/blog/claude-code-in-github-actions)
