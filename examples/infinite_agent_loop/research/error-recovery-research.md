# Research: Error Recovery - Built-in Error Recovery Mechanisms for Multi-Agent Scenarios

## Summary
Claude Code provides basic error handling through intelligent retry mechanisms and observability features, but lacks sophisticated multi-agent error recovery. Most error recovery in multi-agent scenarios requires external implementation using patterns like exponential backoff, circuit breakers, and manual coordination.

## Key Findings

### 1. Built-in Error Recovery Features

**Intelligent Retry Mechanisms**
- Automatic retry for transient failures
- Heartbeat monitoring for agent health
- Basic timeout detection
- Limited to single-agent context

**Autonomous Feedback Loops**
- Agents can assess their own failures
- Access to error codes and stack traces
- Self-correcting behavior possible
- No cross-agent coordination

**Error Observability**
- Detailed error logging
- Stack trace capture
- Error code visibility
- `/doctor` command for health checks

**Verbose Mode Support**
- `--verbose` flag for debugging
- Turn-by-turn output visibility
- Helpful for diagnosing failures
- Manual intervention required

### 2. API Error Handling

**Common Error Types**
- 429 Rate Limit Errors
- 529 Overloaded Errors
- Network timeouts
- Context window exceeded
- Permission denied

**Retry Strategies (External Implementation Required)**
```python
# Example exponential backoff implementation
import time
import random

def retry_with_backoff(func, max_retries=5):
    for attempt in range(max_retries):
        try:
            return func()
        except Exception as e:
            if attempt == max_retries - 1:
                raise
            wait_time = (2 ** attempt) + random.uniform(0, 1)
            time.sleep(wait_time)
```

**Error Response Handling**
- Clear error messages provided
- Actionable feedback when possible
- Graceful degradation patterns
- User notification of failures

### 3. Multi-Agent Error Scenarios

**Agent-Level Failures**
- Individual agent crashes
- Context overflow errors
- Permission violations
- Resource exhaustion

**Coordination Failures**
- No built-in agent communication
- File lock conflicts possible
- Race conditions in shared resources
- Synchronization errors

**Cascade Failures**
- One agent's failure affects others
- No automatic isolation
- Manual intervention required
- Potential data corruption

### 4. Recovery Patterns (Manual Implementation)

**Circuit Breaker Pattern**
```python
class CircuitBreaker:
    def __init__(self, failure_threshold=5, recovery_timeout=60):
        self.failure_count = 0
        self.failure_threshold = failure_threshold
        self.recovery_timeout = recovery_timeout
        self.last_failure_time = None
        self.state = 'closed'  # closed, open, half-open
```

**Checkpoint and Resume**
```bash
# Manual checkpointing for long-running tasks
save_checkpoint() {
    echo "Saving state at iteration $1"
    cp -r output/ checkpoints/iteration_$1/
}

resume_from_checkpoint() {
    iteration=$1
    cp -r checkpoints/iteration_$iteration/* output/
    echo "Resumed from iteration $iteration"
}
```

**Dead Letter Queue**
```python
# Failed tasks go to dead letter queue
failed_tasks = []

def process_with_dlq(task):
    try:
        process_task(task)
    except Exception as e:
        failed_tasks.append({
            'task': task,
            'error': str(e),
            'timestamp': time.time()
        })
```

### 5. Limitations in Multi-Agent Scenarios

**No Native Coordination**
- Agents can't detect peer failures
- No health monitoring across agents
- Manual orchestration required
- External monitoring needed

**Limited Recovery Options**
- No automatic agent restart
- No state synchronization
- No distributed transactions
- Manual cleanup required

**Resource Management**
- No automatic resource release
- File locks may persist
- Memory not reclaimed
- API quota not redistributed

## Practical Implementation Strategies

### For Infinite Loop Error Recovery

1. **Wave-Level Recovery**
```python
class WaveManager:
    def execute_wave_with_recovery(self, agents):
        results = []
        failed_agents = []
        
        for agent in agents:
            try:
                result = self.execute_agent(agent)
                results.append(result)
            except Exception as e:
                failed_agents.append((agent, e))
                
        # Retry failed agents once
        for agent, error in failed_agents:
            try:
                result = self.execute_agent(agent)
                results.append(result)
            except:
                # Log permanent failure
                self.log_failure(agent, error)
                
        return results
```

2. **State Persistence**
```bash
# Persist state between failures
persist_state() {
    echo "{
        'iteration': $CURRENT_ITERATION,
        'completed': $COMPLETED_COUNT,
        'failed': $FAILED_COUNT,
        'timestamp': $(date +%s)
    }" > .state/progress.json
}

recover_state() {
    if [ -f .state/progress.json ]; then
        source <(jq -r 'to_entries|.[]|"export \(.key)=\(.value)"' .state/progress.json)
    fi
}
```

3. **Health Monitoring**
```python
# External health monitor
class AgentHealthMonitor:
    def __init__(self):
        self.agents = {}
        self.check_interval = 30
        
    def register_agent(self, agent_id):
        self.agents[agent_id] = {
            'last_heartbeat': time.time(),
            'status': 'healthy'
        }
        
    def check_health(self):
        current_time = time.time()
        for agent_id, info in self.agents.items():
            if current_time - info['last_heartbeat'] > 60:
                info['status'] = 'unhealthy'
                self.trigger_recovery(agent_id)
```

## Best Practices for Error Recovery

### Single Agent
1. Use verbose mode for debugging
2. Implement retry with backoff
3. Monitor context usage
4. Save progress frequently

### Multi-Agent
1. **Isolate Failures**
   - Use git worktrees
   - Separate output directories
   - Independent state files

2. **Monitor Collectively**
   - External health checks
   - Aggregate error logs
   - Central monitoring dashboard

3. **Graceful Degradation**
   - Continue with working agents
   - Mark failed iterations
   - Generate partial results

### Recovery Strategies

1. **Preventive Measures**
   - Resource limits per agent
   - Early context window checks
   - Input validation
   - Sanity checks

2. **Detective Controls**
   - Comprehensive logging
   - Real-time monitoring
   - Anomaly detection
   - Performance metrics

3. **Corrective Actions**
   - Automatic retries
   - Manual intervention points
   - Rollback capabilities
   - Clean restart procedures

## Comparison Table

| Feature | Built-in Support | External Required |
|---------|-----------------|-------------------|
| Single retry | ✓ Basic | Enhanced patterns |
| Error logging | ✓ Comprehensive | Aggregation |
| Health checks | ✓ `/doctor` | Multi-agent monitoring |
| State recovery | ✗ None | Checkpointing |
| Agent coordination | ✗ None | Orchestration |
| Cascade prevention | ✗ None | Circuit breakers |

## Future Considerations

### Potential Improvements
- Native multi-agent monitoring
- Built-in checkpoint/resume
- Distributed error handling
- Automatic recovery strategies

### Community Solutions
- Error recovery frameworks
- Monitoring dashboards
- Orchestration tools
- Recovery automation scripts

## Conclusion

Claude Code provides foundational error recovery mechanisms suitable for single-agent scenarios, including retry logic and comprehensive error observability. However, multi-agent error recovery requires significant external implementation. The lack of native coordination between agents means that sophisticated patterns like circuit breakers, checkpoint/resume, and health monitoring must be built on top of Claude Code's basic features. For production multi-agent systems, teams should implement comprehensive error recovery strategies using external orchestration and monitoring tools to ensure reliability at scale.