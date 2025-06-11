# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose
This is a curated collection of creative CLAUDE.md examples for Claude Code workflows. It's a documentation repository, not an executable codebase.

## Key Guidelines

### Working with Examples
- Examples are organized by category in `/examples/`
- Some examples are practical implementations, others are conceptual designs
- Each example demonstrates different CLAUDE.md patterns and techniques

### Common Tasks
- **Find examples**: Use `find examples/ -name "*.md"` to list all examples
- **Search patterns**: Use grep to find specific CLAUDE.md patterns across examples
- **Add new example**: Create appropriately categorized `.md` file in `/examples/`

### Example Categories
- `general/` - Basic CLAUDE.md patterns (e.g., $ARGUMENTS usage)
- `infinite_agent_loop/` - Advanced conceptual patterns for agent workflows
- `multi_agent_coordination/` - Team-based development methodologies
- `simon_couch/` - Content injection and documentation techniques

### Contributing
When adding or modifying examples:
1. Maintain clear categorization
2. Include practical use cases where possible
3. Mark conceptual designs clearly
4. Follow existing formatting patterns

### Permissions
The repository uses minimal permissions (see `.claude/settings.local.json`):
- Allowed: `Bash(find:*)`
- This is intentional to limit operations to documentation tasks