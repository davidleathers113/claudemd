# Research: Undocumented Flags

## Status: Fictional Flags

### Research Date: June 11, 2025

## Summary
The undocumented flags described in the infinite loop pattern (`--prompt-file`, `--spec_file`, `--output_dir`, `--count`) **do not exist**. Claude Code has a limited set of documented flags, and no evidence supports the existence of these specific undocumented flags.

## Research Findings

### Documented Flags (Official)

1. **Core Flags**
   - `-p, --print`: Headless mode with prompt
   - `--output-format`: Output format (json, stream-json)
   - `--verbose`: Verbose logging
   - `--mcp-debug`: Debug MCP configuration
   - `-h, --help`: Show help
   - `--version`: Show version

2. **Tool Control Flags**
   - `--allowedTools`: Specify allowed tools
   - `--disable-tool`: Disable specific tools
   - `--disable-all-tools`: Disable all tools

3. **Configuration Flags**
   - `--global, -g`: Apply to global configuration
   - Various config-related flags through `claude config`

### Flags That Don't Exist

The following flags from the infinite loop pattern are **completely fictional**:
- `--prompt-file`: Load prompts from file
- `--spec_file`: Specify input specification
- `--output_dir`: Set output directory
- `--count`: Control iteration count

These flags would be useful for the pattern but are not implemented.

### Internal/Hidden Features (From Research)

1. **Thinking Modes** (From decompiled source)
   - Triggered by keywords in prompts:
   - "think" < "think hard" < "think harder" < "ultrathink" < "megathink"
   - Allocates different thinking budgets
   - Not a CLI flag but prompt-based

2. **Internal Code Name**
   - Claude Code's internal name is "tengu"
   - Uses CommanderJS for CLI parsing
   - Built with React Ink for terminal UI

3. **Unminified Prompts**
   - GitHub gist exists with decompiled prompts
   - Shows internal tool definitions
   - Not accessible via flags

### Community Findings

1. **Decompilation Efforts**
   - Source code is obfuscated
   - ~20MB single file (cli.mjs)
   - ~200k lines when prettified
   - Uses CommanderJS and React Ink

2. **No Hidden Flag Discovery**
   - No reports of hidden flags
   - Community focuses on documented features
   - External tools fill gaps

3. **Feature Requests**
   - `.claudeignore` file (Issue #79)
   - More granular permissions
   - Better automation support

### What Actually Works

1. **Headless Automation**
```bash
# Real command
claude -p "Your prompt" --output-format json --verbose

# NOT real
claude --prompt-file infinite.md --count 50
```

2. **Tool Permissions**
```bash
# Real
claude --allowedTools Edit,Bash --disable-tool Read

# NOT real
claude --spec_file spec.md --output_dir output
```

3. **MCP Configuration**
```bash
# Real
claude --mcp-debug

# NOT real
claude --agent-mode parallel
```

### Why The Confusion

1. **Wishful Documentation**
   - Pattern describes ideal interface
   - Not actual implementation
   - Inspires external tools

2. **Community Extensions**
   - People create wrappers
   - Add missing functionality
   - Document as if native

3. **Conceptual vs. Real**
   - Shows desired workflow
   - Requires external implementation
   - Mixed with real features

### Implementation Reality

To achieve the undocumented flag behavior:

1. **Wrapper Script**
```bash
#!/bin/bash
# Simulate --prompt-file
PROMPT=$(cat $1)
claude -p "$PROMPT"

# Simulate --output_dir
OUTPUT_DIR=$2
claude -p "Save output to $OUTPUT_DIR"

# Simulate --count
for i in $(seq 1 $3); do
  claude -p "Iteration $i"
done
```

2. **Configuration File Approach**
```json
// config.json (custom, not Claude)
{
  "prompt_file": "infinite.md",
  "spec_file": "spec.md",
  "output_dir": "output",
  "count": 50
}
```

3. **External Tools**
- Build custom CLI wrapper
- Parse custom flags
- Translate to real Claude commands

## Conclusion
The undocumented flags in the infinite loop pattern are entirely fictional. Claude Code has a simple, limited set of flags focused on basic operation, output formatting, and tool control. Any complex orchestration requires external scripting and tooling.

## References
- [Claude Code CLI Usage](https://docs.anthropic.com/en/docs/claude-code/cli-usage)
- [Claude Code Settings](https://docs.anthropic.com/en/docs/claude-code/settings)
- [Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)
- [Unminified Claude Code Prompts (Gist)](https://gist.github.com/transitive-bullshit/487c9cb52c75a9701d312334ed53b20c)
- [Claude Code: Anthropic's Agent in Your Terminal](https://www.latent.space/p/claude-code)
