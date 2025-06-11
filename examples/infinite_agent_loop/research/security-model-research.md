# Research: Security Model - How Claude Code Handles Security in Multi-Agent Contexts

## Summary
Claude Code implements a tiered permission system with container-based isolation options for secure multi-agent operation. While each agent runs independently with its own permissions, advanced security features like Docker sandboxing and git worktree isolation enable safe parallel execution of up to ~10 agents simultaneously.

## Key Findings

### 1. Core Permission System

**Tiered Permission Model**
- Read-only tools: No approval needed
- Bash commands: Project-level approval required
- File modifications: Explicit approval required
- Sensitive operations: Always require confirmation

**Permission Configuration Methods**
- `/allowed-tools` command for session permissions
- `--allowedTools` flag for startup configuration
- `.claude/settings.json` for persistent rules
- `--dangerously-skip-permissions` for automated environments

**Security Safeguards**
- Protection against prompt injection
- Context-aware analysis of requests
- Input sanitization
- Command blocklist (curl, wget, etc.)

### 2. Multi-Agent Isolation

**Git Worktree Isolation**
- Each agent operates in separate directory
- No file system conflicts between agents
- Independent branch states
- Complete working directory separation

**Process Isolation**
- Each Claude instance runs as separate process
- No shared memory between agents
- Independent context windows
- Isolated conversation states

**Resource Isolation**
- Separate API usage per instance
- Independent file system access
- No cross-agent communication by default
- Individual permission states

### 3. Container-Based Security

**Docker Sandbox Options**

1. **claude-code-sandbox**
   - Run Claude Code in isolated Docker containers
   - Safe environment for AI-assisted development
   - Pre-configured security policies
   - Community-maintained solution

2. **claude-sandbox**
   - Docker sandbox for running Claude Code
   - Container runs as root (for file permissions)
   - Mounted volumes for project access
   - Network isolation capabilities

**Development Container Configuration**
- Enhanced security measures
- Isolation from main system
- Firewall rules verification at startup
- Default-deny network policy

**Network Access Control**
- Restricted to whitelisted domains:
  - api.anthropic.com
  - statsig.anthropic.com
  - sentry.io
  - npm registry
  - GitHub
- Blocks all other external access
- Precise access control implementation

### 4. Parallel Agent Security

**Cluster Management**
- Up to ~10 agents manageable simultaneously
- Each agent maintains own security context
- No automatic permission inheritance
- Manual coordination required

**Security Boundaries**
- File system: Git worktrees provide isolation
- Network: Container-level restrictions
- Permissions: Per-instance configuration
- Context: No cross-contamination

**Best Practices for Multi-Agent**
```bash
# Secure multi-agent setup
# 1. Create isolated worktrees
git worktree add ../agent-1 feature-1
git worktree add ../agent-2 feature-2

# 2. Launch with specific permissions
cd ../agent-1 && claude --allowedTools "Edit,Read"
cd ../agent-2 && claude --allowedTools "Read,Grep"

# 3. Use containers for additional isolation
docker run -v $(pwd):/workspace claude-sandbox
```

### 5. Security Considerations

**Attack Surface in Multi-Agent**
- Increased API exposure (multiple instances)
- Potential for confused deputy attacks
- File system race conditions
- Resource exhaustion risks

**Mitigation Strategies**
- Use minimal permissions per agent
- Implement rate limiting externally
- Monitor aggregate resource usage
- Regular security audits

**Container Security**
```dockerfile
# Example secure container setup
FROM claude-code-base
# Default-deny network policy
RUN iptables -P OUTPUT DROP
# Whitelist specific domains
RUN iptables -A OUTPUT -d api.anthropic.com -j ACCEPT
# Verify rules at startup
CMD ["verify-firewall", "&&", "claude"]
```

## Comparison: Single vs Multi-Agent Security

| Aspect | Single Agent | Multi-Agent |
|--------|-------------|-------------|
| Permission Scope | Single context | Per-agent contexts |
| File Isolation | Working directory | Worktrees/containers |
| Network Control | Process-level | Container possible |
| Resource Limits | API quotas | Multiplied by agents |
| Attack Surface | Limited | Expanded |

## Implementation Examples

### Secure Multi-Agent Workflow
```yaml
# GitHub Actions with security isolation
jobs:
  agent-1:
    runs-on: ubuntu-latest
    container: claude-sandbox
    permissions:
      contents: read
    steps:
      - uses: actions/checkout@v3
      - run: claude -p "Implement feature A" --allowedTools "Read,Edit"
  
  agent-2:
    runs-on: ubuntu-latest
    container: claude-sandbox
    permissions:
      contents: read
    steps:
      - uses: actions/checkout@v3
      - run: claude -p "Write tests for feature A" --allowedTools "Read,Write"
```

### Permission Configuration
```json
// .claude/settings.json for multi-agent project
{
  "agents": {
    "developer": {
      "allowedTools": ["Edit", "Write", "Bash(npm*)"],
      "deniedTools": ["Bash(rm*)", "Bash(sudo*)"]
    },
    "reviewer": {
      "allowedTools": ["Read", "Grep", "LS"],
      "deniedTools": ["Edit", "Write"]
    },
    "tester": {
      "allowedTools": ["Read", "Bash(npm test)"],
      "deniedTools": ["Edit", "Write"]
    }
  }
}
```

## Security Best Practices

### For Parallel Execution
1. **Principle of Least Privilege**
   - Grant minimal permissions per agent
   - Different roles get different permissions
   - Review and audit regularly

2. **Isolation Strategies**
   - Always use git worktrees
   - Consider Docker for sensitive work
   - Implement network restrictions

3. **Monitoring and Auditing**
   - Log all agent activities
   - Monitor resource consumption
   - Track permission usage
   - Regular security reviews

### For Teams
1. **Standardized Configurations**
   - Team-wide security policies
   - Approved tool lists
   - Container templates
   - Permission presets

2. **Automated Security**
   - CI/CD integration with containers
   - Automated permission validation
   - Security scanning of outputs
   - Compliance checking

## Limitations and Risks

### Current Limitations
- No native agent-to-agent security
- Manual permission management
- Limited visibility across agents
- No centralized security control

### Security Risks
- Aggregate resource consumption
- Potential for permission creep
- Coordination vulnerabilities
- Shared file system risks

### Mitigation Recommendations
1. Use container isolation for production
2. Implement external monitoring
3. Regular permission audits
4. Automated security testing

## Future Considerations

### Potential Improvements
- Centralized permission management
- Agent communication protocols
- Enhanced isolation mechanisms
- Security policy templates

### Community Solutions
- Docker sandbox implementations
- Permission management tools
- Security monitoring dashboards
- Multi-agent orchestrators

## Conclusion

Claude Code's security model for multi-agent contexts relies on a combination of its tiered permission system, process isolation, and external tools like Docker containers and git worktrees. While the core security features are robust, multi-agent deployments require careful planning and additional security layers. The ability to run up to ~10 parallel agents is achievable with proper isolation strategies, but teams must implement comprehensive security practices beyond Claude Code's built-in features. Container-based isolation and git worktree separation provide the strongest security boundaries for parallel agent execution.