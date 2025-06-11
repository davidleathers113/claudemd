# Getting Started with CLAUDE.md

Welcome! This guide will help you create your first CLAUDE.md file and understand how to leverage Claude Code effectively.

## 🎯 What You'll Learn

1. What CLAUDE.md files do
2. How to create your first configuration
3. Basic patterns that save time
4. How to create custom commands
5. Next steps for advanced usage

## 📚 Understanding CLAUDE.md

### What is CLAUDE.md?

CLAUDE.md is a special markdown file that Claude Code reads when you start a session. Think of it as:
- **Project memory** - Information that persists across sessions
- **Quick reference** - Commands and conventions at Claude's fingertips
- **Behavior guide** - How Claude should approach your project

### Where to Place CLAUDE.md

You can have CLAUDE.md files at different levels:

1. **Global** (`~/.claude/CLAUDE.md`)
   - Personal preferences across all projects
   - Your coding style preferences
   - Common tools and commands

2. **Project** (`/path/to/project/CLAUDE.md`)
   - Project-specific information
   - Build commands and scripts
   - Team conventions

3. **Directory** (`/path/to/project/subdir/CLAUDE.md`)
   - Specialized rules for parts of your project
   - Module-specific commands

## 🚀 Your First CLAUDE.md

### Step 1: Create the File

In your project root, create `CLAUDE.md`:

```markdown
# My Project

## Overview
This is a Node.js web application using Express and PostgreSQL.

## Quick Commands
- **Start Dev**: `npm run dev`
- **Run Tests**: `npm test`
- **Build**: `npm run build`

## Coding Standards
- Use TypeScript for all new files
- Follow ESLint rules
- Write tests for new features

## Project Structure
- `/src` - Application source code
- `/tests` - Test files
- `/docs` - Documentation
```

### Step 2: Test It

Start Claude Code in your project:
```bash
cd /path/to/project
claude
```

Ask Claude: "What are the quick commands for this project?"

Claude should respond with the commands from your CLAUDE.md!

## 💡 Essential Patterns

### 1. Command Reference
Always include your most-used commands:

```markdown
## Commands
- **Install**: `npm install`
- **Dev Server**: `npm run dev` (port 3000)
- **Test**: `npm test`
- **Test Watch**: `npm run test:watch`
- **Lint**: `npm run lint`
- **Format**: `npm run format`
- **Build**: `npm run build`
- **Deploy**: `npm run deploy`
```

### 2. Context That Matters
Help Claude understand your project:

```markdown
## Important Context
- We use React 18 with TypeScript
- State management via Zustand (not Redux)
- Tailwind CSS for styling
- Vitest for testing (not Jest)
- API calls go through `/src/services`
```

### 3. Rules and Constraints
Prevent common mistakes:

```markdown
## Important Rules
- NEVER commit directly to main branch
- ALWAYS run tests before committing
- Use conventional commits (feat:, fix:, etc.)
- Keep components under 200 lines
- Extract hooks to `/src/hooks`
```

### 4. Examples and Templates
Show Claude your patterns:

```markdown
## Code Patterns

### New Component Template
\```typescript
import { FC } from 'react';

interface ComponentNameProps {
  // props here
}

export const ComponentName: FC<ComponentNameProps> = (props) => {
  return <div>Component</div>;
};
\```

### API Service Pattern
\```typescript
export const userService = {
  async getUsers() {
    return api.get('/users');
  }
};
\```
```

## 🎨 Creating Custom Commands

### Basic Command Structure

Create `.claude/commands/generate-component.md`:

```markdown
# Generate Component

Parse component name from $ARGUMENTS.

Create a new React component with:
1. TypeScript interface
2. Styled components
3. Basic test file

Place files in:
- Component: `/src/components/{name}/{name}.tsx`
- Test: `/src/components/{name}/{name}.test.tsx`
```

### Using Your Command

In Claude Code:
```
/generate-component Button
```

### Advanced Command Example

```markdown
# Feature Generator

Parse from $ARGUMENTS:
1. Feature name (required)
2. Include API? (optional, default: yes)
3. Include tests? (optional, default: yes)

Generate complete feature structure:
- Page component
- API service
- State management
- Tests
- Update routing
```

## 📈 Leveling Up

### Next Steps

1. **Study Examples**
   - Browse our [examples directory](../examples/)
   - Start with patterns matching your tech stack

2. **Create Commands**
   - Identify repetitive tasks
   - Create custom commands for them
   - Share successful patterns

3. **Try Orchestrators**
   - For complex multi-file changes
   - For exploring multiple solutions
   - For systematic refactoring

### Common Progressions

**Week 1**: Basic CLAUDE.md with commands
**Week 2**: First custom command
**Month 1**: Multiple commands, refined CLAUDE.md
**Month 2**: Simple orchestrators
**Month 3**: Advanced patterns

## 🆘 Troubleshooting

### Claude Isn't Reading CLAUDE.md
- Check file name (exactly `CLAUDE.md`)
- Ensure it's in the project root
- Restart Claude Code session

### Commands Not Working
- Check `.claude/commands/` directory exists
- Verify command file has `.md` extension
- Ensure `$ARGUMENTS` is parsed correctly

### Too Much Information
- Start simple, add incrementally
- Focus on what saves time
- Remove unused sections

## 📚 Resources

### Templates
- [Basic Template](../templates/claude-md/basic.md)
- [Web Dev Template](../templates/claude-md/web-dev.md)
- [Command Templates](../templates/commands/)

### Advanced Guides
- [Custom Commands Deep Dive](./features/custom-commands.md)
- [Multi-Agent Patterns](./features/multi-agent.md)
- [Performance Optimization](./reference/performance.md)

### Community
- [Contributing Guide](../CONTRIBUTING.md)
- [Examples Collection](../examples/)
- [Research Findings](../examples/infinite_agent_loop/research/)

## 🎉 You're Ready!

You now know how to:
- ✅ Create CLAUDE.md files
- ✅ Add useful commands and context
- ✅ Create custom commands
- ✅ Find more advanced patterns

Start simple, iterate based on your needs, and don't hesitate to experiment!

---

*Questions? Check our [FAQ](./faq.md) or [open an issue](https://github.com/davidleathers113/claudemd/issues).*