# PG-Engine — Design Brief

PG-Engine (Party Game Engine) is an engine, a server and a design studio for retro-style 2D and 3D games. Each game is a **pack**: a folder of JSON, Markdown and assets, with small sandboxed handlers where data alone can't express the rules. Everything else comes from the engine and is served by the server: rendering, simulation, input, audio, networking, phones as private hands, and the studio.

Conventions for this brief, including the truth rule and the naming rule for third-party games, are in [`00-meta.md`](00-meta.md).

## Navigation

| Folder | Purpose |
|---|---|
| [`01-product/`](01-product) | Why and what: press release, context, mental model, scope, personas, framing |
| [`02-constraints/`](02-constraints) | Locked decisions: platform, dependencies, invariants, naming |
| [`03-evidence/`](03-evidence) | What worked, what didn't, open questions, trade-offs |
| [`04-surfaces/`](04-surfaces) | What people touch: shared screen, hand, studio, host, CLI and MCP, pack index, display client |
| [`05-internals/`](05-internals) | The machinery those surfaces depend on |
| [`06-delivery/`](06-delivery) | Build sequence (milestones), verification matrix, out of scope |
| [`glossary/`](glossary) | The canonical terms |

## Reading order

1. [`01-product/01-press-release.md`](01-product/01-press-release.md): the press release, and the product principles that decide what wins when goals clash.
2. [`01-product/03-mental-model.md`](01-product/03-mental-model.md): packs, the engine, hosts, screens and hands.
3. [`02-constraints/01-platform.md`](02-constraints/01-platform.md): what is locked.
4. [`06-delivery/01-build-sequence.md`](06-delivery/01-build-sequence.md): the order things ship in.
5. [`03-evidence/03-open-questions.md`](03-evidence/03-open-questions.md): what is still to be decided.
