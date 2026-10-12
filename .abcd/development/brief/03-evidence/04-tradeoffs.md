# Trade-offs

Each row records a decision the owner made in the brief interview, the alternatives considered, and what PG-Engine gives up by choosing it.

| Decision | Alternatives considered | Cost accepted |
|---|---|---|
| **Extract the engine from the predecessor**, then the predecessor runs on PG-Engine from a separate games repository | Port the game into PG-Engine and retire the old repo; keep it standalone and re-implement it | The predecessor's game-specific coupling has to be unpicked during extraction, not avoided |
| **Milestone 1 proves two genres**: the scavenger hunt (turn-based, hidden hands, phones) and the takeover shooter (real-time, single-player) | The predecessor game alone; studio first | The studio waits for milestone 2. The generality claim is tested before creators are invited in |
| **Apple TV: AirPlay at M1, then a native display client** in its own milestone; the simulation stays on the host | A Rust core everywhere (standalone Apple TV); AirPlay only; the native client at M1 | Two renderers (web and Swift) and a display-list protocol to keep stable. Apple TV can't play without a host |
| **Data plus sandboxed JS handlers** | Data only, with new blocks arriving through engine releases; a Lua sandbox | A sandbox, a step budget and determinism shims to maintain. Handlers make review heavier for shared packs |
| **4-player co-op: shared screen by default, own device per mode** | Shared screen only; own screen each | Viewports must move between devices mid-game |
| **Couch and LAN for real-time in v1**; internet for turn-based and slow-tick games | Internet real-time in v1; couch only for ever | Friends in different homes can't play the action games in v1 |
| **AI surface: MCP and CLI first, then the built-in chat** (own key or a local OpenAI-compatible server such as Dessau), with hosted credits last | Built-in first; both at milestone 1 | Non-experts without an AI tool wait for the built-in chat |
| **One web codebase for the studio**, packaged with the server as a Tauri desktop app | Desktop-first; web only | The desktop shell is an extra build target |
| **Layered LAN security**: plain HTTP plus typed codes as the baseline; TLS through device-managed root certificates; domain certificates opt-in. This revises an earlier "paired TLS" choice after research found iOS Safari rejects self-signed certificates | Paired self-signed TLS for browsers; domain certificates as the default; a native hand app | On guests' iPhones, camera, motion sensors and wake lock are unavailable unless the host opts into domain certificates |
| **Schools self-host for under-13s**; the hosted service is 13+ | All ages on the hosted service; decide later | The hosted service is not the classroom product |
| **Pack policies:** CC0/CC-BY built-ins; AI assets labelled; clear-check publishing; federated signed indexes | Mixed-licence built-ins; unlabelled AI assets; a central gallery | No central discovery in v1. Publishing takes one extra step (record a winning run) |
| **Licence split from the first commit** (MIT, MPL-2.0, AGPL-3.0) | Everything proprietary for now; decide later | Per-directory licence bookkeeping (REUSE) from day one |
| **Gamepads are first-class for action genres** | Phones only; gamepads as an optional extra | Input rules and verification for two controller types |
| **No third-party names** (neutral codenames, game-type naming, public banlist removable by key) | Private faithful packs with names; names in the repository | Reference games can't be called by their famous names, even privately in this repository |
