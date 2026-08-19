# Audit log column spec

The audit log is the most useful artifact from this workflow. A single rewrite is a tactic; a
column of 30-day CTR deltas across audited pages is evidence.

The bundled spreadsheet at `assets/meta-audit-log.xlsx` already has these columns set up. This
doc explains what goes in each one.

## Columns

| Column | What goes in it | When to fill it |
| --- | --- | --- |
| Page URL | The full URL of the page being audited. | At audit time. |
| Top AIO query | The highest-impression query for this page that triggers an AI Overview. | At audit time. |
| Audit date | When the audit ran. YYYY-MM-DD. | At audit time. |
| Original meta | The meta description before the rewrite. Copy it verbatim. | At audit time. |
| Rewrite shipped | The version actually deployed. Often a blend of the 3 candidates. | When the rewrite goes live. |
| Ship date | When the rewrite went live. YYYY-MM-DD. | When the rewrite goes live. |
| Impressions 30d before | From Search Console, for the top AIO query. The 30 days before the ship date. | Day the rewrite ships. |
| Impressions 30d after | From Search Console, same query. The 30 days after the ship date. | 30 days after ship. |
| CTR 30d before | From Search Console, same query. | Day the rewrite ships. |
| CTR 30d after | From Search Console, same query. | 30 days after ship. |
| CTR delta | (CTR after - CTR before) / CTR before. Auto-calculated. | Auto. |
| Notes | What you'd do differently next time. | Anytime. |

## How to read the delta column

- **+10% or more.** Strong win. Capture what the rewrite did differently and apply it to similar
  pages.
- **+0 to +10%.** Marginal. Could be noise, could be real. Watch the next 30 days.
- **-5% to +0%.** Likely noise. Move on.
- **-5% or worse.** The rewrite hurt. Roll back, study what changed, try again.

## How to use the log in a budget conversation

The 30-day CTR delta column, across 10-20 audited pages, is the most defensible artifact this
workflow produces. It shows that the team is measuring outcomes, not just shipping tactics.

When organic budget gets questioned, the log answers: "we rewrote 18 pages, 14 of them had CTR
gains over 30 days, weighted average +12%, here's the math".

Don't lose the log. Keep it in the same place every month.
