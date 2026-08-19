---
name: meta-data-audit-v3
description: >
  Audit and rewrite meta descriptions and title tags for AI Overview SERPs, using a 5-dimension
  scoring framework (differentiation density, front-load, specificity, re-read survivability, job
  alignment). V3 adds three rewrite reflexes: replace category words with concrete
  differentiation, front-load the strongest differentiator into the first 60 characters, and
  strip words shared by 3+ competitor snippets. Keeps the v2 layers: SERP intent decode (micro-
  intents, human primary job, hook angles), query-coverage gap analysis from GSC data plus query
  fan-out, and GSC MCP support. Use to audit meta descriptions, rewrite title tags, score SERP
  listings, improve CTR on AI Overview queries, run a meta data audit, check snippet
  differentiation, decode search intent, or find queries a snippet misses. Also triggers on a
  pasted GSC export or a URL plus keyword. Adapts to connected tools (GSC MCP, Semrush, Ahrefs,
  browser, or none) with a manual paste-in fallback.
---

# Meta Data Audit (v3)

A prompt-driven audit that scores meta descriptions and title tags against a 5-dimension
framework designed for AI Overview SERPs, then proposes rewrites grounded in live competitor
data, the psychology behind the query, and the real query demand the page already ranks for.

The base framework comes from clickstream research showing that AI Overview SERPs change how
users read: 47.5% of cursor movement is back-scrolling, vs. 27% on non-AIO SERPs. That means
the "second pass" matters more than ever, and your listing has to survive a re-read without
sounding redundant.

V2 added two layers the original 4-dimension audit could not see:

1. **Intent decode.** What the human behind the query is actually trying to get done (the
   "human primary job"), reconstructed from SERP evidence — and turned into snippet hook angles.
2. **Query coverage.** Which real queries the page ranks for (from Search Console) and which
   fan-out queries AI systems generate are NOT reflected in the current title/description.

V3 makes the rewrite step sharper. Three rewrite reflexes are now mandatory whenever you propose
copy (full detail in `references/scoring-rubric.md` -> "Rewrite principles"):

1. **Replace category words with specific differentiation.** "Best CRM software" tells a
   re-reader nothing they don't already know. "CRM with Salesforce migration in 24 hours" gives
   the re-reader a specific reason to pick you on the second look.
2. **Front-load your strongest differentiator.** Cursor movement on AIO SERPs is vertically
   dominated, and the median user spends 47.5% of their scrolling going back up the page (vs.
   27% without an AIO). A description gets read on the way down and again on the way back up. The
   opening has to carry it through both passes — the first 60 characters do more work than the
   last 60. Move your strongest claim there.
3. **Strip words shared by 3+ competitors.** Audit your meta description for words that show up
   in 3 or more competitors' descriptions on the same SERP. Those words have lost their
   information value. Replace them with anything specific to your brand.

## When to use this skill

Trigger on phrases like:

- "audit my meta descriptions"
- "rewrite these title tags"
- "score these listings"
- "what should I change about this snippet"
- "is my meta description differentiated enough"
- "improve CTR on AI Overview queries"
- "decode the intent behind this keyword"
- "which queries does my snippet miss"

Also trigger if the user pastes a Google Search Console export, pastes a SERP screenshot, or
shares a single URL and asks how its meta description stacks up against competitors.

Do NOT use this skill for: full SEO audits, keyword research, content gap analysis as a primary
deliverable, or backlink work. This skill is narrowly about meta descriptions and title tags.
Insights that would require changing the page itself stay out of scope (see Working rules).

## The 5 scoring dimensions

Every listing gets scored on all 5. Full rubric with examples is in
`references/scoring-rubric.md`. Read that file before running the first scoring pass.

1. **Differentiation density.** Count of words in the meta description that also appear in 2+
   competitor descriptions on the same SERP. Lower is better. Shared category words are dead
   weight. (Rewrite reflex 3 applies the conservative 3+ threshold when deciding what to cut.)
2. **Front-load score.** Whether the strongest differentiator lands in the first 60 characters.
   AI Overview SERPs push users into back-scrolling behavior, so a buried differentiator gets
   missed.
3. **Specificity index.** Ratio of category words ("best CRM software") to concrete
   differentiators ("CRM with Salesforce migration in 24 hours"). High specificity wins the
   second look.
4. **Re-read survivability.** Whether the listing reads as redundant on a second pass, or whether
   it adds something new. This is the dimension most listings fail on.
5. **Job alignment** *(new in v2)*. Whether the snippet addresses the human primary job behind
   the query, or just echoes the SERP-dominant pressure (usually "buy now" claims everyone else
   also makes). Requires the intent decode from Step 5a.

