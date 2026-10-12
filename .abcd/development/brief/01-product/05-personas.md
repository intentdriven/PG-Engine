# Personas

PG-Engine serves three personas. **Alice** is the primary one, and every design choice must work for her first.

## Alice: the creator (primary)

Alice has an idea for a game, often a remembered one, and an AI assistant. She isn't a game programmer.

- **What she wants:** to see her landscape on screen within minutes, to describe a change in words and get a playable result, and to share the game with friends.
- **What she needs from PG-Engine:**
  - built-in tiles and characters, so she isn't blocked on art;
  - play-in-editor;
  - AI changes that arrive as checked diffs, never as broken games;
  - error messages that her AI can act on;
  - one-click publishing to a place she controls (her own GitHub).
- **What fails her:** a blank canvas, setup friction, AI changes that break the game silently, and art that doesn't match the palette.

## Bob: the teacher and school IT

Bob runs PG-Engine on the school network so a class can build games. Pupils may be under 13.

- **What he wants:** a self-hosted server that installs without a terminal, needs no pupil accounts and keeps data on site. He also wants AI that runs on a local model on the school network, through an OpenAI-compatible server such as Dessau, with no cloud keys.
- **What he needs from PG-Engine:**
  - a desktop app or single binary that hosts everything;
  - full TLS on school-managed iPads and tablets, by pushing the host's root certificate through device management. Schools in England are phone-free by default from September 2026, so in class a "hand" is a school tablet, not a pupil's phone;
  - a starter library that is CC0 or CC-BY only;
  - no dependence on the hosted service.
- **What fails him:** cloud-only features, accounts and data collection for minors, and certificate errors on pupils' devices.

## Carol: the couch host

Carol hosts game night. She never opens the studio.

- **What she wants:** to open a game on the TV or iPad, have everyone scan a QR code, and play. Each phone is a private hand or a controller.
- **What she needs from PG-Engine:**
  - joining in under 30 seconds;
  - reconnection that survives a phone going to sleep;
  - the AI taking over a seat whose player leaves;
  - the Apple TV app or AirPlay;
  - LAN play with no internet.
- **What fails her:** setup steps, phones that drop and can't rejoin, and lag in action games.

## Stakeholder (not a persona): the owner

The owner steers and funds the platform, and may publish specific IP-free PG-Engine games as native store apps (open question 2). If that happens, the owner's needs add constraints, such as store-review compatibility of downloaded content and per-asset licence metadata. They never override Alice's experience.
