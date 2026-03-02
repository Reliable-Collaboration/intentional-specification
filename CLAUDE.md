# CLAUDE.md

## Project Overview

This repository defines **Intentional Specification**, a documentation strategy for pairing specification documents with ICD (Intentions, Considerations, and Decisions) files that capture design reasoning.

## Repository Structure

- `intentional-specification.md` — The strategy specification (follows its own rules)
- `intentional-specification-ICD.md` — The ICD file for the strategy itself
- `LICENSE` — Apache 2.0

## Key Conventions

- **Paired files:** Every specification has a companion `-ICD` file in the same directory. Both files link to each other.
- **Completeness header:** Every specification carries a blockquote header after the title declaring the strategy, linking to the ICD, and showing a completeness phase + open question count.
- **Completeness phases:** Outline → Early Draft → Working Draft → Review Ready → Stable.
- **ICD structure:** Status line, numbered journal-style sections (not rewritten, only appended), and an "Unanswered Questions and Considerations" section at the end.
- **Open question tracking:** The ICD's final section is the source of truth for what remains unresolved. Resolved questions get struck through with a reference to the section where they were resolved.

## Working With These Files

- **Read the ICD before modifying a specification.** Understand which decisions are settled and why before proposing changes.
- **Write to the ICD when making decisions.** Add a new numbered section capturing context, alternatives, the decision, and reasoning.
- **Keep open questions current.** Resolve items by graduating them to numbered sections; add new questions as they surface.
- **Update the completeness header** when the open question count or document maturity changes.
- **Do not rewrite existing ICD sections.** Append new sections instead. Annotate older sections if a decision is later revised.
