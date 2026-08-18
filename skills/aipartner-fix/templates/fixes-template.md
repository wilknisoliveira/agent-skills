# Fixes: [FEATURE NAME]

**ID**: `[NNN-slug]`

Post-implementation changes. Every `/aipartner-fix` run appends an entry here.

<!--
  RULES:
  - Newest entry first.
  - One entry per fix request, even when it touches several files.
  - Record what the user reported in their words, not your interpretation of it.
  - "Spec impact" is the important column: it says whether the agreed behaviour changed,
    which is what keeps agent-artifacts/ from drifting away from reality.
  - Write in the user's language.
  - Delete this comment block in the generated file.
-->

---

## [DATE] — [short title]

**Reported**: [what the user said was wrong, in their words]

**Cause**: [why it happened — a wrong assumption in the spec, a bug in the implementation,
or a scope decision the user disagrees with. One or two lines.]

**Changed**:

| File | Change |
|---|---|
| [exact path] | [what changed] |

**Spec impact**: [None — implementation-only fix] OR [agent-artifacts/spec.md updated:
FR-00X now says ...] OR [agent-artifacts/tasks.md updated: ...]

**Verify**: [command to run or thing to check]

---
