# Research: Parallel Execution Architecture

## Status: Limited Native Support

### Research Date: June 11, 2025

## Summary
Claude Code has **limited native support** for parallel execution. While git worktrees enable multiple instances and Claude 4 supports parallel tool use, there is **no built-in process management** or resource allocation system. True parallel execution architecture requires external orchestration.

## Research Findings

### Native Parallel Capabilities

1. **Git Worktrees (Official Method)**
   - Create multiple working directories
   - Run separate Claude instances
   - Each has isolated file system
   - Shared git history
   ```bash
   git worktree add ../feature-a feature-a
   git worktree add ../feature-b feature-b
   # Run Claude in each worktree independently
   ```

2. **Claude 4 Parallel Tool Use**
   - Models can "use tools in parallel"
   - Applies to API-level operations
   - Not for orchestrating multiple agents
   - Improves single-instance performance

3. **Concurrent Read Operations**
   - Read-only tools execute in parallel
   - Write operations run sequentially
   - Automatic classification of operations
   - Results maintain original ordering

### Parallel Execution Implementation

**From Claude Code Architecture Research:**
```javascript
// Concurrent execution for read-only operations
async function runConcurrently(toolUses) {
  const generators = toolUses.map(toolUse => {
    const tool = findToolByName(toolUse.name)!;
    return tool.call(toolUse.parameters);
  });
  
  const results = [];
  for await (const result of all(generators)) {
    results.push({ ...result, toolIndex: result.generatorIndex });
  }
  
  return results.sort((a, b) => a.toolIndex - b.toolIndex);
}

// Sequential execution for stateful operations
async function runSequentially(toolUses) {
  const results = [];
  for (const toolUse of toolUses) {
    const tool = findToolByName(toolUse.name)!;
    const generator = tool.call(toolUse.parameters);
    for await (const result of generator) {
      results.push(result);
    }
  }
  return results;
}
```

### Resource Management

1. **No Built-in Management**
   - No process limits
   - No memory allocation
   - No CPU throttling
   - No queue management

2. **Manual Control Required**
   - OS-level process management
   - External monitoring tools
   - Custom resource limits
   - Manual coordination

3. **Practical Limits**
   - 3-10 instances manageable
   - API rate limits apply
   - Context window per instance
   - System resources constrain total

### External Orchestration Patterns

1. **Shell Script Orchestration**
```bash
#!/bin/bash
# Simple parallel execution
MAX_PARALLEL=5
for i in $(seq 1 $MAX_PARALLEL); do
  (
    cd worktree-$i
    claude -p "Task $i" > output-$i.log 2>&1
  ) &
done
wait # Wait for all background jobs
```

2. **Process Management Tools**
```bash
# Using GNU Parallel
parallel -j 5 'claude -p "Task {}" > output-{}.log' ::: {1..20}

# Using tmux
for i in {1..5}; do
  tmux new-window -n "claude-$i" "claude"
done
```

3. **GitHub Actions Parallel**
   - Multiple Claude agents in workflows
   - Parallel task processing
   - Managed by GitHub infrastructure
   - Example: Depot runners for optimization

### Community Implementations

1. **claude-parallel-work**
   - Docker containerization
   - Task breakdown and analysis
   - SQLite state management
   - Git-based workflow

2. **async-code**
   - Web UI for parallel management
   - Codex-style interface
   - Docker isolation
   - Support for multiple agents

3. **Claude-SPARC BatchTool**
   - Conceptual parallel operations
   - Task coordination patterns
   - Not actual implementation
   - Requires external scripting

### Architecture Patterns

**Pattern 1: Worker Pool**
```python
import subprocess
from concurrent.futures import ThreadPoolExecutor

def run_claude_task(task_id, prompt):
    cmd = f'claude -p "{prompt}"'
    result = subprocess.run(cmd, shell=True, capture_output=True)
    return task_id, result.stdout

with ThreadPoolExecutor(max_workers=5) as executor:
    tasks = [(i, f"Task {i}") for i in range(20)]
    futures = [executor.submit(run_claude_task, *task) for task in tasks]
    results = [f.result() for f in futures]
```

**Pattern 2: Queue-Based**
```javascript
// Node.js queue implementation
const Queue = require('bull');
const claudeQueue = new Queue('claude tasks');

claudeQueue.process(5, async (job) => {
  const { prompt } = job.data;
  const result = await execAsync(`claude -p "${prompt}"`);
  return result;
});

// Add tasks
for (let i = 0; i < 100; i++) {
  claudeQueue.add({ prompt: `Task ${i}` });
}
```

**Pattern 3: Orchestrator Service**
- Central coordinator
- Task distribution
- Result collection
- State management
- Error handling

### Performance Considerations

1. **Parallel Benefits**
   - Multiple tasks simultaneously
   - Better resource utilization
   - Reduced total time
   - Independent failures

2. **Parallel Challenges**
   - Context window per instance
   - API rate limiting
   - Resource contention
   - Coordination overhead

3. **Optimization Strategies**
   - Batch similar tasks
   - Share read-only resources
   - Use lightweight instances
   - Monitor resource usage

### What Doesn't Exist

- Built-in process spawning
- Automatic load balancing
- Native task queues
- Resource pooling
- Distributed execution
- Cluster management
- Native parallel primitives

## Conclusion
Claude Code's parallel execution architecture is **minimal by design**. While git worktrees and concurrent tool use provide some parallelism, true parallel agent orchestration requires extensive external tooling. The infinite loop pattern's vision of automatic parallel execution would need a complete orchestration layer built on top of Claude Code.

## References
- [Claude Code Best Practices - Git Worktrees](https://www.anthropic.com/engineering/claude-code-best-practices)
- [Building an Agentic System - Parallel Execution](https://gerred.github.io/building-an-agentic-system/parallel-tool-execution.html)
- [How To Use Claude Code To Wield Coding Agent Clusters](https://www.pulsemcp.com/posts/how-to-use-claude-code-to-wield-coding-agent-clusters)
- [claude-parallel-work GitHub](https://github.com/ddfourtwo/claude-parallel-work)
- [Claude 4 Announcement - Parallel Tool Use](https://www.anthropic.com/news/claude-4)
