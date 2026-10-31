# Test case CGPT-T01 — Coffee mug queries, India vs US

- **Platform:** ChatGPT (consumer web app). Manual runs only (see `../methodology.md`, Compliance).
- **Status:** designed, not run.
- **Questions it answers:** report §10 gaps 5 and 10; the India inference in report §9.

## Hypotheses

| ID | Hypothesis | Basis |
|---|---|---|
| H1 | From an India location, ChatGPT shows no product carousel for these queries; answers are text with citations. | CGPT-022, CGPT-031, CGPT-046 (inference) |
| H2 | From a US location, ChatGPT shows a product carousel for the USD variants. | CGPT-011, CGPT-022 |
| H3 | Amazon.in product pages never appear as cited sources; at most as navigational links. | MKT-001, CGPT-006 |
| H4 | Flipkart product pages can appear as cited sources from India. | MKT-008 |
| H5 | Shopify stores that sell to the US appear in US carousels; India-only Shopify stores do not. | SHOP-001, SHOP-003 |
| H6 | Item sets vary heavily across same-day repeats. | RES-014, RES-016, RES-022 |

## Queries (fixed strings — never edit; add new IDs instead)

| ID | Text | Market |
|---|---|---|
| Q01 | Best ceramic coffee mug under ₹1,000 | IN |
| Q02 | Premium handmade coffee mug | IN, US |
| Q03 | Microwave-safe coffee mug | IN, US |
| Q04 | Best coffee mug for office use | IN, US |
| Q05 | Minimalist coffee mug with a wooden handle | IN, US |
| Q01-US | Best ceramic coffee mug under $15 | US |

## Conditions

| ID | Location | Account | Personalization | Plan |
|---|---|---|---|---|
| C1 | India, no VPN | logged-out | none | — |
| C2 | India, no VPN | logged-in, fresh account | Temporary Chat (no memory, no ads) | Free |
| C3 | US, physical location (collaborator), no VPN | logged-out | none | — |
| C4 | US, physical location (collaborator), no VPN | logged-in, fresh account | memory off, normal chat | Free (ads may appear; label them) |

VPN-based US runs are a separate, weaker condition. Record VPN use if a US collaborator is unavailable.

## Volume

- 8 runs per query per condition (RES-016: per-brand detection SE < 0.10 needs 7–8).
- Spread over 3 calendar days. All conditions for a query on the same day.
- Total: 6 queries × relevant conditions × 8 runs ≈ 160–200 runs.

## Probe products (fill before the first run)

Capture ground truth on each run day from the product's own page.

| Probe | Seller type | Store/marketplace | URL | Sells to US? | Ground truth (price, stock, material, GTIN) |
|---|---|---|---|---|---|
| P1 | Shopify, sells to US and IN | | | yes | |
| P2 | Shopify, sells to US and IN | | | yes | |
| P3 | Shopify, India only | | | no | |
| P4 | Shopify, India only | | | no | |
| P5 | Amazon.in listing | | | — | |
| P6 | Flipkart listing | | | — | |
| P7 | Etsy listing | | | yes | |
| P8 | Independent non-Shopify store | | | | |

Shopify detection: record the method (e.g. `/cart.js` response, `cdn.shopify.com` assets). It is an inference.

## Recording

- One JSON per run per `../methodology.md`, plus a full-page screenshot.
- Extra fields for this test: `carousel_present` (bool), `merchant_list` (array, when a product is opened), `ad_units` (count and labels).

## Analysis

| Metric | Per | Tests |
|---|---|---|
| Carousel presence rate | condition × query | H1, H2 |
| Source-type share (marketplace / Shopify / other) | condition | H3, H4, H5 |
| Probe appearance rate | probe × condition | H5 |
| Amazon.in and Flipkart citation counts | condition | H3, H4 |
| Mean pairwise Jaccard of item sets | query × condition × day | H6 |
| Attribute accuracy vs ground truth | probe | report §6 |

Findings go to `../findings/` with run IDs. Promote to the registry as `EXP-###`, classification EXPERIMENTALLY OBSERVED, with conditions and limits.

## Known limits

- Results describe outputs under these conditions only. They do not reveal the ranking algorithm.
- Model updates during the run window change results (RES-004). Record the model shown in the UI and any release notes in the window.
