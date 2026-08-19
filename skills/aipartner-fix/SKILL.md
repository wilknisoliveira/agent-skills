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

Post-implementation corrections. Two kinds. Both touch **code only** — the difference is what
gets recorded, not what gets rewritten:

| Kind | Meaning | What it touches |
|---|---|---|
| **Defect** | The implementation does not do what the spec says | Code, logged as `Defect` |
| **Disagreement** | The implementation matches the spec, but the spec was wrong | Code, logged as `Disagreement` naming the stale requirement |

Work out which one you are dealing with before changing anything. The classification is the
most useful line in the log — it tells the next reader whether `spec.md` can still be trusted.

## Hard rules

- **Never run a git write command.**
- **Never edit `agent-artifacts/spec.md`, `agent-artifacts/tasks.md` or `plan.md`.**
  `specs/NNN-slug/fixes.md` is the only file you write under `specs/`. Those documents record
  what was agreed at spec time; `fixes.md` records everything that happened after it. Rewriting
  them on every correction costs more than it returns, and it erases the fact that the agreement
  changed.
- **Fix what was asked.** Do not take the request as licence for a broader refactor. If you
  see something else worth fixing, mention it after — do not bundle it in.

## Templates

Template paths in this file — `templates/fixes-template.md` — are relative to **this
skill's own directory**, not to the project root. Resolve them there.

## Steps

### 1. Load context

1. `.aipartner/memory/` and its **Required reading** list
2. `specs/NNN-slug/agent-artifacts/spec.md`
3. `specs/NNN-slug/fixes.md`, if it exists — the problem may be a repeat
4. The code the complaint points at

Do not read `tasks.md`. It is a completed checklist and it no longer gets updated.

Resolve the feature from `$ARGUMENTS` or the most recent folder in `specs/`. Ask if it is
ambiguous.

### 2. Understand the complaint

Reproduce or locate the problem in the code before touching it.

Ask at most **one** clarifying question, and only when the request genuinely has two readings
that lead to different fixes. Otherwise state your reading and proceed — the user can correct
you faster than they can answer a question.

If the implementation actually matches the spec, say so plainly and ask whether they want the
behaviour changed anyway. That is a disagreement, not a defect, and it is worth naming.

### 3. Apply the fix

Follow the project standards. Keep the change proportional to the complaint.

**If the request is a redesign rather than a correction — new behaviour, a new requirement, a
different shape — stop and say so.** Point at `/aipartner-talk` + `/aipartner-spec`. That is the
only path that rewrites a spec, and it does it deliberately and once. Do not improvise a
redesign here and do not patch the spec to match it.

### 4. Log it

Create or update `specs/NNN-slug/fixes.md` from `templates/fixes-template.md`.
Newest entry first. One entry per request, in the user's language:

| Field | Content |
|---|---|
| Reported | what the user said, in their words |
| Cause | why it happened — bad assumption, bug, or scope disagreement |
| Changed | table of files and what changed in each |
| Kind | `Defect`, or `Disagreement` plus the one requirement that is now stale |
| Verify | how the user confirms it |

### 5. Report

What you changed, why, and how to check it. A few lines. If the entry was a `Disagreement`, say
in one line which requirement in `spec.md` no longer describes reality. Then run the relevant
quality gates and report the result honestly.
