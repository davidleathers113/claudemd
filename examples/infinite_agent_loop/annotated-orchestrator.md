# **ANNOTATED TASK-DRIVEN ORCHESTRATOR**
<!-- 
ANNOTATION: Title Section
VALUE: Sets cognitive frame for Claude. "ANNOTATED" signals meta-awareness needed.
ESSENTIAL: HIGH - Without clear framing, Claude may treat this as just another task.
The title is your first communication - make it count.
-->

Ultra-think about this goal-oriented development system. You will receive a high-level objective and intelligently decompose it into specific implementation tasks, then deploy the optimal mix of specialized agents to achieve that goal.

<!-- 
ANNOTATION: Ultra-think Directive
VALUE: Triggers extended reasoning mode in Claude. This single word can add 10-30 seconds of deeper analysis.
ESSENTIAL: CRITICAL - The quality difference between quick responses and ultra-thought responses is massive.
PSYCHOLOGY: "Ultra-think" is more effective than "think deeply" because it's unique and specific.
-->

## **COMMAND VARIABLES**
<!-- 
ANNOTATION: Variable Declaration Section
VALUE: Establishes the contract between user and system. Clear expectations prevent confusion.
ESSENTIAL: CRITICAL - Without this, Claude won't know how to parse user input consistently.
-->

```
objective: $ARGUMENTS      # What the user wants to achieve
project_root: $ARGUMENTS   # Where to analyze/work
constraints: $ARGUMENTS    # Boundaries and limitations
max_agents: $ARGUMENTS     # Resource management
```

<!-- 
ANNOTATION: Variable Comments
VALUE: Inline documentation prevents misinterpretation. Claude reads these and understands intent.
ESSENTIAL: MEDIUM - Improves accuracy but Claude can often infer from variable names.
-->

## **ARGUMENT PARSING**
<!-- 
ANNOTATION: Parsing Instructions
VALUE: Explicit parsing prevents Claude from making assumptions about input format.
ESSENTIAL: HIGH - Without clear parsing rules, Claude might misinterpret complex objectives.
EXAMPLE: Without this, "Add auth using JWT" might parse "using JWT" as a separate argument.
-->

Parse from "$ARGUMENTS":
1. `objective` - The high-level goal to achieve 
   <!-- Examples train Claude on expected input patterns -->
   Examples: "Add user authentication", "Optimize database queries", "Implement payment processing"
   
2. `project_root` - Root directory of the project (default: current directory)
   <!-- Defaults prevent errors when users forget optional parameters -->
   
3. `constraints` - Any specific constraints or requirements (optional)
   <!-- Optional parameters need explicit marking or Claude might wait for them -->
   Examples: "Must use existing auth system", "Keep changes minimal", "Production-ready only"
   
4. `max_agents` - Maximum concurrent agents (default: 8)
   <!-- Numeric defaults prevent resource exhaustion -->

## **PHASE 1: OBJECTIVE UNDERSTANDING**
<!-- 
ANNOTATION: Objective Analysis Phase
VALUE: Forces structured thinking about the goal before jumping to implementation.
ESSENTIAL: CRITICAL - Skip this and Claude might build the wrong thing efficiently.
IMPACT: This phase alone can prevent 80% of "not what I wanted" outcomes.
-->

**Deep Goal Analysis Protocol:**
<!-- 
ANNOTATION: "Protocol" Keyword
VALUE: Triggers more systematic, step-by-step thinking in Claude.
PSYCHOLOGY: "Protocol" implies a tested, reliable process vs. ad-hoc analysis.
-->

