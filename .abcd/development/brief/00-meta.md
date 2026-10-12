# Meta

This file holds the brief's stable conventions: its directory structure, its file-naming rules and its truth rule. The brief describes PG-Engine's *current* state. It has no versions, snapshots or archive; history lives in `git log`.

## The truth rule

Everything in the brief is decided. A section describes machinery that is either **shipped** or **staged** (a design target that a later change builds towards), and never an undecided option. A brand-new repository has shipped nothing yet, so every capability here is staged until its intent reaches `intents/shipped/`. Unsettled questions are recorded *as questions* in [`03-evidence/03-open-questions.md`](03-evidence/03-open-questions.md), never as claims.

## Origin

The product owner wrote this brief through a structured interview, and it rests on three sources of evidence:

1. the predecessor game's packed lifeboat (a single vibe-coded couch game, held in a private repository);
2. state-of-the-art research in six themes (the engine and module format; multiplayer and second screens; the studio, AI authoring and packs; the reference games' capabilities and IP; hybrid digital/physical games; the predecessor's record);
3. seven interview rounds, in which every question was one only the owner could answer. The last round confirmed or corrected the findings of an independent review of the draft.

The research notes and the verbatim interview log are machine-local experiment records (lab `lab-261002171217-c372ff6`) and are never committed. This brief carries their sanitised conclusions.

## Naming rule for third-party games

PG-Engine carries no third-party game titles, game characters or game brands, whether in the brief, docs, code, ids, file names, tests or fixtures (see [`02-constraints/04-naming.md`](02-constraints/04-naming.md)). Reference games go by neutral codenames (`ref-*`), each describing what the game *is*. The codename-to-original mapping is kept off the repository.

## Directory structure and naming

Numbered folders (`01-` … `06-`) with two-digit prefixes and kebab-case file names. `README.md` files are indexes and carry no number. The layout is the same shape as an abcd lifeboat, so a later `disembark` coverage pass reads this brief section by section.
