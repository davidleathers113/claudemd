# Code Generator Command

This command generates boilerplate code based on templates.

## Variables
Parse from $ARGUMENTS:
1. `type` - What to generate: "component" | "service" | "test" | "model"
2. `name` - Name for the generated code
3. `options` - Additional options (optional)

## Execution

### Phase 1: Validation
- Verify `type` is supported
- Check `name` follows naming conventions
- Ensure target directory exists

### Phase 2: Template Selection
Based on `type`, select appropriate template:

#### Component Template
```typescript
import React from 'react';
import styles from './${name}.module.css';

interface ${name}Props {
  // TODO: Define props
}

export const ${name}: React.FC<${name}Props> = (props) => {
  return (
    <div className={styles.container}>
      <h2>${name}</h2>
      {/* TODO: Implement component */}
    </div>
  );
};
```

#### Service Template
```typescript
export class ${name}Service {
  constructor(private readonly apiClient: ApiClient) {}
  
  async get${name}(): Promise<${name}[]> {
    // TODO: Implement
  }
  
  async create${name}(data: Create${name}Dto): Promise<${name}> {
    // TODO: Implement
  }
}
```

#### Test Template
```typescript
import { describe, it, expect } from 'vitest';
import { ${name} } from './${name}';

describe('${name}', () => {
  it('should exist', () => {
    expect(${name}).toBeDefined();
  });
  
  // TODO: Add test cases
});
```

### Phase 3: Generation
1. Create file at appropriate location
2. Apply template with name substitution
3. Add necessary imports
4. Update index files if needed

### Phase 4: Post-Generation
- Format generated code
- Add to git
- Suggest next steps

## Example Usage
```
/generator component UserProfile
/generator service Authentication
/generator test UserProfile
```

## Advanced Options
- `--typescript` / `--javascript` - Language choice
- `--style css|scss|styled` - Styling approach
- `--with-tests` - Also generate test file
- `--dry-run` - Preview without creating files