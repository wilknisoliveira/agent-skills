# [FEATURE NAME]

**ID**: `[NNN-slug]` | **Created**: [DATE] | **Status**: Planned

<!--
  AUDIENCE: the user. This is the ONLY document in this feature meant to be read by a human.

  RULES:
  - Write in the user's language.
  - It must fit on roughly one screen. If it does not, you are duplicating the agent artifacts.
  - Summarise; never restate agent-artifacts/spec.md or agent-artifacts/tasks.md.
  - Tables over prose lists. Short sentences. Technical register — the reader is a developer.
  - Delete any section with nothing real in it.
  - Delete this comment block in the generated file.
-->

## Summary

[Up to 10 lines. What gets built, why, and the one technical decision that shapes everything
else. Someone who reads only this paragraph should be able to approve or reject the plan.]

## What changes

| Area | Change | Impact |
|---|---|---|
| [module or layer] | [what happens to it] | [what the user or system notices] |

## Scope

| In | Out |
|---|---|
| [included] | [excluded, and it stays excluded] |

## Work overview

| Phase | What | Files touched | Depends on |
|---|---|---|---|
| [1. Foundation] | [one line] | [paths, abbreviated] | [—] |

## Risks and assumptions

| # | Item | Type | Impact if wrong |
|---|---|---|---|
| 1 | [what we assumed or what could go wrong] | Assumption / Risk | [consequence] |

## How to validate

[How you confirm this works once it is built — the commands to run and what to look at.
Two or three lines.]

## Details for agents

The full specification and task list live in `./agent-artifacts/`. You do not need to read
them — they exist so `/aipartner-execute` has everything it needs.

## Changelog

<!-- One line per revision after the first. Append; do not rewrite history. -->

| Date | Change |
|---|---|
| [DATE] | Initial plan |
