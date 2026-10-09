# Quality beyond function (NFR baseline)

Version: **1.2** · 2026-10-09 · Status: active

Every system built with this framework passes this list. QA does it in **round 3 of stage 6**, after the core functions pass.

**How to use**: copy the table in section 1 into the project's `QA/test_plan.md` and fill in the result on every row. Done when no row is empty.

- `pass` — tested under **normal working conditions** and true: the devices, internet, data volume, and number of users of the real site, not extreme conditions.
- `fail` — open an issue. If a fix still cannot meet the bar, state **what blocks it** (a limit of the tech stack, an outside service, budget, or time) and report to the human. The human accepts the reason → record an accepted risk (CLAUDE.md section 4.2). The human does not accept → the issue stays open.
- `not applicable` — the system has nothing for the row to test, per the "Skip when" column. Write a one-line reason and do not test.

Security rows (N1–N4) are tested the way someone trying to break in would. "Normal" for these rows means a real attempt.

## 1. Tested on every project

| # | Area | Must be true | How to check | Skip when |
|---|---|---|---|---|
| N1 | Security | Each role reaches only its own pages and data | Sign in as one role, then call another role's or another tenant's URLs and APIs directly. They must be refused | No sign-in and no per-person data |
| N2 | Security | The server validates every input | Send wrong types, negative values, over-long text, and script to the APIs directly, bypassing the screen | No API and no form — the front end only displays |
| N3 | Security | No secret in the repo or in client-side code · https on every page | CI secret scan passes · search the repo and the built files · opening with http must redirect to https | – |
| N4 | Security | Code and libraries have no high-severity vulnerability | `/security-review` has nothing open · the stack's dependency audit (for example `npm audit`) shows no high or critical | – |
| N5 | Data | Personal data is stored only as far as it is used, and seen only by those who must | Compare the personal-data columns in the DB with the requirement · confirm none appears in logs or URLs | No personal data stored |
| N6 | Data | Data can really be restored from a backup | Back up, then restore into a test database once. The data is complete | No database |
| N7 | Data | A failure midway neither loses nor duplicates data | Press save twice · cut the internet during a save · refresh mid-form | Nothing is saved |
| N8 | Usability | Each role finishes its main job with nobody teaching | Walk the main jobs from `BA_analysis.md` role by role, counting the points where the user must guess | – |
| N9 | Usability | Error messages use the user's language and say what to do next | Trigger every kind of error in the main jobs and read the message | No form or transaction |
| N10 | Usability | Works on the devices and screen sizes of the real site | Test on the devices named in grilling · none named → phone, tablet, computer | – |
| N11 | Usability | People with poor eyesight and keyboard-only users can use it | Skill `accessibility-testing`, axe-core + keyboard parts: no level A/AA item open in the main jobs | – |
| N12 | Speed | Main pages open within 3 seconds with real-volume data | Load data at the volume named in grilling, then time it on site-level internet | – |
| N13 | Operations | Failures are noticed, and the release can be rolled back | There is a place to see production errors · the rollback steps in `deploy/README.md` have been carried out once for real (stage 8) | – |

Rows with – under "Skip when" are tested on every project. Numeric bars (N12) are defaults; a project's requirement may set another value.

## 2. Extra items (added when the requirement or the use calls for them)

Chosen during grilling ("quality beyond function") and written into the requirement.

| When the system has | Also test |
|---|---|
| Payments or accounting figures | Totals match to every decimal · later edits leave a trail |
| Many simultaneous users, or several branches | Load test at the agreed maximum number of users |
| Several people editing the same data | Two people edit at once; neither result silently overwrites the other |
| Use while the internet is down | Work continues, and the data arrives complete when back online |
| Legal requirements specific to the business | Documents and reports match the form the law prescribes |
| Connections to outside systems | The outside system fails and the rest of ours still works |
