# Decomposition calibration: 2026-10-03

## The obligations of the banned-term adjudication decision

Proposal: "shadow log and everything else that's required" by the accepted
[adjudication ADR](../../decisions/adrs/2610031742534388-banned-term-adjudication-a-judge-in-session-with-a-local.md).

| Part | Type | Home |
|---|---|---|
| Judge `warn` hits in session, owner approves, local decision model logged in shadow | intent | itd-2610032153275513 |
| Shadow review: would-be misses, miss-rate range, "enough to revisit the decision?" | intent | itd-2610032153313848 (blocked by the first) |
| Offline judging with a person in the loop | intent | itd-2610032153311281 (blocked by the first; held) |
| Shadow log entry fields | plumbing | brief, `02-constraints/04-naming.md` § Adjudication |
| Reasoning bounded on every judge request | rule | brief, `02-constraints/04-naming.md` § Adjudication |
| Revisit the decision once evidence suffices | trigger | inside the shadow review intent |
| Local server's decision-model support; abcd's non-streaming adapter | other repositories | already recorded there; dependency lines in the ADR |

- **Typed links:** none. The three intents carry out the ADR and neither supersede nor refine an existing intent (the
  store was empty). No reversal flagged.
- **Verdict proposed:** SPLIT into three. **Confirmed by the owner:** three items, built in this repository only (abcd
  was offered as the home and declined).
- **Did the initial routing survive confirmation?** Yes, unchanged.
- **Routing revised (2026-10-07).** The owner reversed "built in this repository only": the three intents are features
  of abcd's name check, so they were proposed to abcd (report `rpt-2610071222173136`) and the PG-Engine drafts removed. The
  table's Home column above records the routing as it stood on 2026-10-03. The ADR stays as PG-Engine's policy.
