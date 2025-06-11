# Research: Context Sharing Between Agents

## Status: Limited File-Based Support

### Research Date: June 11, 2025

## Summary
Claude Code supports **file-based context sharing** between agents through "working scratchpads," but there is **no automatic context sharing mechanism**. Each Claude instance maintains separate context, and sharing requires explicit file operations.

## Research Findings

### Official Support for Context Sharing

From Anthropic's Best Practices documentation:
> "You can even have your Claude instances communicate with each other by giving them separate working scratchpads and telling them which one to write to and which one to read from. This separation often yields better results than having a single Claude handle everything."

Key points:
- Context sharing is achieved through files
- Each agent writes to designated scratchpad files
- Other agents read from these files
- This is a manual, explicit process

### How Context Sharing Works

1. **File-Based Communication**
   - Agent A writes to `scratchpad_a.md`
   - Agent B reads from `scratchpad_a.md`
   - Agents coordinate through shared files

2. **Git Worktrees Isolation**
   - Each worktree has isolated files
   - Shared repository history
   - Context sharing requires explicit file operations

3. **No Automatic Mechanism**
   - No built-in context synchronization
   - No shared memory between instances
   - Each instance has independent context window

### Practical Examples

**Basic Scratchpad Pattern:**
```bash
# Agent 1 instruction
"Write your findings about the authentication system to auth_analysis.md"

# Agent 2 instruction
"Read auth_analysis.md and implement tests based on the findings"
```

**Multiple Agent Coordination:**
```
Agent 1: Code writer → writes to implementation.md
Agent 2: Code reviewer → reads implementation.md, writes to review.md
Agent 3: Test writer → reads both files, creates tests
```

### Context Management Strategies

1. **Shared Documentation**
   - CLAUDE.md for project-wide context
   - Accessible by all instances
   - Manual updates required

2. **State Files**
   - Progress tracking files
   - Task completion markers
   - Dependency tracking

3. **Communication Protocols**
   - Define clear file naming conventions
   - Establish read/write patterns
   - Document communication flow

### Limitations

1. **No Real-Time Sync**
   - Files must be explicitly written and read
   - No automatic updates between agents
   - Potential for stale information

2. **Context Window Independence**
   - Each agent has its own context limit
   - Shared files count against each agent's context
   - No pooled context window

3. **Coordination Overhead**
   - Manual orchestration required
   - Explicit instructions for each agent
   - Potential for conflicts

### Community Implementations

1. **claude-squad**
   - External tool for managing multiple agents
   - No mention of advanced context sharing

2. **async-code**
   - Web UI for parallel agents
   - Docker isolation may complicate sharing

3. **Claude-SPARC**
   - Uses "memory_bank" directory structure:
     ```
     coordination/
     ├── memory_bank/
     │   ├── calibration_values.md
     │   ├── test_failures.md
     │   └── dependencies.md
     ```
   - Structured approach to shared knowledge

### Implementation Patterns

**Pattern 1: Sequential Handoff**
```bash
# Agent 1
claude -p "Analyze the codebase and write findings to analysis.md"

# Agent 2 (after Agent 1 completes)
claude -p "Read analysis.md and create implementation plan in plan.md"
```

**Pattern 2: Parallel with Merge**
```bash
# Run in parallel
claude -p "Research approach A, write to approach_a.md" &
claude -p "Research approach B, write to approach_b.md" &
wait

# Synthesis agent
claude -p "Read approach_a.md and approach_b.md, synthesize best solution"
```

**Pattern 3: Continuous Communication**
```
1. Create shared directories:
   mkdir -p shared/{input,output,state}

2. Agent instructions include:
   - "Check shared/input/ for new tasks"
   - "Write results to shared/output/"
   - "Update progress in shared/state/"
```

### Best Practices

1. **Clear File Organization**
   ```
   project/
   ├── agent_communication/
   │   ├── tasks/
   │   ├── results/
   │   └── state/
   ```

2. **Explicit Communication Protocol**
   - Define what each file contains
   - Specify read/write permissions
   - Document update frequencies

3. **Avoid Conflicts**
   - Assign unique output files per agent
   - Use timestamps or agent IDs in filenames
   - Implement locking mechanisms if needed

### What Doesn't Exist

- Automatic context synchronization
- Shared memory or state
- Built-in message passing
- Real-time communication
- Centralized context management
- Native inter-agent protocols

## Conclusion
Context sharing between Claude Code agents is possible but requires explicit file-based communication. The pattern described in the infinite loop documentation would need extensive external orchestration to manage context sharing at scale. While functional, this approach is far more manual than the seamless context sharing implied by the conceptual pattern.

## References
- [Claude Code Best Practices - Multiple Instances](https://www.anthropic.com/engineering/claude-code-best-practices)
- [How To Use Claude Code To Wield Coding Agent Clusters](https://www.pulsemcp.com/posts/how-to-use-claude-code-to-wield-coding-agent-clusters)
- [Claude-SPARC Coordination System](https://gist.github.com/ruvnet/e8bb444c6149e6e060a785d1a693a194)