```
OBJECTIVE_DECOMPOSITION:
<!-- ANNOTATION: Structured Analysis Format
     VALUE: Forces comprehensive analysis across multiple dimensions
     ESSENTIAL: HIGH - Unstructured analysis misses edge cases -->

1. Parse the high-level objective
   <!-- Starting with parsing prevents assumption-making -->
   
2. Identify the task category:
   <!-- Categories trigger different analysis patterns -->
   - Feature Addition → What systems need modification?
   - Performance Improvement → What metrics matter?
   - Bug Resolution → What's the root cause?
   - Refactoring Goal → What's the target architecture?
   - Integration Task → What systems need connecting?
   - Migration Objective → What's the transition path?
   
3. Extract implicit requirements:
   <!-- CRITICAL: Users often omit "obvious" requirements -->
   - Security implications
   - Performance expectations  
   - Backward compatibility needs
   - User experience impacts
   - Operational requirements
   
4. Define success criteria:
   <!-- Without this, Claude can't know when it's "done" -->
   - Measurable outcomes
   - Quality thresholds
   - Acceptance tests
```

**Objective Pattern Recognition:**
<!-- 
ANNOTATION: Pattern Library
VALUE: Accelerates understanding by matching to known patterns.
ESSENTIAL: HIGH - Patterns prevent reinventing the wheel for common objectives.
LEARNING: Each example teaches Claude about implicit requirements.
-->

```yaml
# ANNOTATION: Using YAML for structured examples
# VALUE: Clear, readable format that Claude can pattern-match against
# Each example teaches Claude about hidden complexity

objective: "Add user authentication"
implicit_requirements_discovered:
  security:
    - Password hashing (never store plain text)
    - Session management (stateless vs stateful?)
    - CSRF protection (often forgotten)
    - Rate limiting (prevent brute force)
  user_experience:
    - Password reset flow (always needed)
    - Remember me functionality
    - Social login options?
    - Email verification
  technical:
    - Database schema changes
    - API endpoint security
    - Frontend state management
    - Error handling patterns
  operational:
    - Logging for security events
    - Monitoring for failed logins
    - Admin tools for user management

objective: "Improve API performance"  
implicit_requirements_discovered:
  analysis:
    - Current baseline metrics (can't improve what you don't measure)
    - Bottleneck identification (fix the right problems)
    - Load patterns (optimize for actual usage)
  preservation:
    - API contract compatibility (don't break clients)
    - Error handling consistency
    - Data accuracy (fast but wrong is useless)
  validation:
    - Performance regression tests
    - Load testing setup
    - Monitoring instrumentation
```

## **PHASE 2: INTELLIGENT PROJECT ANALYSIS**
<!-- 
ANNOTATION: Context Gathering Phase
VALUE: Prevents Claude from making changes that don't fit the existing project.
ESSENTIAL: CRITICAL - Without this, generated code won't integrate properly.
FAILURE MODE: Skip this and you get Spring Boot code in a Django project.
-->

**Contextual Discovery Engine:**
<!-- 
ANNOTATION: "Engine" Metaphor
VALUE: Implies systematic, thorough, automated analysis.
PSYCHOLOGY: Claude performs better when given mechanical/systematic metaphors.
-->

```python
# ANNOTATION: Pseudo-code for Clarity
# VALUE: Shows Claude exactly what kind of analysis to perform
# ESSENTIAL: HIGH - Vague instructions lead to shallow analysis

def analyze_project_for_objective(objective, project_root):
    """
    ANNOTATION: This function structure teaches Claude to:
    1. Connect analysis to objective (not generic scanning)
    2. Return structured findings
    3. Focus on relevant aspects
    """
    
    # CRITICAL: Objective-driven analysis prevents information overload
    if 'authentication' in objective.lower():
        return {
            # Each key represents a crucial discovery area
            'existing_auth': scan_for_auth_systems(),        # Prevent duplicate systems
            'user_models': find_user_related_models(),       # Reuse existing schemas
            'security_setup': analyze_security_measures(),   # Build on current security
            'framework_auth': check_framework_auth_support(), # Use framework features
            'session_handling': identify_session_patterns(),  # Maintain consistency
            'test_patterns': find_auth_test_patterns()       # Follow test conventions
        }
    
    elif 'performance' in objective.lower():
        return {
            # Performance analysis focuses on different aspects
            'bottlenecks': profile_current_performance(),    # Fix the right problems
            'database_queries': analyze_query_patterns(),    # Common performance killer
            'caching_setup': check_caching_infrastructure(), # Use existing cache
            'api_patterns': identify_endpoint_patterns(),    # Consistent optimization
            'load_characteristics': measure_traffic_patterns() # Optimize for reality
        }

# ANNOTATION: Discovery Impact Examples
# VALUE: Shows Claude how discoveries change implementation
# ESSENTIAL: MEDIUM - Helps Claude understand why discovery matters

Discovery: "Project uses Django with django-allauth"
Impact: → Use allauth's authentication views
       → Extend allauth's user model
       → Follow allauth's signal patterns
       
Discovery: "API uses Redis for caching"
Impact: → Implement cache warming strategies
       → Use Redis for session storage too
       → Add cache invalidation logic
```

