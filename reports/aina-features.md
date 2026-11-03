# AINA — features for ChatGPT and Gemini product discovery

As of 2026-11-02.

- **Platform:** ChatGPT, Gemini (Gemini app, AI Mode, AI Overviews), or Both.
- **Status:** Mandatory = a platform requirement. Recommended = a documented benefit. Experimental = indirect evidence; test before relying on it. Unverified = no evidence.
- **In AINA:** **Built** = already in AINA. **Fix** = built, but needs a change. **To build** = missing. **Not needed** = skip, with the reason.

---

## 1. Features

| # | Feature | Platform | Does | Status | In AINA |
|---|---|---|---|---|---|
| 1 | Crawler access check | Both | Fetch `/robots.txt` and show allow/block per bot: OAI-SearchBot (ChatGPT search), GPTBot (OpenAI training only), Googlebot (AI Overviews, AI Mode), Storebot-Google (Google Shopping), Google-Extended (Gemini app grounding and training).<br>Apply Google's rule: the most specific group wins; `*` is the fallback, also for Storebot-Google.<br>Flag a customized `robots.txt.liquid`. It stops inheriting Shopify's defaults, which allow all bots.<br>**Gemini:** checklist item to keep Search Console's "Search generative AI control" on include. AINA cannot read this setting.<br>robots.txt does not affect the Shopify Catalog path into ChatGPT. | Recommended · Mandatory (Search Console control) | **To build:** robots.txt per bot; Search Console checklist row (same pattern as the existing manual "Review your AI channels" row).<br>**Not needed:** `read_themes` scope. Detect a custom file by comparing the live robots.txt with Shopify's default output. |
| 2 | Product page checks | Gemini | Fetch a sample product page's HTML without running JavaScript. Check that:<br>• price and availability are in the HTML; JavaScript-only data makes Google Shopping crawls less reliable;<br>• no `nosnippet` or `max-snippet` robots meta limits AI Overviews and AI Mode input;<br>• Product JSON-LD is present. Offer shipping, returns and rating markup through an app embed; Google recommends them for merchant listings. | Recommended · Unverified (JSON-LD as an AI-ranking factor; no ChatGPT evidence) | **To build:** robots meta check; JSON-LD audit and app-embed markup.<br>**Not needed:** server-rendered price check on Liquid themes, which Shopify renders on the server. Keep it only for headless storefronts. |
| 3 | ChatGPT eligibility | ChatGPT | **Store:** sells to US buyers; plan Starter or higher; no storefront password; terms, privacy and refund policies present. ChatGPT access stays on by default in Sales channels > Agentic.<br>**Product:** title, at least one image, price above 0, not Unlisted, not `seo.hidden`, category not on Shopify Catalog's exclusion list.<br>**India-only stores:** show that ChatGPT's path is closed (it needs US selling) and Google's path is open. | Mandatory | **Built:** plan and password checks; terms, privacy, refund and shipping policy checks; manual "Review your AI channels" row (no Admin API exposes the Agentic channel); manual "Content compliant" row; Unlisted badge.<br>**Fix:** the shipping check passes "US or Canada" or rest-of-world. ChatGPT needs US buyers. Show US for ChatGPT and US/CA/AU for Google checkout.<br>**To build:** per-product pass/fail gate (price > 0, `seo.hidden`, Catalog-excluded categories); India-only notice. |
| 4 | Google Merchant Center feed | Gemini | Detect the Google & YouTube sales channel with the `publications` query. Count products published to it. Any Merchant Center feed works; this channel is the Shopify-managed one.<br>If it is missing, show a setup guide: install, connect Merchant Center, confirm free listings (on by default), confirm product sync. Warn that the app overwrites an existing feed.<br>Flag shipping rates outside the General shipping profile; only those rates sync. | Mandatory | **To build:** channel detection (`read_publications` is already granted); setup guide; shipping-profile check (needs `read_shipping`). |
| 5 | Image checks | Both | **ChatGPT:** at least one image. More images raise Shopify Catalog's listing quality.<br>**Gemini:** every image at least 500×500, enforced from 2027-01-31. Read image width and height. | Mandatory (≥1 image; Gemini size from 2027-01-31) · Recommended (image count) | **Built:** image-count rule (minimum 5); image alt-text rule.<br>**To build:** width and height check (the scan reads only image ID and alt text). The description-vs-image rule exists but is switched off until a later slice. |
| 6 | Product identity data | Both | **Identifiers:** variant barcode → GTIN on both. Without a GTIN, Gemini needs MPN + brand or the "custom product" flag in the Google channel.<br>**Brand:** vendor → brand on both. For own-brand products, vendor should name the maker; ChatGPT lists the maker or primary seller first.<br>**Category:** Shopify category for ChatGPT; Catalog infers its own if unset. Google product category in the Google channel for Gemini; Google assigns one if unset.<br>**Attributes:** Shopify taxonomy attributes such as color, size, target gender for ChatGPT (Catalog search filters). Color, size, age group and gender for apparel on Gemini (required). | Mandatory (Gemini identifiers, apparel attributes) · Recommended | **Built:** Shopify category rules (assigned, depth, accepted list) and bulk category suggestions; category attribute rules (required, 75% completeness) and bulk attribute fill.<br>**To build:** GTIN/MPN check (barcode is read but not scored); vendor check; Google product category; Google age group and gender. |
| 7 | Variants, stock and price | Both | **Gemini:** option names and values in English, or sync fails.<br>**ChatGPT:** complete variants, a high in-stock share, no acronyms or bare numbers in option names. Flag variants without inventory tracking or with stale availability. ChatGPT's merchant list ranks sellers by availability and price. | Mandatory (Gemini English) · Recommended | **To build:** English option check; readable option names; variant completeness and in-stock share; inventory-tracking check.<br>Variant, in-stock, Unlisted and $0 counts were removed on 2026-10-20. Confirm why before rebuilding them. |
| 8 | Title and description | Both | **Checks (ChatGPT):** description word count, a Catalog listing-quality signal. Legal disclosures in the first 6,000 characters.<br>**Copy for ChatGPT:** write an AI-ready title and description to metafields. The merchant maps them in Shopify Catalog's channel mapping. ChatGPT may still rewrite titles.<br>**Copy for Gemini:** write an attribute-rich SEO title and meta description. The Google channel can send them instead of the product title and description. | Recommended (checks) · Experimental (copy) | **Built:** description present, length (300–2,000 words), caps and uniqueness rules; title caps, word and pattern rules; Agentic listing metafields (`aina.agentic_title`, `aina.agentic_description`) for Catalog channel mapping.<br>**To build:** SEO title and meta description writes (the product update writes no `seo` field today); 6,000-character disclosure check, only for products that carry legal disclosures. |
| 9 | Reviews health | Both | **Product reviews (ChatGPT, via Shopify Catalog):** read `reviews.rating` and `reviews.rating_count`. Flag products with no or few reviews. Flag review apps that skip these standard fields. Catalog counts only reviews from verified sources.<br>**Store ratings (Gemini):** guide for Google Customer Reviews or a review partner; about 100 reviews in 24 months per country. Shopify cannot read them. | Recommended (effect on AI ranking not documented) | **To build:** review metafield read and health flags (today AINA only filters review metafields out of AI input); store-rating guide. |
| 10 | Google AI Mode enrichment | Gemini | Build a Merchant Center supplemental feed: `question_and_answer`, `related_product` (from Shopify's related and complementary product metafields), `popularity_rank` (from recent sales), `product_highlight`. Google designed these for AI Mode; in one brand test they appeared in half of relevant answers.<br>Flag products without video. Product videos appear in AI Mode. | Experimental | **To build:** supplemental feed (needs `read_orders` and Merchant Center access); video check (the scan reads images only). |
| 11 | Google checkout readiness | Gemini | Show eligibility: buyers in the US, Canada or Australia. Checklist: return cost, window and link set in Merchant Center; the Shopify app does not sync them. Warn that pixels and GA do not fire in Google checkout. Opting out of checkout keeps discovery. | Mandatory (return policy, for checkout) · Recommended | **To build:** all of it. |
| 12 | Visibility tracking | Both | **ChatGPT:** run merchant queries against Shopify Catalog search and show top-10 presence. ChatGPT re-ranks, so the result is directional. Report ChatGPT-referred orders.<br>**Gemini:** import the Merchant Center AI performance report: share of voice in AI Mode and AI Overviews, English queries, India included. | Recommended | **Built:** Agent lens store rank (top 250) and tracked prompts (top 10) on Shopify Catalog search; Agent traffic report of AI-referred orders and sessions (not yet checked against live data).<br>**To build:** Merchant Center AI performance report. |

---

## 2. Product attributes by platform

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
| | JSON-LD shipping, returns, rating | |

ChatGPT-only items are Shopify Catalog signals. Shopify documents them; ChatGPT's own use of them is inferred.

---

## 3. Do not build

| Item | Platform | Why |
|---|---|---|
| `llms.txt` / `agents.md` generator | Both | Shopify serves defaults. Google Search does not use them. No source says ChatGPT reads them. |
| JSON-LD for ChatGPT ranking | ChatGPT | No OpenAI source mentions structured data. One study found no citation lift. |
| UCP support aimed at ChatGPT | ChatGPT | No source says ChatGPT uses UCP. |
| Direct OpenAI feed for Shopify stores | ChatGPT | Shopify catalogs already reach ChatGPT through Shopify Catalog. |
| Google checkout as a ranking lever | Gemini | Google says checkout integration does not influence ranking. |
| Ads to lift organic answers | Both | Both platforms say ads do not influence organic answers. |
