# Changelog

## 3.0 — 2026-10-09

First release as a framework.

- Human approval: the AI stops at the end of each stage 1–8 and waits for explicit approval. Every report ends with the hand-off block (next · how · who · needs approval). Approvals are recorded in `APPROVALS.md`.
- Structure: a short `CLAUDE.md` core, one file per stage in `process/stages/`, blank forms in `templates/`, project specifics in `PROJECT.md`.
- Human roles (Decider · Risk reviewer · Client) and the list of actions the AI never does alone.
- Evidence: CI run links close stages 5 and 6 · core cases approved by the human before development · human risk review · restore and rollback drills · production error review · one commit per task.
- Grilling gains a seventh kind: law and regulation of the business.
- Requirement revisions are counted by cause.
- Marketing moved out of the core into `extensions/`.
- Framework files are in English; the human is addressed in their own language.
