```markdown
# Rin Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill provides a comprehensive guide to the development patterns, coding conventions, and workflows used in the Rin TypeScript codebase. Rin is structured as a monorepo with both backend and frontend components, but does not use a specific framework. The repository emphasizes clear commit practices, consistent code style, and robust workflows for feature development, schema migrations, localization, and testing.

## Coding Conventions

### File Naming
- Use **camelCase** for file names.
  - Example: `userProfile.ts`, `getUserData.tsx`

### Import Style
- Use **relative imports** within modules.
  - Example:
    ```typescript
    import { getUser } from './userService';
    ```

### Export Style
- Use **named exports** for all modules.
  - Example:
    ```typescript
    // userService.ts
    export function getUser(id: string) { ... }
    export function updateUser(id: string, data: User) { ... }
    ```

### Commit Messages
- Prefixes: `feat`, `chore`, `fix`
- Average message length: ~52 characters
- Example:
  ```
  feat: add user profile page with localization
  fix: correct validation schema for email field
  ```

## Workflows

### Feature Development with Schema Migration, Tests, and i18n
**Trigger:** When adding a new feature that involves user-facing changes, database modifications, and needs to be fully tested and localized.  
**Command:** `/feature-with-schema-i18n-tests`

1. **Create or update SQL migration:**
   - Add a new migration file in `server/sql/NNNN.sql`.
   - Example:
     ```sql
     ALTER TABLE users ADD COLUMN nickname VARCHAR(255);
     ```
2. **Update Drizzle schema:**
   - Edit `server/src/db/schema.ts` to reflect DB changes.
     ```typescript
     export const users = pgTable('users', {
       id: serial('id').primaryKey(),
       nickname: varchar('nickname', { length: 255 }),
     });
     ```
3. **Update shared API types:**
   - Modify `packages/api/src/types.ts` as needed.
     ```typescript
     export interface User {
       id: string;
       nickname?: string;
     }
     ```
4. **Update validation schemas:**
   - Edit `packages/api/src/schemas.ts`.
     ```typescript
     export const userSchema = z.object({
       nickname: z.string().max(255).optional(),
     });
     ```
5. **Implement backend logic:**
   - Update or add files in `server/src/services/*.ts`.
6. **Update or create frontend UI:**
   - Edit or add pages in `client/src/page/*.tsx`.
7. **Add or update locale translation files:**
   - Update `client/public/locales/*/translation.json`.
     ```json
     {
       "nickname": "Nickname"
     }
     ```
8. **Update test fixtures:**
   - Edit `server/tests/fixtures/index.ts` for new data.
9. **Add or update backend tests:**
   - Write tests in `server/src/services/__tests__/*.test.ts`.

### Atomic Revert of Multi-file Feature
**Trigger:** When you need to quickly undo a recently merged feature or fix that touched multiple files.  
**Command:** `/revert-feature`

1. **Identify all files changed by the feature/fix commit(s):**
   - Use `git log` or your code review tool to list affected files.
2. **Create a revert commit:**
   - Restore all affected files to their previous state in a single commit.
   - Example:
     ```bash
     git revert <commit-hash>
     # Or manually checkout previous versions and commit
     ```

## Testing Patterns

- **Test Framework:** Not explicitly detected; test files use the pattern `*.test.*`.
- **Test Location:** Backend tests are in `server/src/services/__tests__/*.test.ts`.
- **Fixtures:** Test data lives in `server/tests/fixtures/index.ts`.
- **Example Test File:**
  ```typescript
  // server/src/services/__tests__/userService.test.ts
  import { getUser } from '../userService';

  test('gets user by id', () => {
    expect(getUser('123')).toEqual({ id: '123', nickname: 'Alice' });
  });
  ```

## Commands

| Command                              | Purpose                                                        |
|---------------------------------------|----------------------------------------------------------------|
| /feature-with-schema-i18n-tests       | Start a feature with DB migration, types, validation, i18n, and tests |
| /revert-feature                      | Atomically revert a multi-file feature or fix                  |
```
