# Installing the pipeline skills

Version: **1.3** · 2026-10-16 · Status: active

Read this file when a skill listed in CLAUDE.md section 7 is missing from `.claude/skills/` or fails to load. Installed skills are listed in `skills-lock.json`.

Every install command asks the human for permission before it runs; wait for confirmation step by step. If the human declines one, say that the pipeline continues without that skill's ability, and carry on.

## 1. Steps

1. `node -v` — no Node.js → tell the human the ponytail hooks will not run. The other skills still install.
2. mattpocock/skills — install only the missing ones:
   ```
   npx skills@latest add mattpocock/skills/skills/engineering/tdd
   npx skills@latest add mattpocock/skills/skills/engineering/diagnosing-bugs
   npx skills@latest add mattpocock/skills/skills/engineering/to-tickets
   npx skills@latest add mattpocock/skills/skills/engineering/triage
   npx skills@latest add mattpocock/skills/skills/productivity/writing-for-agents
   npx skills@latest add mattpocock/skills/skills/engineering/improve-codebase-architecture
   ```
   Then run `/setup-matt-pocock-skills` once per repo (if not done before).
3. ponytail — done when `ponytail` is in `.claude/skills/` and `~/.claude/ponytail/hooks/` exists. `/plugin` is not available in the Claude Code CLI or extension, so run:
   ```
   npx skills@latest add DietrichGebert/ponytail/skills/ponytail
   git clone --depth 1 https://github.com/DietrichGebert/ponytail.git /tmp/pt && mkdir -p ~/.claude/ponytail && cp -R /tmp/pt/hooks ~/.claude/ponytail/
   ```
   Then **the human** points the three hooks (`SessionStart`, `SubagentStart`, `UserPromptSubmit`) in `.claude/settings.json` at `~/.claude/ponytail/hooks/ponytail-{activate,subagent,mode-tracker}.js` on their own machine — the paths in the committed file are absolute and belong to the machine that wrote them. An example is in `/tmp/pt/hooks/claude-codex-hooks.json` (replace `${CLAUDE_PLUGIN_ROOT}` with the full path). Restart the session afterwards.
   > Claude cannot write hooks into settings.json itself (the self-modification guard blocks it). The human does this step.
4. qa-skills — install only the missing ones:
   ```
   npx skills@latest add petrkindlmann/qa-skills/skills/exploratory-testing
   npx skills@latest add petrkindlmann/qa-skills/skills/risk-based-testing
   npx skills@latest add petrkindlmann/qa-skills/skills/playwright-automation
   npx skills@latest add petrkindlmann/qa-skills/skills/ai-test-generation
   npx skills@latest add petrkindlmann/qa-skills/skills/accessibility-testing
   npx skills@latest add petrkindlmann/qa-skills/skills/release-readiness
   ```
5. humanizer — if missing:
   ```
   npx skills@latest add blader/humanizer
   ```
6. Report briefly which were newly installed and which were already present.

## 2. When a skill fails to load

Read its SKILL.md first. If it is a stub pointing at another skill, check that the target exists — if not, tell the human the upstream is broken and do that work yourself. Reinstall at most once.

- **`grill-me` is not installed** — its upstream SKILL.md is a 157-byte stub that calls a skill named `grilling`, which does not exist in that repo (checked 2026-09-22). Grilling uses CLAUDE.md section 3.1.
- **`to-tickets`, `triage`, `improve-codebase-architecture`** set `disable-model-invocation: true` — Claude cannot invoke them; the human types `/skill-name`.
- **ponytail** — the SKILL.md alone is not picked up by the model (tested: 0 self-activations in 10 sessions). The three hooks make it automatic, and they need Node.js in PATH.

## 3. Why each skill was chosen

| Skill | Source | What it gives |
|---|---|---|
| `tdd` | mattpocock/skills | Red-green-refactor; fewer bugs reach QA |
| `diagnosing-bugs` | mattpocock/skills | A disciplined debug loop: reproduce → minimise → hypothesise → instrument → fix → regression-test |
| `to-tickets` | mattpocock/skills | Breaks the SA document into vertical slices |
| `triage` | mattpocock/skills | Lifecycle of the issues QA opens |
| `writing-for-agents` | mattpocock/skills | Quality of CLAUDE.md, process files, and skills |
| `improve-codebase-architecture` | mattpocock/skills | Keeps the code clean over time |
| `ponytail` | [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) | The shortest solution that works (YAGNI; standard library and native features before custom code) |
| `exploratory-testing` | petrkindlmann/qa-skills | Session-based testing and heuristics for unexpected input |
| `risk-based-testing` | petrkindlmann/qa-skills | A risk matrix (likelihood × impact) to order what is tested first |
| `playwright-automation` | petrkindlmann/qa-skills | Automated tests of the real UI, including negative input |
| `ai-test-generation` | petrkindlmann/qa-skills | Coverage matrix and assertions; fewer missed edge cases |
| `accessibility-testing` | petrkindlmann/qa-skills | axe-core and keyboard checks (NFR N11) |
| `release-readiness` | petrkindlmann/qa-skills | Go/no-go checklist, smoke test, rollback — staged rollout and canary only when the system is large enough to need them |
| `humanizer` | [blader/humanizer](https://github.com/blader/humanizer) | Removes AI-sounding patterns from text people read (staged contrasts, filler closers, inflated words), keeping the meaning |
| `/code-review`, `/simplify`, `/security-review` | Built into Claude Code | Nothing to install — bugs in the diff · less duplicated code · security of the changed code |

qa-skills has 50 skills; install only the ones used: `npx skills@latest add petrkindlmann/qa-skills/skills/<name>`

**Looked at and not used**
- `bug-reproduction` — overlaps with `diagnosing-bugs`, which covers more.
- `chaos-engineering` — infrastructure-level resilience testing, beyond the scope here. Reconsider when a system reaches that scale.
