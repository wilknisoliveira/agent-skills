# Agent Skills

Source repository for **aipartner** — a workflow built around a conversation, with optional
specifications for larger features. Four skills, no scripts or installer.

## Install

Copy the `aipartner-*` folders from `skills/` into `.agents/skills/` in your project by
default, or `.claude/skills/` when using Claude.
Each skill carries the templates it needs.

| Skill | Command |
|---|---|
| `aipartner-initial` | `/aipartner-initial` — scan the project and maintain its standards |
| `aipartner-talk` | `/aipartner-talk` — discuss a feature without implementing it |
| `aipartner-spec` | `/aipartner-spec` — turn the discussion into a plan and agent artifacts |
| `aipartner-execute` | `/aipartner-execute` — implement from a spec or directly from the conversation |

## Workflow

Run `/aipartner-initial` to detect project conventions and maintain them in root
`AGENTS.md`, and ensure `.agents/.gitkeep` exists. For a project already following Claude
conventions, or at your explicit request, it uses `CLAUDE.md` and `.claude/.gitkeep` instead.
Installing the skills in `.claude/skills/` alone does not select that convention. When both
root instruction files exist, the skills read both and maintain standards in `CLAUDE.md`.
Existing content and documentation
conventions are preserved; conflicts with aipartner guidance are raised for your decision.
Detailed guidance stays in its established documents and is linked from the root file.
Initialization also creates an empty root `PROMPT.md` if missing and ensures it is ignored
in `.gitignore`, preserving existing content and avoiding duplicate ignore entries. It is
not added to generated project guidance. Supporting files are verified on every run.

Use `/aipartner-talk` to discuss an idea. It loads all skills you request before analyzing
the topic. Decisions stay in session context; it writes no notes or memory files.

For a larger feature, run `/aipartner-spec`, then `/aipartner-execute`. For a small change,
run `/aipartner-execute` alone to implement directly from the settled conversation. It tracks
progress in the session without requiring or generating specification files.

After implementation, keep requesting changes in the conversation. No separate correction
command is needed. You can describe observations across multiple messages. The agent
investigates without editing, presents conclusions and suggested corrections, and asks
whether you have finished describing the changes and authorize implementation. It waits
for explicit authorization before making corrections; each delivery starts a new collection
and authorization cycle. The initial `/aipartner-execute` invocation authorizes the initial
implementation.

For spec-based features, authorized corrections are logged in `fixes.md`, identifying
defects or changed decisions and stale requirements. The original spec and plan remain the
agreement at implementation time. For direct work without a spec, fix decisions stay in
session context and no fix log is created.

Execution and corrections update every affected project guideline, including README,
architecture documents, and root instruction files. All commands leave git writes to you.
After every implementation or correction, the final response includes a proposed commit
message following Conventional Commits and its SemVer meaning, without running the commit
or changing the project version.

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