> When proposing rewrites (Step 7), always apply the three rewrite principles in
> `references/scoring-rubric.md` -> "Rewrite principles": category words -> concrete
> differentiation, strongest differentiator into the first 60 characters, and strip words that
> appear in 3+ competitor descriptions on the same SERP.

## SERP retrieval hygiene (incognito)

Personalized SERPs invalidate the audit: "frequently visited" badges and history-based
re-ranking can show the user's own site far above its real average position.

- Always retrieve Google SERPs in an incognito/private browser window with no logged-in
  Google account.
- If the available browser tooling cannot open an incognito window, depersonalize as far as
  possible: append `&pws=0` and explicit `hl`/`gl` parameters to the search URL, or use a
  logged-out web fetcher instead of the user's logged-in browser.
- Treat these as proof of personalization: "Häufig besucht" / "You've visited this page"
  badges, or the user's site ranking far better than its GSC average position.
- A personalized SERP must never be scored. Discard it, re-fetch cleanly, or ask the user to
  paste the listings from a manual incognito search.

## The workflow

This is a 10-step audit. Do not skip steps and do not assume tool access. Confirm what's
available before running.

### Step 1. Confirm data inputs

Ask the user which of these they can provide, and wait for the answer:

- **Search Console data.** Check first whether a GSC MCP is connected for the domain (tool names
  typically contain `gsc` or `search_console`). If yes, pull data directly — no paste needed.
  If no MCP, ask for an export (CSV, pasted table, or screenshot) showing pages, top queries per
  page, impressions, position, and CTR. See `references/gsc-export-guide.md`.
- A SERP data source: a browser tool (preferred — sees SERP features), Semrush MCP, Ahrefs MCP,
  or a web fetcher that can retrieve live Google SERPs. Browser-based SERP retrieval must
  happen in an incognito/private window (see "SERP retrieval hygiene").
- A spreadsheet tool (Google Sheets, Excel) for logging results.

Adapt to what the user has. Do not assume access to anything they have not confirmed.

If the user cannot provide GSC data, ask which specific pages and queries they want to audit and
proceed without traffic prioritization. Tell them what they lose by skipping it (no impression
weighting, and Step 5b query coverage runs on fan-out queries only).

If the user cannot provide live SERP data, ask them to paste the top 3-5 organic listings (title
+ meta description) per query from a manual Google search, plus the People Also Ask questions
verbatim. Tell them you cannot verify AI Overview presence or SERP features without it.

### Step 2. Confirm scope

Ask:

- Which domain are we auditing?
- How many pages? (Default to 10 if no answer.)
- Any sector or page-type filter? (e.g., shopping pages only, blog posts only.)
- Which market and language? (Default to US English; use the country's Google domain and `hl`/
  `gl` parameters when fetching SERPs.)

Per the underlying research, shopping, finance, jobs, travel, and education pages see the
biggest AI Overview reading-mode shift. If the user is on the fence about scope, suggest those
sectors first.

### Step 3. Process Search Console data

For each page in scope (via MCP or pasted export). Default window: **the last 90 days** (3
months) — it smooths seasonality and weekly noise; use 28 days only if the user asks for recent
data or the page is new.

- Identify the top 3-5 queries by impressions.
- Pull the full query list for the page (top 50-100 by impressions) — Step 5b needs it.
- **Exclude brand queries — two passes, always.** Brand demand does not belong in
  snippet-coverage calculations.
  1. *Derive the brand from the audited domain* (e.g. solakon.de -> "solakon",
     homeandsmart.de -> "homeandsmart" / "home and smart" / "home&smart"), plus any brand or
     product names the user provides. Build a fuzzy regex that catches misspellings, not just
     the exact string: allow swapped/substituted characters in the brand stem (c/k, on/om/un,
     dropped or doubled letters, split or joined words). Example for "solakon":
     `s[ao]l[ao][ck][ck]?[oa][nm]` catches solakon, solarkon, solacon, solakom, salokon,
     solokon. Show the regex to the user before applying it.
  2. *Post-filter review:* scan the filtered list for brand leftovers the regex missed. Tells:
     queries at position ~1 with far-above-average CTR that resemble the brand string. Remove
     them manually and note what slipped through so the regex can be tightened next run.
- Note current average position and CTR for each query.
- Flag any page where the top query has fewer than 100 monthly impressions and ask whether to
  keep or drop it.

If no GSC data is available, skip this step. Use the pages and queries named in Step 2 instead.
Do not invent traffic numbers.

### Step 4. Check AI Overview presence

