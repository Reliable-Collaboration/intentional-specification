---
title: "Intentional Specification"
---

# Intentional Specification

> **Intentional Specification**
> This document is self-documenting — it follows the strategy it describes. Design history: [ICD](./intentional-specification-ICD). **Completeness: Stable** — 2 open questions

## What This Is

**Intentional Specification** is a documentation strategy for specification documents. The strategy has two rules:

1. **Every specification has a paired ICD file** that captures the intentions, considerations, and decisions behind it.
2. **Every specification carries a header** that links to the strategy, links to its ICD file, and declares how complete it is.

That is the entire strategy. The rest of this document explains why it matters and how to follow it.

---

This document was authored by Matt Christenson at The Reliable Collaboration Company, learn more about Matt at https://christenson.dev/

## The Problem

Documentation decays for two reasons. The first is that decisions get made and nobody writes down *why*. Six months later, someone encounters a design choice that looks arbitrary, changes it, and inadvertently breaks something that depended on it. The second is that the reasoning that shaped a document lives only in the conversation where it was discussed — a Slack thread, a meeting, a Claude session. When that context is gone, the document becomes an orphan: it says what was decided but not why, and nobody knows which parts are settled and which are still open.

This matters more with AI co-authoring. When an AI agent helps write or revise a specification, it needs the reasoning behind existing decisions to avoid contradicting them. Without that context, the AI works from the document's surface — its text — rather than its depth — the reasoning that shaped the text. The result is plausible-looking revisions that subtly undermine decisions the author already made.

## The Paired File Pattern

Every specification document gets a companion **ICD file** (Intentions, Considerations, and Decisions). The two files serve different readers with different needs:

| File | Audience | Purpose |
|------|----------|---------|
| **Specification** | Everyone | What was decided. Concise, authoritative, designed for readers who want to understand the current state. |
| **ICD** | Authors, reviewers, AI agents | *Why* it was decided. Journal-style, captures the reasoning journey, preserves rejected alternatives and the arguments against them. |

The specification is what you read to learn the system. The ICD is what you read before you change the system.

### Naming Convention

The ICD file shares its specification's filename with an `-ICD` suffix:

| Specification | ICD File |
|---------------|----------|
| `authentication.md` | `authentication-ICD.md` |
| `api-design.md` | `api-design-ICD.md` |
| `data-model.md` | `data-model-ICD.md` |

Both files live in the same directory. This keeps the pairing discoverable — when you find the specification, the ICD is right next to it.

### Internal Title

ICD files use the title pattern: **"{Document Name}: Intentions, Considerations, and Decisions"**

Example: *"API Design: Intentions, Considerations, and Decisions"*

---

## The ICD File

An ICD file is a journal of the specification's design. It captures what was considered, what was decided, what was rejected, and why. Its structure follows a numbered-section journal style.

### Structure

**Status line** — A one-line description of the file's role.

> **Status:** ICD file for [Document Name]. Captures the reasoning journey behind the specification.

**Numbered sections** — Each section represents a significant consideration or decision. Sections accumulate as the specification evolves. They are not rewritten — new sections are added, and earlier sections are annotated if a decision is later revised.

Each section may include any combination of:

- **Context** — What was the situation or question?
- **Alternatives considered** — What options existed?
- **The decision** — What was chosen?
- **Reasoning** — Why this option over others?
- **Why this matters for the future** — What should someone know before revisiting this decision?

Not every section needs every element. A straightforward decision might be a paragraph. A contentious one might be a page.

**Unanswered Questions and Considerations** — The final section. A numbered list of open items that affect the specification's completeness. Each item carries enough context for someone (human or AI) to pick it up and make progress. When a question is resolved, it graduates into a numbered section above, and a brief note replaces it in the list:

> ~~3. Should the completeness score be a percentage or a phase label?~~ — Resolved in §4.

This section is the single source of truth for what remains open in the specification.

---

## The Completeness Header

Every document that follows Intentional Specification carries a header block immediately after the title. The header serves three purposes:

1. **Signals the strategy** — so readers know an ICD file exists
2. **Links to both documents** — the strategy and the ICD
3. **Declares completeness** — so readers can calibrate their trust

### Format

The header is a blockquote or callout placed immediately after the document title:

```markdown
> **Intentional Specification**
> This document follows [Intentional Specification](path/to/intentional-specification). Design history: [ICD](./document-name-ICD). **Completeness: Working Draft** — 3 open questions
```

Projects using static site generators may adapt this to their platform's callout or admonition syntax (e.g., `:::` containers, `[!NOTE]` blocks).

### Completeness Phases

| Phase | Meaning |
|-------|---------|
| **Outline** | Structure and section headers exist; most content is placeholder or missing. |
| **Early Draft** | Core ideas are captured in prose; significant sections remain incomplete. |
| **Working Draft** | All major sections have content; open questions are being actively resolved. |
| **Review Ready** | Content is complete; all open questions resolved; awaiting consistency review against the broader documentation. |
| **Stable** | Reviewed, internally consistent, and aligned with the rest of the project documentation. |

The open question count comes directly from the ICD file's "Unanswered Questions and Considerations" section. When a question is resolved, the ICD is updated, the count decreases, and the phase may advance.

---

## For AI Agents

ICD files are designed to be consumed by AI agents co-authoring specifications. When working on a specification:

1. **Read the ICD first.** Before proposing changes to a specification, read its ICD file to understand which decisions are settled, which alternatives were already rejected, and what reasoning led to the current state. This prevents re-litigating closed questions.

2. **Write to the ICD as you work.** When you make a decision during co-authoring — choose one approach over another, resolve an ambiguity, adopt a convention — capture the reasoning in a new numbered section of the ICD. This preserves context for the next session.

3. **Update the open questions.** When you resolve an open question, move it out of the "Unanswered Questions" list and into a numbered section. When a new question surfaces, add it to the list. Update the completeness header to match.

4. **Use the ICD for continuity across sessions.** AI sessions have finite context. The ICD is the mechanism for carrying reasoning forward. A well-maintained ICD means the next session (or the next agent) can pick up where you left off without repeating the reasoning journey.

The ICD is not a log of what the AI did. It is a record of what was considered and why — the same content a human author would write if they were documenting their own reasoning. Write it in that voice.

---

## Adopting the Strategy

### For New Documents

1. Create the specification file and its ICD file together.
2. Add the completeness header to the specification.
3. Start the ICD with a status line and at least one section capturing the initial intentions.
4. List initial open questions in the "Unanswered Questions and Considerations" section.
5. Set the completeness phase to **Outline** or **Early Draft**.

### For Existing Documents

Many existing specification documents may have been written before this strategy was adopted. They can adopt it incrementally:

1. **Create the ICD file.** Populate it with whatever reasoning history is available — from commit messages, from memory, from design conversations. Even a partial ICD is better than none.
2. **Add the completeness header** to the specification.
