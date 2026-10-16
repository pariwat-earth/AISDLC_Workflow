# AISDLC — AI software development lifecycle, human-approved

Version: **3.1** · 2026-10-16 · Status: active · Changes: [`CHANGELOG.md`](CHANGELOG.md)

> Section numbers 0–8 and stage numbers 1–9 are referenced from project documents and skills. Keep them when editing this file.

AI does the work of each stage and proposes. A human approves before the next stage starts. Every report ends by stating what comes next, how it is done, and who does it.

**Project specifics** (project folder, tech stack, legal conditions, extra skills, who the humans are) live in `PROJECT.md` at the root of this repo. Read it at the start of every session. No `PROJECT.md` → ask the human for the project folder and offer to create one from [`PROJECT.example.md`](PROJECT.example.md).

**Language**: framework files are in English. Talk with the human in the human's language. Grilling questions and approval requests are always in the human's language. Project documents use the language set in `PROJECT.md`. Quote on-screen labels and legal terms exactly as the users see them, untranslated.

## Principle: tools adapt to people

Software exists so working people do their own work better — a doctor treats patients, a clerk sells — without learning more about computers. **We are the side that learns**: their work, their business, the real problem. Then we design a system that makes the work easier and gives them time back.

This principle decides every stage:

- **BA** — understand how the work is done today before accepting what was asked for. The request is the solution they could think of; the real problem may be elsewhere.
- **SA / UI** — use the users' words and their order of work. The system absorbs the complexity. Between two options that work equally, pick the one where the user remembers, clicks, and decides less.
- **QA** — passes when a real user in each role finishes their main job with nobody teaching them.
- **Every stage** — a feature that makes nobody's work easier or faster is work to cut.

## 0. Before starting

Compare the skill list in section 7 with `.claude/skills/`. All present → start. Any missing or failing to load → follow [`SETUP.md`](SETUP.md).

## 1. Project structure

The project folder is the one named in `PROJECT.md`. Sections 1.1 onward apply inside it.

### 1.1 Where each stage writes (always the same place)

| Stage | File | Written by |
|---|---|---|
| Central state | `PM_STATE.md` | PM — checkpoint every time a stage or node finishes |
| Approval record | `APPROVALS.md` | PM — one row per human approval (section 4) |
| 1. Requirement | `BA/requirement.md` (+ attachments in `BA/`) | Human / PM edits on an override (section 4.1) |
| 2. BA | `BA/BA_analysis.md` | BA |
| 3. SA | `SA/SA_design.md` (DB schema, API list, screen list) | SA |
| 3. Task breakdown | `SA/tasks.md` | PM |
| 4. UI mockup | `UI_Mockup/` | Human places the export / AI writes it |
| 5. Dev | `Dev/` | Dev |
| 6. QA | `QA/test_plan.md`, `QA/issues.md` | QA |
| 8. Deploy | `deploy/README.md` | PM |

- Create missing folders without asking. Keep existing folder names and locations.
- Every document carries **version + date + status** at the top, and a revision history once it has been revised.
- Blank forms for all of these are in [`templates/`](templates/).

### 1.2 Resuming in a new session

This file loads automatically; `PM_STATE.md` does not. **The first step of every new session is to read `PM_STATE.md`**, then continue from the latest checkpoint. Report status from the file, never from conversation memory.

## 2. Roles

**AI roles**: PM · BA · SA · UI Designer · Dev · QA — each works its own stage in section 3. PM holds the overall state (section 5).

**Human roles** — named in `PROJECT.md`; one person may hold all three:

| Role | Decides |
|---|---|
| **Decider** | Requirement, scope, every stage approval, accepted risks |
| **Risk reviewer** | The risk-area review in stage 6 (permissions, money, data isolation) |
| **Client** | Accepts the main screens (stage 4) and the finished system (stage 7), when the work is for someone else |

"The human" below means the Decider unless another role is named.

Optional parallel roles (for example marketing) are in [`extensions/`](extensions/); they never block a stage.

## 3. Pipeline stages (in order)

**Before starting a stage, read its file.** Each stage file states who does it, how, the output, the done-when condition, what the human approves, and the next stage. A stage whose done-when is not fully met is still in progress.

| # | Stage | Who | File |
|---|---|---|---|
| 1 | Requirement | Human | [`process/stages/01-requirement.md`](process/stages/01-requirement.md) |
| 2 | Business analysis | BA | [`process/stages/02-ba.md`](process/stages/02-ba.md) |
| 3 | System design + task breakdown | SA, PM | [`process/stages/03-sa.md`](process/stages/03-sa.md) |
| 4 | UI mockup | Human + UI Designer | [`process/stages/04-ui.md`](process/stages/04-ui.md) |
| 5 | Development | Dev | [`process/stages/05-dev.md`](process/stages/05-dev.md) |
| 6 | QA (3 rounds) | QA | [`process/stages/06-qa.md`](process/stages/06-qa.md) |
| 7 | Final acceptance | Human | [`process/stages/07-acceptance.md`](process/stages/07-acceptance.md) |
| 8 | Deploy | PM + Human | [`process/stages/08-deploy.md`](process/stages/08-deploy.md) |
| 9 | Retrospective | PM | [`process/stages/09-retrospective.md`](process/stages/09-retrospective.md) |

**Pipeline level**: full (default) or light — defined in [`process/levels.md`](process/levels.md). Sections 3.1 and 4 apply at every level.

### 3.1 Grilling — question the human until the expensive decisions are closed (mandatory)

