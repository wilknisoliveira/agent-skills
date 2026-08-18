---
name: "aipartner-fix"
description: "Correct something after implementation — a bug, or a decision you disagree with — and log the change."
argument-hint: "What is wrong or what you want changed"
user-invocable: true
disable-model-invocation: true
---

## User Input

```text
$ARGUMENTS
```

This is the complaint. Take it at face value — the user is looking at the result and you are
not.

## What this command is for

Post-implementation corrections. Two kinds, and they are handled differently:

| Kind | Meaning | What it touches |
|---|---|---|
| **Defect** | The implementation does not do what the spec says | Code only |
| **Disagreement** | The implementation matches the spec, but the spec was wrong | Code **and** `agent-artifacts/` |

Work out which one you are dealing with before changing anything. Getting this wrong is how
the spec drifts away from the code.

## Hard rules

- **Never run a git write command.**
- **Keep the artifacts honest.** If the agreed behaviour changed, update
  `agent-artifacts/spec.md` and `agent-artifacts/tasks.md` to match. A `specs/` folder that
  describes something other than what shipped is worse than no folder at all.
- **Fix what was asked.** Do not take the request as licence for a broader refactor. If you
  see something else worth fixing, mention it after — do not bundle it in.

## Templates

Template paths in this file — `templates/fixes-template.md` — are relative to **this
skill's own directory**, not to the project root. Resolve them there.

## Steps

### 1. Load context

1. `.aipartner/memory/` and its **Required reading** list
2. `specs/NNN-slug/agent-artifacts/spec.md` and `tasks.md`
3. `specs/NNN-slug/fixes.md`, if it exists — the problem may be a repeat
4. The code the complaint points at

Resolve the feature from `$ARGUMENTS` or the most recent folder in `specs/`. Ask if it is
ambiguous.

### 2. Understand the complaint

Reproduce or locate the problem in the code before touching it.

Ask at most **one** clarifying question, and only when the request genuinely has two readings
that lead to different fixes. Otherwise state your reading and proceed — the user can correct
you faster than they can answer a question.

If the implementation actually matches the spec, say so plainly and ask whether they want the
spec changed. That is a disagreement, not a defect, and it is worth naming.

### 3. Apply the fix

Follow the project standards. Keep the change proportional to the complaint.

If the fix is large enough to need real planning, say so and suggest `/aipartner-talk` +
`/aipartner-spec` instead of improvising it here.

### 4. Update the artifacts

**Disagreement**: update `agent-artifacts/spec.md` (the requirement, the scope, or the
assumption that was wrong) and `agent-artifacts/tasks.md` where it no longer describes what
exists. Note the same change in the `plan.md` Changelog.

**Defect**: leave the artifacts alone. The spec was right; the code was not.

### 5. Log it

Create or update `specs/NNN-slug/fixes.md` from `templates/fixes-template.md`.
Newest entry first. One entry per request, in the user's language:

| Field | Content |
|---|---|
| Reported | what the user said, in their words |
| Cause | why it happened — bad assumption, bug, or scope disagreement |
| Changed | table of files and what changed in each |
| Spec impact | `None`, or which requirement changed |
| Verify | how the user confirms it |

### 6. Report

What you changed, why, and how to check it. A few lines. Then run the relevant quality gates
and report the result honestly.
