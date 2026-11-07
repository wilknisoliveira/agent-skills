---
name: "aipartner-initial"
description: "Scan the project and maintain its standards in root AGENTS.md or existing CLAUDE.md."
argument-hint: "Optional: standards or conventions you already want enforced"
user-invocable: true
disable-model-invocation: true
---

## User Input

```text
$ARGUMENTS
```

Treat supplied conventions as the user's intended standards. If they conflict with existing
instructions or documentation practices, explain the conflict and ask how to resolve it
before changing the affected guidance.

## Purpose and boundaries

Detect how the project is actually built and maintain its standards in a root instruction
file. Use root `CLAUDE.md` if it exists; otherwise use root `AGENTS.md`, creating it if needed.
When both exist, read both and update `CLAUDE.md`. Preserve existing content and links to
more detailed guidance; do not duplicate standards between the files.

Never run git write commands or change project code. This command writes only the selected
root instruction file. Discussion decisions stay in session context; do not create a
separate memory directory or session notes.

Template paths are relative to this skill's directory. Use
`templates/project-guidelines-template.md` as a checklist for new content, not as a replacement
for the project's existing structure.

## 1. Read guidance and resolve conflicts

Read root `AGENTS.md` and `CLAUDE.md` when present, their Required reading, and relevant
project guidance: `README.md`, contribution guides, architecture documents, `docs/`, and
`.github/` guidance. Follow applicable directory-specific instructions as well.

Compare existing rules and documentation conventions with aipartner guidance before writing.
If they conflict, describe the specific rules and files and ask the user how to resolve them.
This includes projects that document architecture or standards in a different location or
format. Do not silently replace their approach or invent an override. Continue independent
detection while waiting, but leave conflicting guidance unchanged.

Do not classify root `AGENTS.md` or `CLAUDE.md` as persona prompts. For other files, skip role
prompts under `prompts/`, `agents/`, `.claude/agents/`, and skill definitions unless they are
relevant project artifacts for this scan. Names such as `*_AGENT.md`, `*-prompt.md`, or
`ORCHESTRATOR*.md` are signals to inspect cautiously. For ambiguous files, inspect the first
20 lines and stop if they define a persona rather than project guidance. Report skips so
the user can correct a false positive.

## 2. Detect the project

Classify it as an existing codebase or greenfield. For an existing project, inspect code and
configuration for the stack and versions, layout, naming, error handling, logging,
configuration, testing, and quality gates. Use representative source files and read-only git
history when useful. Distinguish observed practice from intended policy; report discrepancies
instead of replacing documented rules with whatever the code happens to do.

For greenfield projects, ask about choices that materially affect setup rather than
pretending they were detected.

## 3. Ask about material gaps

Use the template as a checklist. Ask at most three questions at a time, with concrete options,
a recommendation, and room for free text. Do not ask to confirm unambiguous facts.
If the user skips questions or ends the interview, write what is known and record remaining
nonblocking gaps under Open questions. An unresolved conflict is not permission to overwrite
guidance.

## 4. Maintain the root instruction file

Merge useful findings into the selected root file. Preserve hand-edited instructions,
unrelated sections, and the established structure. If detection contradicts an existing rule,
ask before replacing it. Update stale facts and add new ones without rewriting the whole file.

Keep detailed architecture and conventions in their existing documents and link to them.
Include a Required reading list of real project guidelines, with the instruction:
**MANDATORY: read these files before working in this project.** Avoid self-links and cycles.
Record supported facts and agreed standards; omit empty template sections.

## 5. Report

State which root file was updated, summarize findings and changes, and list skipped prompts
or unresolved questions when relevant. Suggest `/aipartner-talk` to discuss a feature.
