# Stage 1 — Requirement

## Who
The human (Decider). PM prepares the project files.

## How
1. The human analyses and groups the requirement before it enters the flow, and names the tech stack in it.
2. PM checks `PROJECT.md` is filled in (project folder, humans and their roles, language, legal conditions the human already knows).
3. PM creates `PM_STATE.md` and `APPROVALS.md` in the project folder from [`templates/`](../../templates/).

The AI does not write the requirement for the human. It may ask what is missing so the file can be completed.

## Output
`BA/requirement.md` (+ attachments in `BA/`), `PM_STATE.md`, `APPROVALS.md`

## Done when
`BA/requirement.md` exists and names the tech stack.

## Human approves
That this requirement is the one to analyse.

## Next
Stage 2 — BA reads the whole requirement and starts grilling ([`process/grilling.md`](../grilling.md)).
