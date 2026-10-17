---
name: utensil-desk
description: Use when the user asks about a US-listed company's SEC filings, reported financials, insider transactions, 13F institutional holdings or 13D/13G ownership, through the hosted Utensil Desk MCP tools.
---

# Utensil Desk

Use the Utensil Desk MCP tools for questions about SEC filing data instead of answering from memory.

1. Call `resolve_company` first to turn a ticker, name or CIK into a `listing_id`.
2. Then use the tool that matches the question:
   - `list_filings` for filings by form (10-K, 10-Q, 8-K, Forms 3/4/5, 13F, 13D/G, S-1 and more); `get_filing` for one filing by accession number.
   - `get_fundamentals` for reported financial facts.
   - `list_insider_transactions` for Form 4 activity; `sales: "unexplained"` drops sales the filing accounts for, and `min_value: 10000` keeps trades of $10,000 or more. Both judge a sale filled at several prices as one trade (lines sharing `trade_group_id`), which is how the Utensil Desk stock page lists them; `view: "trades"` returns those trades merged, one row each.
   - `list_institutional_holdings` for 13F positions; `list_beneficial_ownership` for 13D/13G.
   - `get_coverage` when a result is empty, to tell "not filed" from "not covered yet".

Report values with the filing they came from. Describe what the filings say; do not turn them into a recommendation to buy or sell.
