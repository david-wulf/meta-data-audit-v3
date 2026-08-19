# Pulling Search Console data for the audit

Google Search Console has no official MCP at the time this skill was written, so GSC data is
always pasted in by the user once at the start. It's a 2-minute task.

## What the audit needs, per page

- Page URL
- Top 3-5 queries driving impressions to that page
- Impressions per query (last 28 or 90 days)
- Average position per query
- Current CTR per query

## 3 ways to pull it

### 1. Export the Performance report (fastest)

1. In Search Console, go to **Performance**.
2. Set the date range to 28 days (90 if you want more signal).
3. Filter by page if you're auditing one page at a time.
4. Click **Export** and choose Google Sheets or CSV.

The export includes every field the audit needs.

### 2. Use the Pages tab (more deliberate)

1. Sort pages by impressions.
2. Pick the top 10-20.
3. Click into each to see its top queries.

Slower than the export, but it lets you choose pages by intuition rather than just by volume.

### 3. Pull from Looker Studio (cleanest for teams)

If your GSC data already flows into Looker, build a page-by-query table with impressions,
position, and CTR. Best if a team is going to run this monthly.

## Format to paste

Any of these formats work. The skill will parse:

**Table:**

```
URL | Query | Impressions | Position | CTR
/pricing | best crm pricing | 4,200 | 6.3 | 2.1%
/pricing | crm cost comparison | 1,800 | 4.1 | 3.4%
```

**CSV:**

```
url,query,impressions,position,ctr
/pricing,best crm pricing,4200,6.3,2.1%
/pricing,crm cost comparison,1800,4.1,3.4%
```

**Screenshot:** also fine. Paste the screenshot and the skill will read the numbers off it.

## What if you skip GSC data

The audit still runs, but you lose:

- Traffic prioritization (no way to sort pages by impression volume)
- The "is this query worth rewriting for" check (no impressions number to compare against)
- The 30-day before/after CTR delta (can still be added later if you backfill)

The skill will name the pages and queries you want to audit instead. Manual but workable.
