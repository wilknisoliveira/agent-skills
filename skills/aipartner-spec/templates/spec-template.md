# Feature Specification: [FEATURE NAME]

**ID**: `[NNN-slug]` | **Created**: [DATE] | **Status**: Draft
**Source**: [agreed discussion or explicit request in session]

> This file records what was agreed at spec time. It is **not** updated after implementation —
> post-implementation corrections handled by execution or follow-up requests are logged in `../fixes.md`.

<!--
  AUDIENCE: agents only. Be precise and complete — verbosity is fine here.
  HARD RULE: nothing in this file that was not agreed in the talk. Anything you inferred
  goes in ## Assumptions, explicitly labelled. Do not invent requirements to fill sections.
  Delete any section that does not apply. Never leave a placeholder or an "N/A" row.
-->

## Overview

[What this feature is and the problem it solves. 3-5 lines.]

## User Scenarios *(mandatory)*

<!--
  User stories are journeys, ordered by importance and prioritised P1, P2, P3.
  Each one must be INDEPENDENTLY TESTABLE: implement only that story and you still have
  something that works and delivers value. If a story cannot stand alone, it is not a
  story — fold it into the one it depends on.
-->

### User Story 1 - [Brief Title] (Priority: P1)

[The journey in plain language.]

**Why this priority**: [what it delivers and why it comes first]

**Independent Test**: [how to verify this story alone, without the others]

**Acceptance Scenarios**:

1. **Given** [initial state], **When** [action], **Then** [expected outcome]
2. **Given** [initial state], **When** [action], **Then** [expected outcome]

---

### User Story 2 - [Brief Title] (Priority: P2)

[The journey in plain language.]

**Why this priority**: [reason]

**Independent Test**: [how to verify this story alone]

**Acceptance Scenarios**:

1. **Given** [initial state], **When** [action], **Then** [expected outcome]

---

[Add stories as needed. Delete the unused ones.]

### Edge Cases

- What happens when [boundary condition]?
- How does the system handle [error scenario]?

## Requirements *(mandatory)*

### Functional Requirements

<!-- Every requirement must be testable. If you cannot write a test for it, rewrite it. -->

- **FR-001**: System MUST [specific capability]
- **FR-002**: Users MUST be able to [key interaction]
- **FR-003**: System MUST [data or behaviour requirement]

### Non-Functional Requirements *(include only if the talk raised them)*

- **NFR-001**: [performance, security, compliance or operational requirement]

### Key Entities *(include if the feature involves data)*

- **[Entity]**: [what it represents, its attributes and relationships — no storage details]

## Success Criteria *(mandatory)*

<!--
  Measurable and technology-agnostic. Describe the outcome, not the implementation.
  Good: "Users complete checkout in under 3 minutes."
  Bad:  "API responds in under 200ms." — that is an implementation target, not an outcome.
-->

- **SC-001**: [measurable outcome]
- **SC-002**: [measurable outcome]

## Out of Scope

<!-- What was explicitly ruled out in the talk. This section prevents scope creep during
     /aipartner-execute — treat it as binding. -->

- [excluded item]

## Rejected alternatives

<!-- Options that were considered and lost, one line each, with the reason. This is the only
     record of the reasoning once the discussion is gone — it is what stops a future session
     re-arguing a decision that was already settled. -->

| Option | Why it lost |
|---|---|
| [alternative considered] | [the reason it was rejected] |

## Assumptions

<!-- Everything you filled in that the user did not explicitly confirm. Be honest here:
     an unlisted assumption is a silent invention. -->

- [assumption and what it was based on]

## Dependencies

- [existing code, service or system this feature relies on]
