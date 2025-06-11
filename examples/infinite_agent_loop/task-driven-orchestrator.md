# **TASK-DRIVEN ADAPTIVE ORCHESTRATOR**

Ultra-think about this goal-oriented development system. You will receive a high-level objective and intelligently decompose it into specific implementation tasks, then deploy the optimal mix of specialized agents to achieve that goal.

## **COMMAND VARIABLES**

```
objective: $ARGUMENTS
project_root: $ARGUMENTS
constraints: $ARGUMENTS
max_agents: $ARGUMENTS
```

## **ARGUMENT PARSING**

Parse from "$ARGUMENTS":
1. `objective` - The high-level goal to achieve (e.g., "Add user authentication", "Optimize API performance", "Add multi-language support")
2. `project_root` - Root directory of the project (default: current directory)
3. `constraints` - Any specific constraints or requirements (optional)
4. `max_agents` - Maximum concurrent agents (default: 8)

## **PHASE 1: OBJECTIVE UNDERSTANDING**

**Deep Goal Analysis:**
```
OBJECTIVE_DECOMPOSITION:
1. Parse the high-level objective
2. Identify the type of task:
   - Feature Addition
   - Performance Improvement  
   - Bug Resolution
   - Refactoring Goal
   - Integration Task
   - Migration Objective
   
3. Extract key requirements:
   - What needs to be built/changed
   - Success criteria
   - Scope boundaries
   - Quality expectations
```

**Example Objective Breakdowns:**

```yaml
objective: "Add user authentication"
decomposed:
  core_requirements:
    - User registration system
    - Login/logout functionality
    - Session management
    - Password security
    - Account recovery
  
  technical_needs:
    - Database schema for users
    - Authentication middleware
    - API endpoints
    - Frontend forms
    - Security measures
    
  quality_requirements:
    - Unit tests for auth logic
    - Integration tests for flows
    - Security audit
    - Documentation
```

```yaml
objective: "Optimize API performance"
decomposed:
  analysis_needs:
    - Performance profiling
    - Bottleneck identification
    - Query analysis
    - Caching opportunities
    
  implementation_needs:
    - Query optimization
    - Caching layer
    - Index creation
    - Code refactoring
    
  validation_needs:
    - Performance benchmarks
    - Load testing
    - Regression tests
```

## **PHASE 2: PROJECT CONTEXT ANALYSIS**

**Targeted Project Scan:**
Based on the objective, perform focused analysis:

```python
def analyze_project_for_objective(objective, project_root):
    if objective.involves('authentication'):
        return {
            'existing_auth': scan_for_auth_systems(),
            'user_models': find_user_related_models(),
            'security_setup': analyze_security_measures(),
            'framework_auth': check_framework_auth_support(),
            'test_patterns': find_auth_test_patterns()
        }
    
    elif objective.involves('performance'):
        return {
            'slow_queries': profile_database_queries(),
            'bottlenecks': identify_performance_issues(),
            'caching_setup': analyze_cache_configuration(),
            'current_metrics': measure_baseline_performance(),
            'optimization_opportunities': find_quick_wins()
        }
    
    elif objective.involves('feature'):
        return {
            'integration_points': find_where_feature_fits(),
            'similar_features': analyze_existing_patterns(),
            'required_models': determine_data_needs(),
            'affected_modules': identify_impact_areas(),
            'test_requirements': assess_testing_needs()
        }
```

## **PHASE 3: INTELLIGENT TASK GENERATION**

**From Objective to Specific Tasks:**

```
TASK_GENERATION_ENGINE:

Given: objective + project_analysis
Output: specific_tasks_with_dependencies

Process:
1. Identify all work needed to achieve objective
2. Break down into atomic, actionable tasks
3. Determine dependencies between tasks
4. Estimate complexity and effort
5. Identify required expertise
6. Plan optimal execution order
```

**Dynamic Task Creation Examples:**

