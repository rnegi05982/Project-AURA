# Platform comparison — ChatGPT vs Google (Gemini app, AI Mode, AI Overviews)

As of 2026-10-31. Every cell cites registry IDs. Platform reports: `research/ai-platforms/chatgpt/report.md`, `research/ai-platforms/gemini/report.md`.

## Product data and discovery

| Question | ChatGPT | Google AI surfaces |
|---|---|---|
| Main product index | Not named. Inputs: first- and third-party structured metadata, crawled pages, model knowledge <sup>[CGPT-012, CGPT-019]</sup> | Shopping Graph, 60+ billion listings <sup>[GOOG-019, GEM-001]</sup> |
| Merchant feed | ACP/OpenAI feed, approved partners only, US by default <sup>[CGPT-025, CGPT-031]</sup> | Merchant Center, open to all, free listings on by default <sup>[GOOG-010]</sup> |
| Shopify path | Shopify Catalog, default-on, US buyers required <sup>[SHOP-001, SHOP-003]</sup> | Merchant Center via Google & YouTube app <sup>[SHOP-025]</sup> |
| Crawler that controls inclusion | OAI-SearchBot <sup>[CGPT-004, CGPT-006]</sup> | Googlebot (Search, AIO, AI Mode); Storebot-Google (Shopping); Google-Extended (Gemini grounding only) <sup>[GOOG-026, GOOG-027, GOOG-031]</sup> |
| Extra site-level AI switch | None documented | Search Console "Search generative AI control" <sup>[GOOG-028]</sup> |
| Named search providers | Microsoft, Shopify <sup>[CGPT-002]</sup> | Google's own index |

## Ranking

| Question | ChatGPT | Google AI surfaces |
|---|---|---|
| Product selection | Model-judged relevance; query + Memory + Custom instructions <sup>[CGPT-011]</sup> | "Search quality and ranking systems"; no product factors documented <sup>[GEM-007]</sup> |
| Seller ordering for one product | Availability, price, quality, maker/primary seller <sup>[CGPT-015]</sup> | No rule published <sup>[GOOG-035]</sup> |
| Checkout integration and rank | Was a factor in 2025, removed <sup>[CGPT-016]</sup> | "Does not influence how we rank your offers" <sup>[GOOG-003]</sup> |
| Closest published factor list | Merchant list (above) | Shopping "Top recommendations": relevance, ratings, price, features <sup>[GOOG-022]</sup> |
| Feed fields aimed at AI | Reviews, ratings; no popularity field <sup>[CGPT-030]</sup> | Conversational attributes incl. Q&A and `popularity_rank` <sup>[GOOG-012, GOOG-014]</sup> |
| Structured data | Not mentioned by OpenAI | "Isn't required" for generative AI search <sup>[GOOG-029]</sup> |

## Ads

| Question | ChatGPT | Google AI surfaces |
|---|---|---|
| Ads near product answers | One labeled unit below the answer; Free and Go plans <sup>[CGPT-043]</sup> | Sponsored items inside AI Mode product lists; Highlighted Answers; Direct Offers <sup>[GEM-008, GEM-009]</sup> |
| Stated separation | Ads don't influence answers <sup>[CGPT-042]</sup> | Ads don't influence organic AI answers <sup>[GEM-007]</sup> |
| India | Advertiser self-serve only documented <sup>[CGPT-046]</sup> | Ads in AI Mode since 2026-10-28 <sup>[GEM-008]</sup> |

## Checkout

| Question | ChatGPT | Google AI surfaces |
|---|---|---|
| In-surface checkout | Standalone Instant Checkout dropped 2026-03-24; beta for select marketplaces <sup>[CGPT-021, CGPT-023]</sup> | UCP checkout "hundreds of thousands" of brands; Universal Cart (US) <sup>[GEM-015, GEM-014]</sup> |
| Shopify merchants | Referral to merchant checkout <sup>[SHOP-002]</sup> | Direct checkout default-on for US/CA/AU buyers <sup>[SHOP-026, SHOP-027]</sup> |

## India

| Question | ChatGPT | Google AI surfaces |
|---|---|---|
| Shopping results documented for Indian users | No <sup>[CGPT-046]</sup> | Yes: Gemini app (EN, HI), AI Mode (EN) <sup>[GEM-002]</sup> |
| India-only Shopify store can enter the product pipeline | No (Catalog channel needs US buyers) <sup>[SHOP-003]</sup> | Yes (Merchant Center supports India) <sup>[SHOP-032]</sup> |
| First-party visibility report for India | None found | Merchant Center AI performance (English queries) <sup>[GOOG-017]</sup> |
| Amazon.in | All OpenAI agents blocked <sup>[MKT-001]</sup> | Googlebot allowed; Google-Extended blocked <sup>[MKT-022]</sup> |
| Flipkart | No OpenAI relationship found <sup>[MKT-016]</sup> | Named UCP partner; Storebot allowed <sup>[GEM-016, MKT-025]</sup> |

## What this means for a Shopify merchant

- The two platforms take product data through different pipes: Shopify Catalog for ChatGPT, Merchant Center for Google. Each needs its own setup check <sup>[SHOP-001, SHOP-025]</sup>.
- For an India-focused store, Google is the only documented AI shopping surface today <sup>[GEM-002, CGPT-046]</sup>.
- Neither platform documents a ranking boost for any feed field, markup, protocol or checkout integration. Both document price and availability as inputs: OpenAI in its merchant ordering <sup>[CGPT-015]</sup>, Google in "Top recommendations" <sup>[GOOG-022]</sup>.
