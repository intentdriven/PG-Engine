# Framing

## PG-Engine is

- **An engine first.** Games are packs, and no game's names, rules or wording live in engine code.
- **Open source first.** The engine, studio and server are open, so anyone, schools included, can host PG-Engine. Public funding is sought for the open, non-commercial side. A commercial layer is intended, and its form (native store apps of IP-free games, hosting tiers, hosted AI credits) is open question 2.
- **Local-first.** A game night or a classroom needs nothing beyond the local network. The hosted service is a convenience, not a dependency.
- **AI-native, not AI-dependent.** The pack format is designed to be written by AI and checked by the engine. Everything the AI does can also be done by hand in the studio.
- **Faithful to mechanics, original in expression.** The reference games are mechanics studies with new names, new art and new wording.

## PG-Engine is not

- **A general-purpose engine.** It is for retro-style games, 2D and 3D: recreating the games people remember, and making new ones in that spirit.
- **A clone factory.** It ships no third-party names, art, audio or text.
- **A platform that owns creators' games.** Creators publish to places they control, through a federated, signed pack index. The hosted service holds only a licence to host and display.
- **A cloud service for children.** Under-13s are served by schools self-hosting PG-Engine, not by accounts on the hosted service.
- **A way around the sandbox.** Pack code runs only in the handler sandbox; there are no plugins and no engine ejection.
- **An art model.** PG-Engine neither trains nor hosts its own art model; it uses external generators and labels what they make.

## How the owner revised the predecessor's monetisation plan

The left-hand column cites the predecessor's monetisation plan (September 2026): its summary and its recommended approach.

| Predecessor plan | PG-Engine |
|---|---|
| Revenue from hosting subscriptions first | The hosted service is **free** for public, GitHub-hosted games |
| Engine runs only in the player's browser; servers only for optional services | The **server is central**: it runs the authoritative simulation and phone pairing, and the browser or native app is a screen. Packs stay static and forkable |
| Licences: MIT for the format and tooling, MPL-2.0 for the engine and editor, AGPL-3.0 for the platform | **Adopted from the first commit** |
| Not covered by the plan | **Native store apps of specific IP-free games** are under consideration as the commercial layer (open question 2) |
| — | **Public funding** for the open, non-commercial side |
