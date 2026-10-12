# Surfaces

Everything a person touches. Every surface is staged.

| Surface | Who uses it | What it is |
|---|---|---|
| Shared screen | Carol, players | The game's main display: a browser (desktop, or iPad Safari; a PWA on TLS hosts), Apple TV via AirPlay, and later the native Apple TV display client |
| Hand | Players | A personal device (phone or school tablet) bound to a seat: private view, prompts and controls |
| Studio | Alice, Bob's pupils | Design, AI-assisted editing, play-in-editor, publishing |
| Host | Carol, Bob | The desktop app or server that runs rooms and pairing |
| CLI and MCP | Alice (with her AI), CI | The tool layer the studio is built on |
| Pack index | Alice, everyone installing packs | A signed, federated list of packs |
| Hosted service | Alice, the public | The free hosted studio and rooms for public games published on GitHub |

## Shared screen

- **Lobby.** Shows the pack's title screen, a QR code (host address plus certificate fingerprint plus a single-use code) and the seats. Seats can be held by a person at the screen, a phone or the AI.
- **Game.** The screen draws its display list (the public world). Viewports may split the screen, for example two tank players, or an overview map plus a zoom window.
- **On the native Apple TV client (its own milestone).** It holds no simulation. It sends input back to the host over the same transport (Siri Remote and gamepads through the GameController framework). If the host connection drops, it shows a paused state rather than guessing. Until it ships, Apple TV shows games through AirPlay.

## Hand

- **Joining.** Scan the QR code, or type the short code printed beneath it, then choose a seat. On a managed device (or a host with a domain certificate) the connection is TLS and secure-context features switch on.
- **During play.** The hand shows only that seat's view: cards, orders, inventory, prompts and private viewports. It sends input and answers. It never mentions keys.
- **Disconnects.** The reconnect token survives sleep. After a grace period the seat falls back to the shared screen or the AI, and the seat can be reclaimed.
- **Own device.** A player can take a viewport onto their own device when the mode allows it (in `ref-coop-adventure`, splitting up from the group).

## Studio

- **Landscape first.** Paint terrain with semantic cells (water, grass, wall). The engine auto-tiles them from the built-in tilesets. A new game opens on a 2D pixel default and paints at once; the art kind (SVG pixel squares, free vector art or pixel images), 2D or 3D, the palette and the tile size are choices found later, then fixed per pack.
- **Placing.** Prefabs come from the built-in library or the pack itself and are configured through forms generated from the schemas.
- **Play.** One key toggles between editing and play in the same window. Live reload picks up changes made on disk by any tool, including an external AI.
- **AI panel (staged after MCP).** The creator gives an instruction, the AI proposes a patch, the validator and linter check it, the studio shows a diff, and the change is applied as one undoable step. The panel works with the creator's own API key or a local OpenAI-compatible server (for example Dessau on a school network).
- **AI art intake.** Generated art is labelled with its generator. In a pixel-art game it is also snapped to the pixel grid and reduced to the pack palette.
- **Publishing.** Record a winning run (the clear check), sign the pack, and push it to the creator's own repository and index.

## Host

- **The desktop app.** Install, open, done. It hosts rooms, serves the studio and screens, and runs pairing. A status view shows the paired devices, the rooms and the LAN address.
- **Headless server mode** for school servers and LAN boxes, with the same code.
- **Recordings** are optional and owner-only.

## CLI and MCP

One tool layer, three front-ends: the CLI, the MCP server and the studio's AI panel. Its tools:

| Tool | What it does |
|---|---|
| `read` / `search` | Read or search a pack |
| `patch` | Propose a change to a pack |
| `validate` | Schema checks plus the semantic linter. Messages are written for AI |
| `playtest start` / `stop` | Run the pack |
| `input` | Simulate input during a playtest |
| `screenshot` | Capture the current frame |
| `console` | Read the playtest console |
| `replay` | Replay a recording headlessly |
| `clear-check` | Check that a recorded winning run still wins |
| `docs` | The pack format manual, served as `AGENTS.md` and `llms.txt` |

**Write tools touch only the creator's own pack.** Text from third-party packs is labelled as untrusted, as a guard against prompt injection.

## Pack index

- **Format.** A static `index.json` over HTTPS, signed. Each entry carries: id, version, engine range, dependencies (required, optional or incompatible, with version operators), sha256 per file, SPDX licences, and the clear-check recording.
- **Where it lives.** GitHub is the default home and the place to start; anyone can host an index elsewhere, a school server included. The studio and hosts install packs from an index URL.

## Hosted service

- The same server and studio, run publicly. It is free for public games published through GitHub.
- It is for users aged 13 and over.
- It needs only a licence to host and display games, and has a published notice-and-takedown process.
