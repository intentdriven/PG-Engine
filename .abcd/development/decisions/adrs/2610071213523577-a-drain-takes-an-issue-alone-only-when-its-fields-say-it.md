---
id: adr-2610071213523577
slug: a-drain-takes-an-issue-alone-only-when-its-fields-say-it
status: accepted
date: 2026-10-07
supersedes: null
superseded_by: null
related_intents: []
related_rfcs: []
related_adrs: []
drain_categories: [tech-debt, documentation, inconsistency, drift, bug, ux]
drain_severities: [nitpick, minor]
drain_security: handback
drain_remedy: required
---

# ADR-2610071213523577: A drain takes an issue alone only when its fields say it needs no decision

## Context

`abcd drain` works the open issue ledger unattended: it fixes what needs no decision and hands the rest back to a person. Which issue a machine may take alone is this repository's decision, and the drain refuses to run here until an accepted record states it.

## Decision

We will let a drain take an open issue alone only when its fields say it needs no decision, and hand every other open issue back by the rule that excluded it. The four `drain_` fields in this record's frontmatter are the rule the drain reads:

- `drain_categories`: the categories a drain may take, from the fixable set (`tech-debt`, `documentation`, `inconsistency`, `drift`, `bug`, `ux`); every other category is a person's.
- `drain_severities`: the severities a drain may take; `major` and `critical` are a person's unless listed here.
- `drain_security`: `handback` keeps every security issue a person's; `take` lets a drain take one that passes every other rule.
- `drain_remedy`: `required`; an issue without a remedy, or with the value an automatic filer writes, is never taken.

These values are abcd's strict baseline. Listing `major` or `critical`, or setting `drain_security: take`, loosens a floor, and `abcd drain --dry-run` and the drain start name every floor loosened.

## Alternatives Considered

- **A model classifies each issue.** Rejected: a model detects its own ambiguity badly, and a classifier that can let an issue through is the failure this rule exists to prevent.
- **Every issue with a remedy.** Rejected: a remedy says what someone proposed, not that the proposal needs no decision.
- **The fields, read in a fixed order (chosen).** Each exclusion names the rule a person reads to act on it.

## Consequences

- A change to what a drain may take is a change to this record, reviewed like code; a pull request that loosens it is one a reviewer reads as a trust change.
- An issue whose remedy waits on a ruling, or whose deferral past the current release is live, is handed back whatever this record says.
