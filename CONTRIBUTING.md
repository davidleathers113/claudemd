# Contributing to Awesome Claude Code & CLAUDE.md

Thank you for your interest in contributing! This repository thrives on community contributions of creative CLAUDE.md patterns and Claude Code techniques.

## 📋 Table of Contents

- [What We're Looking For](#what-were-looking-for)
- [How to Contribute](#how-to-contribute)
- [Submission Guidelines](#submission-guidelines)
- [Example Format](#example-format)
- [Quality Standards](#quality-standards)
- [Getting Help](#getting-help)

## 🎯 What We're Looking For

### ✅ Great Contributions
- **Creative CLAUDE.md configurations** that solve real problems
- **Custom command examples** that showcase advanced usage
- **Orchestration patterns** for complex workflows
- **Integration examples** with tools, frameworks, or services
- **Performance optimizations** and best practices
- **Educational examples** that teach concepts clearly

### ❌ What We Don't Accept
- Malicious or harmful code
- Examples that violate API terms of service
- Poorly documented or untested patterns
- Duplicate submissions without significant improvements
- Content that doesn't relate to Claude Code or CLAUDE.md

## 🚀 How to Contribute

### 1. Fork and Clone
```bash
# Fork the repository on GitHub, then:
git clone https://github.com/YOUR_USERNAME/claudemd.git
cd claudemd
git checkout -b feat/your-contribution-name
```

### 2. Create Your Contribution

#### For New Examples
Create a directory structure like:
```
examples/
└── your-category/
    ├── README.md          # Explains your example
    ├── example-name.md    # Your CLAUDE.md or command
    └── supporting-files/  # Any additional files
```

#### For Documentation
```
docs/
└── appropriate-section/
    └── your-doc.md
```

### 3. Test Your Example
- Ensure your example works with current Claude Code
- Test edge cases and document limitations
- Include sample outputs where relevant

### 4. Submit Pull Request
```bash
git add .
git commit -m "feat: add [example-name] pattern"
git push origin feat/your-contribution-name
```

Then create a PR on GitHub with:
- Clear title: `feat: add [example-name] for [use-case]`
- Description of what your contribution does
- Why it's useful
- Any special requirements or limitations

## 📝 Submission Guidelines

### File Naming
- Use lowercase with hyphens: `my-example-name.md`
- Be descriptive but concise
- Group related files in directories

### Documentation Requirements
Every contribution must include:

1. **Overview** - What does this do?
2. **Use Cases** - When should someone use this?
3. **Requirements** - Any prerequisites or dependencies
4. **Implementation** - The actual code/configuration
5. **Example Usage** - Demonstration with expected results
6. **Limitations** - Known issues or constraints

## 📄 Example Format

Use this template for new examples:

```markdown
# [Pattern Name]

## Overview
Brief description of what this pattern/configuration does and why it's useful.

## Use Cases
- Specific scenario 1
- Specific scenario 2
- When NOT to use this pattern

## Requirements
- Claude Code version X.X+
- Any specific dependencies
- Required file structure

## Implementation

### CLAUDE.md Configuration
\```markdown
[Your CLAUDE.md content here]
\```

### Custom Commands (if applicable)
\```markdown
# .claude/commands/command-name.md
[Command content]
\```

## Example Usage

### Input
\```bash
claude [your command or workflow]
\```

### Expected Output
\```
[Show what users should expect to see]
\```

## Advanced Tips
- Performance considerations
- Customization options
- Integration with other patterns

## Limitations
- Known constraints
- Scenarios where this doesn't work well
- Potential improvements

## Credits
- Original author: [@your-github]
- Based on: [any inspirations]
- License: [if different from repo]
```

## ✅ Quality Standards

### Code Quality
- ✅ **Tested** - Actually works with Claude Code
- ✅ **Clear** - Easy to understand and modify
- ✅ **Documented** - Explains what and why
- ✅ **Efficient** - Doesn't waste tokens or time

### Documentation Quality
- ✅ **Complete** - All sections filled out
- ✅ **Accurate** - No misleading information
- ✅ **Practical** - Real-world applications
- ✅ **Accessible** - Clear to newcomers

### Community Standards
- ✅ **Respectful** - Inclusive language
- ✅ **Original** - Cite sources and inspirations
- ✅ **Helpful** - Genuinely useful to others

## 🤔 Getting Help

### Before Asking
1. Check existing examples for similar patterns
2. Review the [documentation](docs/)
3. Search [closed issues](https://github.com/davidleathers113/claudemd/issues?q=is%3Aissue+is%3Aclosed)

### Where to Ask
- **GitHub Issues** - For bugs or feature requests
- **Discussions** - For questions and ideas
- **Pull Request** - For feedback on your contribution

### Response Time
We aim to review PRs within a week. Popular or high-quality contributions may be fast-tracked.

## 🏆 Recognition

Contributors are added to:
- The README's Hall of Fame
- The example's credits section
- Our contributors list

Top contributors may be invited as maintainers!

---

Thank you for helping make Claude Code better for everyone! 🎉