# Context

## Where PG-Engine comes from

PG-Engine generalises a predecessor: a single vibe-coded browser remake of a 1986 hidden-hand board-and-computer game, built in about 450 commits over ten days. The predecessor proved several things:

- one deterministic rules core can serve both hot-seat and networked play;
- phones work as private card hands for a shared screen;
- content can live as JSON and Markdown under JSON Schemas;
- golden-game hashes keep play stable while everything else changes.

It also showed where a one-game codebase strains (see [`03-evidence/02-what-didnt.md`](../03-evidence/02-what-didnt.md)). Its engine layer still carries that game's verbs, the loader hard-codes its file list, and the UI has collected in one large stylesheet and one large client file.

PG-Engine is the engine the predecessor was turning into, made explicit. **The engine is extracted from the predecessor and generalised.** The predecessor game, along with the other reference games, then lives as packs in a separate games repository and depends on a released PG-Engine version.

## The landscape (as of October 2026)

- **Data-driven game systems all have an escape hatch.** Rewrite-rule puzzle languages, room-and-dialogue makers, handheld-console studios, fantasy consoles, event-sheet tools, general game systems and the RTS/sim mod formats all hit a ceiling where data stops and code begins. The pattern that works is engine-provided building blocks as data, an event layer, and a sandboxed script for whatever is left.
- **AI authoring has converged on tool layers.** Major studios now ship MCP servers (read, patch, validate, playtest, screenshot) and in-editor assistants built on the same tools. Schema-constrained output and validate-then-apply are standard. Research on LLM-written game DSLs shows that compile rates and solvability depend heavily on examples and on error feedback from the engine.
- **Couch play with phones is proven.** Phone-as-controller and room-code party games established QR or room-code joining with a browser controller. The hidden-hand case needs a server that sends each player only their own view.
- **Hosting vendors come and go.** Several game-backend services closed in 2026. Player-hosted servers, self-hosting by schools and federated pack hosting are a hedge, not a compromise.
- **Apple TV has no browser or WebView.** Reaching it means a native app, so PG-Engine's Apple TV app is a native display client that draws what the host sends.

## Business and funding context

PG-Engine is open source, and the owner plans to apply for public funding for the open, non-commercial side. A commercial layer is intended, but its form is an open question.

- **Free hosted service.** The service hosts the engine and the studio, and creators publish games through public GitHub repositories. The predecessor's deployment runs on a free hosting tier today.
- **Open-source code.** The code is published so that others, schools first, can host PG-Engine on their own networks.
- **Native store apps (under consideration).** The owner may publish native store apps (Apple TV, iPad, iPhone, Android) of specific IP-free games built on PG-Engine. Building those apps would also feed improvements back into the studio (open question 2).
- **AI credits and a share of sales.** A predecessor monetisation plan (September 2026) adds hosting tiers, hosted AI credits and an optional share of sales as later revenue lines. This brief adopts that plan's direction as revised by the owner. The revisions are recorded in [`06-framing.md`](06-framing.md).

Whether PG-Engine counts as publicly funded research, a private venture or a mix is still open (see the open questions). It matters for the IP status of code extracted from the predecessor.
