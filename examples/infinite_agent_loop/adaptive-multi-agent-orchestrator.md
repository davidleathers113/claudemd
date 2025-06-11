# **ADAPTIVE MULTI-AGENT ORCHESTRATOR**

Ultra-think about this self-organizing development system. You are about to deploy a sophisticated AI workforce that dynamically adapts to project needs, spinning up specialized agents of various types based on intelligent analysis of the codebase and requirements.

## **COMMAND VARIABLES**

```
project_root: $ARGUMENTS
objectives: $ARGUMENTS  
constraints: $ARGUMENTS
max_agents: $ARGUMENTS
```

## **ARGUMENT PARSING**

Parse from "$ARGUMENTS":
1. `project_root` - Root directory of the project
2. `objectives` - High-level goals (optional - will auto-detect if not provided)
3. `constraints` - Time/resource/quality constraints
4. `max_agents` - Maximum concurrent agents (default: 10)

## **PHASE 1: INTELLIGENT PROJECT ANALYSIS**

**Deep Discovery Protocol:**
```
PROJECT_SCAN:
1. Codebase Health Analysis
   - Test coverage detection
   - Documentation completeness
   - Code quality metrics
   - Technical debt indicators
   - Security vulnerabilities
   - Performance bottlenecks

2. Architecture Understanding
   - Technology stack identification
   - Module dependency mapping
   - API surface analysis
   - Database schema comprehension
   - Build system understanding
   - Deployment configuration

3. Development State Assessment
   - TODO/FIXME comment extraction
   - Incomplete implementations
   - Missing test files
   - Undocumented modules
   - Broken integrations
   - Outdated dependencies

4. Project Maturity Evaluation
   - Development phase (prototype/production)
   - Code stability metrics
   - Change frequency patterns
   - Critical path identification
```

**Automated Need Detection:**
```python
def analyze_project_needs():
    needs = {
        'development': [],
        'testing': [],
        'refactoring': [],
        'documentation': [],
        'integration': [],
        'performance': [],
        'security': [],
        'maintenance': []
    }
    
    # Smart detection algorithms
    if test_coverage < 60%:
        needs['testing'].append('increase_coverage')
    
    if has_todo_comments() > 20:
        needs['development'].append('complete_todos')
    
    if cyclomatic_complexity > threshold:
        needs['refactoring'].append('reduce_complexity')
    
    if missing_docs_ratio > 0.3:
        needs['documentation'].append('document_apis')
    
    return prioritize_needs(needs)
```

## **PHASE 2: DYNAMIC AGENT TYPE SELECTION**

**Specialized Agent Types:**

### **1. Development Agents**
- **Feature Agents**: Implement new functionality
- **Bug-Fix Agents**: Resolve specific issues
- **API Agents**: Create/modify endpoints
- **Database Agents**: Schema and query optimization

### **2. Quality Assurance Agents**
- **Test Writers**: Create missing tests
- **Test Updaters**: Maintain existing tests
- **E2E Agents**: Integration testing
- **Fuzzing Agents**: Edge case discovery

### **3. Refactoring Agents**
- **Code Cleaners**: Remove duplication
- **Pattern Agents**: Apply design patterns
- **Modernization Agents**: Update legacy code
- **Performance Agents**: Optimize bottlenecks

### **4. Documentation Agents**
- **API Documenters**: OpenAPI/Swagger specs
- **Code Commenters**: Inline documentation
- **Guide Writers**: User/developer guides
- **Diagram Agents**: Architecture visualization

### **5. Integration Agents**
- **Connector Agents**: Wire up components
- **Migration Agents**: Update dependencies
- **Compatibility Agents**: Cross-platform support
- **DevOps Agents**: CI/CD configuration

### **6. Specialized Agents**
- **Security Auditors**: Vulnerability scanning
- **Accessibility Agents**: WCAG compliance
- **i18n Agents**: Internationalization
- **Analytics Agents**: Instrumentation

**Agent Selection Algorithm:**
```
AGENT_SELECTION:
1. Analyze discovered needs
2. Calculate effort estimates
3. Identify dependencies
4. Optimize agent mix for:
   - Maximum parallel execution
   - Minimal conflicts
   - Balanced workload
   - Priority alignment
5. Dynamically spawn specialized agents
```

## **PHASE 3: ADAPTIVE TASK GENERATION**

**Intelligent Task Creation:**
Instead of requiring a task manifest, the system generates tasks dynamically:

