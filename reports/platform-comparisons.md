# Platform comparison — ChatGPT vs Google (Gemini app, AI Mode, AI Overviews)

As of 2026-10-31. Every cell cites registry IDs. Platform reports: `research/ai-platforms/chatgpt/report.md`, `research/ai-platforms/gemini/report.md`.

## Product data and discovery

| Question | ChatGPT | Google AI surfaces |
|---|---|---|
| Main product index | Not named. Inputs: first- and third-party structured metadata, crawled pages, model knowledge [CGPT-012, CGPT-019] | Shopping Graph, 60+ billion listings [GOOG-019, GEM-001] |
| Merchant feed | ACP/OpenAI feed, approved partners only, US by default [CGPT-025, CGPT-031] | Merchant Center, open to all, free listings on by default [GOOG-010] |
| Shopify path | Shopify Catalog, default-on, US buyers required [SHOP-001, SHOP-003] | Merchant Center via Google & YouTube app [SHOP-025] |
| Crawler that controls inclusion | OAI-SearchBot [CGPT-004, CGPT-006] | Googlebot (Search, AIO, AI Mode); Storebot-Google (Shopping); Google-Extended (Gemini grounding only) [GOOG-026, GOOG-027, GOOG-031] |
| Extra site-level AI switch | None documented | Search Console "Search generative AI control" [GOOG-028] |
| Named search providers | Microsoft, Shopify [CGPT-002] | Google's own index |

## Ranking

| Question | ChatGPT | Google AI surfaces |
|---|---|---|
| Product selection | Model-judged relevance; query + Memory + Custom instructions [CGPT-011] | "Search quality and ranking systems"; no product factors documented [GEM-007] |
| Seller ordering for one product | Availability, price, quality, maker/primary seller [CGPT-015] | No rule published [GOOG-035] |
| Checkout integration and rank | Was a factor in 2025, removed [CGPT-016] | "Does not influence how we rank your offers" [GOOG-003] |
| Closest published factor list | Merchant list (above) | Shopping "Top recommendations": relevance, ratings, price, features [GOOG-022] |
| Feed fields aimed at AI | Reviews, ratings; no popularity field [CGPT-030] | Conversational attributes incl. Q&A and `popularity_rank` [GOOG-012, GOOG-014] |
| Structured data | Not mentioned by OpenAI | "Isn't required" for generative AI search [GOOG-029] |

## Ads

| Question | ChatGPT | Google AI surfaces |
|---|---|---|
| Ads near product answers | One labeled unit below the answer; Free and Go plans [CGPT-043] | Sponsored items inside AI Mode product lists; Highlighted Answers; Direct Offers [GEM-008, GEM-009] |
| Stated separation | Ads don't influence answers [CGPT-042] | Ads don't influence organic AI answers [GEM-007] |
| India | Advertiser self-serve only documented [CGPT-046] | Ads in AI Mode since 2026-10-28 [GEM-008] |

## Checkout

| Question | ChatGPT | Google AI surfaces |
|---|---|---|
| In-surface checkout | Standalone Instant Checkout dropped 2026-03-24; beta for select marketplaces [CGPT-021, CGPT-023] | UCP checkout "hundreds of thousands" of brands; Universal Cart (US) [GEM-015, GEM-014] |
| Shopify merchants | Referral to merchant checkout [SHOP-002] | Direct checkout default-on for US/CA/AU buyers [SHOP-026, SHOP-027] |

## India

| Question | ChatGPT | Google AI surfaces |
|---|---|---|
| Shopping results documented for Indian users | No [CGPT-046] | Yes: Gemini app (EN, HI), AI Mode (EN) [GEM-002] |
| India-only Shopify store can enter the product pipeline | No (Catalog channel needs US buyers) [SHOP-003] | Yes (Merchant Center supports India) [SHOP-032] |
| First-party visibility report for India | None found | Merchant Center AI performance (English queries) [GOOG-017] |
| Amazon.in | All OpenAI agents blocked [MKT-001] | Googlebot allowed; Google-Extended blocked [MKT-022] |
| Flipkart | No OpenAI relationship found [MKT-016] | Named UCP partner; Storebot allowed [GEM-016, MKT-025] |

## What this means for a Shopify merchant

- The two platforms take product data through different pipes: Shopify Catalog for ChatGPT, Merchant Center for Google. Each needs its own setup check [SHOP-001, SHOP-025].
- For an India-focused store, Google is the only documented AI shopping surface today [GEM-002, CGPT-046].
- Neither platform documents a ranking boost for any feed field, markup, protocol or checkout integration. Both document price and availability as inputs: OpenAI in its merchant ordering [CGPT-015], Google in "Top recommendations" [GOOG-022].
