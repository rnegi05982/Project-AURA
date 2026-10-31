# Shopify merchant actions — Gemini, AI Mode, AI Overviews

Derived from `research/ai-platforms/gemini/report.md`. Evidence as of 2026-10-31. Status values as in `shopify/chatgpt.md`: Mandatory, Recommended, Experimental, Unverified.

Three paths reach Google's AI surfaces for a Shopify store:
- **Feed path:** Google & YouTube app → Merchant Center → free listings → Shopping Graph → Gemini app and AI Mode product cards [SHOP-025, GOOG-010, GEM-001].
- **Crawl path:** Googlebot and Storebot-Google → Search index and Shopping Graph → AIO/AI Mode citations and products [GOOG-010, GOOG-026, GOOG-031].
- **Checkout path:** Shopify-powered direct checkout via UCP, US/CA/AU buyers only, on by default [SHOP-026, SHOP-027].

Key difference from ChatGPT: Shopify Catalog does **not** feed Google. Merchant Center does [SHOP-025]. A store can be live in ChatGPT and invisible to Google's product cards, or the reverse.

---

## Mandatory (feed path)

| # | Action | Why | Evidence | How to verify |
|---|---|---|---|---|
| GM1 | Install the Google & YouTube app (or another Merchant Center feed) and turn on automatic product and shipping sync. | Shopify states Google AI discovery is powered by Merchant Center. No feed = no Shopify-managed path into Gemini/AI Mode product cards. | SHOP-025, SHOP-027, SHOP-029 | Merchant Center > Products shows items "Approved". |
| GM2 | Get products approved for free listings and keep the account in good standing. | Free listings can appear on Gemini; free-listings approval is the base for every Google AI commerce feature. | GOOG-002, GOOG-010 | Merchant Center > Free listings status; Diagnostics. |
| GM3 | Fix feed-blocking data: GTIN in the variant barcode (or MPN + brand, or "custom product"), product options in English, rates in the General shipping profile only. | These fields gate sync and approval. | SHOP-030 | Merchant Center Diagnostics shows no item-level errors. |
| GM4 | Meet the 500×500 minimum for all product images before 2027-01-31. | Google enforces the new minimum from that date. | GOOG-016 | Audit image sizes in Shopify admin or via the Admin API. |

## Mandatory (crawl path)

| # | Action | Why | Evidence | How to verify |
|---|---|---|---|---|
| GW1 | Allow Googlebot in robots.txt and at any CDN/firewall. | Googlebot is the crawl control for AIO and AI Mode. | GOOG-026 | Fetch `/robots.txt`; URL Inspection in Search Console. |
| GW2 | In Search Console, keep the "Search generative AI control" on include. | Exclusion removes the site from AIO, AI Mode and Discover AI features. | GOOG-028 | Search Console > Settings. |
| GW3 | If the theme has a custom `robots.txt.liquid`, check Storebot-Google separately. It falls back to `*`, not to a Googlebot group. | A custom file can block Shopping crawling while allowing Search. | GOOG-034, SHOP-017 | Read the live file group by group. |

Note: blocking Google-Extended removes the store from Gemini app grounding and training but not from Search, AIO or AI Mode [GOOG-027]. One study found Gemini never cited sites that block it [RES-039]. Leave it allowed unless training opt-out matters more than Gemini app citations.

## Mandatory (checkout path — only if selling to US, CA or AU buyers)

| # | Action | Why | Evidence | How to verify |
|---|---|---|---|---|
| GC1 | Sell to US, Canadian or Australian buyers; keep products Catalog-eligible; complete three store policies. | Shopify eligibility for Google direct checkout. | SHOP-027 | Sales channels > Agentic > Google AI Mode and Gemini. |
| GC2 | Set the return policy in Merchant Center (cost, window, link) and a customer-support contact. | Google requires it for UCP checkout; the Shopify app does not document syncing it. | SHOP-031, GOOG-002 | Merchant Center > Business info > Returns. |
| GC3 | Plan server-side attribution for Google checkout orders. | Client-side pixels and Google Analytics do not fire in this checkout. | SHOP-028 | Compare Shopify orders by channel with GA4. |

