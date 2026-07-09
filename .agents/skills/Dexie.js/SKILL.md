```markdown
# Dexie.js Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill teaches you the core development patterns, coding conventions, and maintenance workflows used in the Dexie.js codebase. Dexie.js is a TypeScript project for IndexedDB, following clear conventions for file naming, imports, exports, and dependency management. This guide will help you contribute code, maintain dependencies, and write tests in a way that aligns with the project's established practices.

## Coding Conventions

### File Naming
- **Style:** kebab-case
- **Example:**  
  `my-helper-file.ts`  
  `database-connection.ts`

### Import Style
- **Style:** Relative imports
- **Example:**
  ```typescript
  import { doSomething } from './utils/do-something';
  ```

### Export Style
- **Style:** Named exports
- **Example:**
  ```typescript
  export function openDatabase() { /* ... */ }
  export const DB_VERSION = 2;
  ```

### Commit Messages
- **Pattern:** Freeform, no enforced prefixes
- **Average Length:** ~64 characters
- **Example:**  
  `Fix bug in transaction handling when upgrading schema`

## Workflows

### Update NPM Dependencies Across Multiple Packages

**Trigger:** When you need to update third-party dependencies to their latest versions across several packages or samples in the monorepo.

**Command:** `/update-dependencies`

**Step-by-step Instructions:**

1. **Identify outdated dependencies**  
   Use tools like `npm outdated`, `pnpm`, or Dependabot to find outdated packages in each sub-package or sample.
   ```bash
   pnpm outdated
   ```
2. **Update version numbers**  
   For each affected package, update the version numbers in the corresponding `package.json` files.
   ```bash
   pnpm up --latest
   ```
3. **Regenerate lock files**  
   After updating, regenerate the lock files (`package-lock.json`, `pnpm-lock.yaml`) for each package to ensure consistency.
   ```bash
   pnpm install
   ```
4. **Commit changes**  
   Commit all updated `package.json` and lock files together with a summary of the changes.
   ```bash
   git add */package.json */package-lock.json pnpm-lock.yaml
   git commit -m "Update dependencies across packages"
   ```

**Files Involved:**
- `pnpm-lock.yaml`
- `*/package.json`
- `*/package-lock.json`

**Frequency:** ~2-4 times per month

## Testing Patterns

- **Testing Framework:** Not explicitly detected; look for test files matching `*.test.*`
- **Test File Naming:**  
  - Files are named with `.test.` in the filename, e.g., `database-connection.test.ts`
- **Example Test File:**
  ```typescript
  import { openDatabase } from './database-connection';

  test('should open database successfully', () => {
    expect(openDatabase()).toBeDefined();
  });
  ```

## Commands

| Command              | Purpose                                                        |
|----------------------|----------------------------------------------------------------|
| /update-dependencies | Update all npm dependencies across multiple packages/samples    |
```
