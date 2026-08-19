# Intent decode framework

A psychological read of the query, reconstructed from SERP evidence. The goal is NOT another
informational/transactional label. The goal is to find the gap between what the SERP rewards and
what the human is actually trying to get done — and turn that gap into snippet hooks.

Inspired by the Intent Decoder approach (GPT Insights / Hanns Kronenberg): treat the query as a
shorthand for a decision the user is trying to make safely, not as a string to match.

## Inputs (all from Step 5 capture + Step 3 GSC data)

Do not decode from intuition alone. Every claim in the decode must trace back to one of:

- PAA questions, verbatim
- Related searches, verbatim
- The domain/format mix of the top 10 (shops vs. tests vs. forums vs. official)
- Commercial SERP features (shopping unit size, compare sites, ads density)
- Content SERP features (videos, featured snippets)
- The page's GSC query list (modifiers reveal micro-intents: "test", "lohnt sich",
  "komplettset", wattage numbers, "erfahrungen", price modifiers)

## Output format (per page / head query)

1. **SERP-dominant intent.** What Google currently rewards, in one sentence, with the evidence
   ("8 of 10 results are shops, 6-product shopping unit → strong purchase pressure").
2. **Micro-intents.** 3-5 questions hiding behind the query, phrased as the user would think
   them. Each must cite its evidence (a PAA question, a query modifier, a SERP feature).
3. **Human primary job.** One sentence: what the person is trying to get done, safely. Format:
   "Decide/find/confirm X for my situation Y without risk Z."
4. **Tension.** Where the SERP-dominant intent and the human primary job diverge. If they don't
   diverge, say so — not every SERP has a tension, and inventing one corrupts the hooks.
5. **Hook angles (1-2).** Snippet-ready angles that exploit the tension. Each hook must be
   phraseable inside 155 characters together with the page's core offer. A hook is an angle,
   not finished copy — the rewrite step turns it into copy.

## What makes a good hook angle

- It answers a micro-intent that no competitor snippet on this SERP addresses.
- It is compatible with the page's actual content (don't hook "calculator" if the page has no
  calculator — the snippet is a promise the page must keep).
- It survives the re-read test: on second pass, it reads as the one listing that understood
  the question.

## Hard scope rule

The decode ends at hook angles. No page recommendations, no content briefs, no product advice.
If the decode reveals that the page itself cannot serve the human primary job, write exactly one
neutral sentence in the audit notes (e.g., "the dominant micro-intent X is not served by this
page type") and move on. Anything more is outside this skill.

## Worked example

**Query:** "Balkonkraftwerk mit Speicher" (DE, shopping)

**Evidence captured:** PAA: "Wie sinnvoll ist ein Balkonkraftwerk mit Speicher?", "Sind 2000
Watt erlaubt?", "Was ist aktuell das beste...?". Related searches lean "Test", "Testsieger",
"Stiftung Warentest". Top 10 = 7 shops + 3 editorial tests. 6-product shopping unit, compare
sites, videos present.

**Decode:**

1. *SERP-dominant intent:* Purchase push — shops and product sets with savings claims dominate;
   shopping unit adds price pressure.
2. *Micro-intents:* "Does a battery actually pay off for me?" (PAA "sinnvoll"); "What size/
   wattage fits my consumption and is legal?" (PAA "2000 Watt erlaubt", wattage queries in GSC);
   "Which vendors are credible vs. marketing?" (related searches "Test/Testsieger"); "Can I use
   solar power in the evening?" (the implicit reason for "mit Speicher").
3. *Human primary job:* Decide safely whether a storage battery pays off for my home and which
   size fits — before spending 700+ euros.
4. *Tension:* Every shop snippet shouts "save & buy now"; the user first needs a credible
   pays-off-and-fits answer. The SERP sells; the user still evaluates.
5. *Hook angles:* (a) Sizing certainty — "which storage size fits your consumption" as the
   lead-in, offer follows. (b) Verifiable payoff — a concrete, calculated payback figure framed
   as an answer ("pays off in X years at Y kWh"), not as a marketing claim.

A snippet built on hook (a): "Welche Speichergröße passt zu Ihrem Verbrauch? Komplettsets ab
749,99 € — mit Notstromfunktion & App." — answers the job, then sells. Every competitor does it
the other way around.

## Job alignment scoring (dimension 5)

The decode feeds the 5th scoring dimension. Score the user's listing AND each competitor:

- **5**: The snippet leads with the human primary job and resolves it credibly before (or while)
  making the offer.
- **4**: The job is addressed, but after the category/offer language.
- **3**: The snippet partially touches a micro-intent but not the primary job.
- **2**: Pure SERP-dominant pressure (e.g., generic savings/buy claims) with one redeeming
  specific.
- **1**: Indistinguishable from the SERP-dominant noise. The user's unresolved question is
  ignored entirely.

As always: every score comes with a 1-sentence justification citing the decode.
