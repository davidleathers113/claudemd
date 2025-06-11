# Research: Sub-Agent Spawning

## Status: Partially Supported

### Research Date: June 11, 2025

## Summary
Claude Code **does support sub-agents**, but not in the automated way described in the infinite loop pattern. Sub-agents can be created through specific prompting, and true parallel execution is achieved through git worktrees or external orchestration tools.

## Research Findings

### Official Support for Sub-Agents
From Boris at Anthropic (Latent Space interview):
> "I want to refactor X to do Y. Can you research three separate ideas for how to do it? Do it in parallel. Use three agents to do it. And so in the UI, when you see a task that's actually like a sub-Claude, it's a sub-agent."

Key points:
- Sub-agents are created when you explicitly ask for parallel research
- They appear in the UI as distinct sub-tasks
- This is a built-in capability of Claude Code

### How Sub-Agents Work
1. **Request-Based**: You must explicitly ask for parallel investigation
2. **Research Tasks**: Best suited for exploration and research, not implementation
3. **Context Isolation**: Each sub-agent works independently
4. **Results Synthesis**: Main Claude instance summarizes findings

### Example Usage
```
"Research three different approaches to implement authentication:
1. JWT tokens
2. Session-based auth
3. OAuth integration
Do this in parallel using three agents."
```

### Git Worktrees for True Parallel Execution
The **official best practice** for parallel Claude instances:

```bash
# Create worktrees for parallel work
git worktree add ../project-feature-a feature-a
git worktree add ../project-feature-b feature-b

# Run separate Claude instances
cd ../project-feature-a && claude
cd ../project-feature-b && claude
```

Benefits:
- Complete isolation between instances
- Shared repository base
- No conflicts between parallel work
- Can run 3-10 instances simultaneously

### Community Tools for Parallel Management

1. **async-code** (GitHub: ObservedObserver/async-code)
   - Web UI for managing multiple Claude agents
   - Codex-style interface
   - Docker containerization for isolation
   - Automatic git integration

2. **claude-squad** (GitHub: smtg-ai/claude-squad)
   - CLI tool for managing multiple AI agents
   - Supports Claude Code, Aider, Codex, Amp
   - Terminal-based management

3. **Claude-SPARC**
   - Uses "BatchTool" for parallel operations
   - Orchestrates multiple development phases
   - Community implementation, not official

### Limitations vs. Infinite Loop Concept
What **doesn't exist**:
- Automatic spawning of unlimited sub-agents
- Wave-based execution (5 agents at a time)
- Built-in orchestration engine
- Automatic directory creation per sub-agent
- Context passing between waves

What **does exist**:
- Manual sub-agent creation through prompting
- Git worktree-based parallel execution
- External tools for orchestration
- Limited parallel research capabilities

### Practical Implementation
To achieve something similar to the infinite loop pattern:

1. **Using Sub-Agents** (Limited):
```
"Investigate 5 different UI component designs in parallel.
For each design, consider:
- Color schemes
- Layout patterns
- User interactions"
```

2. **Using Git Worktrees** (Recommended):
```bash
#!/bin/bash
# Script to spawn multiple Claude instances
for i in {1..5}; do
  git worktree add ../gen-$i main
  cd ../gen-$i
  claude -p "Generate variation $i based on spec.md" &
done
```

3. **Using External Tools**:
- async-code for web-based management
- claude-squad for CLI management
- Custom scripts for orchestration

### Key Insights
1. **Sub-agents exist** but are limited to research/exploration tasks
2. **Git worktrees** provide the best official method for parallel execution
3. **External orchestration** is required for complex patterns
4. **Community tools** fill the gap for advanced use cases

## Conclusion
Sub-agent spawning is a real Claude Code feature, but it's much more limited than the infinite loop pattern suggests. The pattern's vision of automatic, unlimited sub-agent orchestration requires external tooling built on top of Claude Code's actual capabilities.

## References
- [Claude Code: Anthropic's Agent in Your Terminal (Latent Space)](https://www.latent.space/p/claude-code)
- [Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)
- [How To Use Claude Code To Wield Coding Agent Clusters](https://www.pulsemcp.com/posts/how-to-use-claude-code-to-wield-coding-agent-clusters)
- [async-code GitHub Repository](https://github.com/ObservedObserver/async-code)
- [Claude-SPARC System](https://gist.github.com/ruvnet/e8bb444c6149e6e060a785d1a693a194)
