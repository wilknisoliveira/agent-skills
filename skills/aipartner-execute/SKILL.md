---
name: "aipartner-execute"
description: "Implement the feature by working through the task list produced by /aipartner-spec."
argument-hint: "Optional: which feature, or a specific phase or task to run"
user-invocable: true
disable-model-invocation: true
---

## User Input

```text
$ARGUMENTS
```

Empty means "implement the current feature, all phases". Otherwise it names a feature, a
phase, or a subset of tasks.

## Hard rules

- **Never run a git write command.** No `commit`, `push`, `pull`, `checkout`, `branch`. The
  user decides when and how their work gets committed.
- **Stay inside the spec.** The **Out of Scope** section of `spec.md` is binding. If you find
  something worth doing that is not in the tasks, finish the tasks first and raise it at the
  end — do not quietly widen the scope.
- **Follow the project standards.** `.aipartner/memory/project-standards.md` describes how
  this codebase is written. Match it. Code that works but does not look like the surrounding
  code is not done.

## Steps

### 1. Load context

1. `.aipartner/memory/` — every file
2. Everything under its **Required reading** list
3. `specs/NNN-slug/agent-artifacts/spec.md` — what is being built and why
4. `specs/NNN-slug/agent-artifacts/tasks.md` — the task list

Resolve the feature from `$ARGUMENTS`, or from the most recently modified folder in `specs/`.
When it is ambiguous, ask which one — do not guess.

If `tasks.md` is missing, stop and point at `/aipartner-spec`.

### 2. Check the Standards Check gate

`tasks.md` opens with a Standards Check. Read it. If it lists deviations, mention them in one
line before starting — the user should not discover a deviation after the fact.

### 3. Execute

Work phase by phase, in order. Do not start a phase before the previous one is done.

- **Foundational blocks everything.** No user story work begins until that phase is complete.
- **`[P]` tasks** in the same phase can be done together. Tasks touching the same file cannot,
  regardless of marking.
- **Within a story**: models → services → interface/endpoints → integration.
- **Inline dependencies** (`depends on T00X`) are binding.
- Where tests exist for the task and the standards call for test-first, write the test first
  and see it fail before implementing.

**Mark each finished task `[X]` in `tasks.md` as you complete it**, not in a batch at the end.
If the session dies, the file is the record of where things stopped.

At each **Checkpoint** in the task list, verify the story actually works before moving on.

### 4. Handle failures

| Situation | What to do |
|---|---|
| A sequential task fails | Stop. Report what failed, with the actual error. Do not carry on past a broken foundation. |
| A `[P]` task fails | Finish the other parallel tasks, then report the failure. |
| A task is wrong or impossible as written | Stop and say why. Do not silently reinterpret it. |
| Something outside the spec needs changing to proceed | Ask first. |

Report failures with the real output. Never describe a failing step as done.

### 5. Validate

Run the quality gates from `.aipartner/memory/project-standards.md` — lint, types, tests,
whatever the project actually uses — plus the checks in the **Validation** section of
`tasks.md`.

Report what passed and what did not, with output. If you skipped a gate, say which and why.

### 6. Report

Close with:

| Section | Content |
|---|---|
| Done | what was implemented, by story |
| Not done | anything skipped or blocked, and why |
| Gates | each gate and its result |
| Verify | how the user can see it working |
| Next | `/aipartner-fix` if something is off |

Be accurate. If tests failed, say so with the output. If a task was skipped, say which one.
