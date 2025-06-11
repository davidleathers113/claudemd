# **PARALLEL MULTI-FILE DEVELOPMENT ORCHESTRATOR**

Ultra-think about this sophisticated parallel development system. You are about to coordinate multiple concurrent development tasks across different files to dramatically accelerate project completion.

## **COMMAND VARIABLES**

```
project_spec: $ARGUMENTS  
task_manifest: $ARGUMENTS
work_mode: $ARGUMENTS
max_agents: $ARGUMENTS
```

## **ARGUMENT PARSING**

Parse the following from "$ARGUMENTS":
1. `project_spec` - Path to project specification or README
2. `task_manifest` - Path to task list file OR inline task description
3. `work_mode` - "parallel" | "wave" | "dependency-aware"
4. `max_agents` - Maximum concurrent agents (default: 5)

## **PHASE 1: PROJECT COMPREHENSION**

**Deep Project Analysis:**
1. Read and understand the project specification/README
2. Map the entire codebase structure and architecture
3. Identify key dependencies and relationships between files
4. Understand coding standards, patterns, and conventions
5. Analyze test structure and requirements
6. Document the technology stack and frameworks

**Codebase Intelligence Gathering:**
```
ANALYZE:
- File structure and organization patterns
- Import/dependency graphs between modules
- Existing code style and conventions
- Test coverage and testing patterns
- Build and configuration files
- Documentation structure
```

## **PHASE 2: TASK MANIFEST PROCESSING**

**Task Manifest Interpretation:**
The task manifest can be:
- A markdown file with task list
- A JSON/YAML file with structured tasks
- Inline description of multiple tasks
- GitHub issues list
- TODO comments extracted from code

**Task Structure:**
```yaml
tasks:
  - id: task-1
    type: create|update|fix|refactor|test|document
    files: 
      - path/to/file1.js
      - path/to/file2.py
    description: "Task description"
    dependencies: [task-ids]
    priority: high|medium|low
    estimated_complexity: simple|moderate|complex
```

**Task Analysis Protocol:**
1. Parse all tasks and their requirements
2. Build dependency graph between tasks
3. Identify independent task groups
4. Estimate complexity and time requirements
5. Plan optimal parallel execution strategy

## **PHASE 3: PARALLEL EXECUTION STRATEGY**

**Work Mode Strategies:**

### **1. Parallel Mode (Maximum Speed)**
- Launch all independent tasks simultaneously
- Best for tasks with no interdependencies
- Maximum throughput, may cause merge conflicts

### **2. Wave Mode (Balanced Approach)**
- Execute tasks in coordinated waves
- Wave 1: Foundation tasks (configs, interfaces, types)
- Wave 2: Core implementations
- Wave 3: Integration and connections
- Wave 4: Tests and documentation

### **3. Dependency-Aware Mode (Intelligent Orchestration)**
- Analyze task dependency graph
- Execute in topological order
- Parallelize within dependency levels
- Automatic blocking and resumption

**Agent Allocation Algorithm:**
```
FOR each execution_wave:
  1. Identify available tasks (no pending dependencies)
  2. Group by file locality to minimize conflicts
  3. Assign complexity scores
  4. Distribute tasks to available agents
  5. Balance workload across agents
```

## **PHASE 4: SUB-AGENT DEPLOYMENT**

**Sub-Agent Architecture:**
Each sub-agent receives:
1. **Project Context**: Full codebase understanding
2. **Task Assignment**: Specific files and operations
3. **Dependency Awareness**: What they must wait for/not break
4. **Integration Points**: How their work connects to others
5. **Quality Standards**: Testing and documentation requirements

**Sub-Agent Task Template:**
```
AGENT [ID] - DEVELOPMENT TASK

ASSIGNMENT:
- Primary Files: [List of files to create/modify]
- Operation Type: [create|update|fix|refactor|test]
- Task Description: [Detailed requirements]

CONTEXT:
- Project Structure: [Relevant architecture info]
- Dependencies: [What this task depends on]
- Dependents: [What depends on this task]
- Related Files: [Files that might need minor updates]

EXECUTION PROTOCOL:
1. Analyze existing code and patterns
2. Plan implementation approach
3. Write/modify code following project standards
4. Update imports and dependencies
5. Add/update tests as needed
6. Update documentation
7. Verify integration points

CONSTRAINTS:
- Do NOT modify: [Protected files list]
- Must maintain compatibility with: [Interfaces/APIs]
- Follow patterns from: [Example files]
- Coordinate through: [Shared state files]

OUTPUT:
- Modified/created files with full implementations
- Test files for new functionality
- Updated imports in dependent files
- Documentation updates
- Status report: COMPLETED|BLOCKED|PARTIAL
```

## **PHASE 5: INTELLIGENT COORDINATION**

**Conflict Prevention System:**
1. **File Locking Simulation**
   - Track which agent is modifying which files
   - Queue overlapping modifications
   - Merge changes intelligently

