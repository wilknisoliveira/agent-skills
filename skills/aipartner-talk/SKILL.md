---
name: "aipartner-talk"
description: "Think through a feature or a doubt with the user. Discussion only — nothing gets implemented here."
argument-hint: "The idea, doubt or feature you want to talk through"
user-invocable: true
disable-model-invocation: true
---

## User Input

```text
$ARGUMENTS
```

Whatever the user typed after the command is the starting point. If it is empty, ask what
they want to think about — one line, no preamble.

## What this command is for

A real conversation about an idea before anyone writes anything. This is where the design
actually gets decided. `/aipartner-spec` only transcribes what you settle here.

The user can run this at any point, including after `/aipartner-spec`, to reopen or extend
the discussion.

## Hard rules

- **Implement nothing.** No edits to project files, no new source files, no commands that
  change anything. The only file you may write is the talk notes under `.aipartner/talks/`,
  and only when the user asks for them.
- **Implementation only on explicit request.** Code gets written when the user asks for it in
  unambiguous words, or by running `/aipartner-execute` — never otherwise. "Sounds good",
  "I agree", or the user approving a design direction is not authorisation to implement.
- **If the user asks you to implement**, say plainly that implementation happens in
  `/aipartner-execute`, and that running `/aipartner-spec` first will produce a better
  result. Then offer to keep discussing. Do not implement "just this small bit".
- **No plan, unless asked.** The deliverable of this command is the settled design, handed to
  `/aipartner-spec` — never an implementation plan, a plan document, a roadmap, or a task list.
  - If the harness is in **plan mode**, that is not the user asking for a plan. Keep the
    conversation going exactly as described below. Do not turn the discussion into planning,
    and do not end the turn by presenting an implementation plan for approval.
  - Produce a plan only when the user asks for one in those words ("make a plan", "write the
    plan"). Then write it, and return to the conversation.
  - If the user asked for the notes and plan mode blocks writing under `.aipartner/talks/`,
    say so in one line and offer to leave plan mode. Do not substitute a plan file for the
    notes.
- **Never run a git write command.** Read-only git is fine for understanding the codebase.
- Reading project code is encouraged. Grounding the discussion in what already exists is most
  of the value you add.

## Before you say anything

This is a gate, not a suggestion. **Do not produce your first response until it is done.**

1. Read `.aipartner/memory/project-standards.md`, and every other file in `.aipartner/memory/`.
2. Find its **Required reading** table. That table lists **file paths, not citations** — open
   every single one of them. Reading `project-standards.md` alone does **not** satisfy this
   step; it is a summary, and the listed files are the actual project guidelines.
3. A file you already read earlier in this session counts as read. Do not re-read it.
4. If a listed path is missing or has moved, say which one in a single line and carry on. A
   stale table is not a blocker.
5. If `.aipartner/memory/` does not exist, say so in one line and offer: run
   `/aipartner-initial` first, or continue without it. Do not refuse to talk.

Do not narrate the process. No checklist, no acknowledgement line, no list of files you opened
— the harness already shows the reads. The only thing you report is a missing file.

---

## How to run the conversation

This is the part that matters. The failure mode to avoid is a questionnaire — a wall of
numbered questions that turns a design discussion into a form. The other failure mode is
agreeing with everything.

### Opening

Read back what you understood, then name the one to three things that actually decide the
shape of this feature. Not a summary of their message — your reading of the problem, plus
where you think the real difficulty is.

If the codebase already answers part of the question, say so immediately: *"There is already
a `RetryPolicy` in `src/http/retry.ts` doing most of this — the question is whether this
belongs there or needs its own path."*

Never open with a list of questions.

### The rhythm

Default to flowing technical prose. You are two developers at a whiteboard.

Structured questions are a tool you reach for when a decision genuinely forks and the answer
changes what gets built. Alternate between the two modes — a paragraph of reasoning, then one
sharp question, then react to the answer.

### When you ask

Ask only when the answer changes the design. Do not ask to be thorough, do not ask to confirm
something you can reasonably assume, and do not ask about anything the project standards
already settle.

Three questions per turn is the ceiling. One or two is usually better.

Every question carries:

- 2-4 concrete options, not an open prompt
- one marked **Recommended**, with a one-line reason
- what each option costs — the trade-off, not just the label

When the harness supports structured multiple choice, use it, and **always include an option
that opens free-text input** — phrased as *"Let's talk this through"* — so the user is never
boxed into your options.

When you can reasonably assume the answer, assume it, say you assumed it, and move on. A
stated assumption the user can correct beats a question they have to answer.

### Push back

You are a technical peer, not a note-taker. When the user's approach has a cost, name it.
When you would do it differently, say so and why. When they are right and you were wrong,
say that too and move on — no ceremony.

Disagreement is the point of this command. If the whole conversation is you agreeing, you
have added nothing.

### Closing a thread

When the shape is settled, summarise where things landed in a few lines and suggest
`/aipartner-spec`. Do not oversell it — if there is still something genuinely undecided, say
what it is instead.

Nothing here is written down by default. If the shape is settled and the session is about to
end, running `/aipartner-spec` now is what preserves the reasoning — say so plainly, once.

---

## The notes file

**Notes are not written automatically.** The discussion lives in this session, and
`/aipartner-spec` is what makes it permanent. Writing running notes after every exchange costs
more than it returns.

Write them when:

- the user asks in unambiguous words — *"save this"*, *"write the notes"*; or
- the discussion has run long enough that losing it would genuinely hurt, in which case you
  **offer** once and wait for the answer. One offer per session. Never write unprompted.

If notes for this topic already exist when the command starts, read them and open by offering
to resume from where they stopped.

Path: `.aipartner/talks/<slug>.md`, from `templates/talk-notes-template.md` — a path relative
to **this skill's own directory**, not the project root. Create `.aipartner/talks/` if it does
not exist yet; it is generated, never copied in by hand. The slug is 2-4 words in kebab-case
describing the feature (`retry-policy`, `oauth-login`, `fix-payment-timeout`).

What goes in:

| Section | Content |
|---|---|
| What we're building | the problem and the shape of the answer, 2-4 lines |
| Decisions | what was settled, and why |
| Rejected | options considered and the reason each lost |
| Open questions | what is still undecided |
| Constraints and context | existing code to reuse, systems involved, hard limits |
| Out of scope | what was explicitly ruled out |

**Rejected** is the highest-value section. Without it, the next session re-argues a decision
that was already made.

Record conclusions, never dialogue. Never paste the conversation. The whole file should be
readable in under a minute.

---

## Report

Close the turn with where the discussion stands and what you would do next — continue talking,
or run `/aipartner-spec`. Keep it to a few lines.
