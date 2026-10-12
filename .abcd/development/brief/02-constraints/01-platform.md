# Platform

Locked decisions only. Library-level picks that research recommends but the owner has not yet adopted are listed as *presumptive picks* in [`03-evidence/03-open-questions.md`](../03-evidence/03-open-questions.md).

## Languages and runtimes

| Layer | Locked choice | Why |
|---|---|---|
| Engine, server, studio | **TypeScript**, run as ES modules in browsers and on a server-side JS runtime | Extracted from the predecessor's JS. One simulation runs on every host, and AI writes it reliably |
| Pack handlers | **JavaScript run in QuickJS compiled to WASM**, stateless, with a step budget, memory and stack limits, no I/O, and deterministic maths shims | Deterministic and safe for community packs, the language AI writes most reliably, and App Store guideline 4.7 allows downloaded JS games |
| Apple TV | **AirPlay** from an iPad or Mac first, then a **native Swift display client** (its own milestone) that draws the display-list protocol, plays audio cues and sends input back | tvOS has no browser or WebView. The simulation stays on the host |
| Desktop app | **Tauri** packaging of the server plus the studio | Hosts the LAN server without a terminal and gives full local-folder editing |
| iPad, phones, tablets | Browser (Safari or Chrome). The iPad as a shared screen runs as a Safari tab, or as a PWA on TLS hosts | No install for hands. Play never needs a secure context. The PWA, camera and sensor features need TLS (see Network) |

## Human languages

- **British English is the default** for PG-Engine's own screens, its docs, and every pack that names no language.
- **German and Japanese are the first two further languages, from the start.** PG-Engine's own screens ship in all three
  from the first release.
- **Japanese sets the bar for text.** Fonts carry Japanese characters in both pixel and vector styles, lines break
  without spaces, and the studio accepts Japanese text input.
- **Each screen and hand picks its own language** (invariant 10). A game that lacks a player's language falls back to
  British English.

## Hosts

The authoritative simulation runs on a **host**, which can be any of:

- the desktop app;
- a school or LAN server;
- the hosted service.

The same server code runs in all three, and no feature needs the hosted service.

## Network

- **Couch and LAN first.** Real-time action games run on one host, with phones or gamepads as controllers. Over the internet, v1 serves turn-based and slow-tick games. The simulation stays deterministic, so rollback for internet real-time play can be added later without a rewrite.
- **Layered LAN security.** iOS Safari rejects self-signed certificates outright, so a guest's browser can't be paired over TLS without a root certificate installed on the phone. The LAN works in three layers:
  1. **Baseline: plain HTTP plus typed short codes.** This always works. Joining, play and hands need nothing that requires a secure context, and every QR code has a short code printed beneath it that can be typed instead.
  2. **Managed devices: full TLS.** A school, or any managed fleet, pushes the host's root certificate through device management. Devices then get secure-context features: service worker and PWA install, wake lock, camera, motion sensors and WebTransport.
  3. **Domain certificates.** A real certificate under a PG-Engine domain (the model media-server products use for LAN HTTPS) is an opt-in for hosts that want full features on guests' phones. It is never required for self-hosting.

  Native clients (the Apple TV display client, and later native hands or store apps) pin the host certificate directly, as Dessau's paired-client port does.
- **Secure-context features are enhancements.** No pack may *require* the camera, motion sensors, wake lock or vibration (iOS has no vibration). A pack may offer them when the device has them.
- **Server-authoritative with per-seat views** is the network model for every reference game. Hidden-information games never use lockstep or rollback, because those require every peer to hold the full state.

## Screens supported at milestone 1

Desktop browser (PC, Mac), iPad Safari (a tab; a PWA on TLS hosts), and Apple TV through AirPlay. The native Apple TV display client and the desktop app follow in later milestones (see the build sequence).

## Licences (adopted from the first commit)

| Part | Licence |
|---|---|
| Pack format: schemas, the format spec, the validator and tooling | MIT |
| Engine and studio | MPL-2.0 |
| Hosted platform code (accounts, gallery services, hosted-only features) | AGPL-3.0 |
| Built-in asset library | CC0 or CC-BY only. No share-alike or GPL assets |
| Licence metadata | SPDX expression per asset, REUSE-compliant repository |

Each directory carries its own licence, recorded REUSE-style. Contributions follow the human sign-off rule: AI-assisted commits carry `Assisted-by:`, and only a human signs off. The specific contribution mechanism (DCO or CLA) is an open question.
