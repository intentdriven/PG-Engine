# Internals

The machinery the surfaces depend on. Everything here is staged. Library-level picks still awaiting an ADR are listed in [`03-evidence/03-open-questions.md`](../03-evidence/03-open-questions.md) (items 16–25).

## 1. Pack format

```
my-pack/
  manifest.json        id, version, engine range, dependencies, palette, tile size, seats, modes, state schema, licences
  prefabs/*.json       entity templates: [{component, params}]
  rules/*.json         event rules: when <event> if <conditions> do <actions>
  levels/*.txt|json    ASCII grids + legend → semantic cells → auto-tiling
  handlers/*.js        stateless sandboxed functions referenced by rules
  lang/<locale>/*.md|json   all words, by key
  art/                 indexed-colour sprites + frame and tag data (format: open question 23), palettes, skins
  audio/               tracker songs (JSON), sound-effect parameter objects
  tests/*.jsonl.gz     recordings: clear-check run, regression replays
  AGENTS.md            the pack's own manual for AI collaborators
```

- **Validation runs in two passes.** The first checks each file against the pack format's published JSON Schemas (draft: open question 19). The second is a **semantic linter**: referenced ids exist, event graphs are reachable, legends cover the grids, palettes match. The linter's messages are written to be fed back to an AI.
- **Versioning.** The manifest declares the engine range it supports, and the engine ships up-migrations for older formats.

## 2. Simulation core

- **Shape.** A pure `step(state, inputs) → state` on a fixed tick. Turn-based games are ticks that wait for prompts.
- **State.** Plain serialisable data. All randomness comes from seeded named streams.
- **Modes.** A generic sub-mode stack. Packs define the sub-modes themselves (a mini-game, a market screen, a menu), with their state, rules and handlers.
- **Prompts.** Ask/respond, with `kind` and `purpose`, is the only way the simulation asks a seat to decide.
- **Building blocks** (engine components) cover the minimal capability set of the six reference games:
  - tile maps with layers, and viewports;
  - entities with tile or box collision and projectiles;
  - A* on grids and routing on graphs;
  - state-machine AI;
  - per-seat observer filtering (fog of war, line of sight and hidden hands are one feature);
  - an economy and simulation tick;
  - dialogue and text;
  - procedural generation hooks;
  - save and load.

## 3. Handler sandbox

- **Runtime.** QuickJS compiled to WASM, with a step budget, memory and stack limits, and no I/O or clocks.
- **Determinism.** Maths runs on a fixed float32 or fixed-point policy (open question 17), plus a deterministic sort.
- **Handler shape.** Handlers are stateless. A pack declares its own state slots in a schema (for example the transfer mini-game's wire grid). The simulation owns that state and serialises it with everything else. Handlers receive a read-only slice and return actions, so snapshots, replays and hot reload stay trivial, and game rules never move into the engine.

## 4. Views and the display list

- **Views.** `view(state, seat)` builds each seat's private view from an allowlist of fields. `display(state, screen)` builds the public display list: sprites, tiles, viewports, UI panels and audio cues.
- **Protocol.** The display list is a versioned protocol. The web renderer and the Swift Apple TV client both implement it, and golden frames pin it.

## 5. Networking and pairing

- **Rooms.** The host is authoritative. Rooms and seats each have reconnect tokens, and the AI takes over absent seats.
- **Transport.** It sits behind an interface (WebSocket presumptive). Each seat receives its view; screens receive display lists.
- **Joining and security layers.**
  - **Baseline.** The QR code carries the host's LAN address and a single-use code. The same code is printed as typable text, and plain HTTP is enough to play.
  - **Managed devices.** The host generates a root certificate that a school pushes through device management. Its devices connect over TLS.
  - **Native clients.** The Apple TV client and later native apps pin the host certificate (its fingerprint is in the QR code), on the model of Dessau's paired-client port.
  - **Domain certificates.** An opt-in that needs a PG-Engine DNS and certificate service.
- **Hardening carried from the predecessor:** rate limits; origin and host checks against DNS rebinding; a static allowlist; signed cookies for password-protected hosts.
- **Internet play (v1).** Turn-based and slow-tick games only. The deterministic core keeps rollback possible later.

## 6. Rendering, audio, input

- **Renderers.** One engine core draws 2D and 3D games. A pixel-art game draws to a low-resolution target, scales it up by a whole number with nearest-neighbour filtering, then applies palette and optional CRT passes; vector and 3D games draw at the screen's own resolution. Skins are sets of atlases with the same frame names; hitboxes live in simulation units, never in skin pixels.
- **Original style and modern take.** Every game carries both as skins over one simulation: the original style, as close as possible with no original assets, and the modern take, the default. They differ in looks and sound only (resolution, aspect, 2D or 3D, palette, music); the rules, the simulation and its replays are identical, and the player switches between them at any time.
- **Audio.**
  - **Music.** A 4-voice chip tracker plays JSON songs.
  - **Sound effects.** Parameter-based synthesis, so an AI can write them.
  - **Platform rules.** One AudioContext, a scheduler that can't stall, and suspension when the page is hidden.
- **Input.** Adapters for keyboard, touch, mouse routing, gamepad and phone, all feeding the same simulation inputs. The maths in each adapter is DOM-free, so it can be tested.

## 7. Recordings and the clear check

- **Format.** Recordings are gzip JSON Lines: a header, inputs per tick, periodic state hashes, and the result.
- **The clear check.** The host replays a pack's winning run headlessly before publishing it.
- **Regression replays.** A pack's recordings rerun after every AI edit.

## 8. AI tool layer

- **One implementation, three front-ends:** the CLI, the MCP server and the studio's AI panel.
- **Model access.** The built-in panel calls any OpenAI-compatible endpoint: the creator's key, or a local server such as Dessau. Hosted credits come later.
- **AI-generated assets** pass through grid-snapping and palette reduction, and record their generator.

## 9. Pack distribution

- **Packaging.** A zip of the pack folder with a manifest; sha256 per file; a signed index.
- **Dependencies.** Resolved by engine range and version operators.
- **No central gallery in v1.**
