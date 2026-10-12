---
id: adr-2610071605254753
slug: banned-term-adjudication-the-in-session-judge-alone-with-no
status: accepted
date: 2026-10-07
supersedes: adr-2610031742534388
superseded_by: null
related_intents: []
related_rfcs: []
related_adrs: [adr-2610031742534388]
---

# ADR-2610071605254753: Banned-term adjudication: the in-session judge alone, with no shadow log

## Context

[ADR-2610031742534388](2610031742534388-banned-term-adjudication-a-judge-in-session-with-a-local.md) settled how PG-Engine
judges `warn`-tier hits: a judge in the developer's session, with a local decision model running alongside in shadow
mode and its verdicts logged, so the screen could earn trust over time. Its evidence (the lab test of 2026-10-03)
stands and is not repeated here.

The judging flow, the shadow log and its review are features of abcd's name check, so they were proposed to abcd
(report `rpt-2610071222173136`) rather than built in PG-Engine. abcd approved the in-session judge and declined the shadow
log and its review for now. PG-Engine's decision therefore promised a log that nothing builds.

## Decision

We will adjudicate `warn`-tier hits with **the in-session judge alone**: the latest Opus model in the developer's
Claude Code session proposes "game reference" or "ordinary word" for each hit, and the product owner approves or
overrides each proposal ("verifier selects, gates decide").

- **No shadow mode.** No local decision model runs alongside the judge, and no shadow log is kept or reviewed.
- **Reasoning is bounded** on every judge request (switched off, or capped), as before.
- **Offline (schools, no cloud)** is unchanged from the superseded record: the local decision model, then a local
  chat model with thinking off, and a person reviews before anything is blocked. It is wanted only once an offline
  use comes up.

## Alternatives Considered

1. **Keep the shadow clause, waiting for abcd.** It keeps the evidence-building intent, but promises a log nothing
   builds and collects nothing meanwhile. Rejected.
2. **Build the shadow log in PG-Engine.** It would collect the evidence now, but it is abcd's tooling, and PG-Engine's convention
   sends tool work to abcd. Rejected.
3. **Chosen: the in-session judge alone.** It is the most accurate judge the lab measured, and it needs nothing abcd
   has not agreed to build.

## Consequences

- **Easier:** one judge per flagged line; nothing to log, store or review.
- **Harder:** the local decision model earns no evidence from real use, so "screen first" cannot be revisited from
  PG-Engine's own data. Revisit this decision if abcd later builds the shadow log.
- **Unchanged:** flagged lines from this private repository go to the cloud judge, as any in-session work does.
