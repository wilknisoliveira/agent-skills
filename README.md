# Agent Skills

Source repository for **aipartner** — a workflow built around a conversation, with optional
specifications for larger features. Four skills, no scripts or installer.

## Install

Copy the `aipartner-*` folders from `skills/` into `.claude/skills/` in your project.
Each skill carries the templates it needs.

| Skill | Command |
|---|---|
| `aipartner-initial` | `/aipartner-initial` — scan the project and maintain its standards |
| `aipartner-talk` | `/aipartner-talk` — discuss a feature without implementing it |
| `aipartner-spec` | `/aipartner-spec` — turn the discussion into a plan and agent artifacts |
| `aipartner-execute` | `/aipartner-execute` — implement from a spec or directly from the conversation |

## Workflow

Run `/aipartner-initial` to detect project conventions and maintain them in root
`AGENTS.md`. If root `CLAUDE.md` already exists, it is used instead. When both exist, the
skills read both and maintain standards in `CLAUDE.md`. Existing content and documentation
conventions are preserved; conflicts with aipartner guidance are raised for your decision.
Detailed guidance stays in its established documents and is linked from the root file.

Use `/aipartner-talk` to discuss an idea. It loads all skills you request before analyzing
the topic. Decisions stay in session context; it writes no notes or memory files.

For a larger feature, run `/aipartner-spec`, then `/aipartner-execute`. For a small change,
run `/aipartner-execute` alone to implement directly from the settled conversation. It tracks
progress in the session without requiring or generating specification files.

After implementation, keep requesting changes in the conversation. No separate correction
command is needed. For spec-based features, corrections are logged in `fixes.md`, identifying
defects or changed decisions and stale requirements. The original spec and plan remain the
agreement at implementation time. For direct work without a spec, fix decisions stay in
session context and no fix log is created.

Execution and corrections update every affected project guideline, including README,
architecture documents, and root instruction files. All commands leave git writes to you.

## Layout

```text
skills/
├── aipartner-initial/    SKILL.md + templates/project-guidelines-template.md
├── aipartner-talk/       SKILL.md
├── aipartner-spec/       SKILL.md + templates/ (plan, spec, tasks)
└── aipartner-execute/    SKILL.md + templates/fixes-template.md
```

Spec-based work generates:

```text
specs/NNN-slug/
├── plan.md                    concise plan in your language
├── agent-artifacts/
│   ├── spec.md                agreed behavior, in English
│   └── tasks.md               implementation tasks, in English
└── fixes.md                   only after post-implementation corrections
```

`talk` and `spec` can loop before implementation. Revisions reuse the same feature folder.
Direct execution creates none of these workflow artifacts.
