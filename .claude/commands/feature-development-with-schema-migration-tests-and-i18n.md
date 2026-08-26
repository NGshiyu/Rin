---
name: feature-development-with-schema-migration-tests-and-i18n
description: Workflow command scaffold for feature-development-with-schema-migration-tests-and-i18n in Rin.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /feature-development-with-schema-migration-tests-and-i18n

Use this workflow when working on **feature-development-with-schema-migration-tests-and-i18n** in `Rin`.

## Goal

Implements a new feature that requires database schema changes, updates to API types and validation, backend and frontend logic, test cases, and i18n/localization keys.

## Common Files

- `server/sql/NNNN.sql`
- `server/src/db/schema.ts`
- `packages/api/src/types.ts`
- `packages/api/src/schemas.ts`
- `server/src/services/*.ts`
- `client/src/page/*.tsx`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Create or update SQL migration file in server/sql/NNNN.sql
- Update Drizzle schema in server/src/db/schema.ts
- Update shared API types in packages/api/src/types.ts
- Update validation schemas in packages/api/src/schemas.ts
- Implement backend logic in server/src/services/*.ts

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.