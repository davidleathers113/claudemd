# Research: Discovered Patterns (Command Syntax)

## Status: Fictional Syntax

### Research Date: June 11, 2025

## Summary
The command syntax pattern `/agent --prompt-file infinite.md --spec_file spec.md --output_dir output --count 50` is **completely fictional**. Claude Code uses standard CLI flags and does not support the complex command structure described in the infinite loop documentation.

## Research Findings

### Actual Claude Code Command Syntax

1. **Basic Usage**
```bash
# Interactive mode
claude

# Single prompt mode
claude -p "Your prompt here"

# Piped input
cat file.txt | claude
```

2. **Real Flags (Documented)**
- `-p, --print`: Non-interactive mode with prompt
- `--output-format`: Output format (stream-json, json)
- `--verbose`: Verbose logging
- `--mcp-debug`: Debug MCP configuration
- `--allowedTools`: Specify allowed tools
- `--disable-tool`: Disable specific tools
- `--disable-all-tools`: Disable all tools

3. **No Support For**
- `--prompt-file`: Does not exist
- `--spec_file`: Not a real flag
- `--output_dir`: Not supported
- `--count`: No such parameter
- `/agent` command: Completely fictional

### What The Pattern Describes

```bash
/agent --prompt-file infinite.md --spec_file spec.md --output_dir output --count 50
```

This command would supposedly:
- Use `/agent` as the command (doesn't exist)
- Load orchestration from `infinite.md`
- Read specification from `spec.md`
- Output to `output` directory
- Run 50 iterations

**Reality**: None of these features exist in Claude Code.

### Actual Implementation Approaches

1. **Using Headless Mode**
```bash
# Real command for automation
claude -p "Generate variation based on spec.md and save to output/"
```

2. **External Script Wrapper**
```bash
#!/bin/bash
# Manual implementation of the pattern
SPEC_FILE="spec.md"
OUTPUT_DIR="output"
COUNT=50

for i in $(seq 1 $COUNT); do
  PROMPT="Generate iteration $i based on $SPEC_FILE, save to $OUTPUT_DIR/gen_$i"
  claude -p "$PROMPT"
done
```

3. **Custom Command Approach**
```markdown
# File: .claude/commands/generate.md
Generate based on specification: $ARGUMENTS

1. Read the specification file
2. Create unique variation
3. Save to output directory
```

Usage: `/project:generate spec.md`

### Community Implementations

The **infinite-agentic-loop** GitHub project shows how this might work:
- Uses `.claude/commands/infinite.md` for the orchestration logic
- Implements the pattern through custom commands
- Still requires manual execution, not automatic

### Real Examples from Research

1. **Harper Reed's Workflow**
```bash
# Uses simple commands repeatedly
claude
# Then types "continue" multiple times
```

2. **files-to-prompt Development**
```bash
# Simon Willison's approach
cat files_to_prompt/cli.py | llm -m opus --system "modify this code..."
```

3. **Headless Automation**
```bash
# From best practices
claude -p "migrate foo.py from React to Vue" --allowedTools Edit Bash
```

### Why The Confusion?

1. **Conceptual vs. Real**
   - Pattern shows desired functionality
   - Not actual implementation
   - Requires external tooling

2. **Community Extensions**
   - People build wrappers
   - Create custom commands
   - Simulate the behavior

3. **Wishful Documentation**
   - Describes ideal system
   - Not current reality
   - Inspires implementations

### Actual Automation Patterns

**Pattern 1: Shell Loop**
```bash
for task in tasks/*.md; do
  claude -p "Execute task from $task"
done
```

**Pattern 2: JSON Pipeline**
```bash
claude -p "Generate plan" --output-format json | \
  jq '.tasks[]' | \
  xargs -I {} claude -p "Execute: {}"
```

**Pattern 3: Custom Commands**
```bash
# Create command
echo "Process: \$ARGUMENTS" > .claude/commands/process.md
# Use it
claude
> /project:process spec.md
```

## Conclusion
The discovered command pattern is entirely fictional. Claude Code uses simple, standard CLI flags without support for the complex orchestration syntax described. Any implementation of the infinite loop pattern requires extensive external scripting around Claude Code's actual, limited command-line interface.

## References
- [Claude Code CLI Usage](https://docs.anthropic.com/en/docs/claude-code/cli-usage)
- [Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)
- [Building files-to-prompt with Claude](https://simonwillison.net/2024/Apr/8/files-to-prompt/)
- [infinite-agentic-loop GitHub](https://github.com/disler/infinite-agentic-loop)