- If a browser or web fetcher is available, check each query in an incognito/private window
  and record whether an AI Overview is showing. If the tooling cannot open incognito, append
  `&pws=0` plus explicit `hl`/`gl` parameters. If the SERP still shows personalization signs
  (e.g. "frequently visited" badges, position far better than GSC average), discard it and
  re-fetch cleanly or ask the user to paste an incognito SERP — do not score it.
- If not, give the user the list of queries to check manually and wait for confirmation.

V2 change (kept in v3): do NOT drop pages without an AIO. The intent decode and query coverage
layers apply to any SERP. Instead, note AIO status per page and weight the re-read dimension
accordingly (AIO present = re-read matters most; absent but heavily fragmented SERP = still
relevant).

### Step 5. Capture the SERP — structured

For each page, for the highest-impression non-brand query, capture more than just listings:

- **Organic listings.** Top 5: title tag + meta description each, plus the user's listing.
  Position above or below the AI Overview if one is present.
- **People Also Ask.** The questions verbatim. These are micro-intent evidence AND Google's own
  fan-out trace.
- **Related searches** ("Wird auch oft gesucht" / "related searches"). Also fan-out evidence.
- **Commercial features.** Shopping unit (and how many products), compare sites, ads count.
- **Content features.** Videos, featured snippets, editorial results.
- **Domain classification.** For each top-10 result: shop/vendor, editorial/test, forum/UGC,
  official/institutional.

If working from manual paste-in, ask the user for the PAA questions and related searches along
with the listings. The intent decode degrades badly without them.

### Step 5a. Decode the intent (new in v2)

Using ONLY the SERP evidence from Step 5 plus the GSC query list, produce a psychological intent
decode. Full framework, output format, and a worked example are in
`references/intent-decode.md`. Read it before the first decode.

Output per page:

- SERP-dominant intent (what Google currently rewards)
- 3-5 micro-intents hiding behind the query (the questions users are really asking)
- The **human primary job** — one sentence
- The tension between SERP-dominant intent and the human primary job
- **1-2 hook angles** for title/meta description that exploit that tension

Hard scope rule: the decode ends in hook angles for the snippet. Do not output page-level,
content, or product recommendations. If the decode surfaces an insight that only a page change
could address, compress it to one neutral sentence in the audit notes and move on.

### Step 5b. Query coverage gap analysis (new in v2)

Find real demand the snippet ignores. Full method in `references/query-fanout.md`.

