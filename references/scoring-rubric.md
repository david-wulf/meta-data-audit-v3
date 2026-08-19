# Scoring rubric

Each listing gets scored on 5 dimensions: differentiation density, front-load score, specificity
index, re-read survivability, and job alignment (v2). Use a 1-5 scale on each, where 5 is best.

Always show your work in 1 sentence per score. A score with no reasoning is not a score.

## 1. Differentiation density

The count of words in the meta description that also appear in 2 or more competitor descriptions
on the same SERP. Stop words (the, a, of, and, etc.) don't count.

Lower shared-word count is better. Shared category words are dead weight on an AI Overview SERP
because the AIO has already summarized the category for the user.

**Scoring:**
- **5**: 0-2 shared content words. The listing reads as genuinely different from the SERP.
- **4**: 3-5 shared content words.
- **3**: 6-9 shared content words.
- **2**: 10-13 shared content words.
- **1**: 14+ shared content words. The listing is mostly competitor vocabulary.

**Example.** SERP for "best project management software for agencies". Three competitor
descriptions all use "project management software" and "for agencies". A listing that repeats
both phrases shares 5 content words before adding anything new. Score: 4 at best, often 3.

## 2. Front-load score

Whether the strongest differentiator appears in the first 60 characters of the meta description.

The 60-character threshold matters because the AI Overview SERP pushes users into back-scrolling.
A buried differentiator gets missed on the second pass.

**Scoring:**
- **5**: The strongest differentiator is in the first 30 characters.
- **4**: The strongest differentiator is in the first 60 characters.
- **3**: The strongest differentiator is in characters 60-100.
- **2**: The strongest differentiator is in characters 100-155.
- **1**: There is no clear differentiator, or the first 60 characters are all category words.

**How to identify "the strongest differentiator".** It's the phrase a reader could not have
written before they read the listing. "Project management software" is not a differentiator;
"used by 12,000 agencies, with retainer billing built in" is.

## 3. Specificity index

The ratio of concrete differentiators to category words across the full meta description.

**Scoring:**
- **5**: Mostly concrete (numbers, named features, named integrations, named outcomes). 1 or
  fewer category phrases.
- **4**: Mixed, but concrete dominates.
- **3**: Mixed, with category and concrete roughly balanced.
- **2**: Mostly category words, with 1 or 2 concrete details.
- **1**: All category words. The description could be on any competitor's page.

**Concrete tells:**
- A number ("24 hours", "12,000 agencies", "$0.02 per request")
- A named integration ("Salesforce", "Stripe")
- A named outcome ("cuts onboarding from 3 weeks to 4 days")
- A named constraint ("no credit card", "free for 5 users")

**Category tells:**
- "Best", "leading", "top", "powerful", "easy to use", "trusted by teams"
- Industry nouns with no qualifier: "platform", "solution", "tool"
- Generic verbs: "streamline", "optimize", "transform"

## 4. Re-read survivability

Whether the listing reads as redundant on a second pass.

The AI Overview SERP reading pattern (47.5% back-scrolling) means most users will see the
listing twice. The second look is the one that drives the click. A listing that reads as
redundant on pass 2 loses to one that reveals a second layer.

**Scoring:**
- **5**: The second pass reveals something the first pass missed. The reader thinks "oh,
  actually..."
- **4**: The second pass holds up. The listing doesn't feel redundant.
- **3**: Neutral. The second pass adds nothing but doesn't subtract either.
- **2**: The second pass feels slightly redundant. Reader thinks "yeah, I read that already."
- **1**: The second pass is pure repetition. Reader thinks "why is this here twice?"

**The re-read test:** read the description twice in a row. If the second read added information,
score 4 or 5. If it didn't, score 3 or below.

## Worked example

**Query:** "best CRM for small business"
**My listing:** "The best CRM for small business. Easy to use, powerful features, trusted by
thousands of teams. Start your free trial today."

| Dimension | Score | Why |
| --- | --- | --- |
| Differentiation density | 1 | Shares "best", "CRM", "small business", "easy to use", "free trial" with 3+ competitors. ~9 shared content words. |
| Front-load score | 1 | First 60 chars are pure category words. No differentiator visible. |
| Specificity index | 1 | Zero concrete details. Every phrase is reusable on any competitor's page. |
| Re-read survivability | 1 | Second pass is pure repetition. Adds nothing. |

**Rewrite candidates:**
1. "CRM with 24-hour Salesforce migration, free for 5 users. Built for teams under 50. No credit
   card." (97 chars, addresses specificity + front-load)
2. "The only CRM with retainer billing for agencies. Used by 12,000 small businesses since 2019."
   (93 chars, addresses differentiation density + specificity)
3. "Set up your pipeline in 8 minutes. Free forever for teams under 5, no credit card." (83
   chars, addresses front-load + re-read survivability)

Each rewrite targets a different scoring weakness. That's the test for whether you've written 3
candidates or just 1 candidate three times.

## 5. Job alignment (v2)

Whether the snippet addresses the human primary job behind the query (from the Step 5a intent
decode, see `intent-decode.md`), or just echoes the SERP-dominant pressure.

Score the user's listing AND each competitor. A competitor that hits the job is the real threat.

**Scoring:**
- **5**: Leads with the human primary job and resolves it credibly before (or while) making the
  offer.
- **4**: The job is addressed, but after the category/offer language.
- **3**: Partially touches a micro-intent but not the primary job.
- **2**: Pure SERP-dominant pressure (generic savings/buy claims) with one redeeming specific.
- **1**: Indistinguishable from the SERP-dominant noise. The user's unresolved question is
  ignored entirely.

**Example.** Query "Balkonkraftwerk mit Speicher"; decoded primary job: "decide safely whether
a battery pays off for my home and which size fits." A snippet opening with "Welche
Speichergroesse passt zu Ihrem Verbrauch?" scores 5; "Bis zu 1.108 EUR/Jahr sparen" scores 3
(touches the pays-off micro-intent, skips sizing/safety); "Jetzt kaufen - Top-Preise" scores 1.

**Caution:** if the decode found no real tension between SERP intent and the human job, this
dimension defaults to "does the snippet serve the dominant intent well?" - do not punish a
listing for missing a tension that does not exist.

## Rewrite principles (three reflexes — v3)

Apply all three whenever you propose a rewrite (Step 7). Each maps to a scoring dimension above.

1. **Replace category words with specific differentiation** (-> Specificity, Dim. 3).
   "Best CRM software" tells a re-reader nothing they don't already know. "CRM with Salesforce
   migration in 24 hours" gives the re-reader a specific reason to pick you on the second look.
   Concrete = a number, a named integration, a named outcome, or a named constraint.

2. **Front-load your strongest differentiator** (-> Front-load, Dim. 2).
   Cursor movement on AIO SERPs is vertically dominated, and the median user spends 47.5% of
   their scrolling going back up the page (vs. 27% without an AIO). A description gets read on
   the way down and again on the way back up — the opening has to carry it through both passes.
   The first 60 characters do more work than the last 60. Move your strongest claim there.

3. **Strip words shared by 3+ competitors** (-> Differentiation density, Dim. 1).
   Audit the meta description for words that appear in 3 or more competitor descriptions on the
   same SERP. Those words have lost their information value — replace them with something
   specific to your brand. (Scoring nuance: Dim. 1 already counts words shared with 2+
   competitors as dead weight for the score; the 3+ threshold is the conservative minimum bar
   for actively cutting a word during the rewrite.)
