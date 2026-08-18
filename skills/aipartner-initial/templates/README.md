# aipartner

A spec-driven workflow built around a conversation instead of a form. Five slash commands,
no scripts, three files per feature.

## Install

Copy the five `aipartner-*` folders into `.claude/skills/` in your project. That is the whole
install — each skill carries its own templates. Everything under `.aipartner/` is created for
you the first time you run a command.

## Commands

| Command | What it does | When |
|---|---|---|
| `/aipartner-initial` | Scans the project and records how it is actually built | Once per project, re-run when things change |
| `/aipartner-talk` | Discusses an idea with you. Implements nothing | Any time, as often as you like |
| `/aipartner-spec` | Turns the discussion into a plan and agent artifacts | When the shape is settled |
| `/aipartner-execute` | Works through the task list | When you approve the plan |
| `/aipartner-fix` | Corrects something after implementation, and logs it | When something is wrong |

`talk` and `spec` loop. Discuss, spec it, discuss some more, re-spec — the folder is updated
in place, never duplicated.

## What lands where

```text
.aipartner/                       generated — you never create any of this by hand
├── README.md                      this file
├── memory/project-standards.md    how this project is built — read before every command
└── talks/<slug>.md                running notes from /aipartner-talk

specs/NNN-slug/
├── plan.md                        for you. The only document meant to be read.
├── agent-artifacts/
│   ├── spec.md                    for agents. What gets built and why.
│   └── tasks.md                   for agents. How it gets built.
└── fixes.md                       only if /aipartner-fix ran
```

`plan.md` is written in your language and fits on one screen. The agent artifacts are in
English and carry the detail.

## Two things worth knowing

**The talk notes are the memory.** `/aipartner-talk` writes to `.aipartner/talks/<slug>.md`
as you go, so you can close the session, come back tomorrow, and run `/aipartner-spec` with
none of the conversation in context.

**No command ever writes to git.** No branch, no commit, no checkout. Committing is your call.

**Commit `.aipartner/` with your project.** The standards and the talk notes are team
knowledge — they are worth as much to the next person as they are to the next session.
