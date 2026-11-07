---
name: "aipartner-execute"
description: "Implement a specified feature or a small change directly from the conversation, and handle follow-up corrections."
argument-hint: "Optional: feature, phase, task, direct implementation request, or correction"
user-invocable: true
disable-model-invocation: true
---

## User Input

```text
$ARGUMENTS
```

Use the request and session context to choose the flow below. Empty input means implement
the current agreed feature or continue its implementation. Ask when the target or scope is
ambiguous. Do not select an unrelated feature just because its folder was modified recently.

## Hard rules

- **Never run a git write command.** No commit, push, pull, checkout, or branch.
- **Keep to the agreed scope.** For spec-based work, Out of Scope in `spec.md` is binding
  unless the user explicitly requests a change. For direct work, the request and settled
  discussion define scope. Ask before unrelated changes required to proceed.
- **Follow project guidance.** Read applicable instructions and required guideline documents.
  Match the project's conventions and keep affected guidance current before declaring done.
- **Do not create session memory or talk notes.** Direct work and correction decisions stay
  in session context; direct work does not need a feature folder or fix log.

Template paths, including `templates/fixes-template.md`, are relative to this skill's directory.

## 1. Load guidance and choose the flow

Read root `AGENTS.md` and `CLAUDE.md` when present, their Required reading, relevant project
guidelines, and applicable directory instructions. Already-read files count unless changed.
For maintaining root standards, prefer existing root `CLAUDE.md`; otherwise use root
`AGENTS.md`. Read both when both exist. Preserve the established documentation structure
and avoid duplicating standards across files.

If project rules or documentation practices conflict with aipartner guidance, explain the
specific conflict and ask how to resolve it before dependent changes. Missing root standards
do not block work: inspect available guidance and code, and suggest `/aipartner-initial`
when useful.

| Flow | When | Context |
|---|---|---|
| Spec-based implementation | The request targets an agreed specification | Read `specs/NNN-slug/agent-artifacts/spec.md`, `tasks.md`, and existing `fixes.md` if any |
| Direct implementation | The user skips spec for a small change or asks to implement the settled conversation | Use the request, session decisions, and relevant code; no `tasks.md` required |
| Follow-up correction | The user requests changes after implementation | Use the active feature, code, and its spec and fix log if it has them |

Resolve a spec folder from the request or established session context. If multiple features
could match, ask. If an explicitly targeted spec lacks `tasks.md`, explain and offer to
regenerate it with `/aipartner-spec` or proceed directly with the user's agreement. Do not
silently abandon an intended spec-based workflow. Direct work must not inherit an unrelated
spec folder or create one merely to track progress.

## 2. Implement

### Spec-based work

Read the Standards Check in `tasks.md`. Mention documented deviations before starting;
unresolved conflicts with current guidance need the user's resolution, not just a mention.

Work phase by phase. Foundational work blocks stories; honor inline dependencies. `[P]` tasks
may be grouped only when they have no shared file or dependency conflict. Within a story,
follow models → services → interface/endpoints → integration where applicable.

Mark each completed task `[X]` in `tasks.md` as it finishes. At checkpoints, verify the story
works before moving on. Use test-first when required by project standards for this change.

### Direct work

State the intended scope briefly. Track the necessary steps with the harness's native task
list when available, or a short list in chat. Implement from the agreed request without
creating `plan.md`, `spec.md`, `tasks.md`, or a persistent decision log. Ask about missing
information only when it materially changes the result.

### Failures

Stop dependent work when a sequential task fails. Independent work may continue when safe.
Report the actual error. If a task is wrong or impossible, explain instead of silently
reinterpreting it. Never mark a failed or unverified task done.

## 3. Handle follow-up corrections

These instructions also apply to ordinary follow-up requests after this skill finishes;
the user does not need a separate command or another invocation to request changes.

Locate or reproduce the issue, then make the requested change proportionally. An explicit
request for changed behavior authorizes that correction even when the original spec described
the old behavior. Explain the difference without asking the user to authorize the same change
again. Ask only when the intended result or scope is genuinely unclear.

For a feature with a spec, distinguish:

- **Defect**: implementation did not match the specification.
- **Disagreement**: the user changed an agreed decision; name the stale requirement.

Read the spec and existing `fixes.md`; the completed task checklist is not a correction
tracker. Preserve `plan.md`, `agent-artifacts/spec.md`, and `agent-artifacts/tasks.md` as the
implementation agreement. Create or update `specs/NNN-slug/fixes.md` using
`templates/fixes-template.md`, newest entry first, one entry per request, in the user's
language. Record the report, cause, changed files, kind, and verification. A Disagreement
entry must identify which requirement no longer describes the behavior. Subsequent work
must read these entries alongside the original specification.

For direct work without a spec, keep correction decisions in session context only. Do not
create a fix log or a specification just to record them.

If the request grows into a substantial new feature or redesign, explain the scope change
and recommend `/aipartner-talk` then `/aipartner-spec`. Do not force that process for a small
correction or quietly broaden the current work.

## 4. Update affected project guidelines

Before finishing every implementation or correction, inspect project guidance for statements
made stale by the change: `README.md`, architecture documents (including `architecture.md`),
root `AGENTS.md` and `CLAUDE.md`, contribution and setup guides, and other relevant documents
or linked guidelines. Update every affected description, command, convention, or diagram.
Check both root instruction files when both exist: keep standards in `CLAUDE.md` by default,
but correct stale implementation facts wherever they occur. Preserve unrelated guidance and
follow established documentation conventions. Ask before resolving a conflict in policy.

Historical feature specs and plans are distinct from current project guidelines: follow-up
corrections update the latter and record spec disagreements in `fixes.md`.

## 5. Validate and report

Run quality gates required by the project for the change, plus applicable task validation and
focused correction checks. Report passes, failures, and skipped gates with reasons. Mark
spec-based work complete only after documentation and validation are done; in direct work,
complete the session task list.

Close with what changed, anything blocked, validation results, and how the user can verify
it. Mention a stale spec requirement when a correction changed one. The user can keep
requesting changes in the same conversation.