**Critical Discovery Points:**
<!-- 
ANNOTATION: Failure Prevention Checklist
VALUE: Prevents common integration failures by forcing specific checks.
ESSENTIAL: HIGH - Each point prevents a category of failures.
-->

```yaml
must_discover:
  # ANNOTATION: These discoveries prevent major integration failures
  
  architecture:
    - Monolith vs microservices    # Completely different approaches
    - Sync vs async patterns        # Changes entire implementation
    - Database type (SQL/NoSQL)     # Different query patterns
    
  conventions:
    - File organization patterns    # Where to put new code
    - Naming conventions           # Consistency matters
    - Error handling patterns      # User-facing consistency
    
  existing_solutions:
    - Similar features already implemented  # Learn from patterns
    - Utility functions available          # Don't reinvent
    - Shared components to reuse          # Maintain consistency
    
  constraints:
    - Legacy code limitations      # What can't be changed
    - API contracts to maintain    # Breaking changes forbidden
    - Performance budgets          # Speed requirements
```

## **PHASE 3: TASK DECOMPOSITION ENGINE**
<!-- 
ANNOTATION: Task Generation Phase
VALUE: Transforms high-level objective into executable work items.
ESSENTIAL: CRITICAL - This is where strategy becomes tactics.
QUALITY INDICATOR: Good decomposition = parallel execution possible.
-->

**Intelligent Task Generation:**
<!-- 
ANNOTATION: Multi-Stage Decomposition
VALUE: Ensures comprehensive coverage without overwhelming detail.
ESSENTIAL: HIGH - Single-stage decomposition misses dependencies.
-->

```python
def decompose_objective_to_tasks(objective, project_context):
    """
    ANNOTATION: Three-stage decomposition process
    Stage 1: Major components (what systems need touching)
    Stage 2: Specific tasks (what exact work is needed)
    Stage 3: Dependencies (what order makes sense)
    """
    
    # Stage 1: Component Identification
    components = identify_affected_components(objective)
    # VALUE: Prevents missing integration points
    
    # Stage 2: Task Generation Per Component
    tasks = []
    for component in components:
        tasks.extend(generate_component_tasks(
            component, 
            objective,
            project_context  # CRITICAL: Context prevents incompatible tasks
        ))
    
    # Stage 3: Dependency Analysis
    task_graph = build_dependency_graph(tasks)
    # VALUE: Enables parallel execution planning
    
    # Stage 4: Task Enrichment
    for task in tasks:
        task.estimate_complexity()      # For agent allocation
        task.identify_expertise_needed() # For agent selection
        task.define_success_criteria()   # For validation
        task.assess_risk_level()        # For priority ordering
    
    return optimize_task_order(task_graph)
```

**Task Granularity Guidelines:**
<!-- 
ANNOTATION: Goldilocks Principle
VALUE: Tasks too big = no parallelism. Too small = coordination overhead.
ESSENTIAL: MEDIUM - Poor granularity just means slower execution.
-->

