# Changing a system that is already live — CLAUDE.md section 3.2

A system past stage 8 does not walk stages 1–8 again. Per change:

1. Name the requirement and SA sections affected, and fix only those parts of the source documents (CLAUDE.md section 4.1). Decisions that are expensive to change later are grilled first ([`grilling.md`](grilling.md)).
2. Break down tasks → Dev → QA tests the changed part plus the whole regression suite → report.
3. A bug affecting real users: fix it with a regression test first, then fix the documents in the same round.
4. **At the start of every round, look at production errors since the last round.** The human opens the place recorded in `deploy/README.md` and passes on what is there, with personal data removed ([`security.md`](security.md)). Every incident that affected users goes into the incident table in `PM_STATE.md`: date · symptom · cause · the stage that should have caught it.

The human approves the change before Dev starts, and approves the result before it is merged to production (CLAUDE.md section 4). Each round ends with the hand-off block.
