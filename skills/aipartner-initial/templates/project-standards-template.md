# [PROJECT_NAME] — Project Standards

**Last updated**: [DATE]

How this project is built. Written by `/aipartner-initial`, read by every other aipartner command
before it does anything.

<!--
  FILL RULES (delete this comment in the generated file):
  - Record what the project ACTUALLY does, detected from code and config. Do not invent policy.
  - When something could not be detected and the user did not answer, put it under
    "Open questions" instead of guessing.
  - Keep every entry to one line. This file is read at the start of every session — it must
    stay scannable.
  - Delete any section that has nothing real to say. Do not leave "N/A" rows behind.
-->

## Required reading

**MANDATORY: read these files before doing anything in this project.**

<!--
  List only real guideline docs found in the repo. Never list agent system prompts
  (REVISOR_AGENT.md, ORCHESTRATOR.md, ...) — they carry no project guidance.
-->

| File | What it covers |
|---|---|
| [path] | [one line] |

<!-- If files were skipped as agent prompts, note them so the user can correct a false positive: -->

**Skipped as agent prompts** (not project guidance): [list, or delete this line]

## Stack

| Area | Choice | Notes |
|---|---|---|
| Language | [e.g. TypeScript 5.4] | [version source: package.json, .python-version, ...] |
| Runtime | [e.g. Node 20] | |
| Framework | [e.g. NestJS] | |
| Storage | [e.g. PostgreSQL via Prisma] | |
| Package manager | [e.g. pnpm] | |

## Layout

```text
[real directory tree of the parts that matter — not every folder]
```

| Path | Holds |
|---|---|
| [src/modules/] | [one line] |

## Conventions

<!-- Detected from the code, not from a style guide nobody follows. -->

- **Naming**: [e.g. files kebab-case, classes PascalCase, DB columns snake_case]
- **Imports**: [e.g. absolute from `@/`, no deep relative paths]
- **Error handling**: [e.g. domain errors thrown, mapped to HTTP in a filter]
- **Logging**: [e.g. structured via pino, never console.log]
- **Configuration**: [e.g. env vars validated at boot in config/env.ts]
- **Commits**: [e.g. Conventional Commits — detected from git log]

## Testing

| Question | Answer |
|---|---|
| Runner | [e.g. vitest] |
| Where tests live | [e.g. next to the source as *.spec.ts] |
| What must be tested | [e.g. domain services and API contracts; UI is manual] |
| Command | [e.g. pnpm test] |

## Quality gates

Commands that must pass before work is considered done:

| Gate | Command |
|---|---|
| [Lint] | [pnpm lint] |
| [Types] | [pnpm typecheck] |
| [Tests] | [pnpm test] |

## Constraints

<!-- Hard rules a contributor would get wrong without being told. Only real ones. -->

- [e.g. No breaking changes to the public API without a version bump]
- [e.g. Never query the DB outside a repository class]

## Open questions

<!-- Undetected and unanswered. Not blockers — just what a future run should pick up. -->

- [ ] [question]
