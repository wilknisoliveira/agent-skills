# Implementation Plan & Tasks: [FEATURE NAME]

**ID**: `[NNN-slug]` | **Created**: [DATE]
**Spec**: `./spec.md` | **Standards**: `.aipartner/memory/project-standards.md`

<!--
  AUDIENCE: agents only. This file merges what spec-kit split across plan.md and tasks.md:
  the technical decisions first, then the executable task list.

  HARD RULES:
  - Every task must be executable by an agent with no extra context. Name exact file paths.
  - Every technical choice must match .aipartner/memory/project-standards.md, or be listed
    as a deviation in ## Standards Check with a justification.
  - Do not introduce technology, patterns or scope that were not agreed in the talk.
  - Replace every sample task below. Do not ship the samples.
-->

## Technical Context

<!-- Fill from detection + the talk. Say "inherits project default" when it does. -->

**Language/Version**: [e.g. TypeScript 5.4]
**Primary Dependencies**: [libraries this feature adds or leans on]
**Storage**: [if applicable]
**Testing**: [runner and what gets tested — from project standards]
**Target Platform**: [e.g. Linux server, browser]
**Project Type**: [e.g. web service, CLI, library]
**Constraints**: [performance, compatibility or operational limits raised in the talk]

## Approach

[How this gets built, in 5-10 lines. The shape of the solution: which layers are touched,
what the data flow is, which existing code is reused. Enough that the task list below reads
as obvious rather than arbitrary.]

## Standards Check

*Gate: must pass before execution starts.*

| Standard (from project-standards.md) | How this feature complies |
|---|---|
| [e.g. Repository pattern for all DB access] | [how] |

**Deviations**:

<!-- Fill ONLY when this feature breaks a documented standard. An empty table means none. -->

| Deviation | Why it is necessary | Simpler alternative rejected because |
|---|---|---|
| [what] | [why] | [why not] |

## Files Touched

| File | Change |
|---|---|
| [exact path] | [new / modified — what changes] |

## Tasks

**Format**: `- [ ] T001 [P] [US1] Description with exact file path`

- **[P]**: safe to run in parallel — different files, no shared dependency
- **[US1]**: the user story this task serves, for traceability
- Dependencies noted inline as `(depends on T00X)`

<!-- Tests: include test tasks only if the project standards require tests for this kind of
     change, or the user asked for them. Do not add a test phase by reflex. -->

### Phase 1: Setup

**Purpose**: anything that must exist before real work starts. Skip this phase entirely when
the project is already set up.

- [ ] T001 [describe with exact path]

### Phase 2: Foundational

**Purpose**: shared groundwork that blocks every user story.

**Blocking** — no story work begins until this phase is done.

- [ ] T002 [describe with exact path]

### Phase 3: User Story 1 - [Title] (P1)

**Goal**: [what this story delivers]

**Independent Test**: [how to verify it alone]

- [ ] T003 [P] [US1] [describe with exact path]
- [ ] T004 [US1] [describe with exact path] (depends on T003)

**Checkpoint**: User Story 1 works end to end and can be demonstrated.

### Phase 4: User Story 2 - [Title] (P2)

**Goal**: [what this story delivers]

**Independent Test**: [how to verify it alone]

- [ ] T005 [P] [US2] [describe with exact path]

**Checkpoint**: User Stories 1 and 2 both work independently.

[Add one phase per remaining story, in priority order.]

### Phase N: Polish

**Purpose**: cross-cutting work that only makes sense once the stories are in.

- [ ] TXXX [docs, cleanup, or cross-story concerns — delete this phase if there is none]

## Execution Order

- Setup → Foundational → stories in priority order (P1 → P2 → P3) → Polish
- Foundational blocks every story. Once it is done, stories are independent.
- Within a story: models → services → interface/endpoints → integration
- `[P]` tasks in the same phase can run together; tasks touching the same file cannot

## Validation

How to confirm the feature works when the tasks are done:

| Check | Command or action | Expected |
|---|---|---|
| [Quality gate from project standards] | [command] | [passes] |
| [Acceptance scenario from spec.md] | [action] | [outcome] |
