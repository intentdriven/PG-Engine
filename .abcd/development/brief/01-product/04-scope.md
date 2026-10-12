# Scope

## The three products in one repository

| Product | What it is | Staged form |
|---|---|---|
| **Engine** | Simulation core, building blocks, handler sandbox, views, renderers, audio, input | A TypeScript library. The web renderer is part of it; the native Swift display client lives alongside |
| **Server** | Rooms, seats, per-seat views, phone pairing, pack loading, recordings, the hosted service | Runs in the desktop app (Tauri), on a school server, on any LAN box, or as the hosted service |
| **Studio** | Landscape and tile editor, prefab placement, play-in-editor, AI tool layer, publishing | A single web codebase served by the server, packaged with the server as the desktop app |

## Reference games

The engine is accepted when it can express these six games as packs. They go by neutral codenames (see [`02-constraints/04-naming.md`](../02-constraints/04-naming.md)), and their packs live in a separate games repository.

| Codename | What it is | Capabilities it proves |
|---|---|---|
| `ref-scavenger-hunt` | Turn-based island treasure hunt for up to 4 players: robots, hidden card hands, a scanner hint, random global events. This is the predecessor game | Turn system, hidden per-seat information, phones as hands, multiple viewports, prompts, AI seats |
| `ref-takeover-shooter` | Single-player real-time top-down shooter on a multi-deck ship. Taking over a robot means winning a timed circuit mini-game | Scrolling tile map, collision and projectiles, line of sight, state-machine AI, a sub-mode stack |
| `ref-capture-the-flag` | 2-player top-down tank combat on a large scrolling map: capture the enemy flag, rescue prisoners, avoid mines and turrets | Split viewports on one screen, local real-time multiplayer, chase AI |
| `ref-coop-adventure` | 4-player co-op action-adventure: puzzles that scale with player count, rivalry over loot, and a shrink mechanic that changes which paths are walkable, in procedurally arranged dungeons | Four viewports, shared screen with optional own-device play, dialogue, saves, two collision scales, procedural generation |
| `ref-real-time-tactics` | 2-player real-time tactics: command units from a base under fog of war, using radar, scouts and remotely piloted drones | Per-player visibility (fog), remote play, grid pathfinding, unit AI |
| `ref-transport-economy` | Large-map railway economic sim: stations with catchment areas, trains, supply and demand, a stock market, rival companies | Economy tick, routing on a track graph, heavy UI panels, save/load, AI rivals |

## Design-conformance set (future reference games)

These games aren't built in v1, but the engine's design is checked against them. Every design decision (pack format, components, views, display list, input, joining) must leave each one expressible without a rewrite. They later become reference packs for testing. Their order is open question 8.

