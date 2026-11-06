---
name: loopeng-branch
description: Execute an approved spec on one feature branch, with no push or PR.
argument-hint: <path to an approved spec file from /crownkeeper:loopeng-plan>
disable-model-invocation: true
---

# Loop engineering: one branch per spec

Spec file: $ARGUMENTS

This skill owns the git hygiene. Read these files, relative to this skill's
base directory, and follow them when a step names them:

- `../../references/loopeng-run.md`
- `../loopeng-loop/SKILL.md`
- `../loopeng-sweep/SKILL.md`

## 1. Prepare

1. Follow **Load the spec** and **Check the repo**.
2. Choose the branch:
   - The spec names a branch that exists: switch to it.
   - The spec names a new branch: create it and switch to it.
   - The spec names no branch and the current branch is the default branch:
     stop and ask for a branch name.
   - Otherwise stay on the current branch.
3. Follow **Commit the spec**.

The base commit is the commit that added the spec. Scope is every subtask.

## 2. Execute

Run the loop skill, then the sweep skill, with the spec path, scope and base
commit. Skip their direct-invocation steps.

## 3. Finish

End the sweep's report with the branch name and a reminder that nothing was
pushed.
