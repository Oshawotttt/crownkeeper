---
name: loopeng-stack
description: Execute an approved spec's Branch plan on a linear stack of local branches, with no push or PR.
argument-hint: <path to an approved spec file with a Branch plan from /crownkeeper:loopeng-group>
disable-model-invocation: true
---

# Loop engineering: stacked branches per spec

Spec file: $ARGUMENTS

This skill owns the git hygiene. Read these files, relative to this skill's
base directory, and follow them when a step names them:

- `../../references/loopeng-run.md`
- `../loopeng-loop/SKILL.md`
- `../loopeng-sweep/SKILL.md`

## 1. Prepare

1. Follow **Load the spec** and **Check the repo**.
2. If the spec has no **Branch plan**, stop and tell the user to run
   `/crownkeeper:loopeng-group <spec file>`.
3. Check the current branch:
   - The first group's branch doesn't exist: the current branch must be the
     plan's starting branch.
   - The first group's branch exists: this is a resume, and the current branch
     must be one of the plan's branches.
   - Otherwise, stop and ask.

## 2. Execute each group, in order

Skip a group when the next group's branch exists, because that branch is created
only after this group's sweep finishes. For every other group:

1. Create the group's branch from the previous group's branch, or from the
   starting branch for the first group. Switch to the branch if it exists.
2. On the first group, follow **Commit the spec**.
3. Set the run context. Scope is the group's subtasks. The base commit is the
   commit that added the spec for the first group, or the previous group's
   branch tip (`git rev-parse <branch>`) for later groups.
4. Run the loop skill, then the sweep skill, with the spec path, scope and base
   commit. Skip their direct-invocation steps.
5. Continue to the next group without pausing.

If a loop or sweep stops, the stack stops with it.

## 3. Finish

Report each group's branch and subtasks, in stack order, then each group's sweep
report. Remind the user that nothing was pushed.
