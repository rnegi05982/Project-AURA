# AINA features — evidence record (internal)

- **Use:** AURA audit trail for `aina-features.md`, the team version. Rows here are ungrouped (F1–F30) and cite registry IDs.

- **As of:** 2026-11-02. Built from `research/ai-platforms/{chatgpt,gemini}/report.md` and both `flow.html` diagrams.
- **Evidence:** every row cites registry IDs (`evidence/registry/`).
- **Platform:** ChatGPT, Gemini (Gemini app, AI Mode, AI Overviews), or Both.
- **Status:** Mandatory (a platform requirement), Recommended (evidence-backed), Experimental (indirect evidence; test first), Unverified (no evidence). Same scale as `shopify/*.md`.
- **In AINA:** New, Extend (an existing feature covers part of it), Exists. Checked against `aeo-saga-app10` on 2026-11-02.

---

## 1. Review of the rough list

| # | Rough point | Verdict | Correction |
|---|---|---|---|
| 1 | Check robots.txt / other files for blocked bots; defaults need no change; check customized files | Correct, needs per-bot scope | Report each bot separately: OAI-SearchBot (ChatGPT search), GPTBot (training only), Googlebot (AIO, AI Mode), Storebot-Google (Shopping), Google-Extended (Gemini app grounding, training) [CGPT-006, CGPT-007, GOOG-026, GOOG-027, GOOG-031]. Storebot-Google falls back to `*`, not to a Googlebot group [GOOG-034]. robots.txt does not affect the Shopify Catalog path into ChatGPT [SHOP-018]. "Other files" should mean robots meta tags (`nosnippet`, `max-snippet`) [GOOG-030], not `llms.txt` [GOOG-029]. |
| 2 | Check whether the Google & YouTube app is installed; guide syncing to Gemini | Correct for Gemini | Any Merchant Center feed counts, not only this app [SHOP-025]. The app overwrites an existing feed [SHOP-029]. It does nothing for ChatGPT: Shopify Catalog feeds ChatGPT by default [SHOP-001]. |
| 3 | Image size check | Correct for Gemini only | Google enforces 500×500 from 2027-01-31 [GOOG-016]. ChatGPT documents no size rule. Its path needs at least one image [SHOP-005] and scores image count [SHOP-009]. |
| 4 | Required product attributes: common, Gemini-only, ChatGPT-only | Correct approach | See §3. |
| 5 | Store reviews: fetch and judge review health | Mixes two signals | Google uses **store** ratings: store level, Google Customer Reviews or partners, ~100 in 24 months [GOOG-023]. Shopify cannot read them. Shopify Catalog (ChatGPT path) uses **product** reviews from verified sources [SHOP-009]. AINA can read those from `reviews.rating` and `reviews.rating_count` [SHOP-036]. Effect on AI ranking is not documented on either platform. |

---

## 2. Feature list

