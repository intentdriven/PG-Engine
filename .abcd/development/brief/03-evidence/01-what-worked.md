# What worked

Evidence from the predecessor game (about 450 commits, a green main branch auto-deploying at handover) and from the research. PG-Engine carries each item forward on purpose.

| What worked | Evidence | Carried into PG-Engine as |
|---|---|---|
| One headless rules core driven by a runner, run by both the hot-seat host and the network host | Hex boards, i18n, phones and key-based messages all landed without changing square-board play | Invariant 4. `05-internals` § simulation core |
| Randomness only from seeded named streams, enforced by a forbidden-globals scan | The scan caught clocks, `Math.random` and DOM access in core code | Invariant 5 |
| Golden games with two hashes (state and behaviour) | Wording changed freely while play stayed pinned | Invariant 11. Verification matrix |
| The ask/respond prompt protocol (`kind`, `purpose`) | The same call served humans, phones, the AI and timeouts | Glossary: prompt |
| Per-seat views as field allowlists, plus a thin phone relay that checks seat stamps | Phones as private card hands, with the relay storing only codes and tokens | Invariants 8 and 9. Surface: hand |
| QR code plus single-use 6-character code, a reconnect token in local storage, a grace period before the seat falls back | The grace period was raised from 4 s to 10 s after real-world drops | Surface: hand |
| Content as JSON under JSON Schemas, with words as Markdown and key-based strings in several languages | All names, cards, terrain, events and rules were data | Pack format |
| Art styles as data plus painter modules, guarded by pixel fingerprints through a software canvas | Styles were swappable without breaking art | Skins. Verification matrix |
| A JSON-defined 4-voice chip tracker plus note-list sound effects | Music released CC0 | Audio internals |
| Server hardening: rate limits, origin and host checks against DNS rebinding, a static allowlist, signed cookies | It ran publicly on a free hosting tier | Server internals |
| Recordings as gzip JSON Lines, with server analysis scripts | Win-rate tuning, and an AI tournament harness run headlessly | Recordings, and the clear check |
| **Research:** deterministic replays with per-tick state hashes as regression tests | A large factory-sim studio's per-tick checksum practice | Verification matrix |
| **Research:** examples plus compiler-style error feedback lift AI DSL success from 25–30% to 80–100% compile rate | A 2025 study of LLM-written grid-puzzle games | Linter messages are written for AI |
| **Research:** play-in-editor with instant toggling, and constraints (palette, tile size) as a creative aid | Every successful beginner studio | Studio surface |
