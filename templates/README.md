# Claude Code Templates

Ready-to-use templates for common CLAUDE.md patterns and custom commands. Copy, customize, and enhance your Claude Code workflow!

## 📁 Template Categories

### [CLAUDE.md Templates](claude-md/)
Complete CLAUDE.md configurations for different project types:
- [Basic Project](claude-md/basic.md) - Minimal setup for any project
- [Web Development](claude-md/web-dev.md) - React/Vue/Angular projects
- [Python Project](claude-md/python.md) - Data science & backend
- [API Development](claude-md/api.md) - REST/GraphQL services
- [Mobile App](claude-md/mobile.md) - React Native/Flutter
- [DevOps](claude-md/devops.md) - Infrastructure & deployment

### [Custom Commands](commands/)
Reusable command templates:
- [Code Generator](commands/generator.md) - Generate boilerplate code
- [Test Creator](commands/test-creator.md) - Automated test generation
- [Refactoring Assistant](commands/refactor.md) - Code improvement
- [Documentation Builder](commands/docs-builder.md) - Auto-documentation
- [Performance Analyzer](commands/performance.md) - Optimization helper

## 🚀 Quick Start

### Using CLAUDE.md Templates

1. Choose a template that matches your project type
2. Copy to your project root as `CLAUDE.md`
3. Customize the sections marked with `TODO`
4. Add project-specific commands and conventions

### Using Command Templates

1. Create `.claude/commands/` directory in your project
2. Copy command template with descriptive name (e.g., `generate-component.md`)
3. Modify the `$ARGUMENTS` parsing for your needs
4. Use with `/command-name` in Claude Code

## 💡 Customization Tips

### Variables to Replace
Look for these placeholders in templates:
- `[PROJECT_NAME]` - Your project's name
- `[TECH_STACK]` - Your technology choices
- `[BUILD_COMMAND]` - Your build script
- `TODO:` - Sections requiring customization

### Adding Project Context
Enhance templates with:
```markdown
## Project-Specific Context
- External APIs we integrate with
- Performance requirements
- Security considerations
- Team conventions
```

### Command Parameters
Customize `$ARGUMENTS` parsing:
```markdown
Parse from $ARGUMENTS:
1. `component` - Component name (required)
2. `type` - Component type: "page" | "widget" | "layout" (default: "widget")
3. `style` - Styling approach: "css" | "styled" | "tailwind" (default: "css")
```

## 📋 Template Checklist

Before using a template:
- [ ] Review all sections
- [ ] Replace placeholder values
- [ ] Add project-specific rules
- [ ] Test with simple tasks
- [ ] Iterate based on results

## 🎯 Best Practices

1. **Start Simple** - Don't over-configure initially
2. **Iterate Often** - Refine based on actual use
3. **Document Why** - Explain reasoning for rules
4. **Share Back** - Contribute improvements

---

*Templates are starting points. The best CLAUDE.md is one that evolves with your project!*