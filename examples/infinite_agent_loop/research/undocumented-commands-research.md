# Research: Command Discovery - Undocumented Commands

## Status: Research Complete

### Research Date: June 11, 2025

## Summary
Most "undocumented" commands in the infinite agent loop are fictional. However, Claude Code does have some genuine undocumented or lesser-known commands that work in practice.

## Documented Commands

### Official Commands
1. **`/init`** - Initialize project context, creates CLAUDE.md
2. **`/compact`** - Compact conversation history
3. **`/doctor`** - Check Claude Code installation health
4. **`/bug`** - Report issues directly within Claude Code
5. **`/allowed-tools`** - Manage tool permissions
6. **`/install-github-app`** - Install GitHub integration

### Custom Commands
- Located in `.claude/commands/` directory
- Accessed via `/project:command-name` or `/user:command-name`
- Support `$ARGUMENTS` placeholder

## Lesser-Known Features

### 1. Quick Memory Shortcut
- Start input with `#` to save to memory files
- Prompts for memory location selection
- Useful for persistent notes

### 2. Auto-Accept Mode
- **Shift+Tab** activates autonomous editing
- Claude edits files, runs tests, iterates
- Reduced manual approval needed

### 3. Verbose Mode
- `--verbose` flag shows turn-by-turn output
- Helpful for debugging
- Available in both interactive and print modes

### 4. Community Commands
From awesome-claude-code repositories:
- `/2-commit-fast` - Auto-select first git commit message
- `/dump` - Export conversation to `.claude/logs/`
- `/do-issue` - Implement GitHub issues

## Fictional Commands from Infinite Loop

### Commands That Don't Exist
1. **`/agent`** - Spawn autonomous agents (fictional)
2. **`/wave`** - Manage agent waves (fictional)
3. **`/orchestrate`** - Coordinate agents (fictional)
4. **`/iterate`** - Manage iterations (fictional)

### Flags That Don't Exist
- `--prompt-file` (fictional)
- `--spec_file` (fictional)
- `--output_dir` (fictional)
- `--count` (fictional)

## Hidden Implementation Details

### From Code Analysis
- Main logic in `cli.mjs` (heavily obfuscated)
- MCP (Model Control Protocol) client support
- Internal codename: "tengu" (found in source)
- Uses Ink for React-based CLI interface

### Undocumented Behaviors
1. **Session Storage**
   - Sessions stored in local directory
   - Can be resumed with `--continue`
   - Conversation picker with `--resume`

2. **Tool Control**
   - `--disable-tool` for specific tools
   - `--disable-all-tools` for safety
   - `--allowedTools` for whitelist

3. **Output Formats**
   - `--output-format json`
   - `--output-format stream-json`
   - Useful for automation

## Real Multi-Agent Patterns

### Without Fictional Commands
```bash
# Parallel execution with git worktrees
for i in {1..5}; do
  git worktree add ../agent-$i
  (cd ../agent-$i && claude -p "Task $i") &
done

# Custom command for coordination
echo "Coordinate agents: \$ARGUMENTS" > .claude/commands/coordinate.md
```

## Conclusion

While the infinite agent loop describes many fictional commands, Claude Code does have genuine undocumented features like auto-accept mode, memory shortcuts, and various debugging flags. The key distinction is between:

1. **Real but undocumented**: Features that exist but aren't well publicized
2. **Fictional/aspirational**: Commands described in conceptual patterns that don't actually exist

Most of the infinite loop's command structure is fictional, designed to illustrate a desired workflow rather than document actual capabilities. Real multi-agent coordination requires external scripting and creative use of documented features like git worktrees and headless mode.