1. Build the query pool: non-brand GSC queries (position <= 20) + a native fan-out set generated
   from the head query + the PAA questions and related searches captured in Step 5 (these ground
   the fan-out in Google's own data — do not skip them).
2. Cluster the pool semantically (the LLM judges clusters directly for pools under ~100 queries;
   use the embedding script in `references/query-fanout.md` for pools over ~100 queries). Show
   the clusters with their member queries so the user can sanity-check.
3. Score each cluster on **demand** (sum of GSC impressions; mark fan-out-only clusters
   "trace-backed" or "model-generated" — never invent numbers), **coverage** (is the concept
   present in the CURRENT title + description? 0 absent / 0.5 implied / 1 explicit, judged
   semantically), and **suitability** (does this intent belong in THIS page's snippet, per the
   Step 5a decode and page type?).
4. Gap score = demand x (1 - coverage), computed only for suitable clusters. Output the **top 2
   gaps (max 3)** that can plausibly fit a 155-character snippet alongside the page's core offer.
   The cap is a hard rule — more than 3 turns the framework into keyword stuffing. List
   high-demand-but-unsuitable clusters as one line each ("ranks here, belongs elsewhere") and
   exclude them from rewrites.
5. Feed the rewrites: rewrite candidate (b) in Step 7 must close the #1 gap. If it conflicts with
   the human-primary-job hook (candidate c), keep them separate — that is why there are 3
   candidates.

### Step 6. Score each listing

Score the user's listing AND each competitor on all 5 dimensions, using
`references/scoring-rubric.md` (read it first). For each score, show your work in one sentence —
a score without reasoning is not a score. A competitor that hits the human primary job (dimension
5) is the real threat; flag it.

### Step 7. Output the audit

For each page, produce:

- The query, current position, current CTR, and AI Overview status.
- A score table: the user's listing vs. each competitor across all 5 dimensions.
- The weakest sentence in the current meta description, flagged with a 1-sentence reason.
- **3 rewrite candidates** for the meta description, each under 155 characters, each pulling a
  different lever:
  - (a) fixes the **worst-scoring dimension** from Step 6,
  - (b) closes the **#1 coverage gap** from Step 5b,
  - (c) leads with the **human-primary-job hook** from Step 5a.
- **1 rewrite candidate** for the title tag, under 60 characters.
- A priority rating (high / medium / low) based on impressions and how far the listing trails
  the strongest competitor.

Apply the three rewrite principles to every candidate (scoring-rubric.md -> "Rewrite principles"):
replace category words with concrete differentiation, front-load the strongest differentiator
into the first 60 characters, and remove words shared by 3+ competitor snippets on this SERP.
Count characters — do not estimate. A meta description at 156 characters fails the test.

### Step 8. Summarize

At the end of the audit, give the user:

- The 3 pages to rewrite first, with reasoning.
- The **1 pattern** that recurs across pages, named by mechanism, not vaguely (e.g. "your first
  sentence restates the H1 on 8 of 10 pages; none add new information in the first 60
  characters"). This is usually the most valuable line in the output.
- A note on anything in the data that surprised you, and any uncertainty worth flagging.

### Step 9. Populate the audit log

Offer to fill the log spreadsheet bundled at `assets/meta-audit-log.xlsx` (columns explained in
`references/audit-log-columns.md`). One row per rewritten page: original meta, shipped rewrite,
ship date, and the before/after impressions and CTR fields to backfill at 30 days.

Tell the user: "The log matters. A single rewrite is one tactic; a column of 30-day CTR deltas
across audited pages is evidence you can use to defend organic investment in a budget
conversation."

### Step 10. Hand off

Confirm what was produced, where the log lives, and what to revisit in 30 days (backfill the
after-columns, read the CTR delta, roll back anything -5% or worse). Keep the log in the same
place every month so the deltas accumulate.

## Working rules

These rules exist because the audit fails silently if you violate them. Treat them as hard
constraints.

- **Never score a personalized SERP.** Retrieve in incognito; discard any SERP with
  personalization markers and re-fetch cleanly.
- **Do not hallucinate SERPs.** If you cannot retrieve a live SERP and the user has not pasted
  one in, say so and stop.
- **Do not invent competitor descriptions, impressions, positions, or fan-out demand.** If a
  data point is missing, ask for it or mark it "model-generated".
- **Use the user's actual data wherever possible.** Do not substitute illustrative examples.
- **Keep rewrites under the character limits.** Count characters, do not estimate. 155 for meta
  descriptions, 60 for title tags.
- **Stay in scope.** Insights end at the snippet. No page-level, content, or product
  recommendations — compress any such insight to one neutral sentence in the notes and move on.
- **If unsure whether a finding is real or an artifact of the data, say so.** The user would
  rather know about uncertainty than be told a confident wrong answer.

## Stack-specific notes

The workflow adapts to whatever the user has connected:

| Stack | What's connected | What the audit produces |
| --- | --- | --- |
| MCPs connected | GSC MCP (or pasted export), Semrush/Ahrefs MCP, web fetcher | Near-full audit. GSC pull, SERP retrieval, AIO checks, scoring, decode, gap analysis, and rewrites automated. |
| Browser only | Web browsing for SERPs, spreadsheet for output | Semi-automated. User pastes GSC export; the audit handles SERP retrieval and scoring. |
| No MCPs | Nothing | Manual. User pastes meta description plus 3-5 competitors per page, PAA, and related searches. Slower, but works. |

Semrush and Ahrefs MCPs use different parameter names and return shapes. If a tool call returns
empty, do not retry blindly. Print exactly what the tool returned, surface the mismatch to the
user, and ask whether to fall back to manual paste-in.

## Troubleshooting

Common failure modes and how to handle them are in `references/troubleshooting.md`. Read it if a
run produces empty results, suspicious rewrites, or output that feels hallucinated.

## What success looks like

A completed audit gives the user:

- A scored audit per page: their listing and 3-5 competitors across all 5 dimensions, each score
  justified in one sentence.
- An intent decode per page (micro-intents, human primary job, hook angles).
- The top 1-2 query-coverage gaps the current snippet misses.
- The weakest sentence flagged on each meta description, with reasoning.
- 3 meta description rewrites under 155 characters (worst dimension / top gap / job hook) and a
  title tag rewrite under 60 characters per page.
- A priority rating per page based on impressions and competitive gap.
- A pattern summary naming the 1 mistake repeated across pages.
- A populated row in the audit log per rewritten page, ready to measure 30-day CTR delta.

## Source

Framework and prompt adapted from Kevin Indig's Growth Memo audit pack, "The Meta Data Audit",
built on clickstream research into the AI Overview reading-mode shift (47.5% back-scrolling on
AIO SERPs; ~846,000 U.S. Google sessions, Feb-Mar 2026, analyzed by Eric Van Buskirk /
Clickstream Solutions with Surfer SEO data). The intent decode (Step 5a) is inspired by the
Intent Decoder approach (GPT Insights / Hanns Kronenberg).
