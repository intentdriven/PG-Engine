---
id: adr-2610031742534388
slug: banned-term-adjudication-a-judge-in-session-with-a-local
status: superseded
date: 2026-10-03
supersedes: null
superseded_by: adr-2610071605254753
related_intents: []
related_rfcs: []
related_adrs: []
---

# ADR-2610031742534388: Banned-term adjudication: a judge in session, with a local decision model in shadow mode

## Context

PG-Engine's public banlist (`.abcd/docs-lint.json`, enforced by `abcd lint docs`) has three tiers (see
[naming](../../brief/02-constraints/04-naming.md)):

- **Coined names:** blocked deterministically.
- **Capitalised ordinary-word game names:** blocked case-sensitively.
- **`warn` entries:** words that are also ordinary English, or that start ordinary sentences. A regex cannot settle
  these; something must judge whether a flagged line refers to the protected game.

A lab evaluated judges for the `warn` tier (lab `lab-261002171217-c372ff6`, the "v3" test).

**The test set:**
- 400 flagged lines from real text plus generated hard cases.
- Labelled blind by two cloud models (98.7% agreement), with the owner settling disagreements and auditing a random
  40.
- Judges were scored once on a held-out test split of 280 items; cut-offs were tuned on a separate dev split.

**Findings that shape this decision:**

| Judge | Accuracy on held-out test | Missed game references | Notes |
|---|---|---|---|
| Frontier model in the cloud (Opus 5.5, low reasoning effort) | 97.8% | 0 | about 3 min for 275 lines |
| Other frontier model in the cloud (Fable 5.1) | 97.5% | 1 | |
| Mid-size open model in the cloud (GLM-4.7, reasoning off) | 95.3% | 4 | about US$0.03 |
| Local decision model (Clef, 4-bit, served on this machine) | 90.0% at its best cut | 10 | 6 min, no cloud |
| Local small chat model (Bonsai-27B, 2-bit) | 90.0% | 16 | 63 min |
| **Live pipeline:** local decision model screen (zero-miss cut 0.05), then Opus in session on the leftovers | **97.5%** | **0** | the screen cleared 73 of 275 lines (27%), none of them a game reference |

- **A local decision model works as a screen, verified once, live.** At its dev-tuned zero-miss cut, the screen
  allowed 73 of 275 flagged lines with **no** missed game reference. The in-session judge answered all 202
  leftovers (195 correct) and did not stall on the hard-only set. The pipeline scored 97.5%, against 97.8% for the
  judge alone: one extra false block, no extra miss.
- **One test is not a track record.** The screen's zero-miss result rests on 275 lines and one cut-off tuned on 120.
  An earlier live run showed that a *weaker* reasoning model, given only hard leftovers, can spiral without answering.
- **Reasoning must be bounded for judging.** At default reasoning, open models spiralled on about half their batches.
  With reasoning switched off, they answered every batch in seconds. This applies in the cloud and on the local
  server, where a per-request "thinking off" switch is passed through.
- **Today's volume is low.** The brief currently has zero `warn` hits.

The owner weighed abcd's script-first principle (add the screen once volume justifies it) and chose to run the screen
from the start, as an experiment, to build evidence over time.

## Decision

We will adjudicate `warn`-tier hits with **a judge in session**: the **latest Opus model** available in the
developer's Claude Code session. The judge is not pinned to a version; Opus 5.5 is the version the evidence above
measured. Its verdict is a **proposal**; the product owner approves any block, under "verifier selects, gates
decide".

We will **always run the local decision model (Clef, via the local model server) alongside it, in shadow mode,
whenever that server is available.**

- **What gets logged:** for every flagged line, the decision model's verdict and probability, next to the in-session
  judge's verdict.
- **The decision model never decides.**
- **What the log measures:** how often the screen's "ordinary" (would-allow) verdict disagrees with the judge or the
  owner, the would-be misses. That is the evidence for or against adopting "screen first".

**Offline (schools, no cloud):** the local decision model, then the local small chat model with thinking off, and a
person reviews every "game" verdict before anything is blocked.

## Alternatives Considered

1. **Frontier judge alone, adding the screen once volume justifies it** (abcd's script-first default). This is
   simplest, and the frontier judge is the most accurate. It was rejected for now because it collects no evidence
   about the screen; we would later have to adopt or reject the screen on a single small experiment.
2. **Screen first, live** (the decision model allows its "ordinary" lines; the judge sees only the rest). This is the
   cheapest at volume, and its one live end-to-end test matched the judge alone on misses (0) at 97.5% versus 97.8%.
   It was rejected *for now* because a single 275-line test cannot establish a miss rate near zero, and a missed game
   reference is the costly error. The shadow log is how it earns adoption.
3. **Local only** (decision model, then local chat model). It works offline and keeps everything on the machine, but
   at 90.4% (screen, then local chat model) it is too weak to block unattended. It was kept as the offline mode,
   with a person in the loop.
4. **Chosen: a judge in session plus the decision model in shadow mode.** It keeps frontier accuracy now and builds a
   longitudinal, real-world measure of the screen at little cost.

## Consequences

- **Easier:** decisions now rest on the most accurate judge available, with no API key or provider routing (the
  session is the host). The screen question gets answered from real use, not inference.
- **Harder:** two judges run per flagged line while the local server is up, and a shadow log has to be kept and
  reviewed. Flagged lines from this private repository are sent to the cloud judge. That is no different from any
  in-session work, but it rules out the online mode for offline or school use.
- **New obligations:**
  - **A shadow log format:** line id, rule, decision-model id and probability, judge model id and verdict, owner
    verdict, date. Model ids are logged because the in-session judge tracks the latest Opus, so comparisons across
    versions must stay possible.
  - **A periodic review:** "would the screen have missed anything?"
  - **Reasoning bounded on every judge request.**
  - **Revisit this decision** once the shadow log holds enough lines to tell the screen's miss rate apart from zero.
- **Dependencies:**
  - **Serving the decision model through the local server** depends on that server's decision-model support (planned
    there).
  - **Until it lands,** the model's reference server runs on loopback.
  - **abcd's provider adapter is non-streaming with a 120 s limit** (recorded in abcd). Long delegated judging steps
    routed to a local provider are therefore not yet reliable through abcd. The in-session judge avoids this.
- **Where it is built (2026-10-07).** The judging flow, the shadow log and its review are features of abcd's name
  check, so they are proposed to abcd (report `rpt-2610071222173136`) rather than built here. This record stays as
  PG-Engine's own policy for its `warn` tier; the three PG-Engine draft intents that carried it out were removed.