Opting out of direct checkout does not remove products from discovery [SHOP-026]. Google says checkout does not change ranking [GOOG-003].

---

## Recommended

| # | Action | Why | Systems affected | Evidence | How to test impact |
|---|---|---|---|---|---|
| GR1 | Set Google product category and accurate product attributes (color, size, material, gender, age group where relevant). | Google uses feed data "to match your products to the right queries"; missing data can limit eligibility. | Merchant Center, Shopping Graph | GOOG-009, SHOP-030 | Merchant Center AI performance report (share of voice; "popular attributes" missing). |
| GR2 | Collect store reviews through Google Customer Reviews or a supported partner (≈100 in 24 months per country). | Store ratings display on free listings and "can help" performance; Top Quality Store badge uses ratings. | Free listings, Shopping | GOOG-021, GOOG-023 | Track badge and rating status; appearance rate in repeated runs. |
| GR3 | Provide shipping speed and cost, and return window and cost, in Merchant Center. | Store Quality "may boost" Shopping-tab visibility; Top Quality Store uses shipping and returns. | Shopping tab (AI surfaces not stated) | GOOG-021 | Store Quality report before/after. |
| GR4 | Keep product data server-rendered; avoid JavaScript-only price and availability. | JS-generated markup makes Shopping crawls less reliable; JS-only text got fewer grounded-Gemini citations. | Shopping crawl, Gemini grounding | GOOG-031, RES-033 | Fetch the product page with JavaScript off and confirm price/stock are in the HTML. |
| GR5 | Use the Merchant Center AI performance report as the baseline for Google AI visibility (India included, English queries). | First-party measurement of AI Mode and AIO share of voice. | Measurement | GOOG-017 | Export monthly into `experiments/raw-observations/`. |

---

## Experimental

| # | Action | Hypothesis | Evidence | How to test |
|---|---|---|---|---|
| GE1 | Submit conversational attributes (`question_and_answer`, `document_link`, `related_product`, `popularity_rank`) via a supplemental feed. | Google designed them for AI Mode; one test shows they enter answer text. Ranking effect unknown. | GOOG-012, GOOG-013, GOOG-014, GEM-013 | A/B on matched products; AI performance report and repeated runs. |
| GE2 | Add product videos (`video_link`). | Videos appear in AI Mode. Ranking effect unknown. | GOOG-016 | Same as GE1. |
| GE3 | Use channel mapping to send attribute-rich titles and descriptions to the Google channel. | Clearer feed text may improve query matching. | SHOP-030, GOOG-009 | Matched-pair test, 4+ weeks. |
| GE4 | Earn coverage on review sites, YouTube and Reddit for the category. | AIO and grounded Gemini cite third-party and community pages heavily for product questions. | RES-030, RES-042 | Track citation domains over time. |

---

## Unverified for Google AI ranking

| Item | Status | Evidence |
|---|---|---|
| Adding AggregateRating, shipping or return JSON-LD for AI ranking | Google: structured data "isn't required" for generative AI search; no citation lift in two studies. Keep default markup for rich results and crawl reliability. | GOOG-029, RES-033, RES-044 |
| Custom `llms.txt` or `agents.md` | Google Search does not use them. | GOOG-029 |
| Enabling UCP checkout to rank higher | Google says native integration does not influence ranking. | GOOG-003 |
| Buying Shopping ads to lift organic AI answers | Google says ads don't influence organic AI answers. | GEM-007 |
| Business Agent for discovery | Brand-query surface only; US stores. | GOOG-008 |

---

## India-only stores

- The Google feed path works: India is a supported sync and free-listings country [SHOP-032]. Gemini-app and AI Mode shopping are live in India [GEM-002].
- The checkout path does not apply: Indian buyers cannot use Google direct checkout [SHOP-027, GEM-014].
- Actions GM1–GM4, GW1–GW3 and GR1–GR5 apply. Measure with the AI performance report (English queries) [GOOG-017].
- Run `experiments/test-cases/gemini-coffee-mug.md` from India to confirm product cards appear for Indian queries.
