# Troubleshooting

Common failure modes for the meta data audit and how to handle them.

## The model says it can't retrieve a SERP

Some models won't fetch live SERPs without a web fetcher MCP connected. If yours can't, either:

- Connect a web fetcher MCP (built-in browser tool, Ahrefs, Semrush, or similar)
- Fall back to the manual stack: paste in 3-5 competitor listings per query yourself

Don't let the audit guess at SERPs. Empty data is better than fabricated data.

## The audit returns empty or wrong results

Usually an MCP issue, not a prompt issue.

Ask the model to print exactly what it received from each tool call before it scored anything.
If the tool returned an empty array, the prompt is doing the right thing with the wrong input.
Reconnect the MCP and re-run.

Semrush and Ahrefs MCPs in particular have different parameter shapes. A call that worked on
Semrush won't work on Ahrefs without parameter renaming.

## The rewrites all sound similar

The audit asks for 3 rewrites that each address a different weakness. If they're converging,
your meta description likely has 1 dominant weakness, not 3.

Ask the model: "which scoring dimension drove each rewrite?" The reasoning often surfaces a
deeper pattern. If all 3 rewrites are targeting specificity, that's your real problem.

## The model is making things up

If you suspect hallucination, ask: "show me the exact text you used as input for the scoring on
this page." If the model can't produce the source data, it invented it.

Stop. Fix the data. Restart from Step 5 (pull the competitive set).

## The character counts are wrong

Models are notoriously bad at counting characters. If a rewrite candidate "feels long", paste it
into a character counter (or ask the model to count character by character, not estimate).

The hard limits are 155 for meta descriptions and 60 for title tags. Anything over is a fail.

## The AI Overview check is unreliable

AI Overview presence varies by location, device, and query refresh. If you check a query and see
no AIO, then re-check an hour later and see one, both readings can be true.

Two ways to handle:

1. Check the query twice from different locations (incognito + VPN if needed). Use the more
   common result.
2. Use a third-party SERP API (Semrush, Ahrefs) that reports AIO presence over a longer window.

If neither is available, skip the AIO filter for that query and audit it anyway. The 4-dimension
framework still works; you just lose the prioritization signal.

## The model wants to skip steps

The audit is 8 steps for a reason. If the model jumps from Step 2 to Step 6, the scoring is
running on assumptions instead of data.

If you notice steps being skipped, tell the model to restart at the last fully completed step
and walk through the remaining steps in order. Quality drops sharply when steps are merged.

## The pattern summary in Step 8 is vague

"You should be more specific" is not a pattern. A real pattern names the mechanism:

- "Your first sentence is always the H1 of the page restated. None of your top-10 pages have a
  meta description that adds new information in the first 60 characters."
- "You name a competitor or category in 8 of 10 audited pages, but never name a specific
  product feature."

If the model's summary feels vague, ask: "name the specific behavior, give me an example from 2
of the audited pages, and tell me what to write instead."
