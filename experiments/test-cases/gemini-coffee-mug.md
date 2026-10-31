# Test case GEM-T01 — Coffee mug queries on Gemini app, AI Mode and AI Overviews, India vs US

- **Platforms:** Gemini app (web), AI Mode, AI Overviews. Manual runs (see `../methodology.md`, Compliance). Check Google's terms before any automation.
- **Status:** designed, not run.
- **Run alongside:** CGPT-T01 (`chatgpt-coffee-mug.md`). Same queries and probe products, so results are comparable across platforms.
- **Questions it answers:** Gemini report §11 gaps 2, 4, 8 and 10, and the India comparison in `reports/platform-comparisons.md`.

## Hypotheses

| ID | Hypothesis | Basis |
|---|---|---|
| H1 | From India, the Gemini app and AI Mode show product cards for Q01–Q05. | GEM-002 |
| H2 | AI Overviews appear on few of these short queries when logged out. | RES-038 |
| H3 | Amazon.in products appear in AI Mode/Gemini product cards even though Amazon blocks Google-Extended. | MKT-022, GEM-016 (Tier 3 lead) |
| H4 | Gemini-app citations never include amazon.in pages. | GOOG-027, RES-039 |
| H5 | An India-only Shopify probe with an approved Merchant Center feed appears in product cards; one without a feed does not. | SHOP-025, SHOP-032, GOOG-010 |
| H6 | Sponsored product items appear in AI Mode from India and are labeled. | GEM-008 |
| H7 | Gemini app and AI Mode show different product sets for the same query. | GEM-004, RES-034 |

## Queries

Use Q01–Q05 and Q01-US exactly as in `chatgpt-coffee-mug.md`. Add question forms, since AIO triggers more on questions [RES-038]:

| ID | Text | Market |
|---|---|---|
| Q06 | What is the best ceramic coffee mug under ₹1,000? | IN |
| Q07 | Which microwave-safe coffee mug should I buy for office use? | IN, US |

## Conditions

| ID | Surface | Location | Account | Device |
|---|---|---|---|---|
| G1 | Gemini app (web) | India, no VPN | logged-in fresh, Personal Intelligence off | desktop |
| G2 | AI Mode | India, no VPN | logged-out | desktop |
| G3 | AI Mode | India, no VPN | logged-out | mobile |
| G4 | Google Search (AIO) | India, no VPN | logged-out | desktop |
| G5 | AI Mode | US (collaborator), no VPN | logged-out | desktop |
| G6 | Gemini app (web) | US (collaborator), no VPN | logged-in fresh | desktop |

Device is fixed per condition: device changes AIO sources more than city does [RES-040]. Record the model name shown in the UI [GEM-005].

## Volume

- 8 runs per query per condition across 3 calendar days [RES-016].
- Run all conditions for a query on the same day.

## Probe products

Reuse the CGPT-T01 probe table. Add one column per probe: "Merchant Center feed approved? (Y/N)". The two India-only Shopify probes should differ on this column, to test H5.

## Recording

Use the JSON schema in `../methodology.md`. Extra fields:
- `surface` (gemini_app | ai_mode | aio)
- `aio_present` (bool, G4 only)
- `product_cards_present` (bool)
- `sponsored_items` (count, with label text)
- `buy_button_present` (bool, per item)
- `model_shown` (string)

## Analysis

| Metric | Per | Tests |
|---|---|---|
| Product-card presence rate | surface × condition × query | H1, H2 |
| Amazon.in presence in cards vs citations | surface | H3, H4 |
| Probe appearance rate by feed status | probe | H5 |
| Sponsored share and labeling | AI Mode conditions | H6 |
| Jaccard of product sets, Gemini app vs AI Mode, same day | query | H7 |

Findings go to `../findings/` and the registry as `EXP-###`.

## Merchant-side cross-check

For probes AURA controls, export the Merchant Center AI performance report (English queries, India) for the same weeks [GOOG-017]. Compare its share-of-voice trend with observed appearance rates.

## Known limits

- Results describe outputs under these conditions only.
- Personalization is excluded by design (logged-out or fresh accounts). Personal Intelligence and Search history are known to change results [GEM-011].
