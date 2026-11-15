---
name: utensil-desk
description: Research a US-listed stock, explain a Utensil Desk chart or valuation, or investigate financials, company guidance and fund ownership using connected Utensil Desk MCP tools and filing-linked evidence. Use for investment questions as well as specific SEC data requests.
---

# Utensil Desk

Use the connected tools first for the evidence they cover. They reach the same data as Utensil
Desk's REST API; a working MCP connection does not need another REST key or installation.
Use the tools actually listed by the client, rather than assuming an unpublished tool is available.
If the connection is absent, use the client's connection flow at https://mcp.utensildesk.com;
never ask the user to paste credentials into the conversation.

## Start with the question

A known ticker can be passed directly as `listing_id`. Use `resolve_company` for a name, CIK or
ambiguous identity; funds and people use the returned filer identity.

For a broad question such as "Is NBIS worth looking at?", establish the latest reported results,
funding needs, management's outlook and material changes. Start with `get_fundamentals` using
`statement: income`, `balance` or `cash_flow` and `view: table`, plus `list_news`, `list_commitments`
and `get_coverage` for that ticker as relevant. Add ownership and other disclosures when they bear
on the question. For a narrow request, call only the relevant tools. Keep the first answer compact;
more returned data is not a better explanation.

| Question | Tools and interpretation |
|---|---|
| Growth, profitability, cash needs or dilution | `get_fundamentals`; compare matching periods and shares outstanding. Use `get_fact` for a row's filing, formula and component evidence. |
| Outlook, delays or changed targets | `list_commitments`, `list_commitment_changes`, `get_commitment`, and `list_news`. Read source dates and sentences; a target is management guidance, not a forecast you verified. Different deadlines can leave old and new targets in separate lineages. |
| Revenue backlog or funding | `get_financial_commitments`, `list_debt_disclosures`, and financial statements. Check currentness and qualifications. Do not add overlapping obligations or equate prepayments with profit. |
| Valuation or sales catching up with price | `get_valuation` with the supplied price and its actual date; `list_per_share_history` for denominators. `get_multiple_history` needs caller-supplied daily closes. The API does not provide quotes, candles or RSI. |
| Fund ownership | `list_institutional_holdings`; `list_manager_holdings` and `list_manager_holding_changes` for a fund. State the quarter end and filing date. Market value held is not purchase cost. Missing positions are not confirmed sales. |
| Insider transactions | `list_insider_transactions`; `view: trades` groups price-split executions. `sales: unexplained` filters out sales explained by the filing; it does not establish suspicious conduct. |
| Large owners | `list_beneficial_ownership` for Schedules 13D/13G; distinguish reported stakes from 13F portfolios. |
| Filing or agreement evidence | `list_filings`, `get_filing`, `list_agreements`, `get_agreement`. Filing tools return metadata and links, not arbitrary full document text. Agreement tools provide only the evidence they return. |

## Check the evidence before concluding

- Inspect period ends, publication dates, `meta.unavailable`, `known_gaps`, endpoint-specific
  coverage and `next_cursor`, including when the result is nonempty. A dataset's healthy ingest
  does not establish that this company's newest figures are normalized.
- A table omits detailed evidence to stay small. Retrieve fact detail for material derived claims.
  Follow required pages before counting funds or calculating aggregate changes; a top-holders page
  cannot establish the chart's aggregate flow. Say when a result is partial.
- Do not silently substitute an annual figure for current TTM data. Check that the periods support
  the proposed comparison. A price without a date cannot establish a historical valuation; don't
  relabel a screenshot's quote as today's. Respect unavailable share-basis results.
  A hypothetical valuation using today's available filings and a supplied price is possible if
  explicitly labeled hypothetical, not a reconstruction of the screenshot. Annualized monthly
  run-rate revenue, realized annual revenue and trailing twelve-month revenue are different measures.
- For a screenshot, read its ticker, period, price and selected disclosure. Treat its numbers as
  user-provided evidence, then compare corresponding API records. A mismatch calls for an
  explanation, not a claim that the screenshot came from another product.
- If the API cannot answer a material question, name the precise limitation: missing filing,
  unprocessed extraction, stale period, unsupported field or caller-supplied price requirement.
  Do not describe absent data as zero or assume a linked document has been read. If external
  research is allowed, use original sources to fill that explicit gap and distinguish it from API
  evidence. For an API-only request, keep the unresolved gap visible instead.

## Answer the investment question

Give a reasoned assessment with the strongest supporting evidence, the main risks and what remains
unknown. Distinguish reported facts, management guidance, your calculations and your judgment.
Cite the returned filing/source links and date material figures. Fund buying, a large price decline
or a low RSI alone does not establish value. Events alongside a price move do not establish its
cause. Explain what would strengthen or weaken the thesis without promising a return or turning
filing events into instructions to trade.
