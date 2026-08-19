# Meta Data Audit (Claude skill) — v3

A Claude skill that audits meta descriptions and title tags against a 5-dimension scoring
framework built on Kevin Indig's Growth Memo. Built for the AI Overview reading-mode shift,
where 47.5% of cursor movement on AIO SERPs is back-scrolling and the "second pass" matters
more than the first.

## What's new in v3

Three rewrite reflexes are now mandatory in the rewrite step (Step 7) and documented in
`references/scoring-rubric.md` -> "Rewrite principles":

1. **Replace category words with specific differentiation.** "Best CRM software" -> "CRM with
   Salesforce migration in 24 hours". Give the re-reader a concrete reason on the second look.
2. **Front-load your strongest differentiator.** The first 60 characters do more work than the
   last 60, because the listing is read on the way down and again on the way back up.
3. **Strip words shared by 3+ competitors.** Words appearing in 3+ competitor snippets on the
   same SERP have lost their information value — replace them with something brand-specific.

Everything from v2 is retained.

## Carried over from v2

- **Intent decode (Step 5a).** Psychological read of the head query from SERP evidence (PAA,
  related searches, domain mix, SERP features): micro-intents, human primary job, SERP-vs-job
  tension — ending in 1-2 hook angles for the snippet.
- **5th scoring dimension: job alignment.** Does the snippet address the human primary job, or
  just echo the SERP-dominant pressure?
- **Query coverage gap analysis (Step 5b).** Non-brand GSC queries + native query fan-out
  (grounded in PAA/related searches) -> semantic clusters -> gap score = demand x (1 - coverage),
  filtered by intent suitability. Max 3 reported gaps.
- **Structured SERP capture, GSC MCP support, mandated 3-candidate rewrite mix, personalization
  flag, optional external fan-out import.**

Hard scope rule throughout: insights end at the snippet. No page-level or content
recommendations.

## What it does

Walks the user through a 10-step audit: confirm data/tools, confirm scope, process Search
Console data, check AIO presence, capture the SERP structured, decode intent (5a), run the
query-coverage gap analysis (5b), score every listing on all 5 dimensions, output the audit with
3 rewrite candidates per page (worst dimension / top gap / job hook) plus a title rewrite,
summarize the recurring pattern, and populate the audit log for 30-day CTR tracking.

## Files

- `SKILL.md` — the workflow.
- `references/scoring-rubric.md` — the 5 dimensions + the three rewrite principles.
- `references/intent-decode.md` — Step 5a framework.
- `references/query-fanout.md` — Step 5b method.
- `references/gsc-export-guide.md` — how to pull Search Console data.
- `references/audit-log-columns.md` — the log spec.
- `references/troubleshooting.md` — common failure modes.
- `assets/meta-audit-log.xlsx` — the before/after CTR log.

## Source

Framework adapted from Kevin Indig's Growth Memo "The Meta Data Audit", built on clickstream
research into the AIO reading-mode shift (47.5% back-scrolling; ~846,000 U.S. Google sessions,
Feb-Mar 2026, analyzed by Eric Van Buskirk / Clickstream Solutions with Surfer SEO data).
