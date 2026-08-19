# Query coverage gap analysis

Finds real demand the current title/description ignores. Two sources of demand: queries the
page already ranks for (GSC), and queries AI systems generate when expanding the head query
(fan-out). Both are checked against the snippet semantically.

## 1. Build the query pool

Merge, then dedupe:

- **GSC queries** for the page: non-brand, position ≤ 20, top 50-100 by impressions over the
  last 90 days. Brand queries are excluded BEFORE pooling using the two-pass method from
  SKILL.md Step 3 (domain-derived fuzzy regex + post-filter review for leftovers).
- **Native fan-out set**: 10-20 sub-queries generated from the head query using the documented
  fan-out types Google's AI Mode uses:
  - *related* (adjacent topics: "Speicher nachrüsten")
  - *implicit* (the unstated need: "Solarstrom abends nutzen")
  - *comparative* ("X vs Y", "Testsieger", "welches ist das beste")
  - *procedural* ("anmelden", "anschließen", "erlaubt")
  - *specification* (wattage, capacity, price brackets — the modifiers buyers actually type)
- **Google's own fan-out trace**: PAA questions and related searches captured in Step 5,
  verbatim. These are mandatory — they anchor the native fan-out in observed data. If the
  native set and the trace diverge wildly, trust the trace and say so.
- **Optional external import**: if the user ran GRAIL, Locomotive AI Coverage, Otterly, Qforia,
  or a similar fan-out tool, accept the pasted query list and merge it here. Mark its origin.

## 2. Cluster

Group the pool into semantic clusters (a cluster = one concept a snippet could address, e.g.
"sizing/wattage", "is it worth it", "complete set", "legality/800W").

- **Pools under ~100 queries (default):** the LLM clusters directly. No embedding setup needed.
  Show the clusters with their member queries so the user can sanity-check.
- **Pools over ~100 queries (domain-scale runs):** use embeddings. Suggested setup in the
  sandbox: `pip install sentence-transformers --break-system-packages`, model
  `intfloat/multilingual-e5-small` (works for German), agglomerative clustering with cosine
  distance threshold ~0.25. Cache embeddings per run. If the environment can't install the
  model, fall back to LLM clustering on the top 100 by impressions and say so.

## 3. Score each cluster

| Metric | How | Notes |
| --- | --- | --- |
| **Demand** | Sum of GSC impressions of member queries | Fan-out-only clusters (no GSC member): demand = "trace-backed" if present in PAA/related searches, else "model-generated". Never invent numbers. |
| **Coverage** | Is the cluster's concept present in the CURRENT title + description? Judge semantically, not by string match. 0 = absent, 0.5 = implied, 1 = explicit. | "Komplettpaket" covers "komplettset" (synonym, ~1). "Jetzt bestellen" does not cover "lohnt sich" (different concept, 0). |
| **Suitability** | Does this cluster's intent belong in THIS page's snippet? Judged via the Step 5a intent decode (micro-intents + page type), NOT via embedding distance. | "test/testsieger" ranks near a shop page semantically but belongs to editorial intent — suitability low unless the page has credible test evidence. |

## 4. Gap score and output

- Gap score = demand × (1 − coverage), computed only for suitable clusters.
- Output the **top 2 gaps** (max 3) that can plausibly fit a 155-character snippet alongside
  the page's core offer. The cap is a hard rule: more than 3 reported gaps turns the framework
  into a keyword-stuffing engine, which contradicts the differentiation scoring.
- For each gap: cluster name, demand figure (or "trace-backed"/"model-generated"), example
  member queries, and the 1-sentence reason the current snippet misses it.
- High-demand but unsuitable clusters: one line each — "ranks here, belongs elsewhere" — and
  excluded from rewrites. No further recommendation (scope rule).

## 5. Feed the rewrites

Rewrite candidate (b) in Step 7 must close the #1 gap. If the #1 gap conflicts with the
human-primary-job hook (candidate c), keep them separate — that's exactly why there are 3
candidates.

## Worked example (compressed)

Page: shop collection for "Balkonkraftwerk mit Speicher". GSC shows "balkonkraftwerk komplettset
mit speicher" (1,158 impressions, 0 clicks), wattage queries ("800w", "2000w"), "kaufen"
variants, "test/testsieger" variants.

- Cluster "complete set": coverage ~1 ("Komplettpaket" in snippet) → no gap despite demand.
- Cluster "wattage/capacity sizing": demand high (sum of wattage queries), coverage 0 (no
  number of watts/kWh in snippet), suitability high (spec-driven buyers, shop page) →
  **top gap**. One competitor (snippet with "800W- oder 1000W... 1,6 bis 2 kWh") already
  exploits it.
- Cluster "test/testsieger": demand high, suitability low for a shop snippet without test
  evidence → "ranks here, belongs elsewhere"