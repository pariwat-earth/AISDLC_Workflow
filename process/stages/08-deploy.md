# Stage 8 — Deploy

## Who
PM prepares and verifies. The human performs every production action ([`process/security.md`](../security.md) section 3).

## How
1. PM writes `deploy/README.md` from [`templates/deploy.md`](../../templates/deploy.md): environments, step-by-step release, smoke test list, how to roll back, how to restore data. Skill `release-readiness`.
2. Deploy to staging and run the smoke test before production.
3. The human releases to production: runs production migrations, sets production secrets, merges the pull request into the production branch.
4. PM runs the smoke test against production and reports what it could and could not check.
5. **Drills** (full level): restore data from a backup into a test database once, and roll back to the previous version once. Do them for real; write the date and the result in `deploy/README.md`.
6. Confirm there is a place to see production errors, and write where it is in `deploy/README.md`.

## Output
`deploy/README.md`, the live system

## Done when
The smoke test passes on production · the restore drill and the rollback drill have each been done once, with date and result recorded (full level) · the place to see production errors is recorded.

## Human approves
That the system is live and the drills are accepted.

## Next
Stage 9 — retrospective. Later changes follow [`process/change.md`](../change.md).
