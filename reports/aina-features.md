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

---

## 4. Sources

Each line: what the source establishes, then the link. Primary sources (platform docs, specs, robots.txt, papers) come first in each group.

### 1 · Crawler access check

- Allowing OAI-SearchBot is the stated eligibility condition for search inclusion: [Searching the web with ChatGPT](https://help.openai.com/en/articles/9237897-searching-the-web-with-chatgpt)
- OAI-SearchBot surfaces sites in search; opt-out removes them from answers within ~24 h: [Overview of OpenAI Crawlers](https://developers.openai.com/api/docs/bots)
- GPTBot (training) is independent of OAI-SearchBot (search): [Overview of OpenAI Crawlers](https://developers.openai.com/api/docs/bots.md)
- Googlebot is the crawl control for AI Overviews and AI Mode; there is no separate AI crawler: [List of Google's common crawlers](https://developers.google.com/crawling/docs/crawlers-fetchers/google-common-crawlers) · [AI features and your website](https://developers.google.com/search/docs/appearance/ai-features)
- Google-Extended controls Gemini Apps and Vertex AI training and grounding; it does not affect Search: [List of Google's common crawlers](https://developers.google.com/crawling/docs/crawlers-fetchers/google-common-crawlers)
- Search Console "Search generative AI control" (worldwide since 2026-08-31) includes or excludes a site from AI Overviews, AI Mode and Discover AI: [Search generative AI control](https://support.google.com/webmasters/answer/16908024) · [Optimizing your website for generative AI features on Google Search](https://developers.google.com/search/docs/fundamentals/ai-optimization-guide)
- Storebot-Google is Google Shopping's crawler; JavaScript-generated Product markup makes Shopping crawls "less frequent and less reliable": [List of Google's common crawlers](https://developers.google.com/crawling/docs/crawlers-fetchers/google-common-crawlers) · [Merchant listing structured data](https://developers.google.com/search/docs/appearance/structured-data/merchant-listing)
- Google applies one robots.txt group per crawler; Storebot-Google falls back to `*`, not to a Googlebot group: [How Google interprets the robots.txt specification](https://developers.google.com/crawling/docs/robots-txt/robots-txt-spec)
- Shopify's default robots.txt allows all bots, names no OpenAI crawler, and opens with comments addressed to AI agents: [kith.com](https://kith.com/robots.txt) · [theme-dawn-demo.myshopify.com](https://theme-dawn-demo.myshopify.com/robots.txt) · [theme-horizon-demo.myshopify.com](https://theme-horizon-demo.myshopify.com/robots.txt) · [brooklinen.com](https://www.brooklinen.com/robots.txt) · [colourpop.com](https://colourpop.com/robots.txt)
- Stores with a custom robots.txt.liquid do not inherit default changes: [allbirds.com](https://www.allbirds.com/robots.txt) · [gymshark.com](https://www.gymshark.com/robots.txt) · [taylorstitch.com](https://www.taylorstitch.com/robots.txt)
- robots.txt and network blocking affect only open-web discovery, not Catalog syndication: [Editing robots.txt.liquid](https://help.shopify.com/en/manual/promoting-marketing/seo/editing-robots-txt)

### 2 · Product page checks

- nosnippet and max-snippet limit AI Overviews/AI Mode inputs; in-page structured data is exempt from max-snippet: [Robots meta tag, data-nosnippet, and X-Robots-Tag specifications](https://developers.google.com/search/docs/crawling-indexing/robots-meta-tag)
- Storebot-Google is Google Shopping's crawler; JavaScript-generated Product markup makes Shopping crawls "less frequent and less reliable": [List of Google's common crawlers](https://developers.google.com/crawling/docs/crawlers-fetchers/google-common-crawlers) · [Merchant listing structured data](https://developers.google.com/search/docs/appearance/structured-data/merchant-listing)
- Google's AI optimization guide: structured data "isn't required"; Merchant Center feeds help products appear in AI responses; llms.txt not used: [Optimizing your website for generative AI features on Google Search](https://developers.google.com/search/docs/fundamentals/ai-optimization-guide)
- Merchant listing markup requires the page to be the point of sale; Google recommends markup plus a Merchant Center feed: [Merchant listing (Product, Offer) structured data](https://developers.google.com/search/docs/appearance/structured-data/merchant-listing) · [Introduction to Product structured data](https://developers.google.com/search/docs/appearance/structured-data/product)
- Default Dawn/Horizon JSON-LD includes GTIN, SKU, offers; no ratings, shipping or return policy: [Shopify/dawn](https://github.com/Shopify/dawn) · [Shopify/horizon](https://github.com/Shopify/horizon) · [Dawn demo product page](https://theme-dawn-demo.myshopify.com/products/studio-denim)
- For grounded Gemini, title match and inbound links associate with citations; schema.org and FAQ blocks show no effect; JS-only text gets fewer: [arxiv.org](https://arxiv.org/html/2610.15033v1)
- Vendor quasi-experiment: adding JSON-LD did not raise AI Mode or AIO citations: [We Tracked 1,885 Pages Adding Schema. AI Citations Barely Moved.](https://ahrefs.com/blog/schema-ai-citations/)

### 3 · ChatGPT eligibility

- The ChatGPT channel is on by default for eligible stores; opt-out takes up to 7 days: [Selling on ChatGPT](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/chatgpt)
- ChatGPT channel eligibility: sells to US buyers, Catalog-eligible products, three policies: [Selling on ChatGPT](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/chatgpt)
- Catalog eligibility gates: plan, title, image, price, published URL, category exclusions: [Requirements for being included in Shopify Catalog](https://help.shopify.com/en/manual/shopify-catalog/requirements)
- "Allow Shopify to manage for me" auto-enrolls stores in new AI channels: [Managing agentic storefronts](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/agentic-home)
- No OpenAI source documents ChatGPT shopping availability in India: [chatgpt.com/merchants](https://chatgpt.com/merchants/) · [Shopping with ChatGPT Search](https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search) · [OpenAI ads announcement](https://openai.com/index/expanding-access-to-ai-with-chatgpt-ads/)
- India: Gemini app shopping in English and Hindi; AI Mode shopping in English, Hindi "soon" (2026-04-07): [New ways Google is using AI to make shopping easier](https://blog.google/intl/en-in/products/explore-communicate/new-ways-google-is-using-ai-to-make-shopping-easier/)
- The app auto-opts stores into free listings; India is a supported sync and free-listings country: [Show your products for free on Google](https://support.google.com/merchants/answer/13692890?hl=en) · [Syncing your products](https://support.google.com/merchants/answer/13427434?hl=en)

### 4 · Google Merchant Center feed

- Google AI Mode and Gemini discover Shopify products through Google Merchant Center, not Shopify Catalog: [Selling on Google AI Mode and Gemini](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google) · [Data sharing and privacy for selling with agentic storefronts](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/data-privacy)
- The Google & YouTube channel is Google's app; it syncs products, shipping and taxes and overwrites any existing feed: [Google & YouTube](https://apps.shopify.com/google) · [Syncing your products](https://help.shopify.com/en/manual/online-sales-channels/marketplaces/google/getting-setup/syncing-products)
- Shopify → Merchant Center field mapping: barcode → GTIN, vendor → brand (default), General shipping profile only; options must be in English: [Google & YouTube channel requirements](https://help.shopify.com/en/manual/online-sales-channels/marketplaces/google/requirements) · [Syncing your products](https://support.google.com/merchants/answer/13427434?hl=en)
- The app auto-opts stores into free listings; India is a supported sync and free-listings country: [Show your products for free on Google](https://support.google.com/merchants/answer/13692890?hl=en) · [Syncing your products](https://support.google.com/merchants/answer/13427434?hl=en)
- The `publications` query lists a store's sales channels by catalog title: [Product and variant publishing](https://shopify.dev/docs/apps/build/sales-channels/product-publishing)
- Free listings are on by default and can appear on Gemini; crawled products can show without Merchant Center: [Free listings for products](https://support.google.com/merchants/answer/13889434?hl=en)

### 5 · Image checks

- Catalog eligibility gates: plan, title, image, price, published URL, category exclusions: [Requirements for being included in Shopify Catalog](https://help.shopify.com/en/manual/shopify-catalog/requirements)
- Catalog has its own search and "Listing quality" signals; AI channels re-rank: [Managing agentic storefronts](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/agentic-home)
- 2026 spec changes: `video_link` (shown in AI Mode), new shipping fields, 500×500 image minimum from 2027-01-31: [Merchant Center product data specification update 2026](https://support.google.com/merchants/answer/16989427?hl=en) · [About using product videos across Google Shopping](https://support.google.com/merchants/answer/18545837?hl=en)

### 6 · Product identity data

- Shopify lists the product fields "AI platforms or shopping sites" consider, including barcode/GTIN: [Optimizing your products for AI platforms](https://help.shopify.com/en/manual/shopify-catalog/optimizing-products)
- Shopify → Merchant Center field mapping: barcode → GTIN, vendor → brand (default), General shipping profile only; options must be in English: [Google & YouTube channel requirements](https://help.shopify.com/en/manual/online-sales-channels/marketplaces/google/requirements) · [Syncing your products](https://support.google.com/merchants/answer/13427434?hl=en)
- Google uses Merchant Center data "to match your products to the right queries"; missing data limits eligibility: [Product data specification](https://support.google.com/merchants/answer/7052112?hl=en)
- Catalog eligibility gates: plan, title, image, price, published URL, category exclusions: [Requirements for being included in Shopify Catalog](https://help.shopify.com/en/manual/shopify-catalog/requirements)
- Default Dawn/Horizon JSON-LD includes GTIN, SKU, offers; no ratings, shipping or return policy: [Shopify/dawn](https://github.com/Shopify/dawn) · [Shopify/horizon](https://github.com/Shopify/horizon) · [Dawn demo product page](https://theme-dawn-demo.myshopify.com/products/studio-denim)
- Global Catalog search takes a query, buyer context and filters; unavailable items are excluded by default: [Global Catalog MCP](https://shopify.dev/docs/agents/catalog/global-catalog)
- Merchant list ordering: availability, price, quality, maker/primary seller: [Shopping with ChatGPT Search](https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search)

### 7 · Variants, stock and price

- Shopify → Merchant Center field mapping: barcode → GTIN, vendor → brand (default), General shipping profile only; options must be in English: [Google & YouTube channel requirements](https://help.shopify.com/en/manual/online-sales-channels/marketplaces/google/requirements) · [Syncing your products](https://support.google.com/merchants/answer/13427434?hl=en)
- Catalog has its own search and "Listing quality" signals; AI channels re-rank: [Managing agentic storefronts](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/agentic-home)
- Catalog syndicates title, description, options, images, price, availability and "other key attributes", continuously updated: [Shopify Catalog and product discovery for agentic storefronts](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/products)
- Prices come from third-party providers; the headline price is the first-listed merchant's: [Shopping with ChatGPT Search](https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search)
- Merchant list ordering: availability, price, quality, maker/primary seller: [Shopping with ChatGPT Search](https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search)

### 8 · Title and description

- ChatGPT channel eligibility: sells to US buyers, Catalog-eligible products, three policies: [Selling on ChatGPT](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/chatgpt)
- Catalog has its own search and "Listing quality" signals; AI channels re-rank: [Managing agentic storefronts](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/agentic-home)
- Merchants can remap Catalog title and description to metafields; compare-at price maps to UCP `list_price`: [Customizing your product data for Shopify Catalog](https://help.shopify.com/en/manual/shopify-catalog/mapping)
- Displayed titles, labels and review summaries are model-generated; reviews come from public websites: [Shopping with ChatGPT Search](https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search)
- One query-matched description rewrite raised selection share in 5 of 6 models: [arxiv.org](https://arxiv.org/html/2508.02630v3)
- Shopify → Merchant Center field mapping: barcode → GTIN, vendor → brand (default), General shipping profile only; options must be in English: [Google & YouTube channel requirements](https://help.shopify.com/en/manual/online-sales-channels/marketplaces/google/requirements) · [Syncing your products](https://support.google.com/merchants/answer/13427434?hl=en)

### 9 · Reviews health

- Catalog has its own search and "Listing quality" signals; AI channels re-rank: [Managing agentic storefronts](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/agentic-home)
- Review apps write `reviews.rating` and `reviews.rating_count`; the standard review metaobject carries a verification status: [List of standard metafield definitions](https://shopify.dev/docs/apps/build/metafields/list-of-standard-definitions) · [Standard product review metaobject definition](https://shopify.dev/docs/apps/build/metaobjects/standard-review-metaobject)
- Product selection is model-judged relevance to intent, using query plus Memory and Custom instructions: [Shopping with ChatGPT Search](https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search)
- Store ratings need ~100 reviews in 24 months and "can help" free-listing performance: [Google store ratings: An overview for Merchants](https://support.google.com/merchants/answer/190657?hl=en)

### 10 · Google AI Mode enrichment

- Six optional "conversational attributes" target AI Mode: [How to use conversational attributes](https://support.google.com/merchants/answer/17085370?hl=en)
- `question_and_answer` is "primarily intended" for AI Mode; Google extracts FAQs from `document_link` PDFs: [Question and answer attribute](https://support.google.com/merchants/answer/17085211?hl=en)
- `popularity_rank`: merchant-declared 0–100 sales popularity for AI Mode: [Popularity rank attribute](https://support.google.com/merchants/answer/17085297?hl=en)
- `related_product` and `variant_option` encode accessories, substitutes and variants: [Product data specification](https://support.google.com/merchants/answer/7052112?hl=en) · [Merchant Center setup](https://developers.google.com/merchant/ucp/guides/overview/merchant-center)
- Brand-submitted conversational attributes appeared in 50% of relevant AI Mode recommendations (lululemon test): [Boost your holiday sales with these agentic commerce updates](https://blog.google/products-and-platforms/products/shopping/google-shopping-updates-holiday-shopping/)
- Standard discovery metafields hold related and complementary products: [List of standard metafield definitions](https://shopify.dev/docs/apps/build/metafields/list-of-standard-definitions)
- 2026 spec changes: `video_link` (shown in AI Mode), new shipping fields, 500×500 image minimum from 2027-01-31: [Merchant Center product data specification update 2026](https://support.google.com/merchants/answer/16989427?hl=en) · [About using product videos across Google Shopping](https://support.google.com/merchants/answer/18545837?hl=en)

### 11 · Google checkout readiness

- Eligibility: sell to US, Canadian or Australian buyers (store anywhere), valid Merchant Center, Catalog-eligible products, three policies: [Selling on Google AI Mode and Gemini](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google)
- Return policy must be set in Merchant Center separately; UCP checkout requires it: [Set up your return policies (for Shopify users)](https://support.google.com/merchants/answer/14232691?hl=en)
- UCP on Google requires Merchant Center in good standing, free-listings approval, return policy and support contact: [Merchant Center setup](https://developers.google.com/merchant/ucp/guides/overview/merchant-center)
- No Shopify fee for Google direct checkout; several product types unsupported: [Selling on Google AI Mode and Gemini](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google)
- Google direct checkout is on by default for eligible Shopify stores; opting out keeps discovery: [Selling on Google AI Mode and Gemini](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google)

### 12 · Visibility tracking

- Catalog has its own search and "Listing quality" signals; AI channels re-rank: [Managing agentic storefronts](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/agentic-home)
- Global Catalog search takes a query, buyer context and filters; unavailable items are excluded by default: [Global Catalog MCP](https://shopify.dev/docs/agents/catalog/global-catalog)
- The Agentic admin page shows queries a store ranks for (2026-05-11): [A new home for Agentic Storefronts in your admin](https://shopify.dev/changelog/a-new-home-for-agentic-storefronts-in-your-admin)
- The ChatGPT channel went live for Shopify merchants the week of 2026-03-24, with referral attribution: [Millions of merchants can sell in AI chats](https://www.shopify.com/news/agentic-commerce-momentum)
- Merchant Center "AI performance" report covers AI Mode and AI Overviews, including India (English queries): [About AI performance insights](https://support.google.com/merchants/answer/17200695?hl=en)

### Product attributes by platform

- Catalog eligibility gates: plan, title, image, price, published URL, category exclusions: [Requirements for being included in Shopify Catalog](https://help.shopify.com/en/manual/shopify-catalog/requirements)
- Catalog syndicates title, description, options, images, price, availability and "other key attributes", continuously updated: [Shopify Catalog and product discovery for agentic storefronts](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/products)
- Merchants can remap Catalog title and description to metafields; compare-at price maps to UCP `list_price`: [Customizing your product data for Shopify Catalog](https://help.shopify.com/en/manual/shopify-catalog/mapping)
- Shopify lists the product fields "AI platforms or shopping sites" consider, including barcode/GTIN: [Optimizing your products for AI platforms](https://help.shopify.com/en/manual/shopify-catalog/optimizing-products)
- Catalog has its own search and "Listing quality" signals; AI channels re-rank: [Managing agentic storefronts](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/agentic-home)
- Shopify → Merchant Center field mapping: barcode → GTIN, vendor → brand (default), General shipping profile only; options must be in English: [Google & YouTube channel requirements](https://help.shopify.com/en/manual/online-sales-channels/marketplaces/google/requirements) · [Syncing your products](https://support.google.com/merchants/answer/13427434?hl=en)
- Google uses Merchant Center data "to match your products to the right queries"; missing data limits eligibility: [Product data specification](https://support.google.com/merchants/answer/7052112?hl=en)
- Six optional "conversational attributes" target AI Mode: [How to use conversational attributes](https://support.google.com/merchants/answer/17085370?hl=en)
- 2026 spec changes: `video_link` (shown in AI Mode), new shipping fields, 500×500 image minimum from 2027-01-31: [Merchant Center product data specification update 2026](https://support.google.com/merchants/answer/16989427?hl=en) · [About using product videos across Google Shopping](https://support.google.com/merchants/answer/18545837?hl=en)
- Store Quality "may boost" Shopping-tab visibility; Top Quality Store badge scores shipping, returns, ratings, site: [About the Store Quality program](https://support.google.com/merchants/answer/14261098?hl=en) · [About the Top Quality Store badge](https://support.google.com/googleshopping/answer/11115998?hl=en)
- Store ratings need ~100 reviews in 24 months and "can help" free-listing performance: [Google store ratings: An overview for Merchants](https://support.google.com/merchants/answer/190657?hl=en)
- Return policy must be set in Merchant Center separately; UCP checkout requires it: [Set up your return policies (for Shopify users)](https://support.google.com/merchants/answer/14232691?hl=en)

### Do not build

- Every Shopify store serves `/agents.md`, `/llms.txt` and `/.well-known/ucp` by default: [Shopify Catalog and product discovery for agentic storefronts](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/products) · [Dawn demo UCP profile](https://theme-dawn-demo.myshopify.com/.well-known/ucp)
- Google's AI optimization guide: structured data "isn't required"; Merchant Center feeds help products appear in AI responses; llms.txt not used: [Optimizing your website for generative AI features on Google Search](https://developers.google.com/search/docs/fundamentals/ai-optimization-guide)
- For the OpenAI web-search API, retrieval explains far more of citation than page features: [What Drives AI Citations? Content, Retrieval and Model Knowledge in Generative Engine Optimization (GEO)](https://arxiv.org/abs/2610.15033)
- UCP is co-developed by Shopify and Google; OpenAI is not listed; no source says ChatGPT uses UCP: [The agentic commerce platform](https://www.shopify.com/news/ai-commerce-at-scale) · [ucp.dev](https://ucp.dev/)
- No OpenAI or ACP statement on UCP; Stripe and Meta sit on both governance bodies: [Universal Commerce Protocol](https://github.com/Universal-Commerce-Protocol/ucp) · [Stripe UCP docs](https://docs.stripe.com/agentic-commerce/protocols/ucp.md)
- Shopify product data reaches ChatGPT through Shopify Catalog with no merchant work: [Powering Product Discovery in ChatGPT](https://openai.com/index/powering-product-discovery-in-chatgpt/) · [Power product discovery in ChatGPT](https://chatgpt.com/merchants/)
- Google: UCP native integration "does not influence how we rank your offers": [Frequently asked questions](https://developers.google.com/merchant/ucp/faq)
- Ads run on separate systems and do not influence answers: [Ads in ChatGPT](https://help.openai.com/en/articles/20001047-ads-in-chatgpt)
- Organic AI Mode and AI Overviews answers come from "Search quality and ranking systems"; ads don't influence them: [About ads in AI-powered experiences in Google Search](https://support.google.com/google-ads/answer/18826097?hl=en)
