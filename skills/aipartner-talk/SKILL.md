---
name: "aipartner-talk"
description: "Think through a feature or a doubt with the user. Discussion only — nothing gets implemented here."
argument-hint: "The idea, doubt or feature you want to discuss, and skills to use"
user-invocable: true
disable-model-invocation: true
---

## User Input

```text
$ARGUMENTS
```

The user's idea and requested skills are the starting point. If no topic is supplied, ask
what they want to think through after completing required skill loading below.

## Load requested skills first — mandatory

Before replying, analyzing the topic, or reading project context, identify and load **every
skill the user requested** for this discussion. Read each skill's instructions through the
available skill mechanism; naming it or relying on its description does not count.
Already-loaded instructions count when current. If any requested skill cannot be found or
loaded, state which one and ask how to proceed; do not silently skip it.

Use these skills to inform the discussion while preserving this command's discussion-only
boundary. A requested implementation skill does not by itself authorize code changes.

## Read project guidance

Read root `AGENTS.md` and `CLAUDE.md` when present, their Required reading, and relevant
project documents, directory instructions, and code. Already-read files count unless changed.
Report a missing required document briefly and continue with available context.
If no root guidance exists, offer `/aipartner-initial` when useful without blocking discussion.

Root `CLAUDE.md` is the standards location when it exists, otherwise root `AGENTS.md`.
When both exist, read both. If existing rules or documentation practices conflict with
aipartner guidance, explain the specific conflict and ask how to resolve it before depending
on an override. Respect existing architecture and documentation conventions.

## Discussion boundaries

- **Implement nothing.** Do not edit project files, create source files, or run mutation
  commands. Read-only code exploration is encouraged.
- **Keep decisions in session context.** Do not write talk notes, memory files, or a running
  decision log. `/aipartner-spec` is the optional way to persist a settled design.
- **Do not treat design agreement as implementation authorization.** If asked to implement,
  explain the two command paths below and let the user choose.
- **Never run git write commands.**
- **No implementation plan unless asked.** Plan mode alone is not a request for one. If asked,
  use the harness's plan tooling when available, or explain the plan in chat. Stay within
  the discussion-only boundary.
- **Use plain language.** Short sentences and familiar words, without puns or wordplay.

## Run the conversation

Open with your reading of the problem and the one to three decisions that shape the feature.
Ground it in existing code when possible. Do not open with a questionnaire or merely repeat
the user's message.

Discuss like two developers at a whiteboard: explain a trade-off, ask a focused question,
then react to the answer. Ask only when the answer changes the design. At most three questions
per turn, usually one or two. For a real fork, offer concrete options, a recommendation with
its reason, and room for free text; use structured questions when supported.
When an assumption is reasonable, state it and proceed with the discussion.

Push back on costly choices with reasons and suggest alternatives. Acknowledge when new
information changes your view. Do not agree automatically or invent requirements.

## Close a settled discussion

Summarize the agreed design and any remaining uncertainty in a few lines. If material
questions remain, continue discussing them. Otherwise explain these paths:

- `/aipartner-spec` then `/aipartner-execute`: recommended for larger features or work across
  sessions, because the specification and tasks preserve the agreement.
- `/aipartner-execute` alone: for a small change, it implements directly from this conversation
  and tracks progress in the session without requiring spec artifacts.

The user selects direct work by invoking `/aipartner-execute`; they do not need an additional
verbal implementation request. Do not implement inside `/aipartner-talk`. Mention once, when
relevant, that discussion decisions remain only in session context until specified.
