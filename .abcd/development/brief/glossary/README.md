# Glossary

The canonical terms. A pack can't redefine them.

| Term | Meaning |
|---|---|
| **pack** | A game: a folder of JSON, Markdown, assets and sandboxed handlers, described by a manifest. It contains no engine code |
| **manifest** | A pack's `manifest.json`: id, version, engine range, dependencies, palette, tile size, seats, modes, the pack's state schema and licences |
| **prefab** | An entity template in a pack: a list of engine components with parameters |
| **component** | An engine building block (collision, AI state machine, inventory, …). New components arrive only through engine releases |
| **event rule** | Data of the form "when this event, if these conditions, do these actions" |
| **handler** | A stateless JS function in a pack, run in the QuickJS-WASM sandbox, used where data can't express a rule. It reads state and returns actions; it holds no state itself |
| **level** | An ASCII grid plus a legend that maps characters to semantic cells |
| **semantic cell** | What a map cell *is* (water, wall, grass). The engine auto-tiles cells into graphics |
| **skin** | An art style: atlases with the same frame names, palettes and optional shader passes. It never changes the simulation |
| **host** | Whatever runs the authoritative simulation: the desktop app, a school or LAN server, or the hosted service |
| **room** | One running game on a host |
| **seat** | A player position in a room. It can be held by a person at the screen, by a phone or by the AI, and can pass between them |
| **hand** | A personal device (a phone, or a school tablet) paired to a seat. It shows the seat's view and sends its input and answers |
| **screen** | A device that draws the public display list: a browser or the Apple TV display client |
| **view** | The allowlisted private data the host sends to one seat |
| **display list** | The versioned description of what a screen draws and plays; it contains only public data |
| **viewport** | A window onto the world. Split-screen, an overview with a zoom window, and a player's own screen are all viewports |
| **tick** | One fixed simulation step. A turn is a tick that waits for prompts |
| **prompt** | The simulation's ask/respond call to a seat (`kind`, `purpose`), answered by a person, a phone, the AI or a timeout |
| **stream** | A seeded, named source of randomness. Streams are the only randomness the simulation has |
| **sub-mode** | A mode pushed on top of the current one: a mini-game, a market screen or a menu |
| **recording** | gzip JSON Lines: a header, inputs per tick, periodic state hashes and the result |
| **clear check** | Proof that a pack can be won: a recorded winning run, replayed on the host before publishing |
| **index** | A signed, static `index.json` listing packs. Anyone can host one |
| **pairing** | Binding a device to a host and a seat by QR code or typed short code. TLS is added where trust is established: a root certificate on managed devices, a pinned fingerprint for native clients, or a domain certificate |
| **reference game** | One of the six `ref-*` packs in scope. Expressing them all is the engine's acceptance test |
| **design-conformance set** | The future `ref-*` games the design is checked against before they are built. A design that can't express one of them is rejected |
