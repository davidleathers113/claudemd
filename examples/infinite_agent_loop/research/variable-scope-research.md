# Research: Variable Scope - Full Scope of Variable Interpolation Support

## Summary
Claude Code officially supports only one variable: `$ARGUMENTS` for simple string replacement in custom slash commands. There is no complex variable interpolation system, no nested variables, and no dynamic variable resolution. Any advanced variable behavior seen in demonstrations relies on Claude's intelligence to understand patterns, not built-in features.

## Key Findings

### 1. Official Variable Support

**$ARGUMENTS - The Only Variable**
- Simple string replacement placeholder
- Used in custom slash commands
- Captures everything after command name
- No parsing or transformation
- Direct substitution only

**How It Works**
```markdown
<!-- .claude/commands/example.md -->
Process the file: $ARGUMENTS
```
Usage: `/project:example myfile.txt`
Result: Claude receives "Process the file: myfile.txt"

**Limitations**
- Single variable only
- No multiple placeholders
- No named parameters
- No default values
- No variable transformation

### 2. What Doesn't Exist

**No Complex Variables**
- ❌ `{spec_file}`
- ❌ `{output_dir}`
- ❌ `{iteration_number}`
- ❌ `{master_plan}`
- ❌ `{previous_iteration_summary}`

**No Variable Features**
- ❌ Nested interpolation
- ❌ Conditional variables
- ❌ Variable scoping
- ❌ Environment variables
- ❌ Dynamic generation

**No Advanced Syntax**
- ❌ `${variable:-default}`
- ❌ `{{variable}}`
- ❌ `%variable%`
- ❌ Variable arrays
- ❌ Variable objects

### 3. How Complex Patterns Work

**Claude's Pattern Recognition**
- When complex variables appear to work, it's Claude understanding the pattern
- Not actual variable substitution
- Intelligence-based interpretation
- Context-aware replacement
- Works because Claude is smart, not because of features

**Example Breakdown**
```markdown
<!-- What appears to work -->
Generate {count} iterations starting from {spec_file}

<!-- What actually happens -->
1. Claude reads the entire prompt
2. Recognizes patterns like {variable}
3. Understands from context what values should be
4. Mentally substitutes while processing
5. No actual variable system involved
```

### 4. Practical Examples

**Basic $ARGUMENTS Usage**
```markdown
<!-- .claude/commands/create-component.md -->
Create a new React component named: $ARGUMENTS

Requirements:
- Use TypeScript
- Include tests
- Follow project conventions
```

**Multiple Values in $ARGUMENTS**
```markdown
<!-- User types: /project:create-component Button primary large -->
<!-- Claude receives: "...named: Button primary large" -->
<!-- Must parse manually in prompt -->
Parse the arguments:
- Component name: first word
- Type: second word  
- Size: third word
```

**Workarounds for Multiple Parameters**
```markdown
<!-- .claude/commands/advanced.md -->
Parse $ARGUMENTS as: [action] [target] [options]
Examples:
- "create user --admin"
- "delete post 123"
- "update config --verbose"
```

### 5. Community Patterns

**Structured Arguments**
```markdown
<!-- Some users structure arguments -->
$ARGUMENTS should be in format: <command>:<target>:<flags>
Example: create:component:--typescript
```

**Fake Variable Syntax**
```markdown
<!-- This works through Claude's intelligence -->
The spec file is {spec_file} and output goes to {output_dir}
<!-- Claude infers from /infinite spec.md output that -->
<!-- {spec_file} = spec.md, {output_dir} = output -->
```

**Context-Based Substitution**
- Claude recognizes placeholder patterns
- Uses conversation context
- Makes intelligent substitutions
- Not a real variable system

### 6. Official Documentation

**From Anthropic Docs**
> "Custom slash commands can include the special keyword $ARGUMENTS"

**From Community Examples**
> "Command files also support interpolation using $ARGUMENTS syntax"

**Key Quote**
> "$ARGUMENTS captures everything after the command name"

### 7. Comparison with Other Systems

| Feature | Claude Code | Shell Scripts | Template Engines |
|---------|------------|---------------|------------------|
| Basic Variables | $ARGUMENTS only | $1, $2, $@ | {{var}} |
| Named Variables | ❌ | ${NAME} | {{user.name}} |
| Defaults | ❌ | ${VAR:-default} | {{var\|default}} |
| Conditionals | ❌ | if/then | {{#if}} |
| Loops | ❌ | for/while | {{#each}} |
| Nesting | ❌ | Yes | Yes |

## Implementation Reality

### What Works
```markdown
<!-- Simple argument passing -->
Create a file named: $ARGUMENTS
Run tests for: $ARGUMENTS
Fix the issue: $ARGUMENTS
```

### What Doesn't Work (Natively)
```markdown
<!-- These require Claude's interpretation -->
<!-- Not actual variable substitution -->
Process {iteration} of {total}
Save to {output_dir}/generation_{number}
Load config from {config_file:-default.json}
```

### Why Confusion Exists
1. Claude is intelligent enough to understand variable-like patterns
2. Demonstrations show Claude replacing placeholders
3. Looks like variable interpolation
4. Actually pattern recognition
5. No documentation clarifying this

## Best Practices

### For Single Arguments
```markdown
<!-- Clear and simple -->
Analyze the file: $ARGUMENTS
```

### For Multiple Arguments
```markdown
<!-- Provide parsing instructions -->
Parse $ARGUMENTS as space-separated values:
1. First value: action
2. Second value: target
3. Remaining: options
```

### For Complex Needs
```markdown
<!-- Use structured format -->
Expect $ARGUMENTS in JSON format:
{"action": "create", "type": "component", "name": "Button"}
```

## Workarounds for Advanced Needs

### External Preprocessing
```bash
# Preprocess before Claude
SPEC_FILE="spec.md"
OUTPUT_DIR="output"
claude -p "$(sed "s/{spec_file}/$SPEC_FILE/g; s/{output_dir}/$OUTPUT_DIR/g" prompt.md)"
```

### Wrapper Scripts
```python
# Python wrapper for complex variables
def run_claude_with_vars(prompt_template, variables):
    prompt = prompt_template
    for var, value in variables.items():
        prompt = prompt.replace(f"{{{var}}}", value)
    subprocess.run(['claude', '-p', prompt])
```

### Using Claude's Intelligence
```markdown
<!-- Let Claude figure it out -->
Based on the command arguments ($ARGUMENTS), determine:
- What file to process
- Where to save output  
- How many iterations
```

## Conclusion

Claude Code's variable interpolation is limited to the single `$ARGUMENTS` placeholder for simple string replacement in custom commands. There is no complex variable system, no multiple placeholders, and no advanced interpolation features. When demonstrations show complex variable-like behavior, it's Claude's intelligence recognizing patterns and making substitutions, not a built-in variable system. This fundamental limitation means that sophisticated variable interpolation must be handled through external preprocessing, wrapper scripts, or by leveraging Claude's ability to understand context and patterns. The simplicity is intentional—keeping Claude Code focused on AI assistance rather than becoming a full scripting language.