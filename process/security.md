# Secrets, real data, and what the AI never does alone — CLAUDE.md section 8

Applies in every stage and at every pipeline level.

## 1. Secrets

A secret is any password, key, or token.

- Secrets live in the service's own environment settings and in the local env file that git ignores. The human enters them. The AI refers to a secret by its variable name.
- `.env.example` in the repo lists variable names with empty values.
- **A secret that appears in a chat, a commit, or a log has leaked.** Change that secret the same day, then note the date in `PM_STATE.md`. This holds even when the leak seems harmless.
- CI scans every push for secrets (see [`templates/ci.example.yml`](../templates/ci.example.yml)).

## 2. Real data

- Conversations with the AI, tests, and demos use made-up data.
- A screenshot or log from the live system has names, phone numbers, ID numbers, and addresses covered before it is given to the AI.
- A bug reported by a real customer is reproduced with made-up data.
- Work done for a Client: tell the Client in the proposal that the system is developed with AI, and ask for sample data that is not real.

## 3. Actions that always need a human

The AI prepares these and the human performs them, or approves each single action before the AI does it:

| Action | Why |
|---|---|
| Deploying to production · merging into the production branch | The human's approval must be the last step before users are affected |
| Running a migration or writing directly to the production database | Cannot be undone by a code rollback |
| Entering, reading back, or changing the value of a secret | Section 1 |
| Deleting data, or any step that cannot be reversed | The cost of a mistake has no ceiling |
| Sending a message to a customer or any third party | It speaks for the human |
| Spending money: paid plans, purchases, upgrades | The human's budget |
| Editing CI workflow files or weakening a check | The AI must not be able to switch off its own gate |

An approval for one action covers that action only.