```yaml
# For "Add user authentication"
generated_tasks:
  foundation:
    - task: "Create user database schema"
      type: database
      dependencies: []
      complexity: medium
      
    - task: "Implement password hashing utility"
      type: security
      dependencies: []
      complexity: low
      
  core_features:
    - task: "Build registration API endpoint"
      type: api_development
      dependencies: ["user_schema", "password_hashing"]
      complexity: medium
      
    - task: "Create login/logout endpoints"
      type: api_development
      dependencies: ["user_schema", "password_hashing"]
      complexity: medium
      
    - task: "Implement JWT session management"
      type: security
      dependencies: ["login_endpoint"]
      complexity: high
      
  frontend:
    - task: "Create registration form component"
      type: frontend
      dependencies: ["registration_api"]
      complexity: medium
      
  quality:
    - task: "Write auth unit tests"
      type: testing
      dependencies: ["core_features"]
      complexity: medium
      
    - task: "Security audit auth flow"
      type: security_review
      dependencies: ["all_features"]
      complexity: high
```

## **PHASE 4: ADAPTIVE AGENT SELECTION**

**Agent Type Determination:**

```
AGENT_SELECTION_LOGIC:

For each generated_task:
    Determine optimal agent type based on:
    - Task type and requirements
    - Existing project patterns
    - Required expertise
    - Dependencies and timing
    
Spawn specialized agents:
    - Right expertise for each task
    - Optimal parallelization
    - Minimal conflicts
    - Maximum efficiency
```

**Specialized Agent Profiles:**

```yaml
Database Schema Agent:
  expertise: [SQL, migrations, ORMs, data modeling]
  responsibilities:
    - Design optimal schema
    - Write migration files
    - Set up indexes
    - Document schema

API Development Agent:
  expertise: [REST, GraphQL, authentication, validation]
  responsibilities:
    - Implement endpoints
    - Add validation
    - Handle errors
    - Follow API patterns

Security Implementation Agent:
  expertise: [cryptography, auth patterns, vulnerabilities]
  responsibilities:
    - Implement secure patterns
    - Hash passwords properly
    - Prevent common attacks
    - Audit security

Frontend Component Agent:
  expertise: [React/Vue/Angular, forms, UX patterns]
  responsibilities:
    - Build UI components
    - Handle user input
    - Manage state
    - Ensure accessibility

Test Specialist Agent:
  expertise: [testing frameworks, TDD, coverage]
  responsibilities:
    - Write comprehensive tests
    - Ensure edge cases
    - Maintain test speed
    - Document test cases

Integration Agent:
  expertise: [system design, APIs, middleware]
  responsibilities:
    - Connect components
    - Ensure compatibility
    - Handle data flow
    - Manage dependencies
```

## **PHASE 5: INTELLIGENT EXECUTION ORCHESTRATION**

**Execution Strategy Based on Task Analysis:**

```python
class TaskDrivenOrchestrator:
    def execute_objective(self, objective, tasks):
        # Group tasks by dependency level
        dependency_levels = topological_sort(tasks)
        
        # Determine execution strategy
        if has_complex_dependencies(tasks):
            return self.dependency_aware_execution(dependency_levels)
        elif all_independent(tasks):
            return self.parallel_blast(tasks)
        else:
            return self.wave_execution(dependency_levels)
    
    def dependency_aware_execution(self, levels):
        for level in levels:
            # Execute all tasks at this level in parallel
            agents = spawn_agents_for_tasks(level)
            execute_parallel(agents)
            wait_for_completion(agents)
            validate_level_output(level)
    
    def adaptive_agent_deployment(self, task):
        # Check what already exists
        if task.type == 'testing' and tests_exist_for(task.module):
            return spawn_test_updater_agent(task)
        elif task.type == 'api' and api_framework_detected():
            return spawn_framework_specific_agent(task)
        else:
            return spawn_generic_expert_agent(task)
```

## **PHASE 6: CONTEXT-AWARE TASK ADAPTATION**

**Real-Time Discoveries Affect Task Execution:**

```
ADAPTIVE_TASK_MODIFICATION:

If SecurityAgent discovers: "Project uses bcrypt"
    → Update all password tasks to use bcrypt
    
If APIAgent discovers: "Project uses GraphQL not REST"  
    → Retrain all API agents for GraphQL patterns
    
If TestAgent discovers: "Project uses Jest + RTL"
    → Configure all test agents with those tools
    
If DatabaseAgent discovers: "Using MongoDB not SQL"
    → Adjust all database tasks for NoSQL patterns
```

**Dynamic Task Refinement:**