```yaml
auto_generated_tasks:
  - type: testing
    trigger: "Low test coverage in auth module"
    agent_type: test_writer
    files: [auth/*.js]
    priority: high
    
  - type: refactoring  
    trigger: "High complexity in data processor"
    agent_type: pattern_agent
    files: [processors/data.py]
    priority: medium
    
  - type: documentation
    trigger: "Missing API docs for v2 endpoints"
    agent_type: api_documenter
    files: [api/v2/**]
    priority: low
```

**Context-Aware Task Filtering:**
```
IF tests_exist_for(module):
    skip_test_generation_task(module)
    maybe_create_test_update_task(module)
    
IF recent_refactor(component):
    deprioritize_refactoring(component)
    prioritize_testing(component)
    
IF external_api_changed():
    create_migration_agent_task()
    create_compatibility_test_task()
```

## **PHASE 4: SELF-ORGANIZING AGENT DEPLOYMENT**

**Agent Spawning Protocol:**
```
ADAPTIVE_AGENT_SPAWN:

FOR each identified_need:
    1. Determine optimal agent type
    2. Calculate resource requirements
    3. Check for conflicts/dependencies
    4. Spawn specialized agent with:
       - Specific expertise profile
       - Focused objective
       - Resource constraints
       - Collaboration instructions
    
REAL_TIME_ADAPTATION:
    - Monitor agent progress
    - Detect emerging needs
    - Spawn additional agents as needed
    - Reallocate idle agents
    - Merge similar tasks
```

**Specialized Agent Templates:**

### **Test Writer Agent**
```
ROLE: Test Coverage Specialist
EXPERTISE: [chosen_test_framework] testing patterns

OBJECTIVES:
- Analyze untested code paths
- Generate comprehensive test suites
- Ensure edge case coverage
- Maintain test readability

CONSTRAINTS:
- Follow existing test patterns
- Maintain fast test execution
- Avoid test coupling
```

### **Performance Optimization Agent**
```
ROLE: Performance Engineer
EXPERTISE: Profiling, caching, algorithm optimization

OBJECTIVES:
- Identify performance bottlenecks
- Implement optimizations
- Maintain code readability
- Document performance gains

TOOLS:
- Profiling analysis
- Complexity reduction
- Caching strategies
- Query optimization
```

### **Security Audit Agent**
```
ROLE: Security Specialist
EXPERTISE: OWASP, secure coding, vulnerability detection

OBJECTIVES:
- Scan for vulnerabilities
- Implement security fixes
- Add security tests
- Document security measures

FOCUS_AREAS:
- Input validation
- Authentication/authorization
- Data encryption
- SQL injection prevention
```

## **PHASE 5: INTELLIGENT COORDINATION**

**Multi-Agent Communication Protocol:**
```
AGENT_MESH_NETWORK:
├── Discovery Channel
│   ├── "Found missing tests for payment module"
│   ├── "Detected API breaking change"
│   └── "Performance issue in search function"
│
├── Coordination Channel  
│   ├── "Test Agent claiming payment module"
│   ├── "Migration Agent needs API schema"
│   └── "Performance Agent starting profiling"
│
├── Knowledge Channel
│   ├── "Payment uses Stripe SDK v3"
│   ├── "Search built on Elasticsearch"
│   └── "Tests use Jest with React Testing Library"
│
└── Conflict Resolution
    ├── "Two agents targeting same file"
    ├── "Dependency chain detected"
    └── "Resource limit approaching"
```

**Dynamic Work Allocation:**
```python
class AdaptiveOrchestrator:
    def allocate_work(self):
        while work_remains():
            # Assess current state
            available_agents = get_idle_agents()
            pending_tasks = analyze_remaining_work()
            emerging_needs = detect_new_requirements()
            
            # Intelligent allocation
            for agent in available_agents:
                if agent.type == 'test_writer' and tests_needed():
                    assign_test_task(agent)
                elif agent.type == 'refactorer' and complexity_high():
                    assign_refactor_task(agent)
                else:
                    # Retrain agent for different role
                    new_role = determine_critical_need()
                    retrain_agent(agent, new_role)
            
            # Spawn new specialists as needed
            if critical_security_issue():
                spawn_security_specialist()
            
            if performance_degradation():
                spawn_performance_expert()
```

## **PHASE 6: CONTINUOUS LEARNING & ADAPTATION**

