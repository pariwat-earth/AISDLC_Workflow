# Stage 5 — Development

## Who
Dev. PM runs the readiness check first.

## How

### Before the first line of code
PM checks once, across documents:

- Every acceptance criterion has a task · every task cites a section that exists · the SA document matches the mockup · no grilling question is open. A conflict → fix the source document first (CLAUDE.md section 4.1).
- **The human has approved the core cases** ([`06-qa.md`](06-qa.md) round 1).
- **The repository is set up**: separate working and production branches · CI runs on every push (start from [`templates/ci.example.yml`](../../templates/ci.example.yml)) including a secret scan · `.env.example` lists variable names only · the test database is separate from production.

### While developing
- Work task by task, to the path each task names. Skills: `ponytail`, `tdd`.
- One commit per task, message starting with the task ID (CLAUDE.md section 6).
- `/simplify` after each batch of tasks. `/code-review` before handing to QA.
- **QA's cases belong to QA.** Dev makes the code pass them. When Dev believes a case in `QA/test_plan.md` or a QA-written test is wrong, report it to the human with the reason; the human decides whether the case or the code changes.
- Secrets and real data: [`process/security.md`](../security.md).

## Output
Code in `Dev/`

## Done when
Every task in the round is finished · the whole test suite passes · `/code-review` has nothing open · the CI run on the latest commit passed.

## Human approves
The stage report: tasks done, the CI run link, and the review result.

## Next
Stage 6 round 2 — QA tests function, starting with the core cases.
