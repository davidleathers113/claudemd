# Research: Prompt File Capabilities

## Status: Basic Markdown Only

### Research Date: June 11, 2025

## Summary
Claude Code prompt files are **simple markdown files** with no extended syntax beyond `$ARGUMENTS` substitution. There is **no support** for conditional logic, loops, dynamic generation, or any programming constructs within prompt files.

## Research Findings

### What Actually Exists

1. **Markdown Command Files**
   - Location: `.claude/commands/` directory
   - Format: Plain markdown files
   - Naming: `command-name.md`
   - Variable: Only `$ARGUMENTS` supported

2. **Basic Structure**
```markdown
# File: .claude/commands/example.md
Task description: $ARGUMENTS

Follow these steps:
1. Step one
2. Step two
3. Step three
```

3. **No Programming Constructs**
   - No if/else conditions
   - No loops or iterations
   - No dynamic content generation
   - No variable beyond `$ARGUMENTS`
   - No includes or imports
   - No template inheritance

### What Doesn't Exist

The following features from the infinite loop pattern are **not supported**:
- Extended syntax for prompts
- Conditional logic (`if`, `else`)
- Loop constructs (`for`, `while`)
- Dynamic prompt generation
- Multiple variables
- Nested prompt files
- Programmatic prompt building

### Real Usage Patterns

1. **Static Templates**
```markdown
# File: .claude/commands/fix-issue.md
Please analyze and fix the GitHub issue: $ARGUMENTS

Follow these steps:
1. Use `gh issue view` to get the issue details
2. Understand the problem described in the issue
3. Search the codebase for relevant files
4. Implement the necessary changes to fix the issue
5. Write and run tests to verify the fix
6. Ensure code passes linting and type checking
```

2. **Structured Instructions**
```markdown
# File: .claude/commands/refactor.md
Refactor the following code: $ARGUMENTS

Guidelines:
- Improve readability
- Remove duplication
- Add appropriate comments
- Maintain functionality
- Follow project coding standards
```

3. **Checklist Approach**
```markdown
# File: .claude/commands/deploy.md
Deploy to environment: $ARGUMENTS

Pre-deployment checklist:
[ ] Run all tests
[ ] Update version number
[ ] Build production bundle
[ ] Run security scan
[ ] Update changelog

Deployment steps:
1. Create deployment branch
2. Run deployment script
3. Verify deployment
4. Update monitoring
```

### External Dynamic Prompts

To achieve dynamic prompts, use external scripting:

1. **Shell Script Generation**
```bash
#!/bin/bash
# Generate dynamic prompt
if [ "$1" == "production" ]; then
  PROMPT="Deploy to production with extra safety checks"
else
  PROMPT="Deploy to $1 environment"
fi

claude -p "$PROMPT"
```

2. **Python Template Engine**
```python
from jinja2 import Template

template = Template("""
{% if mode == 'debug' %}
Enable debug logging and verbose output.
{% endif %}

Process {{ file_count }} files:
{% for file in files %}
- {{ file }}
{% endfor %}
""")

prompt = template.render(mode='debug', files=['a.py', 'b.py'])
subprocess.run(['claude', '-p', prompt])
```

3. **Node.js Dynamic Prompts**
```javascript
const conditions = {
  hasTests: true,
  needsDocs: false,
  complexity: 'high'
};

let prompt = 'Refactor the code\n\n';

if (conditions.hasTests) {
  prompt += '- Ensure all tests pass\n';
}
if (conditions.needsDocs) {
  prompt += '- Add documentation\n';
}
if (conditions.complexity === 'high') {
  prompt += '- Break into smaller functions\n';
}

execSync(`claude -p "${prompt}"`);
```

### Workarounds for Complex Prompts

1. **Multiple Command Files**
   - Create separate commands for different scenarios
   - Use descriptive names: `deploy-prod.md`, `deploy-staging.md`
   - Let user choose appropriate command

2. **External Prompt Builder**
```bash
# prompt-builder.sh
cat base-prompt.md
if [ -f "context/$1.md" ]; then
  cat "context/$1.md"
fi
echo "Additional instructions: $2"
```

3. **Markdown Includes (Manual)**
```markdown
# Main prompt
Execute the following task: $ARGUMENTS

# Standard instructions (copy-paste from shared file)
[Include content from standards.md manually]

# Task-specific instructions
[Add specific requirements here]
```

### Best Practices

1. **Keep Prompts Simple**
   - Focus on clear instructions
   - Use numbered steps
   - Include examples where helpful

2. **Handle Variability**
```markdown
Process: $ARGUMENTS

If no arguments provided:
- List available options
- Ask for clarification

If arguments provided:
- Parse as: [format description]
- Execute appropriate action
```

3. **Use External Tools**
   - Complex logic in scripts
   - Generate prompts programmatically
   - Pass to Claude via `-p` flag

### Limitations

1. **Static Nature**
   - Cannot adapt based on conditions
   - No runtime logic evaluation
   - Fixed structure only

2. **Single Variable**
   - Only `$ARGUMENTS` available
   - Cannot access environment
   - No computed values

3. **No Composition**
   - Cannot include other files
   - No template inheritance
   - No partial prompts

## Conclusion
Claude Code prompt files are intentionally simple, supporting only basic markdown with `$ARGUMENTS` substitution. The advanced prompt file capabilities described in the infinite loop pattern (conditional logic, loops, dynamic generation) are **purely conceptual** and would require external scripting to implement.

## References
- [Claude Code Best Practices - Custom Commands](https://www.anthropic.com/engineering/claude-code-best-practices)
- [Poking Around Claude Code - Control Logic](https://leehanchung.github.io/blogs/2025/03/07/claude-code/)
- [GitHub Issues - Markdown Generation](https://github.com/anthropics/claude-code/issues/198)
