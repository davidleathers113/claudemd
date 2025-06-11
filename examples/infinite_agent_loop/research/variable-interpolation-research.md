# Research: Advanced Variable Interpolation

## Status: Limited to $ARGUMENTS Only

### Research Date: June 11, 2025

## Summary
Claude Code officially supports **only `$ARGUMENTS`** for variable interpolation in custom slash commands. The advanced variables mentioned (`{spec_file}`, `{output_dir}`, `{iteration_number}`, etc.) are **not supported** and appear to be conceptual extensions.

## Research Findings

### Official Variable Support
According to Anthropic's official documentation:
- **Only `$ARGUMENTS` is supported** in custom slash commands
- This placeholder is replaced with everything typed after the command name
- Located in `.claude/commands/` directory files

### Example Usage
```markdown
# File: .claude/commands/fix-issue.md
Please analyze and fix the GitHub issue: $ARGUMENTS

Follow these steps:
1. Use `gh issue view` to get the issue details
2. Search the codebase for relevant files
3. Implement the necessary changes
```

Usage: `/project:fix-issue 1234` → `$ARGUMENTS` becomes "1234"

### What Does NOT Exist
The following variable patterns are **not supported** in Claude Code:
- `{spec_file}`
- `{output_dir}`
- `{count}`
- `{iteration_number}`
- `{master_plan}`
- `{previous_iteration_summary}`
- Any other curly-brace variable syntax

### Related Variable Systems (Not in Claude Code)
1. **Anthropic Console**: Uses `{{double brackets}}` for variables
2. **Template literals**: Programming languages use various interpolation syntaxes
3. **External scripts**: Could implement custom variable systems

### Implementation Reality
To achieve advanced variable interpolation:
1. **External Orchestration Required**: Build a wrapper script that:
   - Parses templates with custom variables
   - Performs string replacement
   - Generates final prompts
   - Passes them to Claude Code via headless mode

2. **Example Implementation**:
```bash
# External script handling variables
SPEC_FILE="spec.md"
OUTPUT_DIR="output"
ITERATION=1

# Replace variables manually
PROMPT="Generate iteration $ITERATION based on $SPEC_FILE"
claude -p "$PROMPT"
```

3. **Template Processing**:
```python
# Python example for variable interpolation
template = "Process {spec_file} and save to {output_dir}/gen_{iteration}"
variables = {"spec_file": "spec.md", "output_dir": "output", "iteration": 1}
prompt = template.format(**variables)
subprocess.run(["claude", "-p", prompt])
```

### Community Practices
From research, developers handle complex variables by:
1. Including all context directly in `$ARGUMENTS`
2. Using external scripts for preprocessing
3. Creating multiple specialized commands instead of one parameterized command
4. Structuring prompts to work with or without arguments

### Best Practices with $ARGUMENTS
1. **Single Parameter**: `/project:analyze file.py`
2. **Multiple Values**: Parse within the prompt
3. **Default Behavior**: Design prompts to work if `$ARGUMENTS` is empty
4. **Clear Instructions**: Document expected argument format

## Conclusion
Advanced variable interpolation beyond `$ARGUMENTS` is a **conceptual feature** not implemented in Claude Code. The infinite loop pattern would require external scripting to handle the complex variable substitution described in the documentation.

## References
- [Claude Code Best Practices - Custom Commands](https://www.anthropic.com/engineering/claude-code-best-practices)
- [Claude Code Tips & Tricks: Custom Slash Commands](https://cloudartisan.com/posts/2025-04-14-claude-code-tips-slash-commands/)
- [Anthropic Documentation - Prompt Templates](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/prompt-templates-and-variables)
