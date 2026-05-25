---
name: atomic-revert-of-multi-file-feature
description: Workflow command scaffold for atomic-revert-of-multi-file-feature in Rin.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /atomic-revert-of-multi-file-feature

Use this workflow when working on **atomic-revert-of-multi-file-feature** in `Rin`.

## Goal

Reverts a multi-file feature by reverting all related files in a single commit, often following a previous feature or fix commit.

## Common Files

- `client/src/page/*.tsx`
- `packages/api/src/schemas.ts`
- `packages/api/src/types.ts`
- `server/sql/NNNN.sql`
- `server/src/db/schema.ts`
- `server/src/services/*.ts`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Identify all files changed by the feature/fix commit(s)
- Create a revert commit that restores all affected files to their previous state

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.