# Claude Code Quick Reference Card

## 🚀 Essential Commands

### CLI Basics
```bash
claude                    # Start interactive session
claude -p "prompt"       # Headless mode (no interaction)
claude --continue        # Resume previous session
claude --resume <id>     # Resume specific session
```

### In-Session Commands
```
/help                    # Show available commands
/compact                 # Reduce context usage
/undo                    # Undo last change
/clear                   # Clear conversation
/save <name>            # Save conversation point
/load <name>            # Load saved point
```

## 📁 File Structure

```
project/
├── CLAUDE.md                    # Project configuration
├── .claude/
│   ├── settings.json           # Local settings
│   └── commands/              # Custom commands
│       ├── generate.md        # /generate command
│       └── refactor.md        # /refactor command
└── ~/.claude/CLAUDE.md         # Global configuration
```

## 📝 CLAUDE.md Essentials

### Minimal Template
```markdown
# Project Name

## Commands
- Build: `npm run build`
- Test: `npm test`

## Conventions
- TypeScript strict mode
- 2 spaces indentation
```

### Key Sections
- `## Commands` - Quick command reference
- `## Conventions` - Coding standards
- `## Structure` - Project organization
- `## Context` - Important background

## 🎯 Custom Commands

### Basic Command
```markdown
# Command Name

Parse from $ARGUMENTS:
1. `param1` - Description

Execute: [Instructions]
```

### Using Commands
```
/mycommand arg1 arg2
/generate component Button
/refactor extract-function
```

## 💡 Power User Tips

### Performance
- Use `/compact` when context gets large
- Keep CLAUDE.md under 500 lines
- Be specific in prompts

### Organization
- One task per message
- Clear success criteria
- Provide examples

### Git Integration
```bash
# Let Claude commit
git add .
# Then in Claude: "commit these changes"

# Review changes
git diff
# Then: "review these changes"
```

## 🔧 Common Patterns

### Feature Development
```
"Add user authentication with email/password"
Claude will:
1. Analyze project structure
2. Create necessary files
3. Implement feature
4. Add tests
```

### Refactoring
```
"Refactor UserService to use async/await"
"Extract validation logic to separate module"
"Improve performance of data processing"
```

### Testing
```
"Write tests for AuthController"
"Increase test coverage to 80%"
"Add E2E tests for login flow"
```

## ⚡ Advanced Features

### Multi-File Operations
```
"Update all API endpoints to use new error format"
"Rename User model to Account throughout codebase"
```

### Code Generation
```
/generate component Header
/generate api users
/generate test UserService
```

### Analysis Tasks
```
"Find all TODO comments"
"Identify performance bottlenecks"
"Check for security issues"
```

## 🚫 Limitations

### What Claude Code CAN'T Do
- Run GUI applications
- Access external websites (without tools)
- Modify system settings
- Run infinitely

### Context Limits
- ~200K tokens per session
- Use `/compact` to free space
- Start new session if needed

## 🔗 Useful Resources

- [Full Documentation](docs/)
- [Example Patterns](examples/)
- [Templates](templates/)
- [Research](examples/infinite_agent_loop/research/)

## 🎨 Best Practices

1. **Be Specific** - Clear instructions = better results
2. **Provide Context** - Share relevant background
3. **Iterative Approach** - Build incrementally
4. **Test Often** - Verify changes work
5. **Document Why** - Explain decisions in CLAUDE.md

---

*Keep this handy for quick lookups during development!*