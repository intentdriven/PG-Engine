# Mental model

## A game is a pack; the engine is everything else

```
          PACK (text)                          ENGINE (code)
  ┌───────────────────────────┐      ┌──────────────────────────────────────┐
  │ manifest.json             │      │ sim core: fixed tick, seeded streams │
  │ prefabs/  (components)    │ ───► │ building blocks (components)         │
  │ rules/    (event rules)   │      │ event-rule runner                    │
  │ levels/   (ASCII grids)   │      │ handler sandbox (QuickJS-WASM)       │
  │ handlers/ (sandboxed JS)  │      │ per-seat views                       │
  │ lang/     (Markdown, i18n)│      │ renderer(s), audio, input            │
  │ art/ audio/ (assets)      │      │ rooms, pairing, phones, recordings   │
  │ tests/    (recorded runs) │      │ validator + semantic linter          │
  └───────────────────────────┘      └──────────────────────────────────────┘
```

A **pack** contains no engine code. Most of it is data, written in the engine's vocabulary:

- **prefabs:** lists of components with parameters;
- **event rules:** of the form "when X, if Y, do Z";
- **levels:** ASCII grids with a legend;
- **words:** Markdown and key-based strings;
- **assets:** sprites, palettes and audio.

Anything the vocabulary can't express goes into **handlers**. A handler is a small, stateless JavaScript function, run deterministically in a sandbox with a step budget. When many packs need the same handler, it graduates into a new engine building block in a later engine release.

## One simulation, many screens

```
                 HOST  (desktop app · hosted service · school server · LAN box)
                 runs the authoritative simulation for each room
                         │
       ┌─────────────────┼──────────────────────┬──────────────────────┐
   per-seat view     per-seat view          display list           display list
       │                 │                      │                      │
   HAND (phone)      HAND (phone)        SCREEN (browser,        SCREEN (Apple TV
   private cards,    controller,          iPad, desktop)          native client)
   orders, prompts   private inventory
```

- The **host** runs the simulation. Every client, the shared screen included, gets only what it is allowed to see: a **view** for a seat, or a **display list** for a screen.
- A **screen** draws. The browser screen and the native Apple TV client draw the same display-list protocol.
- A **hand** is a personal device bound to a seat: a guest's phone at home, a school tablet in class. It shows that seat's private information and sends that seat's input and answers.
- A **seat** is a player position in a room. A seat can be held by a person at the shared screen, by a phone, or by the AI, and can pass between them mid-game.
- **Prompts** (ask and respond) are the single way the simulation asks a seat for a decision. The same prompt reaches a human, a phone, the AI or a timeout.

## Turn-based and real-time are one clock

The simulation always runs on a fixed tick. A turn-based game is a game whose tick waits for input. Real-time and turn-based reference games share one core, and real-time is not a second engine.

## Viewports, not split-screen

Split-screen, an overview map alongside a zoomed window, a console mini-map and a player's own screen are all **viewports** onto one world. A game declares viewports. Where they are drawn (one shared screen, or a player's own device) is a per-mode choice.

## Creating a game: mock up → AI → play → publish

1. **Mock up** in the studio: paint the landscape with built-in tiles, place prefabs, press play.
2. **Ask an AI.** An external assistant edits the pack folder through PG-Engine's MCP tool layer, or the studio's built-in chat does the same through those tools. Every change is checked by the validator and the semantic linter and shown as a diff.
3. **Play** it in the studio straight away. Live reload picks up changes made on disk.
4. **Publish.** You record a winning run (the clear check), sign the pack and list it in an index you host. Anyone can install it from that index URL.
