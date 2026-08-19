---
name: "aipartner-spec"
description: "Turn the discussion into a plan: one readable document for you, and the detailed artifacts the implementation agent needs."
argument-hint: "Optional: which feature, or what to adjust in an existing plan"
user-invocable: true
disable-model-invocation: true
---

## User Input

```text
$ARGUMENTS
```

Empty means "spec the feature we just discussed". Otherwise it names a feature or describes an
adjustment to an existing plan.

## What this command produces

```text
specs/NNN-slug/
├── plan.md                      ← for the user. The only document meant to be read.
└── agent-artifacts/
    ├── spec.md                  ← for agents. What gets built and why.
    └── tasks.md                 ← for agents. How it gets built, as executable tasks.
```

Three files. Not seven.

## Hard rules

- **Never run a git write command.** No branch, no commit, no checkout. You create
  directories and files under `specs/` and nothing else.
- **Do not implement anything.** This command writes documents. Implementation is
  `/aipartner-execute`.
- **Do not invent.** Nothing enters these files that was not agreed in the talk or detected
  in the codebase. Anything you inferred goes in an explicit **Assumptions** section.
- **No unresolved markers.** Do not leave `[NEEDS CLARIFICATION]` or an empty placeholder
  behind. If something is genuinely undecided and matters, ask — at most three questions,
  each with options and a recommendation.

## Language

- `agent-artifacts/spec.md` and `agent-artifacts/tasks.md`: **always English.**
- `plan.md` and everything you say in chat: **the user's language.**

## Templates

Template paths in this file — `templates/spec-template.md`, `templates/tasks-template.md`, `templates/plan-template.md` — are relative to **this
skill's own directory**, not to the project root. Resolve them there.

## Steps

### 1. Load context

Read, in this order:

1. `.aipartner/memory/` — every file
2. Everything under its **Required reading** list
3. `.aipartner/talks/<slug>.md` for this feature, **if it exists** — notes are written only
   when the user asks for them, so most of the time there are none. Their absence is normal.
4. The parts of the codebase the talk touched

Normally the discussion is in this session's context and that is the source you work from. Only
when there is **neither** a notes file **nor** a discussion in context, say so and offer
`/aipartner-talk` first. If the user wants to proceed anyway, do — but everything you write will
be an assumption, and it must be labelled as one.

### 2. Resolve the feature folder

**New feature**: list `specs/`. Take the highest `NNN-` prefix, add one, pad to three digits.
No `specs/` directory yet → `001`. The slug is the one from the talk notes.

**Updating an existing feature**: reuse its folder. Never create a second folder for the same
feature.

### 3. Write `agent-artifacts/spec.md`

From `templates/spec-template.md`.

This file is read only by agents, so be precise and complete — detail is welcome. But detail
is not licence to invent. Every requirement traces back to something the user said or
something the code shows.

- User stories prioritised P1, P2, P3, each **independently testable** — implement only that
  story and something useful works.
- Acceptance scenarios in `**Given** … **When** … **Then** …` form.
- Requirements as `FR-001`, each testable. If you cannot imagine the test, rewrite it.
- Success criteria as `SC-001`, measurable and technology-agnostic — outcomes, not response
  times.
- **Out of Scope** — what the talk ruled out. This is binding during execution.
- **Rejected alternatives** — the options considered and the reason each lost. This is the only
  place the reasoning survives once the session ends; without it a future session re-argues a
  decision that was already made.
- **Assumptions** — everything you filled in that the user did not confirm. An unlisted
  assumption is a silent invention.

### 4. Write `agent-artifacts/tasks.md`

From `templates/tasks-template.md`. This merges what spec-kit split across
`plan.md` and `tasks.md`.

- **Technical Context** — the stack, from project standards plus whatever this feature adds.
- **Approach** — how it gets built in 5-10 lines, so the task list reads as obvious rather
  than arbitrary.
- **Standards Check** — how the feature complies with `.aipartner/memory/project-standards.md`.
  Anything that breaks a documented standard goes in the deviations table with a
  justification. A deviation you cannot justify is a design you should reconsider.
- **Files Touched** — exact paths.
- **Tasks** — `- [ ] T001 [P] [US1] Description with exact file path`. Phased: Setup →
  Foundational → one phase per user story in priority order → Polish. Drop any phase with
  nothing in it; most existing projects need no Setup phase.
- Include test tasks only when the project standards require tests for this kind of change,
  or the user asked. Do not add a test phase by reflex.

Each task must be executable by an agent holding no other context.

### 5. Write `plan.md`

From `templates/plan-template.md`, in the user's language.

This is the only document the user reads. It must fit on roughly one screen.

| Section | Content |
|---|---|
| Summary | ≤10 lines — what gets built, why, and the decision that shapes everything else |
| What changes | table: area · change · impact |
| Scope | table: in / out |
| Work overview | table: phase · what · files touched · depends on |
| Risks and assumptions | table |
| How to validate | the commands to run and what to look at |

Summarise the agent artifacts. Do not restate them. If `plan.md` is getting long, you are
duplicating.

### 6. Report

Your reply is:

1. The **Summary** section, as written in `plan.md`
2. The assumptions and decisions the user genuinely needs to know about — the ones where you
   chose something they did not explicitly confirm
3. The paths, in one line
4. Next step: `/aipartner-execute`, or `/aipartner-talk` if something is still open

Nothing else. Do not paste the plan, do not list every task, do not summarise your own
summary.

## Adjustments and re-runs

The user can ask for changes right after this command, or run it again later after more
`/aipartner-talk`.

Either way: update the files in the existing `specs/NNN-slug/` folder in place, and append a
dated line to the **Changelog** table in `plan.md` saying what changed. Never create a new
feature folder for a revision.

When the change contradicts something already agreed, say so before rewriting it.
