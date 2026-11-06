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

- `mattpocock-skills`: required. The loopeng execution skills call its `tdd` and `code-review` skills.
- `diagram-design`: needed only for `/crownkeeper:generate-summary`.

## Workflow

1. `/crownkeeper:generate-map`: add a docs map to the repo's `CLAUDE.md`.
2. `/crownkeeper:loopeng-plan <task>`: write and approve a spec in `docs/specs/`.
3. Run the spec with the git hygiene you want. Both build, verify and commit each subtask, review the work, then update the docs:
   - `/crownkeeper:loopeng-branch <spec file>`: one branch per spec, no push.
   - `/crownkeeper:loopeng-group <spec file>`, then `/crownkeeper:loopeng-stack <spec file>`: a linear stack of local branches, no push. The first skill suggests a grouping, and you approve it.
4. `/crownkeeper:generate-summary`: build or update `docs/summary.html`, a visual summary for people.

To step through a run by hand on a feature branch, use the parts directly:

- `/crownkeeper:loopeng-loop <spec file> [subtask ID]`: every remaining subtask, or only the one named.
- `/crownkeeper:loopeng-sweep <spec file>`: the code review, docs update and report.

Only a person or a loopeng branch skill runs these. They set `disable-model-invocation`, so Claude can't fire them on its own, and the branch skills read their files directly.

## Contents

| Item | Role |
|---|---|
| `plugins/crownkeeper/skills/loopeng-plan` | Discovery and approved spec |
| `plugins/crownkeeper/skills/loopeng-branch` | Git hygiene: one branch per spec |
| `plugins/crownkeeper/skills/loopeng-group` | Spec phase: suggests a grouping and writes the approved Branch plan |
| `plugins/crownkeeper/skills/loopeng-stack` | Git hygiene: linear stack of branches from the Branch plan |
| `plugins/crownkeeper/skills/loopeng-loop` | Main execution loop: build, verify and commit each subtask, or one named subtask |
| `plugins/crownkeeper/skills/loopeng-sweep` | Final code review, docs update and report |
| `plugins/crownkeeper/references/loopeng-run.md` | Run terms and checks shared by the execution skills |
| `plugins/crownkeeper/skills/commit-message` | Commit message style, called by the execution skills |
| `plugins/crownkeeper/skills/generate-map` | Docs map in `CLAUDE.md` |
| `plugins/crownkeeper/skills/generate-summary` | Visual summary from the docs |
| `plugins/crownkeeper/agents/objectiveness-verifier.md` | Checks each verification prompt is objective |
| `plugins/crownkeeper/agents/main-verifier.md` | Verifies one subtask or code-review fix round |
| `plugins/crownkeeper/agents/docs-updater.md` | Updates docs from the spec and the diff |