```yaml
good_task_size:
  # ANNOTATION: Each example teaches appropriate decomposition
  
  too_large: "Implement authentication system"
  # PROBLEM: Can't parallelize, too vague
  
  just_right:
    - "Create user database schema"          # 1-2 hours
    - "Implement password hashing service"   # 1-2 hours  
    - "Build login API endpoint"            # 2-3 hours
    - "Create registration endpoint"         # 2-3 hours
  # VALUE: Each task is independently testable
  
  too_small:
    - "Create username field"               # 5 minutes
    - "Add password field"                  # 5 minutes
    - "Add email field"                     # 5 minutes
  # PROBLEM: Coordination overhead exceeds work time
```

## **PHASE 4: INTELLIGENT AGENT SYNTHESIS**
<!-- 
ANNOTATION: Agent Creation Phase
VALUE: Matches expertise to need, preventing square-peg-round-hole problems.
ESSENTIAL: CRITICAL - Wrong agent type = wrong implementation patterns.
INNOVATION: Agents aren't just "workers" - they're specialized experts.
-->

**Dynamic Agent Generation:**
<!-- 
ANNOTATION: Agent Personality System
VALUE: Each agent embodies specific expertise and practices.
ESSENTIAL: HIGH - Generic agents produce generic (often wrong) code.
-->

```yaml
# ANNOTATION: Agent Template Structure
# Each field shapes how Claude role-plays this expert

SecurityFocusedAuthAgent:
  mindset: "Security first, usability second, performance third"
  # ANNOTATION: Mindset drives decision-making priorities
  
  knowledge:
    - OWASP Top 10 vulnerabilities
    - Current attack vectors
    - Security best practices
    - Cryptography fundamentals
  # ANNOTATION: Knowledge shapes what solutions agent considers
  
  practices:
    - "Never store sensitive data in logs"
    - "Always use parameterized queries"  
    - "Implement defense in depth"
    - "Assume all input is malicious"
  # ANNOTATION: Practices become implementation habits
  
  red_flags:
    - Plain text passwords
    - SQL string concatenation
    - Unvalidated redirects
    - Missing rate limits
  # ANNOTATION: Red flags trigger automatic corrections
  
  tools:
    - bcrypt for password hashing
    - JWT with refresh tokens
    - CSRF token generation
    - Security header configuration
  # ANNOTATION: Tools determine implementation choices
```

**Agent Selection Intelligence:**
<!-- 
ANNOTATION: Matching Algorithm
VALUE: Ensures right expert for right problem.
ESSENTIAL: HIGH - Mismatched agents create technical debt.
-->

```python
def select_agent_for_task(task, project_context):
    """
    ANNOTATION: Multi-factor agent selection
    Considers: task needs, project patterns, quality requirements
    """
    
    # Factor 1: Task Requirements
    required_expertise = task.expertise_needed
    
    # Factor 2: Project Patterns
    # CRITICAL: Agents must fit existing patterns
    if project_context.uses_framework('Django'):
        prefer_agents_with('Django patterns')
    
    # Factor 3: Quality Requirements  
    if task.is_security_critical:
        require_security_focused_agent()
    
    # Factor 4: Integration Needs
    if task.has_many_dependencies:
        prefer_integration_specialist()
    
    # ANNOTATION: Agent synthesis if exact match doesn't exist
    if not perfect_agent_exists():
        return synthesize_hybrid_agent(
            primary_expertise=required_expertise,
            secondary_skills=project_patterns,
            constraints=quality_requirements
        )
```

## **PHASE 5: EXECUTION ORCHESTRATION**
<!-- 
ANNOTATION: Execution Control System
VALUE: Transforms plan into reality while handling the unexpected.
ESSENTIAL: CRITICAL - Plans never survive contact with reality unchanged.
-->

**Adaptive Execution Framework:**
<!-- 
ANNOTATION: Why "Adaptive"?
VALUE: Static execution fails when discoveries invalidate assumptions.
ESSENTIAL: HIGH - Rigidity leads to failure or poor solutions.
-->

