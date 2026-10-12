# Build sequence

The roadmap is driven by intents, and each phase ends in a milestone. Order sets priority. The roadmap carries no dates. Open-question numbers refer to [`03-evidence/03-open-questions.md`](../03-evidence/03-open-questions.md).

## M0: Foundations

- **The repository:** the licence split (REUSE), the naming guard (hashes-only banned-names test plus the private banlist), and a test runner that discovers tests.
- **The pack format, v0:** manifest, pack-declared state schema, schemas, validator and semantic linter, written for AI feedback.
- **Languages:** PG-Engine's own strings and the pack format's language files in British English (the default), German and
  Japanese, with fonts that carry Japanese characters.
- **ADRs** for the technical presumptive picks needed by M1 (open questions 16–21).
- **Milestone:** an empty pack validates. A deliberately broken pack produces linter messages an AI can act on.

## M1: The engine is real (extraction plus the scavenger hunt)

- **Engine extraction from the predecessor:** simulation core, runner, streams, prompts, views, room server and hardening, phone relay, recordings, chip audio, input adapters, fingerprints. Game verbs are moved out of the engine as they go.
- **`ref-scavenger-hunt` as a pack** in the games repository. Turn-based play, hidden hands on phones, AI seats. During M1 the pack may depend on PG-Engine by path. From M1's end it depends on a released PG-Engine version.
- **Joining:** QR code plus typed short code over plain HTTP.
- **Screens:** the web renderer in desktop browsers and in iPad Safari (as a tab), and Apple TV through AirPlay from an iPad or Mac, in British English, German and Japanese.
- **CLI tools:** `validate`, `replay`, `clear-check`, `screenshot`.
- **Milestone:** the scavenger hunt plays end to end as a pack on desktop and iPad, and on Apple TV through AirPlay. Phones work as hands. The golden games and replays are green.

## M2: Second genre (real-time)

- **`ref-takeover-shooter` as a pack:** real-time single-player with scrolling, collision, line of sight, state-machine AI, and the transfer mini-game as a pack-defined sub-mode with pack-declared state.
- **3D, proved by the modern take:** the takeover shooter's original style is 2D; its modern take, the default, is a
  3D ship. The engine core serves both, and the player switches between them.
- **Gamepad input**, which is first-class for action genres.
- **The desktop app** (Tauri) hosting the server.
- **TLS for managed devices** (a root certificate pushed through device management) and the iPad shared screen as a PWA on those devices.
- **Milestone:** both genres run on one engine with no game verbs in engine code, and the takeover shooter plays in
  its 2D original style and its 3D modern take. Replays are green on every host.

## M3: Studio and the AI tool layer

- **Studio:** landscape painting with semantic cells and auto-tiling; the built-in CC0/CC-BY library; prefab forms from the schemas; play-in-editor; live reload.
- **MCP server** over the shared tool layer, plus the pack `AGENTS.md` and `llms.txt` manuals.
- **Publishing:** the clear check, signing, the federated index, and installing a pack from a URL.
- **Milestone:** Alice builds and publishes a small new game from a starter template, with an external AI tool, without touching engine code.

## M4: Native Apple TV display client

- **Display-list protocol v1**, pinned by golden frames that both the web renderer and the Swift client render.
- **The Swift client:** renderer, audio cues, an input return channel (Siri Remote and gamepads), and certificate pinning.
- **Measured before release:** frame rate and input-to-screen latency on Wi-Fi.
- **Distribution:** through the Apple developer programme (open question 7).
- **Milestone:** both reference games play on Apple TV through the native client within the measured latency budget.

## M5: Couch real-time multiplayer

- **`ref-capture-the-flag`:** two local players with split viewports, using gamepads or phones.
- **`ref-coop-adventure`:** four players, shared screen by default, with viewports moving onto a player's own device per mode; dialogue; saves; two collision scales; procedural dungeons.
- **Milestone:** four players on one LAN play the co-op adventure, and the Wi-Fi latency is measured against a recorded budget.

## M6: Built-in AI and the asset pipeline

- **The studio's AI panel** on the shared tool layer, with the creator's own key or a local OpenAI-compatible server (Dessau).
- **The AI art intake:** grid-snapping, palette reduction, generator labels.
- **Milestone:** a creator builds a game with the built-in panel against a local model, without a cloud key.

## M7: Remote play and simulations

- **`ref-real-time-tactics`:** per-player fog over LAN and internet (server-authoritative).
- **`ref-transport-economy`:** economy tick, graph routing, heavy UI, save and load.
- **Internet rooms** for turn-based and slow-tick games on the hosted service.
- **Milestone:** all six reference games run as packs. The engine's acceptance claim is met.

## M8: Schools pilot

- **Pupil workspaces** on a school-hosted PG-Engine (open question 13).
- **Milestone:** Bob's class builds a game on a school-hosted PG-Engine with a local model and no accounts.

## Later (to be decided)

- **The commercial layer** (open question 2).
- **The design-conformance set as built packs** (open question 9).
- **Internet real-time action** (open question 8).
