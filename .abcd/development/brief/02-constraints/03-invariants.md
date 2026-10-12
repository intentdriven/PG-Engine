# Invariants

These hold for every change. Each one is guarded by a test or a lint, never by memory alone.

## Engine and pack separation

1. **Engine first.** No game's names, rules or wording appear in engine code. Game-specific verbs (scan, teleport, transfer) belong to packs, never to the server's command list.
2. **Packs carry no engine code.** A pack is data plus sandboxed handlers. A handler can reach only what the sandbox exposes.
3. **New building blocks arrive only through engine releases.** When a handler pattern recurs across packs, it graduates into an engine component, with a schema and a migration.

## Determinism

4. **One simulation for every host.** Hot-seat, LAN and hosted play run the same simulation code.
5. **Randomness only from seeded named streams.** A scan fails the build if it finds clocks, `Math.random`, timers or DOM access in the simulation or engine core.
6. **Same inputs plus same seed give the same state hash on every host.** Recordings replay identically, and that is what makes the clear check and regression replays possible.
7. **Game state is plain, serialisable data.** Save/load, network sync and rollback all depend on it.

## Privacy of views

8. **Never trust a client.** Every move is validated on the host. Phone answers are stamped with the phone's seat, not the seat the phone claims.
9. **Views are allowlists.** A seat's view lists its fields one by one. Hidden state is never sent and then hidden on the client.
10. **The wire carries keys, not text.** Every screen and hand renders in its own language.

## Stability

11. **Golden games and fingerprints change only on purpose.** That covers game-state and behaviour hashes, pixel fingerprints and sound prints, and any change to them is named in the commit.
12. **The pack format is versioned.** A manifest declares the engine range it supports. The engine ships up-migrations, so an older pack keeps loading.

## Content and IP

13. **No third-party game titles, characters or game brands** anywhere in the repository (see [`04-naming.md`](04-naming.md)).
14. **Every asset carries an SPDX licence, an author and a source.** AI-generated assets also declare their generator. The credits screen is generated from this metadata.

## Platform hygiene

15. **The audio engine is a platform concern.** One AudioContext per page, a scheduler that can't stall, suspension when the page is hidden, and verification on real iPad hardware.
16. **Touch interfaces never mention keys.**