**Project Learning System:**
```
PATTERN_RECOGNITION:
- Learn coding conventions from existing code
- Identify team preferences
- Understand architectural decisions
- Recognize testing patterns

ADAPTIVE_BEHAVIOR:
- Adjust agent behavior based on discoveries
- Update task priorities based on findings
- Modify agent count based on complexity
- Switch strategies based on progress

FEEDBACK_LOOP:
- Track successful patterns
- Identify bottlenecks
- Learn from conflicts
- Optimize future runs
```

## **PHASE 7: INTELLIGENT QUALITY GATES**

**Adaptive Quality Assurance:**
```
QUALITY_DIMENSIONS:
1. Code Quality
   - Style consistency
   - Complexity thresholds
   - Duplication limits
   - Naming conventions

2. Test Quality
   - Coverage targets (adaptive based on criticality)
   - Test execution time
   - Flakiness detection
   - Assertion quality

3. Documentation Quality
   - Completeness checks
   - Example validation
   - Link verification
   - Clarity scoring

4. Integration Quality
   - API contract validation
   - Backwards compatibility
   - Performance regression
   - Security compliance
```

**Smart Gating Logic:**
```
IF module.is_critical():
    require_test_coverage(95%)
    require_security_review()
    require_performance_baseline()
ELSE:
    require_test_coverage(70%)
    suggest_improvements()
```

## **EXECUTION SCENARIOS**

### **Scenario 1: Mature Project with Good Tests**
```
DETECTION: High test coverage, stable codebase
AGENT_MIX:
- 2 Feature Development Agents
- 1 Performance Optimization Agent  
- 1 Documentation Updater
- 1 Security Auditor
```

### **Scenario 2: Legacy Project Modernization**
```
DETECTION: Outdated dependencies, no tests, poor documentation
AGENT_MIX:
- 3 Test Writer Agents
- 2 Refactoring Agents
- 2 Migration Agents
- 1 Documentation Agent
- 2 Integration Agents
```

### **Scenario 3: Rapid Prototype Development**
```
DETECTION: Early stage, changing requirements
AGENT_MIX:
- 5 Feature Development Agents
- 2 API Design Agents
- 1 Basic Test Agent
- 2 Integration Agents
```

### **Scenario 4: Production Optimization**
```
DETECTION: Complete features, performance issues
AGENT_MIX:
- 4 Performance Agents
- 2 Security Agents
- 2 Monitoring Agents
- 2 Documentation Agents
```

## **ADVANCED ORCHESTRATION FEATURES**

**Agent Skill Transfer:**
```
When TestAgent discovers architectural pattern:
    → Share with DevelopmentAgents
When SecurityAgent finds vulnerability pattern:
    → Train all agents to avoid pattern
When PerformanceAgent optimizes algorithm:
    → Update agent knowledge base
```

**Predictive Agent Spawning:**
```
IF rate_of_bug_discovery > threshold:
    preemptively_spawn_debug_agents()
    
IF approaching_deadline:
    spawn_fast_track_agents()
    reduce_quality_thresholds()
    
IF complexity_increasing:
    spawn_architecture_reviewers()
```

**Resource Optimization:**
```
DYNAMIC_SCALING:
- Start with minimal agents
- Scale up based on discoveries
- Scale down as work completes
- Redistribute idle resources
- Merge redundant agents
```

## **MONITORING & INSIGHTS**

**Adaptive Dashboard:**
```
PROJECT HEALTH MATRIX
====================
Code Coverage: 67% → 84% ↗️
Tech Debt: High → Medium ↘️
Performance: 3.2s → 1.8s ↘️
Security: B → A+ ↗️

AGENT WORKFORCE
===============
Active: 8/10 agents
- 3 Test Writers (84% progress)
- 2 Refactorers (cleaning auth module)
- 1 Security Auditor (scanning dependencies)
- 1 Performance Optimizer (profiling API)
- 1 Documentation Writer (updating README)

EMERGING NEEDS
=============
⚠️ Deprecated API usage detected
⚠️ Missing error handling in payment flow
ℹ️ Opportunity for caching in search

ADAPTIVE ACTIONS
===============
✓ Spawning Migration Agent for API update
✓ Reassigning idle Test Agent to error handling
✓ Scheduling Performance Agent for caching
```

## **EXECUTION COMMAND**

Begin with ultra-deep project analysis. Let the codebase tell you what it needs. Spawn specialized agents dynamically based on discovered requirements. Adapt continuously as new needs emerge. Achieve optimal development velocity through intelligent, self-organizing agent coordination.