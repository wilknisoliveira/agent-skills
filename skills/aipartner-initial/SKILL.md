---
name: "aipartner-initial"
description: "Scan the project, detect how it is actually built, and record the standards every other aipartner command will follow."
argument-hint: "Optional: standards or conventions you already want enforced"
user-invocable: true
disable-model-invocation: true
---

## User Input

```text
$ARGUMENTS
```

If the user passed anything, treat it as a standard they want enforced. It outranks anything
you detect — record it even when the code currently does otherwise, and note the discrepancy.

## What this command does

Produces `.aipartner/memory/project-standards.md`: how this project is actually built. Every
other aipartner command reads it before doing anything.

You are documenting reality, not designing policy. Detect first, ask only about what you
could not detect.

## Hard rules

- **Never run a git write command.** `git log`, `git status`, `git diff` are fine. Never
  `commit`, `push`, `pull`, `checkout`, `branch`, or anything else that mutates the repo.
- **Never read agent system prompts** (see step 2). They are markdown, but they are not
  project guidance, and reading them pollutes your understanding of the project.
- **Never change project code.** The only file you write is
  `.aipartner/memory/project-standards.md`.
- **The user is never obliged to answer.** "Skip", "I don't know" and "that's enough" all end
  the interview immediately. Write the file with what you have.

## Voice

Short paragraphs. Tables over bulleted prose. Technical register — you are talking to a
developer. Do not restate what is already on their screen. No progress theater.

## Templates

Template paths in this file — `templates/project-standards-template.md` — are relative to **this
skill's own directory**, not to the project root. Resolve them there.

## Steps

### 1. Classify the project

Look at the repo root. Decide: **existing codebase** or **greenfield**.

Greenfield (empty, or only scaffolding and config): skip detection, go to step 4, and frame
the questions as choices for a new project rather than as gaps.

### 2. Find the guideline documents

Look for markdown that carries project guidance:

`README.md`, `CLAUDE.md`, `AGENTS.md`, `CONTRIBUTING.md`, `ARCHITECTURE.md`, `CONVENTIONS.md`,
`STYLEGUIDE.md`, `docs/**/*.md`, `.github/*.md`.

**Exclude agent system prompts.** Many projects run multi-agent architectures and keep each
agent's system prompt as a markdown file. These files are instructions to a model, not
guidance about the project. Reading them is actively harmful here.

Skip a file when **either** test hits:

| Test | Signal |
|---|---|
| Filename | `*_AGENT.md`, `*-agent.md`, `*_PROMPT.md`, `*-prompt.md`, `ORCHESTRATOR*.md`, `REVISOR*.md`, or an ALL-CAPS name that reads as a role (`FINANCIAL_AGENT.md`) |
| Location | anything under `prompts/`, `agents/`, `.claude/agents/`, `.claude/skills/` |
| Content | the first ~20 lines address a model directly — "You are…", "Your role is…", a `## Role`, `## Tools` or `## Instructions` heading, or a persona description |

Use the filename and location tests **before** opening the file. Use the content test only
when the name is ambiguous: read the first 20 lines, and stop reading the moment it looks
like a system prompt.

Report which files you skipped. A skip is a judgement call and the user may want to overrule
one.

Read everything that survives the filter.

### 3. Detect how the project is actually built

From code and config, not from what the docs claim:

| Signal | Where to look |
|---|---|
| Language and version | `package.json`, `pyproject.toml`, `go.mod`, `*.csproj`, `.nvmrc`, `.python-version` |
| Frameworks | dependency manifests, entrypoint files |
| Layout | the real directory tree — which folders hold what |
| Naming | actual filenames and symbol names, not a style guide |
| Testing | test runner config, where test files live, how many there are |
| Quality gates | lint/format config, CI workflow files, git hooks, package scripts |
| Commit style | `git log --oneline -30` |
| Error handling, logging, config | read two or three representative source files |

Where docs and code disagree, the code wins. Note the disagreement.

### 4. Ask about the gaps

Load `templates/project-standards-template.md` and work out which sections you
still cannot fill. Ask about **those only**.

How to ask:

- Small batches — three questions at most per turn.
- Every question carries 2-4 concrete options, one marked **Recommended** with a one-line
  reason. When the harness offers structured multiple choice, use it, and always include an
  option that opens free-text input.
- Lead with what you detected: *"Tests live next to the source and cover the domain services
  only. Is that the rule, or just where it ended up?"* — that is a better question than
  *"What is your testing policy?"*
- Skip anything the code already answers unambiguously. Confirming detected facts is the
  fastest way to make this feel like a form.

Stop asking when the user signals they are done, or when the remaining gaps are minor.
Unanswered gaps go in **Open questions** in the file — they are not blockers.

### 5. Write the file

`.aipartner/` is generated by these commands — nothing is copied in by hand. Before writing:

- Create `.aipartner/memory/` if it is not there.
- Copy this skill's `templates/README.md` to `.aipartner/README.md`, unless that file already
  exists. Never overwrite it — the user may have edited their copy.

Then write `.aipartner/memory/project-standards.md` from the template. Fill only what is real;
delete sections that have nothing to say. One line per entry.

The **Required reading** section lists the guideline files from step 2 and carries the line
**"MANDATORY: read these files before doing anything in this project."** Also list the files
you skipped as agent prompts, so a false positive is visible and correctable.

### 6. Re-running

If `.aipartner/memory/project-standards.md` already exists, update it in place:

- Preserve anything the user hand-edited. If detection now contradicts a hand-edited line,
  do not overwrite it — raise it and ask.
- Add what is new, correct what is stale.
- Report what changed, in a short table. Do not print the whole file back.

### 7. Report

Close with:

- Where the file is
- What you detected, in a compact table
- What was skipped as an agent prompt, if anything
- What is still open
- Next step: `/aipartner-talk` to discuss a feature