| # | Feature | Platform | Does | Status | Evidence | In AINA |
|---|---|---|---|---|---|---|
| F1 | Bot access checker | Both | Fetches `/robots.txt`. Shows allow/block for OAI-SearchBot, GPTBot, Googlebot, Storebot-Google, Google-Extended. Applies Google's rule: the most specific group wins; `*` is the fallback. Explains each bot's effect. | Recommended | CGPT-004, CGPT-006, CGPT-007, GOOG-026, GOOG-027, GOOG-031, GOOG-034, SHOP-016 | New |
| F2 | Custom robots.txt warning | Both | Flags a customized `robots.txt.liquid`. Custom files stop inheriting Shopify's default updates. Detect by comparing the live file with Shopify's default output (`read_themes` would allow reading the template). | Recommended | SHOP-016, SHOP-017 | New (needs `read_themes` to read the template) |
| F3 | Snippet controls on product pages | Gemini | Fetches a sample product page. Flags `nosnippet` and `max-snippet` robots meta, which limit AI Overviews and AI Mode input. | Recommended | GOOG-030 | New (AINA fetches no storefront HTML yet) |
| F4 | Search Console AI control | Gemini | Checklist item: keep "Search generative AI control" on include. Exclude removes the site from AI Overviews and AI Mode. AINA cannot read this setting. | Mandatory | GOOG-028 | New |
| F5 | ChatGPT store eligibility | ChatGPT | Checks: sells to US buyers, plan Starter or higher, no storefront password, terms + privacy + refund policies. Notes that ChatGPT access is on by default in Sales channels > Agentic. | Mandatory | SHOP-001, SHOP-003, SHOP-005 | Extend: plan, password and policy checks exist (`app/lib/storeReadiness.js`); add a US-buyers check (current shipping gate also passes CA or rest-of-world) |
| F6 | Catalog eligibility per product | ChatGPT | Per product: title, at least one image, price above 0, not Unlisted, not `seo.hidden`, category not on Shopify's exclusion list. | Mandatory | SHOP-005, SHOP-010 | Extend: Unlisted badge and image rule exist; add pass/fail gate, price > 0, `seo.hidden`, excluded categories |
| F7 | Merchant Center feed detection | Gemini | Lists sales channels through `publications`. Finds the Google & YouTube channel and counts products published to it. Shows F8 when it is missing. | Mandatory | SHOP-025, SHOP-029, SHOP-037 | New (`read_publications` already granted; no publication query left in code) |
| F8 | Google & YouTube setup guide | Gemini | Guide: install, connect Merchant Center, confirm free listings (auto opt-in), confirm product sync. Warns that the app overwrites an existing feed. | Mandatory | GOOG-010, SHOP-029, SHOP-032 | New |
| F9 | Market fit notice | Both | India-only store: ChatGPT's Catalog path is closed (needs US selling); Google's path is open (India supported). | Recommended | CGPT-046, GEM-002, SHOP-003, SHOP-032 | New |
| F10 | Image checks | Both | ChatGPT: at least one image, more images score higher. Gemini: every image at least 500×500, enforced from 2027-01-31. Reads image width and height from product media. | Mandatory (Gemini from 2027-01-31, ChatGPT ≥1 image) · Recommended (image count) | SHOP-005, SHOP-009, GOOG-016 | Extend: image-count rule exists (min 5); add width/height (scan reads only `id`, `alt`) |
| F11 | Product identifiers | Both | Variant barcode → GTIN on both paths. Without a GTIN, Gemini needs MPN + brand or the "custom product" flag in the Google channel. | Mandatory (Gemini approval) · Recommended (ChatGPT) | SHOP-008, SHOP-030, GOOG-009 | New (barcode is read for Fix product but not scored) |
| F12 | Product category | Both | ChatGPT: set the Shopify category; Catalog otherwise infers its own, and default JSON-LD shows an empty category. Gemini: set Google product category in the channel; Google otherwise assigns one. | Recommended | SHOP-005, SHOP-022, SHOP-030 | Extend: Shopify category rules and bulk suggestions exist; add Google product category |
| F13 | Category attributes | Both | ChatGPT: color, size, target gender (Shopify taxonomy; Catalog search filters). Gemini: color, size, age group, gender required for apparel. | Recommended (ChatGPT) · Mandatory (Gemini apparel) | SHOP-030, SHOP-034, GOOG-009 | Extend: Shopify taxonomy attributes and bulk fill exist; add Google channel age group and gender |
| F14 | Variant and option hygiene | Both | Gemini: option names and values in English, or sync fails. ChatGPT: complete variants, high in-stock share, no acronyms or bare numbers in option names. | Mandatory (Gemini) · Recommended (ChatGPT) | SHOP-009, SHOP-030 | New (variant and in-stock counts were removed 2026-10-20) |
| F15 | Description quality | ChatGPT | Scores description word count (a Catalog listing-quality signal). Checks that legal disclosures sit in the first 6,000 characters. | Recommended | SHOP-003, SHOP-009 | Extend: word-count rule exists (300–2,000 words); add the 6,000-character disclosure check |
| F16 | Brand / maker | Both | Vendor maps to brand on both paths. For own-brand products, vendor should name the maker: ChatGPT ranks the maker or primary seller first. | Recommended | CGPT-015, SHOP-022, SHOP-030 | New (vendor is read only as AI input) |
| F17 | Price and stock accuracy | ChatGPT | Flags variants without inventory tracking or with stale availability. ChatGPT's merchant list ranks by availability and price; the headline price is the first merchant's. | Recommended | CGPT-014, CGPT-015, SHOP-006 | New |
| F18 | AI title and description for Shopify Catalog | ChatGPT | Writes AI-ready title and description to metafields. Merchant maps them in Catalog > Channel mapping. ChatGPT may still rewrite titles. | Experimental | SHOP-007, CGPT-013, RES-005 | Exists (`aina.agentic_title`, `aina.agentic_description` metafields) |
| F19 | SEO title and meta description for Google | Gemini | Writes attribute-rich SEO title and meta description. The Google channel can send them instead of the product title and description. | Experimental | SHOP-030, GOOG-017 | New (product update mutation has no `seo` input) |
| F20 | Shipping profile check | Gemini | Flags rates outside the General shipping profile. Only General-profile rates sync to Merchant Center. | Mandatory | SHOP-029, SHOP-030 | New (needs `read_shipping`) |
| F21 | Server-rendered price and stock | Gemini | Fetches the product page HTML without running JavaScript. Confirms price and availability are present. | Recommended | GOOG-031, RES-033 | New |
| F22 | JSON-LD audit and enrichment | Gemini | Audits Product JSON-LD. Adds shipping, returns and rating markup through an app embed. Google recommends them for merchant listings; no AI-ranking lift is shown. | Recommended (Shopping crawl) · Unverified (AI ranking) | GOOG-029, GOOG-033, SHOP-022, RES-044 | New |
| F23 | Product review health | Both | Reads `reviews.rating` and `reviews.rating_count`. Flags products with no or few reviews. Flags review apps that skip the standard fields. | Recommended | SHOP-009, SHOP-036, CGPT-011, GOOG-022 | New (review metafields are only filtered out of AI input today) |
| F24 | Store rating readiness | Gemini | Guide: Google Customer Reviews or a review partner; about 100 reviews in 24 months per country. Not readable through Shopify. | Recommended | GOOG-023 | New |
| F25 | Conversational attributes feed | Gemini | Builds a Merchant Center supplemental feed: `question_and_answer`, `related_product` (from Shopify related/complementary metafields), `popularity_rank` (from recent sales), `product_highlight`. Needs Merchant Center access and `read_orders`. | Experimental | GOOG-009, GOOG-012, GOOG-013, GOOG-014, GOOG-015, GEM-013, SHOP-038 | New (needs `read_orders` and Merchant Center access) |
| F26 | Product video check | Gemini | Flags products without video. Product videos (`video_link`) appear in AI Mode. Whether the Google channel syncs Shopify videos is not documented. | Experimental | GOOG-016 | New (scan reads only `MediaImage`) |
| F27 | Return policy in Merchant Center | Gemini | Checklist item: set return cost, window and link in Merchant Center. The Shopify app does not sync it. Google checkout requires it. | Mandatory (Google checkout) | GOOG-002, SHOP-031 | New |
| F28 | Google checkout readiness | Gemini | Shows eligibility (US, Canadian or Australian buyers). Warns that pixels and GA do not fire in Google checkout. Notes that opting out keeps discovery. | Recommended | SHOP-026, SHOP-027, SHOP-028 | New |
| F29 | Catalog search preview and rank | ChatGPT | Runs merchant queries against Shopify Catalog search. Shows whether products reach the top 10. ChatGPT re-ranks, so the result is directional. | Recommended | SHOP-009, SHOP-013, SHOP-034 | Exists (`app/services/ucpCatalog.server.js` search and rank; rank checks the top 250) |
| F30 | AI referral and visibility reporting | Both | ChatGPT: referral-attributed orders from Shopify. Gemini: Merchant Center AI performance report (share of voice; English queries, incl. India). | Recommended | SHOP-012, GOOG-017 | Extend: ChatGPT agent traffic exists (ShopifyQL agentic channels); add the Merchant Center AI performance report |

