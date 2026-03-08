# Intentional Specification

A documentation strategy that pairs every specification with a record of the reasoning behind it.

## The Strategy

Intentional Specification has two rules:

1. **Every specification has a paired ICD file** — an *Intentions, Considerations, and Decisions* file that captures the reasoning journey behind the specification.
2. **Every specification carries a header** — linking to its ICD file and declaring how complete the document is.

The ICD file preserves *why* decisions were made, what alternatives were rejected, and what questions remain open. This context prevents future authors (human or AI) from inadvertently undoing carefully reasoned decisions.

## For AI Agents

If you arrived here from a link in an ICD file's status line: read the [full specification](./intentional-specification.md), particularly the **"For AI Agents"** section, before editing the specification or ICD you were working on. It explains how to read, write, and maintain ICD files correctly.

## Files

| File | Purpose |
|------|---------|
| [intentional-specification.md](./intentional-specification.md) | The strategy specification (start here) |
| [intentional-specification-ICD.md](./intentional-specification-ICD.md) | Design history for the strategy itself |
| [CLAUDE.md](./CLAUDE.md) | Key conventions for AI agents working in this repository |

The specification is self-documenting — it follows the strategy it describes.

## Quick Start

To adopt Intentional Specification in your project:

1. Create your specification file (e.g., `authentication.md`)
2. Create a paired ICD file with the `-ICD` suffix (e.g., `authentication-ICD.md`)
3. Add a completeness header to the specification linking to both the strategy and the ICD
4. Capture your design reasoning in the ICD as you write

See the [full specification](./intentional-specification.md) for details on file structure, completeness phases, and guidance for AI agents.

## License

Apache 2.0 — see [LICENSE](./LICENSE).

## Attribution

This document was authored by Matt Christenson at The Reliable Collaboration Company, learn more about Matt at https://christenson.dev/