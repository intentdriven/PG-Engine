# Decisions

Working decisions for this repository, newest first. Durable architectural decisions are ADRs under
`.abcd/development/decisions/adrs/`; this log keeps the smaller calls a later session should not have to rediscover.

## 2026-10-07

- **abcd's tooling is reported, not built here.** Anything about abcd itself, a feature or an inconsistency found
  while working in PG-Engine, goes to abcd through `/abcd:report`. What PG-Engine decides about its own use of the tool stays here
  and cites the report.
- **The name-check adjudication features moved to abcd** (report `rpt-2610071222173136`). The adjudication ADR stays
  as PG-Engine's policy for its `warn` tier.
- **abcd's conventions block lives in `AGENTS.md` alone** (`docs.target: agents_md`); `CLAUDE.md` was removed.
- **This file exists by hand.** abcd's install does not create the shared work tier its lint requires (report
  `rpt-2610071228213002`); if abcd later scaffolds it differently, follow abcd.