| Codename | What it is | What it demands of the design |
|---|---|---|
| `ref-auction-economy` | 4-player colony economy: land grants, producing and trading resources, and simultaneous real-time auctions. Players compete but the colony must survive | Simultaneous private input from phones (bidding), a shared market sim, a mix of turn-based and real-time phases |
| `ref-hidden-roles` | Social deduction: each device holds a private role and ballot, and the screen narrates timed discussion and voting. Non-violent themes for schools | A different role per device, voting, timers, spoken narration |
| `ref-asymmetric-relay` | Asymmetric co-op: one player sees the "device", the others hold different manuals or control panels and must talk to win | Different views per device, printable or exported manuals, procedurally generated rules, audio cues |
| `ref-case-file` | Investigation and deduction: printed cards with QR codes and typable codes, private results on the phone, deduction grids. Pupils can write cases as packs | Code entry (QR optional), printable export, an event graph triggered by scans, private results |
| `ref-eco-sim` | Ecology and economy simulation: managing a shared environment where players' economic choices change the ecosystem | Simulation ticks over linked systems, charts and reports, cooperative versus competitive scoring |
| `ref-settlement-trading` | Settlement-building board game: a hex map, dice-driven resource production, trading between players, building | Hex topology, private hands of resources, trade negotiation between seats, a physical or printable board |
| `ref-hidden-movement` | One versus many: one player moves in secret across a transit network, and the others deduce and close in from partial reveals | Hidden movement with timed reveals, routing on a graph, asymmetric sides, private moves on one seat's device |
| `ref-hide-and-seek` | One versus many, the reverse of hidden movement: one seeker on the shared screen hunts many hiders, each of whom sees only their own surroundings on their own device | Real-time, low-latency phone input; a different view per role; optional motion controls |
| `ref-location-trail` | Exploring real places: either a journey across a real map (a historical route with resources, hazards and choices along the way) or a walk through a specific city, with checkpoints found on site | Real-world map data, optional geolocation, code or QR checkpoints, offline queuing with later sync, printable checkpoint sheets |
| `ref-grand-strategy` | Large-scale wartime strategy board game for 2–5 players in two alliances: territories on a world map, many unit types, production funded by income, multi-phase turns and dice-resolved battles. Hosted in a later version | A territory-graph map, turns of many ordered phases, a production economy, mass combat resolution, team seats that each control several powers, sessions saved and resumed over several evenings, heavy UI panels |
| `ref-explore-and-conquer` | Turn-based world conquest: explore a hidden map, capture cities, set what each city builds, and move armies, ships and planes against AI rivals | Fog of war on a large generated map, per-city production, many unit types, AI rivals, long games saved and resumed |
| `ref-secret-orders` | Up to four players plot their moves in secret at the same time; all orders then resolve together | Simultaneous secret orders entered on each player's own device, order resolution, per-player fog of war |
| `ref-real-time-global` | Two commanders fight a real-time war on a world map, managing oil, production and transport | Real-time strategy at world scale, supply lines, two players in different homes (real-time between homes is deferred in v1) |

### Design rules drawn from the hybrid-games research

- **The app does the chores, not the core activity.** Automate the bookkeeping that is pure labour. Keep the table talk.
- **Speak rather than show.** Audio narration keeps eyes on the table, not on a screen.
- **The camera is a convenience, never a requirement.** Every QR code has a typable short code.
- **A game must outlive its vendor.** A self-hosted pack is complete on its own, with no dependency on any external server.

## Capabilities in scope (staged)

- **World:** tile maps with layers and auto-tiling from semantic cells; ASCII-grid levels; square and hex topologies; viewports; a camera and scrolling.
- **Simulation:** a fixed-tick deterministic simulation; seeded named streams; serialisable state; save and load; a sub-mode stack; prompts.
- **Gameplay:** entities with tile or box collision and projectiles; A* on grids and routing on graphs; state-machine AI; line of sight and per-seat observer filtering (fog and hidden hands are one feature).
- **Recreating:** every game in its original style and a modern take (the default), switchable by the player, differing in looks and sound only.
- **Presentation:** renderers for 2D and 3D (pixel-perfect integer scaling, palettes and art styles where a game chooses pixel art); a 4-voice chip tracker plus parameter-based sound effects; input from keyboard, touch, mouse, gamepad and phone.
- **Multiplayer and phones:** rooms, seats, QR plus room-code joining, layered LAN security (plain HTTP plus short codes as the baseline; TLS on managed devices), reconnect tokens, the AI taking over absent seats; recordings and replays.
- **Packs:** a pack format with a manifest, JSON Schemas and a semantic linter; the handler sandbox; signed federated pack indexes; the clear check.
- **Studio and AI:** the studio, and the AI tool layer (CLI and MCP first, then the built-in chat using the creator's own key or a local OpenAI-compatible server).
- **Platforms:** the desktop app, iPad as a PWA, and the Apple TV native display client.

What is explicitly *not* in scope is listed in [`06-delivery/03-out-of-scope.md`](../06-delivery/03-out-of-scope.md).
