# aws-claude-agent

Independent research track. Self-contained: does not read from or write to any other folder in this
repo. Follows the evidence rules in `/CLAUDE.md` but keeps its own registry so IDs cannot collide
with the main one.

**Research question (round 1):** When a user asks ChatGPT a shopping question such as "best running
shoes under $100", what mechanism selects and displays the products, and what can an independent
Shopify merchant change to be selected?

**Platform chosen:** ChatGPT (OpenAI). Reason: OpenAI publishes a merchant-facing product feed spec,
a crawler policy, a commerce policy, merchant feed terms, and a named ranking-factor list, and
Shopify publishes a matching merchant-side integration. Gemini has a comparable surface
(UCP + Google Merchant Center) but its ranking documentation is thinner. Gemini is round 2.

## Files

| File | What it is |
|---|---|
| `01-chatgpt-shopping-pipeline.md` | Step-by-step mechanism: query → retrieval → ranking → product card → checkout |
| `02-shopify-merchant-playbook.md` | What a merchant implements, in priority order, with code and test procedures |
| `03-evidence-registry.md` | Every source, with tier, excerpt, access date, and the claims it supports |
| `04-reading-list.md` | Primary docs and third-party articles, all URLs status-checked this session |
| `05-gaps-and-experiments.md` | What no source establishes, contradictions found, and experiment designs |
| `notes/raw/` | Raw captures. Unedited. No interpretation. |

## Reading order

Read `01` for the mechanism, `02` to act on it, `05` before you trust anything in `01` that is
marked as inference.

## Status

Round 1 complete. All sources accessed 2026-10-30. Re-fetch before 2027-01-28 (90 days).
