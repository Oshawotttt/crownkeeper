---
name: loopeng-group
description: Suggest how to split an approved spec into stacked branches and, once the user approves, write the Branch plan into the spec.
argument-hint: <path to an approved spec file from /crownkeeper:loopeng-plan>
disable-model-invocation: true
---

# Loop engineering: group subtasks into branches

Spec file: $ARGUMENTS

This skill only edits the spec file. It makes no commits and creates no
branches. `/crownkeeper:loopeng-stack <spec file>` executes the plan it writes.

Follow **Load the spec** in `../../references/loopeng-run.md`, relative to this
skill's base directory.

## 1. Suggest

The branches form a linear stack: the first starts from the starting branch, and
each later one starts from the branch before it. The starting branch is the
current branch, unless the user names another.

Suggest groups, and show the starting branch and each group's name, subtask IDs
and branch. Every group must:

- hold subtasks that are contiguous in the spec's run order
- have every blocker in its own group or an earlier one
- pass the full test suite at its branch tip
- be a change a reviewer can judge in one sitting

A prefactor gets its own group.

## 2. Approve

Wait for explicit approval. Questions and change requests are not approval:
revise the grouping and show it again.

## 3. Write the plan

On approval, add this section to the spec, after **Suggested splits**:

```
## Branch plan

Starting branch: `<branch>`

| Group | Subtasks | Branch |
|---|---|---|
| <name> | <IDs> | `<branch>` |
```

Then stop and give the user the command to run:
`/crownkeeper:loopeng-stack <spec file path>`.
