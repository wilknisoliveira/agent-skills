# Fixes: [FEATURE NAME]

**ID**: `[NNN-slug]`

Post-implementation changes handled by `/aipartner-execute` or ordinary follow-up requests.
Used only for features with an existing specification.

<!--
  RULES:
  - Newest entry first.
  - One entry per fix request, even when it touches several files.
  - Record what the user reported in their words, not your interpretation of it.
  - "Kind" is the important field. agent-artifacts/ is deliberately NOT updated after
    implementation — a "Disagreement" entry is how the next reader learns that spec.md no
    longer describes what shipped.
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

**Kind**: [Defect — implementation did not match the spec] OR [Disagreement — spec.md FR-00X
no longer describes the agreed behaviour]

**Verify**: [command to run or thing to check]

---