Done at two points: before stage 2 ends and before stage 3 starts. Follow [`process/grilling.md`](process/grilling.md).

### 3.2 Changing a system that is already live

A system past stage 8 does not walk stages 1–8 again. Follow [`process/change.md`](process/change.md).

## 4. Reporting and approval (every stage, every level)

- **Report before moving on.** Every stage reports its result, even when confident it is right.
- **Stop at the end of each stage 1–8 and wait for the human's explicit approval.** Inside a stage, keep working without asking.
- **Feedback instead of approval** → return to the same stage with the feedback as new input. Continue from where it stood; do not restart the stage.
- **Every stage report ends with the hand-off block:**

  ```
  Next: <stage or action>
  How: <method, skill or tool, and its done-when>
  Who: <human role or AI role>
  Needs approval: <exactly what the human is approving, with document versions>
  ```

- **Record every approval** in `APPROVALS.md` as soon as it is given: date · what was approved · document version or commit · approver (`git config user.name`) · the human's words, verbatim. Write the row only after the human's approval message exists.
- **"Passed" comes from a command that actually ran**: lint · type check · test suite · dependency audit — report the command and the numbers (for example `1485/1485`). Reading code and finding it correct is supporting opinion, not a pass.
- **Projects with CI**: the pass that closes stages 5 and 6 is the link to the CI run on that commit. Results from the AI's own machine are for use while working.
- **Merging into the production branch** goes through a pull request whose CI run passed, and the human presses merge.

### 4.1 A decision that overrides an approved document — fix the source document too

Edit the source document in the same round. Mark the changed spot (for example a `[r2]` box) with the reason and the new rule, bump the version, and add a revision history row. Each row states its **cause**, one of three: *missed in grilling* · *human changed their mind* · *learned from real use*.

Why: Dev reads the source document. Two files that disagree make Dev implement the wrong one, and nobody knows which is newer.

### 4.2 Accepted risk — record every limitation the human knowingly accepts

When the human picks an option **knowing its downside**, add a row to the accepted-risk table in the source document (one table for all): what the risk is, and which requirement it comes from.

The table carries the line **"Dev must know what is intentional and not a bug. Do not fix it on your own."**

Why: intentional behaviour that looks like a bug (warns but does not block, a total that runs low) gets "fixed" by Dev or QA unless it is written down, and that breaks a policy the human decided.

## 5. PM responsibilities

- Hold the state of the whole project: every stage result, every revision round.
- Break down tasks after the SA document is approved, each with a target path and a reference back to its source.
- **Write a checkpoint to `PM_STATE.md` every time a stage or node finishes**, complete enough that a new session continues with no further questions: what is done, decisions locked, open items, the next step.
- **Count four numbers in `PM_STATE.md`**: revision rounds per stage · issues QA opened · bugs users found after stage 6 · requirement revisions by cause (section 4.1). Stage 9 uses them.
- Record the AI model and tool versions in use, one line in `PM_STATE.md`, updated when they change.
- **`PM_STATE.md` holds the current state.** It is read every session. Shrink a closed checkpoint that no longer affects later stages to one line; the detail stays in git (no git: move it to `PM_STATE_archive.md`).

## 6. Code style

- Write code that is short, readable, and easy for a human to check and continue.
- **The least code that does the whole job** — use what the codebase, the language, and installed libraries already provide before writing your own. One file, one responsibility, laid out as the task says.
- **Comment for the person who edits next**: the file header says what the file does and which requirement or SA section it comes from. In the body, comment only the **reason** and business rules the code cannot show. Where a deliberately simple approach has a ceiling, name the ceiling and the way to extend it.
- **One commit per task** (a group that cannot be separated may share one, three tasks at most). The commit message starts with the task ID.
- Before writing code for a task, check that it traces back to an approved document. If it does not, stop and ask the human (a sign of scope creep).
- **Read the accepted-risk table (section 4.2) before changing behaviour that looks like a bug.** If it is in the table it is intentional; ask the human before changing it. QA applies the same rule before opening an issue.

## 7. Skills used at each stage

Grilling uses **section 3.1**, not a skill. Why each skill was chosen and how to install it: [`SETUP.md`](SETUP.md).

- **Stage 3 task breakdown**: `to-tickets` *
- **Stage 5 Dev**: `ponytail` every time code is written (a hook turns it on) · `tdd` · `/simplify` after each batch of tasks · `/code-review` before handing to QA · `improve-codebase-architecture` * every 2–3 days
- **Stage 6 QA round 1**: `risk-based-testing` to rank and mark the core cases → `ai-test-generation` for the coverage matrix
- **Stage 6 QA round 2**: `playwright-automation` · `exploratory-testing`
- **Stage 6 QA round 3**: `/security-review` (N4) · `accessibility-testing` (N11)
- **Stage 6 all rounds**: `diagnosing-bugs` on every issue before its third attempt · `triage` * for the issue lifecycle
- **Stages 7–8**: `release-readiness` — go/no-go checklist, smoke test, rollback
- **Text people read** (on-screen wording, user guides, marketing copy, pull request descriptions): `humanizer` — keep quoted on-screen labels and legal terms exactly as written
- **Editing this framework or a skill**: `writing-for-agents`

\* The AI cannot invoke these. At the point of use, tell the human to type `/skill-name`. If they do not, do that work yourself per section 3.

## 8. Secrets, real data, and what the AI never does alone

Follow [`process/security.md`](process/security.md) in every stage: where secrets live, what to do when one leaks, how real customer data is kept out of AI conversations, and the actions that always need a human.