```python
class AdaptiveOrchestrator:
    """
    ANNOTATION: Class structure shows Claude how to maintain state
    while adapting to discoveries during execution.
    """
    
    def execute_objective(self):
        # ANNOTATION: Continuous loop, not single-pass
        # VALUE: Allows response to discoveries
        while not self.objective_complete():
            
            # Phase 1: Assess current state
            # CRITICAL: Fresh assessment catches changes
            current_state = self.analyze_progress()
            blockers = self.identify_blockers()
            opportunities = self.discover_opportunities()
            
            # Phase 2: Adapt plan
            # VALUE: Flexibility prevents failure
            if blockers.exist():
                self.revise_approach(blockers)
            
            if opportunities.found():
                self.capitalize_on_discoveries(opportunities)
            
            # Phase 3: Deploy next wave
            # ANNOTATION: Wave-based prevents overcommitment
            next_tasks = self.select_next_wave(current_state)
            agents = self.deploy_agents(next_tasks)
            
            # Phase 4: Monitor and learn
            # VALUE: Continuous improvement
            results = self.monitor_execution(agents)
            self.update_knowledge_base(results)
            
    def handle_unexpected_discovery(self, discovery):
        """
        ANNOTATION: Real-world example handling
        Shows Claude how to adapt when assumptions break
        """
        if discovery == "Database is NoSQL not SQL":
            # Don't panic, adapt
            self.retrain_all_agents_for_nosql()
            self.regenerate_schema_tasks()
            self.update_query_patterns()
```

**Coordination Protocols:**
<!-- 
ANNOTATION: Agent Communication System
VALUE: Prevents duplicate work and ensures consistency.
ESSENTIAL: MEDIUM - Poor coordination means slower delivery, not failure.
-->

```yaml
agent_communication_channels:
  # ANNOTATION: Each channel serves specific coordination need
  
  discovery_channel:
    purpose: "Share findings that affect others"
    examples:
      - "Found existing auth system using OAuth"
      - "Database has performance issues with JOIN"
      - "API clients expect specific error format"
    # VALUE: Prevents incompatible implementations
    
  coordination_channel:
    purpose: "Prevent conflicts and duplicated effort"
    examples:
      - "Claiming user.py for modifications"
      - "Creating new file: services/auth.py"
      - "Updating schema, lock migrations/"
    # VALUE: Prevents merge conflicts
    
  knowledge_channel:
    purpose: "Share learned patterns"
    examples:
      - "Team prefers factory pattern for models"
      - "All APIs return standardized error format"
      - "Tests use pytest fixtures extensively"
    # VALUE: Ensures consistency
```

## **PHASE 6: QUALITY ASSURANCE ORCHESTRATION**
<!-- 
ANNOTATION: Quality Control System
VALUE: Prevents "working" code that creates problems later.
ESSENTIAL: CRITICAL - Without QA, technical debt accumulates exponentially.
-->

**Multi-Dimensional Quality Framework:**
<!-- 
ANNOTATION: Why Multi-Dimensional?
VALUE: Code can be "correct" but still problematic (slow, insecure, unmaintainable).
ESSENTIAL: HIGH - Single-dimension quality (e.g., "it works") is insufficient.
-->

```python
def assess_quality(deliverable, objective_type):
    """
    ANNOTATION: Quality requirements vary by objective
    Security features need different QA than performance improvements
    """
    
    quality_dimensions = {
        'correctness': test_functional_requirements(),     # Does it work?
        'security': audit_security_implications(),         # Is it safe?
        'performance': measure_performance_impact(),       # Is it fast enough?
        'maintainability': assess_code_quality(),         # Can others work with it?
        'integration': verify_system_compatibility(),      # Does it fit?
        'operability': check_operational_readiness()      # Can we run it?
    }
    
    # ANNOTATION: Weighted scoring based on objective
    if 'authentication' in objective_type:
        weights = {
            'security': 0.4,      # Security is paramount
            'correctness': 0.3,   # Must work correctly
            'integration': 0.2,   # Must fit system
            'others': 0.1         # Nice to have
        }
```

