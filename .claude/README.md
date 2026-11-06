# Loop engineering workflow

## Install

Copy `skills/` and `agents/` into `~/.claude/`, then restart Claude Code.

Install the plugins. These are not in this zip:

```
/plugin marketplace add mattpocock/skills
/plugin install mattpocock-skills@mattpocock
/plugin marketplace add cathrynlavery/diagram-design
/plugin install diagram-design@diagram-design
```

- `mattpocock-skills`: required. `/loopeng-auto` calls its `tdd` and `code-review` skills.
- `diagram-design`: needed only for `/generate-summary`.

## Workflow

1. `/generate-map`: add a docs map to the repo's `CLAUDE.md`.
2. `/loopeng-plan <task>`: write and approve a spec in `docs/specs/`.
3. `/loopeng-auto <spec file>`: build, verify and commit each subtask, review the task, then update the docs.
4. `/generate-summary`: build or update `docs/summary.html`, a visual summary for people.

## Contents

| Item | Role |
|---|---|
| `skills/loopeng-plan` | Discovery and approved spec |
| `skills/loopeng-auto` | Execution loop with auto-commit |
| `skills/commit-message` | Commit message style, called by `/loopeng-auto` |
| `skills/generate-map` | Docs map in `CLAUDE.md` |
| `skills/generate-summary` | Visual summary from the docs |
| `agents/objectiveness-verifier.md` | Checks each verification prompt is objective |
| `agents/main-verifier.md` | Verifies one subtask or code-review fix round |
| `agents/docs-updater.md` | Updates docs from the spec and the diff |