```yaml
original_task: "Create user registration"
after_discovery: 
  refined_task: "Create user registration with:"
    - "Existing validation middleware"
    - "Team's error handling pattern"
    - "MongoDB user collection"
    - "Jest test suite"
    - "Existing email service"
```

## **PHASE 7: OBJECTIVE-DRIVEN QUALITY ASSURANCE**

**Quality Gates Specific to Objective:**

```python
def determine_quality_requirements(objective):
    if 'authentication' in objective:
        return {
            'security_audit': 'mandatory',
            'test_coverage': 95,
            'penetration_testing': True,
            'documentation': 'comprehensive'
        }
    
    elif 'performance' in objective:
        return {
            'benchmarks': 'before_and_after',
            'regression_tests': 'mandatory',
            'load_testing': True,
            'profiling_proof': True
        }
    
    elif 'mvp' in objective or 'prototype' in objective:
        return {
            'test_coverage': 60,
            'documentation': 'basic',
            'code_review': 'light'
        }
```

## **EXECUTION FLOW EXAMPLE**

**User Objective: "Add real-time chat feature"**

```
PHASE 1 - Understand Objective:
✓ Real-time bidirectional communication
✓ Multiple users per chat room
✓ Message persistence
✓ Online status indicators

PHASE 2 - Analyze Project:
✓ Found: Express.js backend
✓ Found: React frontend  
✓ Found: PostgreSQL database
✓ Found: Existing WebSocket setup
✓ Found: Current auth system

PHASE 3 - Generate Tasks:
Backend Tasks:
  1. Create message schema
  2. Create room schema  
  3. Implement Socket.io events
  4. Add message persistence
  5. Build chat REST endpoints
  
Frontend Tasks:
  6. Create chat UI component
  7. Implement Socket.io client
  8. Add message display
  9. Build user list component
  
Integration Tasks:
  10. Connect auth to chat
  11. Add real-time sync
  
Testing Tasks:
  12. Unit test chat logic
  13. Test real-time events
  14. E2E test full flow

PHASE 4 - Select Agents:
✓ Spawning Database Agent for schemas
✓ Spawning 2 Backend Agents for Socket.io
✓ Spawning 2 Frontend Agents for UI
✓ Spawning Integration Agent
✓ Spawning Test Specialist

PHASE 5 - Execute:
Wave 1: [Database schemas] [Socket.io setup]
Wave 2: [Chat endpoints] [UI components]  
Wave 3: [Integration] [Real-time sync]
Wave 4: [Testing] [Documentation]
```

## **MONITORING & PROGRESS TRACKING**

**Objective-Focused Dashboard:**

```
OBJECTIVE: Add User Authentication
================================
Progress: ████████████░░░░░░ 72%

DISCOVERED CONTEXT:
✓ Using Express + MongoDB
✓ Found existing User model
✓ JWT library available
✓ Test pattern established

TASK BREAKDOWN:
[✓] Database schema updates
[✓] Password hashing setup
[✓] Registration endpoint
[⟳] Login/logout endpoints (80%)
[⟳] JWT implementation (60%)
[○] Frontend forms
[○] Tests
[○] Documentation

ACTIVE AGENTS:
[API-1] Completing login endpoint
[API-2] Implementing JWT refresh
[SEC-1] Auditing auth flow
[TEST-1] Writing auth tests

BLOCKERS:
⚠️ Waiting for JWT implementation before frontend work

NEXT STEPS:
→ Frontend agents ready to spawn
→ Test specialist preparing
→ Documentation agent queued
```

## **ADVANCED FEATURES**

**Objective Chaining:**
```
If objective_completed successfully:
    suggest_next_logical_objective()
    
Example:
    Completed: "Add user authentication"
    Suggested: "Add role-based permissions"
```

**Learning from Execution:**
```
For future similar objectives:
    - Remember discovered patterns
    - Reuse successful task breakdowns
    - Apply learned optimizations
    - Avoid previous bottlenecks
```

**Intelligent Rollback:**
```
If objective_partially_failed:
    - Identify working components
    - Preserve successful changes
    - Rollback problematic parts
    - Suggest alternative approach
```

## **EXECUTION COMMAND**

Begin by deeply understanding the user's objective. Analyze the project to understand what specifically needs to be done to achieve that objective. Generate precise tasks, spawn specialized agents, and orchestrate their execution to deliver the objective efficiently and completely.