2. **Shared State Management**
   ```
   .dev-orchestrator/
   ├── task-status.json      # Real-time task status
   ├── file-locks.json       # File modification tracking
   ├── dependencies.json     # Dependency resolution
   ├── integration-points.md # Shared interfaces
   └── agent-reports/        # Individual agent outputs
   ```

3. **Communication Protocol**
   - Agents write status updates to shared state
   - Check for blocking dependencies before proceeding
   - Report interface changes that affect others
   - Flag integration points needing attention

**Progressive Integration Strategy:**
```
WHILE tasks_remaining:
  1. Check completed tasks
  2. Update dependency graph
  3. Identify newly unblocked tasks
  4. Assign to available agents
  5. Monitor for conflicts
  6. Merge completed work
  7. Run integration tests
  8. Update project state
```

## **PHASE 6: CONTINUOUS DEVELOPMENT CYCLES**

**Iterative Improvement Protocol:**
1. **Initial Implementation Wave**
   - Core functionality
   - Basic structure
   - Primary interfaces

2. **Enhancement Wave**
   - Error handling
   - Edge cases
   - Performance optimization

3. **Quality Wave**
   - Comprehensive tests
   - Documentation
   - Code cleanup

4. **Integration Wave**
   - Cross-component testing
   - System integration
   - Final polish

**Adaptive Execution:**
```python
while not all_tasks_complete():
    # Assess current state
    completed = check_completed_tasks()
    blocked = identify_blocked_tasks()
    available = find_available_tasks()
    
    # Adaptive agent allocation
    if blocked > available:
        focus_on_unblocking_tasks()
    elif critical_path_at_risk():
        prioritize_critical_path()
    else:
        maximize_parallelism()
    
    # Launch next wave
    deploy_agents(optimized_task_assignment)
    
    # Monitor and adjust
    handle_agent_completions()
    resolve_conflicts()
    update_project_state()
```

## **PHASE 7: QUALITY ASSURANCE ORCHESTRATION**

**Parallel Quality Checks:**
1. **Syntax Validation** - Immediate per-file
2. **Unit Testing** - Per component completion
3. **Integration Testing** - Per wave completion
4. **Linting & Formatting** - Continuous
5. **Documentation Verification** - Per feature

**Test Coordination:**
```
TEST AGENT PROTOCOL:
- Monitor file modifications
- Generate/update tests in parallel
- Run tests incrementally
- Report failures immediately
- Block dependent tasks on test failure
```

## **EXECUTION PRINCIPLES**

**Maximum Velocity:**
- Parallelize everything possible
- Minimize blocking dependencies
- Use speculative execution where safe
- Cache shared computations

**Quality Maintenance:**
- Never sacrifice correctness for speed
- Maintain test coverage throughout
- Document as you go
- Regular integration checkpoints

**Intelligent Coordination:**
- Dynamic task reallocation based on progress
- Automatic conflict resolution
- Smart dependency management
- Continuous optimization of execution plan

**Failure Resilience:**
- Graceful handling of task failures
- Automatic retry with different approaches
- Dependency graph updates on failures
- Progress preservation

## **ULTRA-THINKING REQUIREMENTS**

Before execution, deeply consider:

**Optimization Strategies:**
- Optimal task grouping for minimal conflicts
- Critical path identification
- Bottleneck prediction and mitigation
- Resource utilization patterns

**Risk Analysis:**
- Potential conflict points
- Complex integration challenges
- Testing bottlenecks
- Documentation gaps

**Acceleration Opportunities:**
- Parallel test generation
- Speculative implementation
- Preemptive integration
- Automated documentation

**Coordination Challenges:**
- Merge conflict prevention
- API contract management
- State synchronization
- Progress tracking

## **MONITORING & REPORTING**

**Real-time Dashboard:**
```
PARALLEL DEVELOPMENT STATUS
========================
Active Agents: 5/5
Tasks Complete: 12/25 (48%)
Current Wave: 3
Estimated Time: 15 mins

AGENT STATUS:
[1] ✓ Created auth module
[2] ⟳ Updating API endpoints (75%)
[3] ⟳ Writing tests for user service
[4] ✓ Refactored database layer
[5] ⟳ Fixing validation bugs

BLOCKED TASKS: 2
CONFLICTS: 0
TEST STATUS: 18/20 passing
```

## **ADVANCED FEATURES**

**Git Worktree Integration:**
When available, use git worktrees for true parallel isolation:
```bash
# For each agent working on separate features
git worktree add ../agent-1-workspace feature-1
git worktree add ../agent-2-workspace feature-2
```

**Speculative Execution:**
- Implement multiple solutions in parallel
- Choose best approach after evaluation
- Merge winning implementations

**Auto-scaling:**
- Dynamically adjust agent count based on:
  - Task complexity
  - Available context window
  - Conflict frequency
  - Progress velocity

Begin orchestration with ultra-deep analysis of the project and task requirements. Deploy sub-agents strategically to achieve maximum development velocity while maintaining code quality and coherence.