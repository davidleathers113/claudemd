# Research: Variable System

## Status: Extremely Limited

### Research Date: June 11, 2025

## Summary
Claude Code's variable system is **limited to `$ARGUMENTS` only** for custom slash commands. There is no support for complex variables, dynamic content injection, nested variables, or context-aware substitution as described in the infinite loop pattern.

## Research Findings

### What Actually Exists

1. **`$ARGUMENTS` in Slash Commands**
   - Only variable placeholder in Claude Code
   - Simple string replacement
   - Everything after command name becomes the value
   - Located in `.claude/commands/` files

Example:
```markdown
# File: .claude/commands/analyze.md
Analyze the following code: $ARGUMENTS

Please provide:
1. Code quality assessment
2. Potential improvements
3. Security considerations
```

Usage: `/project:analyze auth.js` → `$ARGUMENTS` becomes "auth.js"

2. **No Other Variables**
   - No `{variable}` syntax
   - No environment variable interpolation
   - No nested variables
   - No dynamic content injection

### Related But Separate Systems

1. **Anthropic Console Variables**
   - Uses `{{double brackets}}` syntax
   - For API-level prompt templates
   - NOT available in Claude Code CLI

2. **Environment Variables**
   - Claude Code reads system environment
   - Security concern: May read local `.env` files
   - Not for prompt interpolation

3. **MCP Server Variables**
   - External tools may implement variables
   - Not native to Claude Code

### What Doesn't Exist

The following variable features from the infinite loop pattern are **not supported**:
- `{spec_file}` - File path variables
- `{output_dir}` - Directory variables
- `{count}` - Numeric variables
- `{iteration_number}` - Dynamic counters
- `{master_plan}` - Content interpolation
- `{previous_iteration_summary}` - Context variables
- Any form of variable nesting or composition

### Implementation Reality

To achieve complex variable interpolation:

1. **External Preprocessing**
```bash
#!/bin/bash
# Manual variable replacement
SPEC_FILE="spec.md"
OUTPUT_DIR="output"
PROMPT="Process file $SPEC_FILE and save to $OUTPUT_DIR"
claude -p "$PROMPT"
```

2. **Template Engine**
```python
# Using Python for complex templates
import subprocess
from string import Template

template = Template("Generate $type variation $num from $spec")
vars = {"type": "UI", "num": 1, "spec": "spec.md"}
prompt = template.substitute(vars)
subprocess.run(["claude", "-p", prompt])
```

3. **Custom Command Wrapper**
```javascript
// Node.js wrapper for variable interpolation
const variables = {
  spec_file: 'spec.md',
  output_dir: 'output',
  iteration: 1
};

let prompt = fs.readFileSync('template.md', 'utf8');
for (const [key, value] of Object.entries(variables)) {
  prompt = prompt.replace(new RegExp(`{${key}}`, 'g'), value);
}

exec(`claude -p "${prompt}"`);
```

### Variable Interpolation Patterns

**Pattern 1: Single Parameter**
```markdown
# Simple command with one variable
Fix the bug in: $ARGUMENTS
```

**Pattern 2: Parse Multiple Values**
```markdown
# Command expects: /project:deploy staging v1.2.3
Deploy to environment: $ARGUMENTS

Parse the arguments to extract:
- Environment (first word)
- Version (second word)
```

**Pattern 3: JSON Arguments**
```markdown
# Command expects: /project:config {"env":"prod","debug":true}
Configure with settings: $ARGUMENTS

Parse as JSON and apply configuration.
```

### Limitations

1. **No Variable Escaping**
   - Cannot escape `$ARGUMENTS`
   - No way to include literal "$ARGUMENTS" in output

2. **No Default Values**
   - If no arguments provided, `$ARGUMENTS` is empty
   - Must design prompts to handle missing arguments

3. **No Variable Validation**
   - No type checking
   - No format validation
   - All validation must be in prompt logic

4. **Single Variable Only**
   - Cannot have multiple variables
   - Cannot reference other files or context

### Best Practices

1. **Design for Single Variable**
   ```markdown
   Process the following: $ARGUMENTS
   
   If no argument provided, list available options.
   If argument provided, proceed with processing.
   ```

2. **Structured Arguments**
   ```markdown
   # Expect format: "filename|operation|options"
   Parse input: $ARGUMENTS
   
   Split by | to get:
   - Filename
   - Operation
   - Options
   ```

3. **External Variable Management**
   - Use shell scripts for complex variables
   - Preprocess templates before passing to Claude
   - Build wrapper tools for advanced needs

## Conclusion
Claude Code's variable system is intentionally minimal, supporting only `$ARGUMENTS` for basic parameter passing. The complex variable interpolation described in the infinite loop pattern (`{spec_file}`, `{output_dir}`, etc.) is purely conceptual and would require extensive external tooling to implement.

## References
- [Claude Code Best Practices - Custom Commands](https://www.anthropic.com/engineering/claude-code-best-practices)
- [Anthropic Console - Prompt Templates](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/prompt-templates-and-variables)
- [GitHub Issue #112 - Environment Variable Concerns](https://github.com/anthropics/claude-code/issues/112)
