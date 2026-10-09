# Pipeline levels

**Full** is the default. Use **light** when `PROJECT.md` says so or the human orders it for a small job. The light level exists because a job of a few hours cannot pay for the full document set.

| | Light | Full |
|---|---|---|
| BA | `BA/requirement.md` only, with the open questions and their answers in it | `BA/BA_analysis.md` with acceptance criteria |
| SA | A list of pages and the parts of each, appended to `requirement.md` | `SA/SA_design.md` + `SA/tasks.md` |
| UI mockup | Skipped — the first page is shown to the human as a real page | Stage 4 in full |
| QA | A checklist in `QA/test_plan.md`: the screen sizes in use · every link and button · every form reaches its destination · https | Three rounds |
| Core cases approved by the human before Dev | Yes | Yes |
| CI on every push | Checks that need no database: lint, type check, build, dependency audit, secret scan | The whole suite |
| One commit per task | Yes | Yes |
| Secrets and real-data rules | Yes | Yes |
| Human risk review · restore and rollback drills · production error review | No | Yes |

At every level: grilling ([`grilling.md`](grilling.md)), reporting, stopping for the human's approval at the end of each stage, and the approval record (CLAUDE.md section 4).

A project may tighten its level in `PROJECT.md` (for example a light job that takes payments adds the human risk review).
