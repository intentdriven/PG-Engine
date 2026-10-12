# Naming

## Rule

PG-Engine carries no third-party game titles, game characters, game brands or game publishers' marks. Platform and dependency names (operating systems, browsers, libraries, hosting services) are not covered by this rule. The rule rules the covered names out of:

- what players see;
- the brief, the docs and the code;
- ids and file names;
- tests and fixtures;
- commit messages.

Names are generic and describe what a thing is or looks like.

**Why:**

- Game titles and character names are trade marks, so carrying them is a takedown risk. One rights holder in particular removes fan projects consistently.
- The names give a game nothing it needs.
- The predecessor retrofitted this rule at a cost of about 70 renamed files. PG-Engine holds it from the first commit.

**Enforcement:**

- **The banlist is private.** The `names/third-party/<codename>/<term>` namespace covers all 17 originals behind the reference games and the design-conformance set. It sits in the private layer (`.abcd/.work.local/private-names.txt`, per machine and gitignored), and the commit hooks enforce it. `abcd banlist` lists its entries by key only.
  - **What it holds:** titles, coined in-game terms (characters, species, places, items, mechanics, ships, units), credits, and a few protected words that turned up along the way (an emblem protected by humanitarian law, live trade marks).
  - **Why it's private:** PG-Engine is public, so no committed file names the originals, not even as a ban pattern. The public layer, `.abcd/docs-lint.json`, holds no third-party names.
  - **Limits:** CI can't enforce the private layer, which protects only machines that opted in. It matches case-insensitively and has no `warn` level. Until abcd supports private entries that are case-sensitive or `warn` (proposed as report `rpt-2610121532502681`), the 13 case-sensitive entries are parked unenforced in the same local tier, and the case-insensitive `warn` entries block. The private layer also carries no successors.
- **Separators.** Patterns allow spaces, underscores and hyphens between words, and straight or curly apostrophes, so `two_words`, `two-words` and possessives are caught. The predecessor's hashed test missed these.
- **Terms kept off every list.** The private banlist also holds terms that must not appear in the repository even as a ban pattern.

## Three tiers of term

| Tier | Example | How it is matched | Outcome |
|---|---|---|---|
| **Coined or proper names** | an invented planet, item or species | case-insensitive, everywhere | always blocked (`blocker`) |
| **Game names that are ordinary words** | a hero named after an ordinary noun, a board-game title that is also an economics term | **case-sensitive** (`(?-i:…)`): the capitalised name is caught, the lowercase word stays free | blocked when nothing else in a sentence would capitalise the word |
| **Collides with sentence-initial capitals or everyday senses** | a unit or race name that also starts ordinary sentences, a title that is also a common noun | case-sensitive, severity `warn` | flagged, then an **adjudicator** decides whether the line refers to the game. Game reference: blocked. Ordinary use: the line gets the lint's per-line allow marker |

Until abcd's private layer can match case-sensitively and warn, the case-sensitive entries of tiers 2 and 3 are parked and nothing checks them, and a case-insensitive `warn` entry blocks instead of flagging.

Plain phrases that any game could use (a wild card, a swamp, a luck card) stay allowed, as the predecessor kept them.

## Adjudication (staged)

*Staged. Decided in the
[adjudication ADR](../../decisions/adrs/2610071605254753-banned-term-adjudication-the-in-session-judge-alone-with-no.md),
which supersedes the first one.*

- **The judge.** The latest Opus model in the developer's Claude Code session proposes "game reference" or "ordinary
  word" for each `warn` hit, and the product owner approves or overrides it. To be built in abcd's name check
  (proposed to abcd as report `rpt-2610071222173136`), not in PG-Engine.
- **No shadow screen.** No local model judges alongside the in-session judge, and no shadow log is kept.
- **Rule: reasoning is bounded on every judge request** (switched off, or capped). In the lab, open models left at
  their default reasoning spiralled without answering on about half their batches.
- **Offline.** The local decision model, then a local chat model with thinking off, with a person reviewing before
  anything is blocked. Proposed to abcd in the same report, and wanted only once an offline use comes up.

## Renaming principles (from the predecessor)

The predecessor's remake replaced every *coined* name from the original before its first public commit, and enforced the rule with a test. PG-Engine packs follow the same principles:

1. **Coined names are replaced; plain English stays.** Ban the original's invented names. Keep phrases any game could use. Where a kept plain-English term has a British spelling, use it ("artefact", "colour", "vigour").
2. **Real people's names are removed.** Places or things named after the original's creators get descriptive or sound-based names instead.
3. **Same pattern, new words.** Keep the *style* of the original's naming (for example alliterative "tech word plus everyday thing" item names, or short punchy robot names) but invent every word. Check new names against the banlist too, because names borrowed from other franchises are just as banned.
4. **Effect items say what they do.** An item's name states its effect ("Beam Blocker", "Turbo Tonic").
5. **Code uses ids; words live in the language files.** Renaming is a one-line change in `lang/`, never a code change.
6. **Copy structure only when it isn't distinctive.** A recognisable numbering scheme, a fixed set of four player colours, or a famous four-tier difficulty ladder is changed, not just renamed.

## Reference-game codenames

Reference games and the design-conformance set use the `ref-<game-type>` form. The name is the *kind* of game, never the original's title.

- **Reference games:**
  - `ref-scavenger-hunt`
  - `ref-takeover-shooter`
  - `ref-capture-the-flag`
  - `ref-coop-adventure`
  - `ref-real-time-tactics`
  - `ref-transport-economy`
- **Design-conformance set:**
  - `ref-auction-economy`
  - `ref-hidden-roles`
  - `ref-asymmetric-relay`
  - `ref-case-file`
  - `ref-eco-sim`
  - `ref-settlement-trading`
  - `ref-hidden-movement`
  - `ref-hide-and-seek`
  - `ref-location-trail`

The mapping from codename to original is kept off the repository.

## Reserved vocabulary

The engine's nouns are fixed and defined in the [glossary](../glossary/README.md):

- pack, module manifest, prefab, component, event rule, handler, level, legend;
- seat, hand, screen, host, room, view, display list, viewport;
- prompt, stream, tick, sub-mode;
- skin (art style), clear check, index.

A pack can't redefine them.
