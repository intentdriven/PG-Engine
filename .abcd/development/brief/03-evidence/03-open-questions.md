# Open questions

These are not decided. Each one names what it blocks. Once decided, an answer becomes an ADR and the brief is updated. Recorded risks follow the questions.

## Ownership, funding, commercial and legal

1. **Is PG-Engine publicly funded research, a private venture or a mix?** It blocks the commercial use of code extracted from the predecessor. The predecessor's record treats it as openly released research, and on that basis an employer-IP check was declined. That reasoning doesn't automatically carry over to a commercial layer.
2. **What form does the commercial layer take?** The owner may publish native store apps (Apple TV, iPad, iPhone, Android) of specific IP-free games built on PG-Engine, which would also feed back into the studio. Other lines from the predecessor's plan: hosting tiers, hosted AI credits, a share of sales. It blocks the commercial milestone and any payment integration.
3. **Contribution terms: DCO or CLA?** A CLA keeps relicensing options open for a commercial layer; a DCO is lighter. It blocks the first outside contribution.
4. **Default licence for new creator packs** (CC BY-SA 4.0, CC BY, CC0 or all rights reserved). CC 4.0's clause against technical protection measures conflicts with app-store builds. It blocks the studio's "new pack" flow.
5. **Does the hosted platform code live in a separate AGPL repository?** It blocks the hosted service's first platform-only feature.
6. **Should the owner ask the original authors or their estates for a blessing** for the scavenger-hunt, real-time-tactics and auction-economy mechanics studies? There is precedent and it costs little. This blocks nothing.
7. **Apple developer programme and distribution.** A tvOS app can't be sideloaded, so the native Apple TV client reaches other people's TVs only through TestFlight or the App Store. It blocks the native-client milestone's release.

## Product

8. **Real-time action between homes.** Which game first earns rollback or prediction over the internet, and when? It blocks nothing in v1.
9. **Order and timing of the design-conformance set.** Which future game is built first, and which hybrid capabilities (printable export, code entry, narration) enter the engine first? It blocks reference game 7.
10. **Multiplayer for `ref-takeover-shooter`.** The owner named it "possibly multiplayer later". Co-op or versus, and on which screens? It blocks nothing in v1.
11. **Answered (2026-10-07, [product principles](../01-product/01-press-release.md#product-principles), principle 5):** a skin may change resolution, aspect and 2D or 3D. The original style and the modern take differ in looks and sound only.
12. **Answered (2026-10-07, [product principles](../01-product/01-press-release.md#product-principles), principle 5):** the original style's sound is as faithful as possible without original assets; the modern take's is free.
13. **Pupils' work on a school-hosted PG-Engine with no accounts.** Where does each pupil's pack live (a per-device workspace on the host, class codes, or export and import), and how does a teacher see and collect the work? It blocks the schools milestone.
14. **Identity on the hosted service** (13+, publishing through GitHub). Is sign-in through GitHub only, or is there anonymous play? It blocks the hosted service's publishing flow.
15. **Domain-certificate service.** Who runs the PG-Engine DNS and certificate service that gives guests' phones full features, and in which milestone? It blocks secure-context features (PWA install, camera, sensors) on unmanaged devices.
15a. **Real-world map data for `ref-location-trail`.** The most complete open source (OpenStreetMap) is licensed ODbL, which is share-alike and conflicts with the CC0/CC-BY built-in library policy. Which map source, under which licence, and kept outside the built-in library? It blocks building the location trail.

## Technical: presumptive picks awaiting an ADR

Research recommends each of these. Adopting one is a recorded decision, not a default.

16. **Transport:** WebSocket behind a transport interface (challenger: WebTransport, now supported by all major browsers but needing a secure context).
17. **Renderer for 2D and 3D** (reopened 2026-10-07: 3D is in from the start). The 2D-only picks (PixiJS v8 as a render-only layer, the predecessor's Canvas2D buffers generalised, or Phaser 4) no longer cover the scope; the choice is now a renderer, or a pair, that draws pixel-art, vector and 3D games from one display list.
18. **Entity storage:** an ECS with typed-array storage (snapshot equals a buffer copy) versus the predecessor's plain-object state. The predecessor's research warned against adopting an ECS before a second game exists. Milestone 1 *is* the second game.
19. **Schema authoring and draft:** TypeScript-first (Zod 4 or TypeBox) emitting JSON Schema 2020-12.
20. **Gameplay maths:** fixed-point integers versus float32 with determinism shims, for both the core and the sandbox.
21. **Server runtime and single-binary packaging** for LAN boxes and schools.
22. **Signing tool** for pack indexes (minisign-class or alternatives).
23. **Sprite and animation metadata:** Aseprite JSON as the frame and tag format, versus a PG-Engine-native format.
24. **The Apple TV client's renderer API** (Metal versus a SpriteKit-class 2D API), its audio mixing, and its input return channel (the GameController framework over the same transport).
25. **Studio local-folder access outside Chromium.** Inside the desktop app it is solved; in Safari it means syncing through the host.

## Recorded risks

- **Determinism across runtimes.** The core runs on four different JS `Math` implementations (Node, Chromium, WebKit, Firefox), and handlers run in QuickJS. Identical per-tick hashes across all of them hold only once question 20 is settled. Until then, the cross-runtime determinism rows of the verification matrix are contingent on it.
- **Deterministic physics.** Physics is in from the start, so its step must give identical per-tick hashes on every runtime, as the rest of the core does (question 20).
- **Real-time over a display-list protocol.** Streaming display lists to a remote screen (the native Apple TV client, later) for real-time games depends on frame rate and Wi-Fi latency, with no measured budget yet. AirPlay at M1 sidesteps this. The native-client milestone has to measure it first.
- **Audio sync** between the host's simulation and a remote screen's audio cues.
- **Prompts that block joining.** The tvOS and iOS local-network permission prompts can't be checked for in advance and may block a native client's first connection.
- **Schools without device management** get only the plain-HTTP baseline: no PWA install, camera or sensors on pupils' devices.
- **Android Wi-Fi power saving** adds input latency for browser controllers. Only native apps can turn it off.