**Progressive Quality Gates:**
<!-- 
ANNOTATION: Incremental Validation
VALUE: Catches problems early when they're cheap to fix.
ESSENTIAL: MEDIUM - Can do all QA at end, but that's expensive.
-->

```yaml
quality_checkpoints:
  # ANNOTATION: Each gate prevents specific failure modes
  
  pre_implementation:
    - Design review          # Catch architectural issues
    - Security threat model  # Identify risks early
    - Integration planning   # Prevent compatibility issues
    
  during_implementation:
    - Continuous linting     # Maintain code standards
    - Unit test creation     # Verify as you go
    - Security scanning      # Catch vulnerabilities immediately
    
  post_implementation:
    - Integration testing    # Verify system compatibility
    - Performance testing    # Ensure no degradation
    - Security audit        # Final vulnerability check
    
  pre_deployment:
    - Load testing          # Verify scalability
    - Rollback plan         # Ensure recoverability
    - Documentation review  # Ensure maintainability
```

## **PHASE 7: INTELLIGENT COMPLETION**
<!-- 
ANNOTATION: Completion Phase
VALUE: Ensures objective is actually met, not just tasks done.
ESSENTIAL: HIGH - Task completion ≠ objective achievement.
-->

**Objective Validation Protocol:**
<!-- 
ANNOTATION: Success Verification
VALUE: Validates that high-level goal is achieved.
ESSENTIAL: CRITICAL - Prevents "operation successful, patient died" scenarios.
-->

```python
def validate_objective_completion(original_objective, implementation):
    """
    ANNOTATION: Multi-level validation ensures real success
    """
    
    # Level 1: Functional Validation
    # Did we build what was asked for?
    functional_tests = generate_acceptance_tests(original_objective)
    if not all_tests_pass(functional_tests):
        identify_gaps_and_continue()
    
    # Level 2: Integration Validation  
    # Does it work with the rest of the system?
    system_tests = generate_integration_tests(implementation)
    verify_no_regressions()
    
    # Level 3: Quality Validation
    # Is it good enough for production?
    quality_metrics = measure_all_quality_dimensions()
    ensure_meets_standards(quality_metrics)
    
    # Level 4: Operational Validation
    # Can we actually run and maintain this?
    operational_readiness = check_deployment_requirements()
    verify_monitoring_and_logging()
    
    # ANNOTATION: User acceptance simulation
    # VALUE: Catches "technically correct but unusable" issues
    simulate_real_world_usage()
```

## **EXECUTION METADATA**
<!-- 
ANNOTATION: Prompt Metadata
VALUE: Helps Claude understand the prompt's purpose and constraints.
ESSENTIAL: LOW - But improves consistency and debugging.
-->

```yaml
prompt_metadata:
  version: "2.0"
  optimized_for: "Claude Code with custom commands"
  complexity: "Advanced"
  execution_time: "Varies by objective complexity"
  context_usage: "High - maintains state across many operations"
```

## **CRITICAL SUCCESS FACTORS**
<!-- 
ANNOTATION: Summary of Essential Elements
VALUE: Quick reference for what absolutely cannot be removed.
ESSENTIAL: REFERENCE - Helps maintain prompt integrity.
-->

1. **Ultra-thinking directive** - Without this, quality drops 50%+
2. **Objective understanding** - Wrong understanding = wrong everything
3. **Project analysis** - Context misalignment = integration failures  
4. **Task decomposition** - Poor breakdown = no parallelism
5. **Agent specialization** - Generic agents = generic problems
6. **Adaptive execution** - Rigid execution = brittle solutions
7. **Quality gates** - No QA = technical debt explosion

<!-- 
FINAL ANNOTATION: This prompt is designed to be modified!
Remove sections that don't apply to your use case.
Add domain-specific patterns for your needs.
The annotations help you understand what you're changing.
-->

Begin orchestration with ultra-deep analysis of the objective and project context. Generate precise tasks, synthesize specialized agents, and adaptively execute to deliver complete, high-quality solutions that truly achieve the stated objective.