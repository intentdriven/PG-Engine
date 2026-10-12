# Decomposition calibration: 2026-10-07

## A grand-strategy reference game, hosted in a later version

Proposal, verbatim apart from the third-party title (named by codename here, per the naming rule): add a
super-complex wartime strategy game with resource management to the list of games; PG-Engine must be able to host such a
game in a later version.

| Part | Type | Home |
|---|---|---|
| A future game the design must stay able to express | plumbing (design constraint) | brief, `01-product/04-scope.md`, design-conformance set, as `ref-grand-strategy` |
| Keeping the original title out of the repository | rule (existing) | the public banned-name list, `names/third-party/grand-strategy/title` |
| Hosting it as a playable pack | intent | none yet: the design-conformance set defers building, and its order is an open question |

- **Typed links:** none. The row extends the design-conformance set; it neither supersedes nor refines an intent (the
  store is empty).
- **Verdict:** HOLD as an intent; route the design constraint to the brief. No question was put: the brief already
  keeps future games the design must allow in this set, so the record settles the home.
- **Did the initial routing survive confirmation?** Pending the owner's review; the routing is a facilitator draft.
- **Owner's confirmation (same day):** the routing stands and the id `ref-grand-strategy` is kept. Initial routing
  survived.

## Three more design-conformance games (same day)

Proposal, verbatim apart from the third-party titles: record three named games (a turn-based explore-and-conquer
game, a simultaneous-orders conquest game and a real-time global war game) in the list of games.

| Part | Type | Home |
|---|---|---|
| Three future games the design must stay able to express | plumbing (design constraint) | brief, design-conformance set: `ref-explore-and-conquer`, `ref-secret-orders`, `ref-real-time-global` |
| Keeping the original titles out of the repository | rule (existing) | the public banned-name list, one title pattern each |

- **Typed links:** none.
- **Verdict:** route to the brief; no intent. No question was put on the home, for the same reason as above.
- **Did the initial routing survive confirmation?** Yes. The owner chose `ref-secret-orders` over the drafted
  `ref-simultaneous-orders`; the other two drafted ids were kept.

## Multilingual from the start (same day)

Proposal, verbatim: "multilangual from the start, with German and Japanese as the first two options. British English
as the default"

| Part | Type | Home |
|---|---|---|
| PG-Engine's own screens (studio, lobby, host, phone hand) in British English, German and Japanese from the first release | intent | itd-2610071608273365 |
| Games carry their words in several languages; each player's device shows its own | intent | itd-2610071608272126 |
| British English is the default | plumbing | brief, `02-constraints/01-platform.md` § Human languages |
| German and Japanese first, from the start | plumbing | brief, platform and build sequence (M0, M1) |
| Japanese fonts, line breaking and text input | plumbing | brief, platform § Human languages |

- **Typed links:** the games intent refines invariant 10 ("The wire carries keys, not text. Every screen and hand
  renders in its own language."). Not a reversal. The two drafts are not linked to each other (filing-time match
  0.22, below the 0.6 threshold).
- **Verdict:** SPLIT. **Confirmed by the owner:** two intents, as proposed.
- **Did the initial routing survive confirmation?** Yes.
