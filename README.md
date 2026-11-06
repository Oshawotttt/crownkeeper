# Loop engineering workflow

## Install

Install this plugin:

```
/plugin marketplace add Oshawotttt/crownkeeper
/plugin install crownkeeper@crownkeeper
```

Install the plugins it depends on. These are not included:

```
/plugin marketplace add mattpocock/skills
/plugin install mattpocock-skills@mattpocock
/plugin marketplace add cathrynlavery/diagram-design
/plugin install diagram-design@diagram-design
```

- `mattpocock-skills`: required. `/crownkeeper:loopeng-auto` calls its `tdd` and `code-review` skills.
- `diagram-design`: needed only for `/crownkeeper:generate-summary`.

## Workflow

1. `/crownkeeper:generate-map`: add a docs map to the repo's `CLAUDE.md`.
2. `/crownkeeper:loopeng-plan <task>`: write and approve a spec in `docs/specs/`.
3. `/crownkeeper:loopeng-auto <spec file>`: build, verify and commit each subtask, review the task, then update the docs.
4. `/crownkeeper:generate-summary`: build or update `docs/summary.html`, a visual summary for people.

## Contents

| Item | Role |
|---|---|
| `plugins/crownkeeper/skills/loopeng-plan` | Discovery and approved spec |
| `plugins/crownkeeper/skills/loopeng-auto` | Execution loop with auto-commit |
| `plugins/crownkeeper/skills/commit-message` | Commit message style, called by `/crownkeeper:loopeng-auto` |
| `plugins/crownkeeper/skills/generate-map` | Docs map in `CLAUDE.md` |
| `plugins/crownkeeper/skills/generate-summary` | Visual summary from the docs |
| `plugins/crownkeeper/agents/objectiveness-verifier.md` | Checks each verification prompt is objective |
| `plugins/crownkeeper/agents/main-verifier.md` | Verifies one subtask or code-review fix round |
| `plugins/crownkeeper/agents/docs-updater.md` | Updates docs from the spec and the diff |
