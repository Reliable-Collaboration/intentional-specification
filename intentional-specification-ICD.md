# Intentional Specification: Intentions, Considerations, and Decisions

**Status:** ICD file for [Intentional Specification](./intentional-specification.md). Follows [Intentional Specification](https://github.com/Reliable-Collaboration/intentional-specification). Captures the reasoning behind the documentation strategy itself.

---

## 1. Why Formalize a Documentation Strategy Now

### Context

A project had already developed a natural pattern for capturing design reasoning: several "considerations and decisions" files that recorded the design journeys for key specifications. These files were valuable — they preserved why decisions were made, what alternatives were rejected, and what reasoning would need to be revisited. But the pattern was informal. Nothing connected each considerations-and-decisions file to its corresponding specification. Nothing required new specifications to have one. The files lived in a developer-facing directory, separated from the user-facing specifications they explained.

Meanwhile, the project was increasingly using AI agents as co-authors for specification documents. Each session started fresh, without the reasoning context from previous sessions. The AI would read the specification text and propose changes that were plausible on the surface but sometimes contradicted decisions that had already been carefully made — decisions whose reasoning lived only in a considerations-and-decisions file the AI hadn't been pointed to, or in a conversation transcript that had been compacted away.

### The decision

Formalize the pattern into a named strategy with explicit rules: paired files, a naming convention, a completeness header, and guidance for AI agents. Make the pairing discoverable (same directory, predictable name) so that both humans and AI agents find the reasoning context naturally.

### Why this matters for the future

If someone proposes removing the ICD requirement for "simple" documents, the question is: how do you know a document is simple before you write it? Specifications that start simple often accumulate decisions as they mature. Starting with an ICD — even a sparse one — costs little and prevents the situation where reasoning is needed but was never captured.

---

## 2. Naming: ICD Over "Considerations and Decisions"

### Context

The existing files used the suffix `-considerations-and-decisions`, which is descriptive but long. File names like `feature-considerations-and-decisions.md` become unwieldy in directory listings, editor tabs, and conversation. The suffix also suggests a purely retrospective document (considerations already considered, decisions already made), which undersells the role of the open questions section as a forward-looking tool.

### Alternatives considered

- **`-design-notes`** — too vague; could be anything
- **`-rationale`** — captures "why" but not the full scope (intentions, open questions)
- **`-decisions`** — misses the "considerations" (rejected alternatives) and "intentions" (original goals)
- **`-CAD`** — "Considerations and Decisions" abbreviated; doesn't capture intentions
- **`-ICD`** — "Intentions, Considerations, and Decisions"; captures all three aspects, three characters

### The decision

Use **`-ICD`** as the suffix. ICD stands for **Intentions, Considerations, and Decisions**, which maps to the three kinds of content the file captures:

- **Intentions** — what the author set out to achieve (the goals that shaped the specification)
- **Considerations** — what alternatives were weighed (the options that existed)
- **Decisions** — what was chosen and why (the reasoning that settles the question)

The abbreviation is part of **Intentional Specification** — the named approach to documentation. The alliterative connection between "Intentional" (the strategy) and "Intentions" (the I in ICD) is deliberate: the strategy is about making specification intentions explicit and preservable.

### Why this matters for the future

If someone encounters `-ICD` and doesn't know what it means, the completeness header on the paired specification links to this strategy document, which explains the convention. The abbreviation is opaque on first encounter but self-documenting through the linking convention.

---

## 3. Journal Style, Not Formal Structure

### Context

The existing considerations-and-decisions files all use a numbered-section journal style. Each section represents a moment of design clarity — a problem understood, an alternative rejected, a decision made. The sections accumulate chronologically (roughly) as the specification evolves. They are not rewritten when new decisions are made; instead, new sections are added, and older sections are annotated if they are later revised.

### Alternatives considered

**Structured template with fixed sections** — "Goals," "Constraints," "Decisions," "Rejected Alternatives," "Open Questions." This would make ICD files uniform and scannable. But it would also make them rigid — forcing content into categories before the reasoning naturally falls into them, and requiring authors to maintain multiple sections for each decision rather than capturing the reasoning as a coherent narrative.

**Freeform prose** — No numbered sections, just continuous narrative. This captures reasoning naturally but makes it hard to reference specific decisions ("see ICD §7" vs. "see somewhere in the middle of the ICD").

### The decision

Keep the **numbered-section journal style** from the existing files. Each section is a self-contained unit of reasoning. Sections can be referenced by number. New sections accumulate without disturbing old ones. The "Unanswered Questions" section at the end provides the structured forward-looking element that the journal body doesn't.

Within each section, use whatever sub-structure fits the content. Some sections will have "Alternatives considered / The decision / Why this matters" sub-headings. Others will be a few paragraphs of narrative. The section structure is flexible; the numbering and accumulation pattern are fixed.

### Why this matters for the future

If someone proposes a rigid template for ICD files, the question is: does the template accommodate both a one-paragraph straightforward decision and a two-page exploration of a complex tradeoff? The numbered journal style does. A rigid template either forces trivial decisions into heavyweight structure or constrains complex decisions into too-small boxes.

---

## 4. Completeness as Phase Plus Open Questions

### Context

The completeness header needs to communicate two things: how mature the specification is (phase) and how much remains unresolved (open questions). These are correlated but independent — a specification could be in "Working Draft" with zero open questions (content exists but hasn't been reviewed for consistency) or "Review Ready" with one remaining question (a minor edge case that doesn't block the review).

### Alternatives considered

**Percentage** — "75% complete." Simple and familiar. But what does 75% mean? Are all sections equally weighted? Is a specification with all sections drafted but none reviewed 100% or 50%? Percentages invite false precision and subjective disagreement about how to calculate them.

**Open question count alone** — "3 open questions." Concrete and traceable, but doesn't communicate document maturity. A specification with 0 open questions might still be an early draft if most sections haven't been written yet.

**Phase label alone** — "Working Draft." Communicates maturity but not the specific gaps. Two "Working Draft" documents might have very different amounts of remaining work.

### The decision

Use **both**: a phase label and an open question count. The phase describes overall maturity. The open question count links directly to the ICD's "Unanswered Questions and Considerations" section, making it traceable and auditable. Together they give enough information for a reader to calibrate trust without requiring them to read the ICD.

Five phases: **Outline**, **Early Draft**, **Working Draft**, **Review Ready**, **Stable**. The progression is not automatic — advancing the phase is a deliberate authorial judgment, not a mechanical consequence of the question count.

---

## 5. Colocation: ICD Alongside Its Specification

### Context

The original considerations-and-decisions files lived in a separate developer-documentation directory, away from the specifications they explained. This separation was intentional — the considerations-and-decisions files were working material, not user-facing.

### Why this was changed

The separation created a discovery problem. An AI agent (or a human reviewer) reading a specification would not naturally find the related considerations-and-decisions file in a different directory tree. The pairing was implicit — you had to know that a file with a certain name in one directory related to a specification in another.

ICD files serve both internal and external audiences. Internally, they guide AI agents and human authors. Externally, they give interested readers the reasoning behind the specification — which builds trust and helps adopters understand not just what the system does but why it works that way. Making them user-facing (colocated with the specification) is a deliberate choice: reasoning transparency is a feature, not a liability.

### The decision

ICD files live in the **same directory** as their specification. The `-ICD` suffix and the completeness header create a bidirectional link: the specification points to the ICD, and the ICD points to the specification.

### Why this matters for the future

If someone proposes moving ICD files to a separate directory (to keep the specification directory "clean"), the question is: how does an agent or reader discover the ICD? The current design makes it impossible to miss — the ICD is right there in the directory listing, and the specification's header links to it. Separation reintroduces the discovery problem that motivated this decision.

---

## 6. Self-Documentation

### The decision

The Intentional Specification strategy document follows its own rules. It has a completeness header, an ICD file, and the ICD captures the reasoning behind the strategy. This is not a special case — it is the simplest proof that the strategy works. If the strategy cannot describe itself, it cannot describe anything else.

---

## Unanswered Questions and Considerations

1. **Should the completeness header be automated?** Currently, the open question count is manually maintained — the author updates the header when they update the ICD's open questions list. A build-time script could count the non-struck-through items in the "Unanswered Questions" section and inject the count into the header. This would prevent the count from drifting. The tradeoff is build complexity vs. accuracy. Deferred until manual maintenance proves to be an actual problem rather than a theoretical one.

2. **Should ICD files be excluded from site navigation?** ICD files are useful for readers who want depth, but they may add visual clutter to navigation. Every ICD doubles the number of visible entries in its section without adding navigational value — readers discover ICD files through the completeness header in the specification, not by browsing. Projects using static site generators may want to exclude ICD files from sidebar navigation while keeping them accessible via direct links from their paired specifications.
