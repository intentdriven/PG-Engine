# Verification matrix

Each claim is listed with the check that proves it and when the check runs. A capability is done only when its check is green.

| Claim | Verification | Runs |
|---|---|---|
| Determinism (invariants 4–6). Cross-runtime identity is contingent on open question 20 | Forbidden-globals scan of the simulation and engine core; golden games with state and behaviour hashes; the same recording replays to identical per-tick hashes on Node, Chromium, WebKit and Firefox | Every change |
| Handler sandbox | Escape tests (no I/O, no clocks, no globals); step-budget exhaustion halts cleanly; memory limit; the same results inside and outside the sandbox | Every change |
| Views are private (invariants 8–9) | For each reference pack, assert that no field outside a seat's allowlist appears in its view; forged seat stamps are rejected; fuzzed client messages | Every change |
| Display-list protocol | Golden frames rendered by the web renderer, and by the Swift client in its own test suite, from the same display lists | Every change (web); every client build (Swift) |
| Pixel art and skins | Pixel fingerprints through the software canvas; integer scaling at common device-pixel ratios | Every change |
| Audio | Sound prints; the scheduler survives stalls; suspend and resume when hidden; **manual check on real iPad hardware** | Every change, plus manual at each milestone |
| Pack format | Schema plus linter on every reference and starter pack; deliberately broken fixture packs produce the expected AI-readable messages; up-migrations load packs in older formats | Every change |
| Clear check | The publish path rejects a pack whose recorded winning run doesn't win on the host | Every change |
| Joining and TLS | Every reference pack is playable over plain HTTP with typed codes only (no secure-context API used on the play path); on a device with the root certificate the service worker registers; the Apple TV client refuses a host whose certificate doesn't match the pinned fingerprint | Every change, plus a real-device check at each milestone |
| Reconnection | A hand that drops and returns within the grace period keeps its seat; after the grace period the seat falls back and can be reclaimed | Every change |
| Server hardening | Rate limits, origin and host checks, static allowlist (carried over from the predecessor's security tests) | Every change |
| LAN latency (couch real-time) | Phone and gamepad input-to-screen latency measured on Wi-Fi for `ref-capture-the-flag` and `ref-coop-adventure` (including Android browser controllers), with a recorded budget | M5 milestone |
| Apple TV native client | Frame rate and input-to-screen latency for both M1–M2 reference games over Wi-Fi, within a recorded budget; the input return channel; certificate pinning | M4 milestone |
| Studio | Edit and play round trip; live reload picks up an external edit to the pack; schema-generated forms reject invalid values | Every change from M3 |
| Regression replays after AI edits | Every MCP or studio AI patch re-runs the pack's recordings before it is applied | Every change from M3 |
| Save and load | Saving mid-game and loading reproduces the same state hash | Every change |
| Joining time | A fresh phone joins a room from the QR code in under 30 seconds (measured on real devices) | Each milestone from M1 |
| Desktop app | A clean-machine install hosts a room with no terminal | M2 milestone |
| Naming rule | Hashes-only banned-names test over the whole tree, plus the private-banlist pre-commit hook | Every commit |
| Licences | REUSE lint; every asset has an SPDX licence, author and source; no share-alike or GPL asset in the built-in library | Every change |
| AI tool layer | MCP and CLI contract tests: patch → validate → diff → apply; write tools refuse paths outside the creator's pack | Every change |
| Design conformance | Every ADR or intent that changes the pack format, components, views, display list, input or joining records a walk-through against each game in the design-conformance set | Each design decision |
| Reference games | Each `ref-*` pack has golden games and a clear-check recording in the games repository, run against each PG-Engine release | Each PG-Engine release |
