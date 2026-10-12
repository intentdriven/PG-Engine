# Dependencies

## Locked

| Dependency | Role | Notes |
|---|---|---|
| QuickJS (WASM build) | Handler sandbox | Interrupt handler, memory and stack limits. Every client runs the same compiled sandbox, which narrows cross-engine maths drift for handlers. The core's maths policy is open question 20 |
| Tauri | Desktop app shell | Packages the server plus the studio. Named in the studio option the owner chose |
| Swift and Apple frameworks (Metal or SpriteKit-class 2D, GameController, AVAudio) | Apple TV display client | Draws the display-list protocol. It contains no simulation |
| JSON Schema (published) | Contract for every pack file | Read by validators, by AI structured output and by the studio's forms. Draft and authoring tool: open question 19 |
| An OpenAI-compatible chat endpoint | Built-in studio AI | The creator's own API key, or a local server such as Dessau. No vendor lock-in |
| Git hosting (GitHub first) | Where creators publish packs and indexes | Federated: any HTTPS host works |
| Signed pack indexes | Pack index and pack integrity | Signing tool: open question 22 |

## Carried from the predecessor (to be extracted, not re-invented)

- the deterministic simulation core and its runner;
- seeded named streams;
- the ask/respond prompt protocol;
- per-seat view filtering (allowlisted fields);
- the room server with its hardening: rate limits, origin and host checks, a static-file allowlist;
- the phone relay and seat tokens;
- recordings (gzip JSON Lines);
- the content loader, schema validator, i18n and Markdown renderer;
- the 4-voice chip tracker and the sound-effect synth;
- the input adapters (keyboard, touch, mouse routing, gamepad);
- the software-canvas pixel fingerprints;
- the golden-game hashes.

## Rejected (research-derived)

These come from the research's "not worth adopting" findings. The owner hasn't ruled on each one individually, and any of them can be reopened through an ADR.

| Rejected | Reason |
|---|---|
| A game framework that owns the loop and scenes | The simulation must stay separate from rendering, so the Swift client can draw the same display list |
| boardgame.io as a dependency | In maintenance mode. PG-Engine copies its patterns (moves, phases, `playerView`), not its code |
| Lua and other VMs for handlers | AI writes them less reliably, and their App Store standing is unclear |
| Lockstep or rollback for hidden-information games | They leak hidden state to every peer |
| A WebGPU-only renderer | Nothing a 2D pixel game needs requires it |
| Training a pixel-art model | Vendors with APIs and MCP servers exist and carry the provenance risk |
| OCI or Sigstore for pack distribution | Too heavy for creators and schools |
| A rigid-body physics engine | No reference game needs one. Tile and box collision is enough |