---

## 3. Attribute matrix

| Common (both) | Gemini only | ChatGPT only |
|---|---|---|
| Title | Google product category | Shopify category (Catalog infers it if unset) |
| Description | MPN or "custom product" flag | Type, collections, tags |
| At least one image | Images ≥ 500×500 (from 2027-01-31) | Image count |
| Price | Age group (apparel) | Compare-at price → `list_price` |
| Inventory → availability | Options in English | Description word count |
| Barcode → GTIN | Shipping rates (General profile) | Legal disclosures in first 6,000 characters |
| Vendor → brand | SEO title, meta description (optional source) | Readable option names; variant completeness |
| Variants and options | Return policy in Merchant Center | Verified product reviews (rating, count) |
| Color, size, gender | Store ratings (Google Customer Reviews) | Not Unlisted, not `seo.hidden`, price > 0 |
| Terms, privacy, refund policies | Store Quality: shipping speed, returns | Catalog title/description metafield mapping |
| | Conversational attributes: `question_and_answer`, `document_link`, `related_product`, `item_group_title`, `variant_option`, `popularity_rank` | |
| | `video_link`, `product_highlight`, `product_detail` | |
| | JSON-LD shipping, returns, rating (crawl) | |

Evidence: common [SHOP-005, SHOP-006, SHOP-008, SHOP-030, GOOG-009]; Gemini only [SHOP-030, SHOP-031, GOOG-012, GOOG-013, GOOG-014, GOOG-015, GOOG-016, GOOG-021, GOOG-023, GOOG-033]; ChatGPT only [SHOP-003, SHOP-005, SHOP-007, SHOP-009, SHOP-010]. ChatGPT-only items are Shopify Catalog signals; ChatGPT's own use of them is inferred, not stated.

---

## 4. Do not build

| Item | Platform | Why | Evidence |
|---|---|---|---|
| `llms.txt` / `agents.md` generator | Both | Shopify serves defaults. Google Search does not use them. No source says ChatGPT reads them. | SHOP-020, GOOG-029 |
| JSON-LD for ChatGPT ranking | ChatGPT | No OpenAI source mentions structured data. One API study found no citation lift. | SHOP-022, RES-012 |
| UCP support aimed at ChatGPT | ChatGPT | No source says ChatGPT uses UCP. | SHOP-014, ACP-006 |
| Direct OpenAI / ACP feed for Shopify stores | ChatGPT | Shopify catalogs are already integrated through Catalog. | CGPT-017, CGPT-025 |
| UCP checkout as a ranking lever | Gemini | Google says native checkout does not influence ranking. | GOOG-003 |
| Ads to lift organic answers | Both | Both platforms say ads do not influence organic answers. | CGPT-042, GEM-007 |
