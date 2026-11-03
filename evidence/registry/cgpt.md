# Registry — CGPT (ChatGPT / OpenAI)

Schema: `evidence/README.md`. All entries accessed 2026-10-30. Help-center pages show relative dates only; "≈" dates are converted from "Updated: N days ago" on the access date.

`Checked` = the lead researcher re-read the excerpt on the live page before promotion. `pending` = taken from the raw notes only.

---

## Search retrieval and crawlers

### CGPT-001 — ChatGPT search uses third-party search providers and partner content
- **Claim:** OpenAI states that ChatGPT search draws on third-party search providers and on content supplied directly by partners.
- **Classification:** VERIFIED FACT · **Confidence:** Medium (2024 launch post; model details on the same page are outdated) · **Tier:** 1
- **Subject / topic:** ChatGPT / discovery
- **Source:** "Introducing ChatGPT search" — OpenAI — https://openai.com/index/introducing-chatgpt-search/
- **Published:** 2024-10-31 (update notes 2024-12-16, 2025-02-05) · **Accessed:** 2026-10-30
- **Excerpt:** > "ChatGPT search leverages third-party search providers, as well as content provided directly by our partners, to provide the information users are looking for."
- **Establishes:** Retrieval is not only an OpenAI-owned index. Partner content is a separate input.
- **Limitations:** The same post names "a fine-tuned version of GPT‑4o" as the search model. GPT-4o was retired from ChatGPT on 2026-02-13 (release notes). Providers are not named here.
- **Related:** CGPT-002, RES-013, RES-019
- **Origin:** notes/a-openai-search-and-shopping.md#A-01, #A-06 · **Checked:** pending

### CGPT-002 — The search help article lists Microsoft and Shopify as search providers
- **Claim:** ChatGPT search rewrites a query into targeted queries and sends them to partner search providers. The current help article links the privacy policies of Microsoft and Shopify for those providers.
- **Classification:** VERIFIED FACT (statement and links). That "Microsoft" means Bing today is an EVIDENCE-BASED INFERENCE: the 2025-10-14 version said "Bing" explicitly. · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / discovery
- **Source:** "Searching the web with ChatGPT" — OpenAI Help Center — https://help.openai.com/en/articles/9237897-searching-the-web-with-chatgpt
- **Published:** ≈2026-10-20 ("Updated: 10 days ago") · **Accessed:** 2026-10-30
- **Excerpt:** > "To provide relevant responses to your questions, ChatGPT search sometimes partners with other search providers. When it does, ChatGPT search typically rewrites your query into one or more targeted queries that it sends those providers." … "For more information about how search providers may process queries, review their privacy policies: Microsoft privacy statement. Shopify privacy policy."
- **Establishes:** Microsoft and Shopify are the only search providers OpenAI names. Shopify acts as a search provider, not only a catalog.
- **Limitations:** No split by query type. No statement that these are the only providers. Merge and ranking logic not described.
- **Related:** CGPT-001, CGPT-017, RES-013 (low SERP overlap), RES-019 (SerpApi report), RES-021 (carousel vs Google Shopping)
- **Origin:** notes/a-…#A-02 · **Checked:** 2026-10-30

### CGPT-003 — Query rewriting may add saved memories and approximate location
- **Claim:** With memory on, ChatGPT may add saved memories to rewritten search queries. It may use IP-derived general location. It does not send the IP address or account data to providers.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / retrieval, personalization
- **Source:** "Searching the web with ChatGPT" — OpenAI Help Center — https://help.openai.com/en/articles/9237897-searching-the-web-with-chatgpt
- **Published:** ≈2026-10-20 · **Accessed:** 2026-10-30
- **Excerpt:** > "If memory is enabled, ChatGPT may use relevant saved memories when rewriting a search query. For example, if you have shared that you are vegan and live in San Francisco, ChatGPT may search for “good vegan restaurants San Francisco” when you ask for nearby restaurants you might like."
- **Establishes:** Personal context enters retrieval at the query-rewrite step.
- **Limitations:** The example is restaurants. Product-query rewriting is not described separately.
- **Related:** CGPT-011, CGPT-045
- **Origin:** notes/a-…#A-03 · **Checked:** 2026-10-30

### CGPT-004 — Allowing OAI-SearchBot is the stated eligibility condition for search inclusion
- **Claim:** OpenAI states one condition for website eligibility: allow OAI-SearchBot and OpenAI's searchbot IPs. Ranking uses unlisted "multiple factors".
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / discovery, crawling
- **Source:** "Searching the web with ChatGPT" — OpenAI Help Center — https://help.openai.com/en/articles/9237897-searching-the-web-with-chatgpt
- **Published:** ≈2026-10-20 · **Accessed:** 2026-10-30
- **Excerpt:** > "ChatGPT ranks search results using multiple factors intended to help users find relevant, reliable information. Placement is not guaranteed." … "To make a website eligible for inclusion, allow OAI-Searchbot to crawl the site and confirm that the website host or content delivery network allows traffic from OpenAI’s published searchbot IP addresses."
- **Establishes:** Crawl access for OAI-SearchBot is a documented precondition for web-result inclusion.
- **Limitations:** Covers web search results. Does not say whether product carousels require it.
- **Related:** CGPT-006, CGPT-019
- **Origin:** notes/a-…#A-04 · **Checked:** 2026-10-30

### CGPT-005 — OpenAI operates a maintained web index (documented for Codex/Work)
- **Claim:** OpenAI's ChatGPT docs describe a first-party web search tool and a cached mode backed by an "OpenAI-maintained index".
- **Classification:** VERIFIED FACT for the Codex/Work context. That consumer ChatGPT search uses the same index is UNVERIFIED. · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** ChatGPT / discovery
- **Source:** "Web search" — ChatGPT docs — https://learn.chatgpt.com/docs/web-search.md
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "For local Codex chats, Codex enables cached search by default. Cached mode uses an OpenAI-maintained index instead of fetching arbitrary pages live, which lowers—but doesn't remove—prompt injection risk."
- **Establishes:** An OpenAI-maintained index exists.
- **Limitations:** Scoped to Codex local chats. Its role in consumer search is not stated.
- **Related:** CGPT-006
- **Origin:** notes/a-…#A-05 · **Checked:** pending

### CGPT-006 — OAI-SearchBot surfaces sites in search; opt-out removes them from answers within ~24 h
- **Claim:** OAI-SearchBot is the crawler for ChatGPT search. Sites that block it are not shown in search answers but can still appear as navigational links. robots.txt changes take about 24 hours.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / crawling
- **Source:** "Overview of OpenAI Crawlers" — OpenAI Developers — https://developers.openai.com/api/docs/bots (`.md` twin; platform.openai.com/docs/bots redirects here)
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "OAI-SearchBot is for search. OAI-SearchBot is used to surface websites in search results in ChatGPT's search features. Sites that are opted out of OAI-SearchBot will not be shown in ChatGPT search answers, though can still appear as navigational links." … "For search results, please note it can take ~24 hours from a site's robots.txt update for our systems to adjust."
- **Establishes:** The robots.txt token that controls ChatGPT search inclusion is `OAI-SearchBot`. Current UA version: `OAI-SearchBot/1.4`.
- **Limitations:** The doc does not mention shopping or product results.
- **Related:** CGPT-004, CGPT-007, CGPT-008
- **Origin:** notes/a-…#A-07 · **Checked:** 2026-10-30 (first sentences and ~24 h sentence)

### CGPT-007 — GPTBot (training) is independent of OAI-SearchBot (search)
- **Claim:** GPTBot collects training data. Blocking it does not affect search. If both bots are allowed, one crawl may serve both purposes.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / crawling
- **Source:** "Overview of OpenAI Crawlers" — OpenAI Developers — https://developers.openai.com/api/docs/bots.md
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Each setting is independent of the others – for example, a webmaster can allow OAI-SearchBot in order to appear in search results while disallowing GPTBot to indicate that crawled content should not be used for training OpenAI’s generative AI foundation models."
- **Establishes:** A merchant can block training and still allow search.
- **Limitations:** Whether training-data presence affects the model's product priors (RES-015, RES-017) is not addressed.
- **Related:** CGPT-006, RES-015
- **Origin:** notes/a-…#A-08 · **Checked:** pending

### CGPT-008 — ChatGPT-User fetches on user request; robots.txt "may not apply"
- **Claim:** ChatGPT-User fetches pages when a user's request triggers it. OpenAI says robots.txt rules may not apply. It does not decide search inclusion.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / crawling
- **Source:** "Overview of OpenAI Crawlers" — OpenAI Developers — https://developers.openai.com/api/docs/bots.md
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Because these actions are initiated by a user, robots.txt rules may not apply. ChatGPT-User is not used to determine whether content may appear in Search."
- **Establishes:** Blocking ChatGPT-User is not a documented control for search or shopping visibility.
- **Limitations:** The date of this wording could not be established (2025 archive is a JS shell).
- **Related:** CGPT-006
- **Origin:** notes/a-…#A-09 · **Checked:** 2026-10-30

### CGPT-009 — OAI-AdsBot visits only ad landing pages
- **Claim:** OAI-AdsBot checks pages submitted as ads and may use their content for ad relevance. Its data is not used for training.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / crawling, ads
- **Source:** "Overview of OpenAI Crawlers" — OpenAI Developers — https://developers.openai.com/api/docs/bots.md
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "OAI-AdsBot only visits pages submitted as ads, and the data collected by OAI-AdsBot is not used to train generative AI foundation models."
- **Establishes:** A fourth OpenAI agent exists, scoped to ads.
- **Limitations:** None material.
- **Related:** CGPT-042
- **Origin:** notes/a-…#A-10 · **Checked:** pending

## Product results (selection and ranking)

### CGPT-010 — Product results are "not ads, nor influenced by any OpenAI partnerships"
- **Claim:** OpenAI states that organic product results are selected independently and are separate from ads.
- **Classification:** VERIFIED FACT (stated policy; the mechanism cannot be audited externally) · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / ranking
- **Source:** "Shopping with ChatGPT Search" — OpenAI Help Center — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- **Published:** ≈2026-10-28 · **Accessed:** 2026-10-30
- **Excerpt:** > "Product results are selected independently by ChatGPT and are not ads, nor influenced by any OpenAI partnerships. Ads are separate from product results, and you can learn more about ads in ChatGPT."
- **Establishes:** Paying OpenAI is not a documented path into organic product results.
- **Limitations:** Policy statement. No audit published.
- **Related:** CGPT-042, CGPT-044
- **Origin:** notes/a-…#A-13 · **Checked:** 2026-10-30

### CGPT-011 — Product selection is model-judged relevance to intent, using query plus Memory and Custom instructions
- **Claim:** A product appears when ChatGPT judges it relevant to the user's intent. Factor weights change with the query.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / ranking, personalization
- **Source:** "Shopping with ChatGPT Search" — OpenAI Help Center — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- **Published:** ≈2026-10-28 · **Accessed:** 2026-10-30
- **Excerpt:** > "A product appears in the carousel when ChatGPT perceives it to be relevant to your intent. It considers your query and context (such as Memory or Custom instructions)." … "Depending on your needs, some of these factors will be more relevant than others. For example, if you specify a budget of $30, ChatGPT will focus more on price, whereas if price isn’t mentioned, it may focus on other aspects instead."
- **Establishes:** No fixed ranking formula is documented. Price, reviews and availability are named example factors ("available options, price, reviews, and ease of use").
- **Limitations:** No weights, thresholds or candidate-set size.
- **Related:** CGPT-012, CGPT-015
- **Origin:** notes/a-…#A-14 · **Checked:** 2026-10-30

### CGPT-012 — Three documented inputs to product selection
- **Claim:** OpenAI lists three inputs: structured metadata from first- and third-party providers plus other third-party content; the model's own pre-search response; safety standards and product policies.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / data sources, ranking
- **Source:** "Shopping with ChatGPT Search" — OpenAI Help Center — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- **Published:** ≈2026-10-28 (same bullets in Wayback snapshots 2025-10-28 and 2026-05-28) · **Accessed:** 2026-10-30
- **Excerpt:** > "Structured metadata from first-party and third-party providers (e.g., price, product description) and other third-party content." / "Model responses generated by ChatGPT before it considers any new search results." / "OpenAI safety standards and product policies."
- **Establishes:** The model's pre-search knowledge is an explicit input. Structured product metadata is the main data input.
- **Limitations:** "First-party" is undefined. Inference: merchant-supplied feeds and catalogs (CGPT-017, CGPT-018).
- **Related:** RES-015, RES-017, RES-018 (brand priors)
- **Origin:** notes/a-…#A-15 · **Checked:** 2026-10-30

### CGPT-013 — Displayed titles, labels and review summaries are model-generated; reviews come from public websites
- **Claim:** ChatGPT may rewrite product titles and descriptions, generate feature labels, and summarize reviews from public websites. OpenAI does not verify reviews.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / data sources
- **Source:** "Shopping with ChatGPT Search" — OpenAI Help Center — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- **Published:** ≈2026-10-28 · **Accessed:** 2026-10-30
- **Excerpt:** > "These model-generated summaries are based on reviews from public websites and are intended to highlight common user likes and dislikes about a product. Reviews and ratings are not verified by OpenAI."
- **Establishes:** Public review text is a documented input to what users see.
- **Limitations:** Review sources are not named.
- **Related:** CGPT-020
- **Origin:** notes/a-…#A-16 · **Checked:** 2026-10-30

### CGPT-014 — Prices come from third-party providers; the headline price is the first-listed merchant's
- **Claim:** The initial price is the first-ranked merchant's price, not necessarily the lowest. A "Best price" label marks the lowest price ChatGPT knows. Price updates can lag.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / data sources, pricing
- **Source:** "Shopping with ChatGPT Search" — OpenAI Help Center — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- **Published:** ≈2026-10-28 · **Accessed:** 2026-10-30
- **Excerpt:** > "Prices shown in ChatGPT’s initial response typically reflect the price from the first merchant listed, which may not be the lowest available price." … "When merchants update their pricing or shipping terms, there may be some delay before it is reflected in the information you see."
- **Establishes:** Merchant rank 1 sets the headline price. Freshness depends on the data pipeline.
- **Limitations:** Lag duration not stated.
- **Related:** CGPT-015, CGPT-047
- **Origin:** notes/a-…#A-17 · **Checked:** 2026-10-30

### CGPT-015 — Merchant list ordering: availability, price, quality, maker/primary seller
- **Claim:** For one product, ChatGPT ranks merchants by factors like availability, price, quality, and whether the merchant is the maker or primary seller. OpenAI expects more personalization.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / ranking
- **Source:** "Shopping with ChatGPT Search" — OpenAI Help Center — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- **Published:** ≈2026-10-28 · **Accessed:** 2026-10-30
- **Excerpt:** > "This list is generated by ChatGPT based on merchant and product metadata from third-party providers or directly from the merchants themselves. Merchants are ranked based on factors like availability, price, quality, and whether they are the maker or primary seller of that item. We expect this to evolve as we continue to improve the shopping experience, such as by personalizing merchant rankings even more to user preferences."
- **Establishes:** The only documented ranking factors in ChatGPT shopping. Selling your own brand ("maker") is a named factor.
- **Limitations:** "factors like" = non-exhaustive. "Quality" undefined. No weights.
- **Related:** CGPT-016 (superseded version)
- **Origin:** notes/a-…#A-18; notes/b-…#B-25 · **Checked:** 2026-10-30

### CGPT-016 — In 2025, Instant Checkout enablement was a merchant-ranking factor (superseded)
- **Claim:** In September 2025 OpenAI listed "whether Instant Checkout is enabled" among merchant-ranking factors, while saying Instant Checkout items were not preferred in product results. The factor is absent from the help article by 2026-05-28.
- **Classification:** VERIFIED FACT (historical statement); superseded by CGPT-015 · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / ranking
- **Source:** "Buy it in ChatGPT: Instant Checkout and the Agentic Commerce Protocol" — OpenAI — https://openai.com/index/buy-it-in-chatgpt/
- **Published:** 2025-09-29 (no update note) · **Accessed:** 2026-10-30
- **Excerpt:** > "Instant Checkout items are not preferred in product results. When ranking multiple merchants that sell the same product, ChatGPT considers factors like availability, price, quality, whether a merchant is the primary seller, and whether Instant Checkout is enabled, to optimize the user experience."
- **Establishes:** Two ranking levels exist: product results and the merchant list. Integration status once affected the merchant list.
- **Limitations:** The 2025 post reads as current but is outdated. Removal date between 2025-10-28 and 2026-05-28 (Wayback).
- **Related:** CGPT-015, CGPT-021
- **Origin:** notes/a-…#A-18, #A-23; notes/b-…#B-24 · **Checked:** pending

## Product data pipelines and merchant programs

### CGPT-017 — Shopify product data reaches ChatGPT through Shopify Catalog with no merchant work
- **Claim:** OpenAI states that Shopify merchants' product data is already integrated into ChatGPT through Shopify Catalog. Individual merchants need no additional work. Etsy catalogs are also integrated.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / data sources, Shopify
- **Source:** "Powering Product Discovery in ChatGPT" — OpenAI — https://openai.com/index/powering-product-discovery-in-chatgpt/ ; "Power product discovery in ChatGPT" — OpenAI — https://chatgpt.com/merchants/
- **Published:** 2026-03-24; merchants page not dated · **Accessed:** 2026-10-30
- **Excerpt:** > "For merchants on Shopify, product data is already integrated into ChatGPT through Shopify Catalog, helping products appear more accurately and completely in relevant user conversations. No additional work is required from individual merchants." / > "If you sell through Shopify or Etsy, your catalog is already integrated, and no additional setup or application is required."
- **Establishes:** Shopify Catalog is a documented first-party data path into ChatGPT. Same wording appears in the help article (CGPT-015 source).
- **Limitations:** Eligibility rules on the Shopify side (market, settings) are in SHOP entries. Whether integration changes ranking is not stated.
- **Related:** CGPT-002, SHOP entries
- **Origin:** notes/a-…#A-19, #A-20; notes/b-…#B-14 · **Checked:** 2026-10-30

### CGPT-018 — ACP was extended to product discovery on 2026-03-24; Salesforce and Stripe are delivery paths
- **Claim:** Merchants share product feeds and promotions with ChatGPT through ACP. Third-party providers such as Salesforce and Stripe can deliver them. Seven named retailers integrated for discovery.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / data sources, protocols
- **Source:** "Powering Product Discovery in ChatGPT" — OpenAI — https://openai.com/index/powering-product-discovery-in-chatgpt/
- **Published:** 2026-03-24 · **Accessed:** 2026-10-30
- **Excerpt:** > "Through ACP, merchants share product feeds and promotions so their catalogs are fully represented in ChatGPT. We support multiple delivery paths, including through third-party providers like Salesforce and Stripe, so merchants can participate with the systems they already use." / > "Already, leading retailers including Target, Sephora, Nordstrom, Lowe’s, Best Buy, The Home Depot, and Wayfair have integrated into ACP for discovery."
- **Establishes:** ACP's main role in ChatGPT is now catalog intake for discovery.
- **Limitations:** Does not say which transport each retailer uses (ACP Feed API vs OpenAI SFTP).
- **Related:** ACP-003, CGPT-022
- **Origin:** notes/b-…#B-13 · **Checked:** 2026-10-30

### CGPT-019 — A product feed is not required if ChatGPT already crawls the site
- **Claim:** OpenAI answers "No" to whether a merchant needs a feed when ChatGPT crawls its site. Feeds add control and freshness.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / data sources, merchant eligibility
- **Source:** "Power product discovery in ChatGPT" (FAQ) — OpenAI — https://chatgpt.com/merchants/
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Do I need a product feed if ChatGPT already crawls my site? No, but feeds give you greater control over how your products appear, helping ensure more accurate and up-to-date information."
- **Establishes:** Crawled pages are a documented product-data path alongside feeds.
- **Limitations:** Does not name the crawler for product data. Inference: OAI-SearchBot (CGPT-004, CGPT-006).
- **Related:** CGPT-004, CGPT-012
- **Origin:** notes/b-…#B-15 · **Checked:** 2026-10-30

### CGPT-020 — OpenAI markets richer data as "better placement" and matching on "past interactions"
- **Claim:** The merchant page says richer product data helps products surface and that ChatGPT matches products to shoppers using preferences and past interactions.
- **Classification:** VERIFIED FACT (marketing statement; mechanism not described) · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** ChatGPT / ranking, personalization
- **Source:** "Power product discovery in ChatGPT" — OpenAI — https://chatgpt.com/merchants/
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Get better placement in results | Richer data helps your products surface with more accurate information when shoppers compare options." / > "ChatGPT helps match your products to people based on shopper preferences and past interactions."
- **Establishes:** OpenAI links data completeness to placement in its own words.
- **Limitations:** Marketing copy. Not quantified. "Placement" is tied to "more accurate information", not to an explicit ranking boost.
- **Related:** CGPT-032, CGPT-030
- **Origin:** notes/b-…#B-21 · **Checked:** 2026-10-30

### CGPT-021 — 2026-03-24: OpenAI dropped the initial Instant Checkout and refocused on discovery
- **Claim:** OpenAI said the first Instant Checkout lacked flexibility. Merchants now use their own checkout while OpenAI focuses on product discovery.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / checkout
- **Source:** "Powering Product Discovery in ChatGPT" — OpenAI — https://openai.com/index/powering-product-discovery-in-chatgpt/
- **Published:** 2026-03-24 · **Accessed:** 2026-10-30
- **Excerpt:** > "We’ve found that the initial version of Instant Checkout did not offer the level of flexibility that we aspire to provide, so we’re allowing merchants to use their own checkout experiences while we focus our efforts on product discovery."
- **Establishes:** The 2025 checkout-in-chat model is no longer the default.
- **Limitations:** No shutdown date given. Instant Checkout help article now returns "page doesn't exist" (removed between 2026-02-10 and 2026-04-07 per Wayback).
- **Related:** CGPT-016, CGPT-022, CGPT-023
- **Origin:** notes/b-…#B-02, #B-04; notes/a-…#A-24 · **Checked:** 2026-10-30

### CGPT-022 — Shopping is live in the US only; purchases complete on merchant sites
- **Claim:** OpenAI's merchant page says shopping is live for US users. Users discover in ChatGPT and buy on merchant-owned sites or apps.
- **Classification:** VERIFIED FACT · **Confidence:** High (statement); scope of "shopping" is ambiguous · **Tier:** 1
- **Subject / topic:** ChatGPT / regions, checkout
- **Source:** "Power product discovery in ChatGPT" — OpenAI — https://chatgpt.com/merchants/
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "We’re moving away from a standalone Instant Checkout experience in ChatGPT and prioritizing better shopping discovery and merchant-owned checkout experiences. Users can discover and evaluate products in ChatGPT, but purchases are completed on merchant-owned websites or apps." / > "Shopping is currently live for ChatGPT users in the U.S. We’re building a merchant platform for self-serve data integration later this year, and plan to expand to more merchants and regions over time."
- **Establishes:** OpenAI's only region statement for shopping is US-only. India is not named.
- **Limitations:** "Shopping" may mean the merchant-feed program, not every product carousel. The consumer help article states no region. The 2026-03-24 release note says the shopping update reached "all ChatGPT users" (CGPT-053). Must be tested from India (EXP).
- **Related:** CGPT-046, CGPT-031 (feed defaults to US), CGPT-053 (contradiction)
- **Origin:** notes/b-…#B-03; notes/a-…#A-39 · **Checked:** 2026-10-30

### CGPT-023 — In-chat checkout survives only as a beta for "select marketplace partners"
- **Claim:** OpenAI's plugin docs describe Instant Checkout / the ChatGPT payment sheet as a beta limited to select marketplace partners. External checkout is the default.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / checkout
- **Source:** "Plugin guidelines" — OpenAI Developers — https://developers.openai.com/plugins/plugin-guidelines.md
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Instant Checkout, which is currently in beta, is currently available only to select marketplace partners and may expand to additional marketplaces and retailers over time."
- **Establishes:** In-chat payment is narrow, not fully retired.
- **Limitations:** Partners not named.
- **Related:** CGPT-021, CGPT-039
- **Origin:** notes/b-…#B-05 · **Checked:** pending

### CGPT-024 — Merchant fees: "small fee" (2025) replaced by "no fees" (2026)
- **Claim:** In 2025 merchants paid a fee on completed Instant Checkout purchases. The current merchant page states no fees on purchases that start in ChatGPT.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / merchant eligibility
- **Source:** https://openai.com/index/buy-it-in-chatgpt/ (2025-09-29); https://chatgpt.com/merchants/ (current)
- **Published:** 2025-09-29; current page not dated · **Accessed:** 2026-10-30
- **Excerpt:** > "Send shoppers to your site or app by default, with no fees for purchases made on your site or app." (current) / > "Merchants pay a small fee on completed purchases, but the service is free for users, doesn’t affect their prices, and doesn’t influence ChatGPT’s product results." (2025)
- **Establishes:** No current per-order fee to appear or sell via ChatGPT.
- **Limitations:** The 2025 rate was never published in a fetched source.
- **Related:** CGPT-021
- **Origin:** notes/b-…#B-06 · **Checked:** 2026-10-30 (current sentence)

### CGPT-025 — Direct feeds are for approved partners via an application and waitlist
- **Claim:** Feed onboarding is limited to approved partners who apply at chatgpt.com/merchants. No approval criteria are published. A self-serve portal is planned "later this year".
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / merchant eligibility
- **Source:** "Get Started" — OpenAI Developers — https://developers.openai.com/commerce/guides/get-started.md ; https://chatgpt.com/merchants/
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Onboarding product feeds in ChatGPT is currently available to approved partners. To apply for access, fill out this form [here](https://chatgpt.com/merchants)"
- **Establishes:** A direct OpenAI feed is gated. Shopify merchants do not need it (CGPT-017).
- **Limitations:** No criteria, SLA or timing published.
- **Related:** CGPT-017, CGPT-019
- **Origin:** notes/b-…#B-27 · **Checked:** pending

### CGPT-026 — Prohibited-products policy filters products before ranking
- **Claim:** OpenAI publishes prohibited product categories for feeds and may remove products or ban sellers from being surfaced.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / merchant eligibility
- **Source:** "Get Started" — OpenAI Developers — https://developers.openai.com/commerce/guides/get-started.md
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "OpenAI may take corrective actions such as removing a product or banning a seller from being surfaced in ChatGPT if these policies are violated."
- **Establishes:** A policy eligibility gate exists (matches the "safety standards and product policies" input in CGPT-012).
- **Limitations:** Enforcement process not documented.
- **Related:** CGPT-012
- **Origin:** notes/b-…#B-28 · **Checked:** pending

## OpenAI product feed specification (developers.openai.com/commerce)

### CGPT-027 — Feed delivery: SFTP push of full snapshots, parquet preferred, at least daily, 14-day retention
- **Claim:** OpenAI's Stable file-upload spec takes full-snapshot feeds by SFTP. Parquet is preferred. Cadence is at least daily. Missing products persist up to 14 days.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / feeds
- **Source:** "File upload — Overview" — OpenAI Developers — https://developers.openai.com/commerce/specs/file-upload/overview.md
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Delivery model | Push feeds to OpenAI via SFTP." / > "A product is not deleted immediately when missing from a processed snapshot. OpenAI retains its most recently processed record for up to 14 days."
- **Establishes:** Feed freshness floor is daily. Stale records can survive two weeks.
- **Limitations:** The merchant FAQ also mentions APIs and feed providers. The Stable spec documents only SFTP for product upload.
- **Related:** CGPT-028
- **Origin:** notes/b-…#B-16 · **Checked:** pending

### CGPT-028 — Nine required feed fields; one row per variant
- **Claim:** The Stable spec requires `item_id`, `title`, `description`, `url`, `brand`, `seller_name`, `image_url`, `availability`, `price`. GTIN, MPN, material, dimensions, reviews and return fields are optional.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / feeds
- **Source:** "Products (file upload)" — OpenAI Developers — https://developers.openai.com/commerce/specs/file-upload/products.md
- **Published:** not stated (schema labeled "Stable") · **Accessed:** 2026-10-30
- **Excerpt:** > "Include the nine required fields in Basic product data, then add the optional data that describes your products."
- **Establishes:** The minimum product record OpenAI accepts. Full field table: notes/b-…§3.
- **Limitations:** A "Draft" schema view exists but was not captured.
- **Related:** CGPT-029, CGPT-030
- **Origin:** notes/b-…#B-17, §3 · **Checked:** 2026-10-30

### CGPT-029 — Search eligibility defaults on; "Eligibility does not guarantee display"
- **Claim:** `is_eligible_search` defaults to true. Eligibility does not guarantee display. `enable_search`/`enable_checkout` are legacy aliases.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / feeds
- **Source:** "Products (file upload)" — OpenAI Developers — https://developers.openai.com/commerce/specs/file-upload/products.md
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "`true` enables search eligibility; `false` disables it and checkout eligibility. Omitted or empty: `true`. Eligibility does not guarantee display."
- **Establishes:** A feed makes a product eligible, not visible.
- **Limitations:** None.
- **Related:** CGPT-028
- **Origin:** notes/b-…#B-18 · **Checked:** 2026-10-30 (last sentence)

### CGPT-030 — Current feed spec carries review fields but no popularity or return-rate fields
- **Claim:** The current spec has `review_count`, `star_rating` and setup-gated store ratings. It has no popularity or return-rate field. The 2025 spec URL 301-redirects to it.
- **Classification:** VERIFIED FACT (field existence). Use of any field in ranking: UNVERIFIED HYPOTHESIS. · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / feeds, ranking
- **Source:** "Products (file upload)" — OpenAI Developers — https://developers.openai.com/commerce/specs/file-upload/products.md
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Raw review entries and question-and-answer lists are not part of this discovery contract. Store aggregates have a separate scope and require the setup in the next section."
- **Establishes:** Which signals a merchant can even send through OpenAI's feed.
- **Limitations:** The 2025 field list (which had popularity fields per older docs) could not be re-fetched.
- **Related:** CGPT-032, ACP-004, ACP-007
- **Origin:** notes/b-…#B-19 · **Checked:** pending

### CGPT-031 — Feed format targets the US by default
- **Claim:** Standard OpenAI-format uploads target the US. Other markets need OpenAI-confirmed setup. The format represents US, CA and MX.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / feeds, regions
- **Source:** "Products (file upload)" — OpenAI Developers — https://developers.openai.com/commerce/specs/file-upload/products.md
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "The standard OpenAI-format upload currently targets the US. Row-level market columns do not change that default."
- **Establishes:** Direct feeds do not reach Indian shoppers today.
- **Limitations:** CA/MX live status not stated.
- **Related:** CGPT-022
- **Origin:** notes/b-…#B-22 · **Checked:** 2026-10-30

### CGPT-032 — An OpenAI guide says recommended attributes "improve ranking" (likely stale page)
- **Claim:** OpenAI's commerce "Key concepts" guide says recommended attributes such as rich media, reviews and performance signals improve ranking.
- **Classification:** VERIFIED FACT (statement exists). That the page predates the 2026 spec is an EVIDENCE-BASED INFERENCE. · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** ChatGPT / ranking, feeds
- **Source:** "Key concepts" — OpenAI Developers — https://developers.openai.com/commerce/guides/key-concepts.md
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Required fields ensure correct display of price and availability, while recommended attributes—like rich media, reviews, and performance signals—improve ranking, relevance, and user trust."
- **Establishes:** OpenAI's only explicit doc link between feed attributes and ranking.
- **Limitations:** The same page opens with Instant Checkout requirements and says feeds are "CSV or JSON". The current spec has no performance-signal field and prefers parquet.
- **Related:** CGPT-020, CGPT-030
- **Origin:** notes/b-…#B-20; notes/a-…#A-21 · **Checked:** pending

## Shopping research, agents, plugins

### CGPT-033 — Shopping research (2025-11-24) read public retail sites and avoided low-quality sites
- **Claim:** Shopping research ran on a GPT-5 mini variant trained with reinforcement learning for shopping. It read product pages directly, cited sources, and avoided low-quality or spammy sites. Merchants were pointed to an allowlisting process.
- **Classification:** VERIFIED FACT (as of 2025-11-24) · **Confidence:** Medium (feature status now unclear, CGPT-035) · **Tier:** 1
- **Subject / topic:** ChatGPT / discovery
- **Source:** "Introducing shopping research in ChatGPT" — OpenAI — https://openai.com/index/chatgpt-shopping-research/
- **Published:** 2025-11-24 · **Accessed:** 2026-10-30
- **Excerpt:** > "Results are organic and based on publicly available retail sites—reading product pages directly, citing sources, and avoiding low-quality or spammy sites. Merchants who want to ensure they are available to appear in shopping research results can follow the allowlisting process here."
- **Establishes:** An agentic retrieval path that fetches merchant product pages directly.
- **Limitations:** The "here" link now resolves to the ChatGPT Work cloud-browser allowlisting article.
- **Related:** CGPT-034, CGPT-035, CGPT-036
- **Origin:** notes/a-…#A-25, #A-26 · **Checked:** pending

### CGPT-034 — Shopping research skipped sites that block automated access (archived help, Aug 2026)
- **Claim:** The archived help article listed ACP merchant data, public product information and other retail sources as inputs. It said shopping research skips retailers that block automated access.
- **Classification:** VERIFIED FACT (archived snapshot 2026-08-05) · **Confidence:** Medium · **Tier:** 1 (archived)
- **Subject / topic:** ChatGPT / discovery, crawling
- **Source:** "Using shopping research in ChatGPT" — OpenAI Help Center (Wayback) — https://web.archive.org/web/20260805232131/https://help.openai.com/en/articles/12911370-using-shopping-research-in-chatgpt
- **Published:** ≈2026-07-30 (snapshot shows "Updated: 6 days ago") · **Accessed:** 2026-10-30
- **Excerpt:** > "In addition, some retailers block automated access to their sites.When this happens, shopping research will either skip those sources or rely on other sites with similar products."
- **Establishes:** Blocking automated access led to exclusion or substitution in shopping research.
- **Limitations:** Archived copy. The live article now redirects (CGPT-035).
- **Related:** MKT entries (robots.txt), CGPT-036
- **Origin:** notes/a-…#A-27 · **Checked:** pending

### CGPT-035 — The shopping research help article now redirects to the general shopping article
- **Claim:** The shopping research help URL redirects to "Shopping with ChatGPT Search", which does not mention shopping research.
- **Classification:** VERIFIED FACT (redirect). That the feature was retired or merged is an UNVERIFIED HYPOTHESIS. · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** ChatGPT / discovery
- **Source:** https://help.openai.com/en/articles/12911370-using-shopping-research-in-chatgpt → https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- **Published:** observed 2026-10-30 · **Accessed:** 2026-10-30
- **Excerpt:** [no text: redirect observed in browser]
- **Establishes:** No current OpenAI documentation for shopping research.
- **Limitations:** No retirement entry in release notes. Pulse (a shopping-research surface) was sunset 2026-06-17.
- **Related:** CGPT-033
- **Origin:** notes/a-…#A-28 · **Checked:** pending

### CGPT-036 — Agent mode is discontinued; the ChatGPT Work cloud browser does browser tasks and sites can block it
- **Claim:** "ChatGPT agent is no longer available." Browser tasks run in the ChatGPT Work cloud browser on paid plans (not Free or Go). It signs requests with Web Bot Auth. Websites can restrict it.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / agentic shopping
- **Source:** "ChatGPT agent" — https://help.openai.com/en/articles/11752874-chatgpt-agent ; "Using cloud browser in ChatGPT" — https://help.openai.com/en/articles/20001280-using-cloud-browser-in-chatgpt ; "ChatGPT Work's Cloud browser allowlisting" — https://help.openai.com/en/articles/11845367-chatgpt-works-cloud-browser-allowlisting (all OpenAI Help Center)
- **Published:** ≈2026-10-27, ≈2026-10-28, ≈2026-10-19 · **Accessed:** 2026-10-30
- **Excerpt:** > "ChatGPT agent is no longer available. Use ChatGPT Work for longer, multi-step tasks and finished deliverables." / > "ChatGPT Work's Cloud browser uses Web Bot Auth to sign outbound HTTP requests, allowing website operators to verify that requests genuinely originate from ChatGPT."
- **Establishes:** Agentic browsing is a separate retrieval path, identified by signature, not by a robots.txt token.
- **Limitations:** How the cloud browser finds or ranks products is undocumented. Atlas was retired (stop date 2026-08-09).
- **Related:** CGPT-034, CGPT-037
- **Origin:** notes/a-…#A-12, #A-36, #A-37 · **Checked:** pending

### CGPT-037 — Site tools: ChatGPT implements the proposed WebMCP standard in its desktop browser
- **Claim:** Websites can expose predefined actions to ChatGPT Work and Codex in the desktop app's built-in browser via WebMCP ("site tools").
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / agentic shopping, protocols
- **Source:** "Site tools" — ChatGPT docs — https://learn.chatgpt.com/docs/webmcp.md
- **Published:** not stated (release note 2026-08-31) · **Accessed:** 2026-10-30
- **Excerpt:** > "Site tools are ChatGPT's implementation of the proposed WebMCP standard. With WebMCP, a website can offer useful actions directly to an agent alongside the interface people already use."
- **Establishes:** A documented non-crawl channel for sites to expose functions to ChatGPT's agent.
- **Limitations:** Shopping is not a documented use case. Desktop app only.
- **Related:** CGPT-036
- **Origin:** notes/a-…#A-38 · **Checked:** pending

### CGPT-038 — Apps became Plugins (2026-07-09); commerce plugins may sell physical goods with external checkout
- **Claim:** OpenAI replaced the App Directory with a Plugin Directory. Plugins may conduct commerce only for physical goods and should use external checkout.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / integrations
- **Source:** "ChatGPT release notes" — OpenAI Help Center — https://help.openai.com/en/articles/6825453-chatgpt-release-notes ; "Plugin guidelines" — OpenAI Developers — https://developers.openai.com/plugins/plugin-guidelines.md
- **Published:** 2026-07-09 (release note) · **Accessed:** 2026-10-30
- **Excerpt:** > "We’re also replacing the App Directory with the Plugin Directory." / > "Plugins should use external checkout, directing users to complete purchases on your own domain."
- **Establishes:** "Apps in ChatGPT" research must target the Plugins docs.
- **Limitations:** Commerce marketing pages still say "apps".
- **Related:** CGPT-039, CGPT-040
- **Origin:** notes/b-…#B-29, #B-31 · **Checked:** pending

### CGPT-039 — Product checkout conversion plugins (beta): feed first, then a seller plugin can open from the product sidebar
- **Claim:** After a partner provides a product feed, OpenAI can connect its MCP server so ChatGPT opens the seller's plugin inline for checkout from the product entity sidebar.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / integrations, checkout
- **Source:** "Product checkout conversion spec" — OpenAI Developers — https://developers.openai.com/plugins/guides/product-checkout-conversion-spec.md
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Once partners provide us with a product feed for search, we can connect their MCP servers for bottom-of-funnel conversion actions." / > "If a seller has a plugin, ChatGPT can open that plugin inline for checkout instead of punching out to an external website."
- **Establishes:** The 2026 replacement for Instant Checkout: feed → merchant list → plugin.
- **Limitations:** Beta, approved partners only. Effect on merchant order not stated.
- **Related:** CGPT-023, CGPT-038
- **Origin:** notes/b-…#B-30 · **Checked:** pending

### CGPT-040 — ChatGPT decides when to call a plugin from its metadata; directory placement is discretionary
- **Claim:** ChatGPT selects plugin tools from the metadata developers provide. Enhanced distribution cannot be requested. OpenAI says most merchants start with feeds; apps suit larger merchants.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / integrations
- **Source:** "Optimize Metadata" — https://developers.openai.com/plugins/guides/optimize-metadata.md ; "Plugin guidelines" — https://developers.openai.com/plugins/plugin-guidelines.md ; https://chatgpt.com/merchants/
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "ChatGPT and Codex decide when to call your tool based on the metadata you provide." / > "Most merchants start with product feeds, which power how products appear in ChatGPT. Apps are optional and are best suited for larger merchants who want more control over the shopping and purchase experience."
- **Establishes:** A plugin is not a discovery shortcut for small merchants.
- **Limitations:** Selection algorithm undisclosed.
- **Related:** CGPT-038
- **Origin:** notes/b-…#B-32 · **Checked:** 2026-10-30 (merchants sentence)

### CGPT-041 — Walmart launched an in-ChatGPT app (2026-03-24)
- **Claim:** Walmart introduced an in-ChatGPT app with account linking, loyalty and Walmart payments.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / marketplaces
- **Source:** "Powering Product Discovery in ChatGPT" — OpenAI — https://openai.com/index/powering-product-discovery-in-chatgpt/
- **Published:** 2026-03-24 · **Accessed:** 2026-10-30
- **Excerpt:** > "Today, we are excited to share that Walmart is introducing an in-ChatGPT app experience that takes users from discovery in ChatGPT into a tailored Walmart environment that supports account linking, loyalty and Walmart payments."
- **Establishes:** Large marketplaces use plugins for deeper integration.
- **Limitations:** Effect on Walmart's organic product visibility not stated.
- **Related:** MKT entries
- **Origin:** notes/b-…#B-33 · **Checked:** 2026-10-30

## Ads

### CGPT-042 — Ads run on separate systems and do not influence answers
- **Claim:** OpenAI states ads do not influence ChatGPT's answers, run on systems separate from the chat model, and are labeled.
- **Classification:** VERIFIED FACT (stated policy) · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / ads, ranking
- **Source:** "Ads in ChatGPT" — OpenAI Help Center — https://help.openai.com/en/articles/20001047-ads-in-chatgpt
- **Published:** ≈2026-10-28 · **Accessed:** 2026-10-30
- **Excerpt:** > "No. Ads do not influence ChatGPT’s answers. Ads run on separate systems from our chat model, and advertisers have no ability to shape, rank, or alter ChatGPT’s responses. Ads are separate and clearly labeled."
- **Establishes:** Paid placement exists only in the ad unit, per OpenAI.
- **Limitations:** Policy statement; no audit.
- **Related:** CGPT-010, CGPT-043, CGPT-044
- **Origin:** notes/a-…#A-29 · **Checked:** pending

### CGPT-043 — Ads appear below the answer on Free and Go plans; ranked by relevance plus bids
- **Claim:** One ad unit appears below a response. Ads show on Free and Go only, not in Temporary Chats. Ad ranking combines relevance and advertiser bids.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / ads
- **Source:** "Ads in ChatGPT" — OpenAI Help Center — https://help.openai.com/en/articles/20001047-ads-in-chatgpt
- **Published:** ≈2026-10-28 · **Accessed:** 2026-10-30
- **Excerpt:** > "You will see one ad unit that may contain one or multiple images below a ChatGPT response." / > "If there are multiple eligible ads, we consider a combination of factors, including relevance and advertiser bids when deciding which ad to show first."
- **Establishes:** Experiments must record plan and label every ad unit separately from organic items.
- **Limitations:** User-side country list for ads not found. India is listed for advertiser self-service only (2026-08-31).
- **Related:** CGPT-042
- **Origin:** notes/a-…#A-30, #A-31, #A-32, #A-33 · **Checked:** pending

### CGPT-044 — Ads Manager product feeds serve ads only, not organic results (beta)
- **Claim:** Products uploaded through Ads Manager feeds are eligible only for ads during the beta. They do not appear in organic conversations.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / ads, feeds
- **Source:** "Create Campaigns from Product Feeds" — OpenAI Help Center — https://help.openai.com/en/articles/20001268-create-campaigns-from-product-feeds
- **Published:** ≈2026-10-27 · **Accessed:** 2026-10-30
- **Excerpt:** > "Products from your feed will only be eligible for use in ads during this beta. They will not appear in organic ChatGPT conversations, though we may offer that capability in the future"
- **Establishes:** An ads feed is not an organic discovery path.
- **Limitations:** "During this beta" may change.
- **Related:** CGPT-042
- **Origin:** notes/a-…#A-22 · **Checked:** pending

## Personalization, regions, accuracy

### CGPT-045 — Location context is used for shopping queries (GPT-5.5 Instant, 2026-06-24)
- **Claim:** The 2026-06-24 model update makes better use of location context to surface nearby options for shopping and local queries.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / personalization
- **Source:** "ChatGPT release notes" (2026-06-24) — OpenAI Help Center — https://help.openai.com/en/articles/6825453-chatgpt-release-notes
- **Published:** 2026-06-24 · **Accessed:** 2026-10-30
- **Excerpt:** > "Shopping and local business queries should also feel more useful. The model makes better use of location context to surface relevant nearby options and can bring together product recommendations, business information, and images more coherently when those elements are helpful."
- **Establishes:** Location is a documented variable for shopping answers. Experiments must fix and record it.
- **Limitations:** Effect size unknown.
- **Related:** CGPT-003, CGPT-011
- **Origin:** notes/a-…#A-35 · **Checked:** pending

### CGPT-046 — No OpenAI source documents ChatGPT shopping availability in India
- **Claim:** No fetched OpenAI page states that product results or shopping are available to users in India. India appears only for ads self-service and plans.
- **Classification:** VERIFIED FACT (absence across fetched OpenAI sources) · **Confidence:** Medium (absence of evidence) · **Tier:** 1
- **Subject / topic:** ChatGPT / regions
- **Source:** https://chatgpt.com/merchants/ ; https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search ; https://openai.com/index/expanding-access-to-ai-with-chatgpt-ads/
- **Published:** various · **Accessed:** 2026-10-30
- **Excerpt:** > "Starting later today, advertisers can purchase ChatGPT ads directly via Ads Manager across India, Europe, the Middle East, and North Africa." (2026-08-31)
- **Establishes:** For the brief's ₹ use case, OpenAI documents no India shopping surface.
- **Limitations:** Press reported an NPCI/Razorpay pilot with OpenAI (TechCrunch, 2025-10-09, Tier 3). See MKT entries. Needs an India-located experiment.
- **Related:** CGPT-022, CGPT-031
- **Origin:** notes/a-…#A-39, #A-40 · **Checked:** pending

### CGPT-047 — OpenAI disclaims accuracy and completeness of product listings
- **Claim:** OpenAI tells users to confirm price, availability and policies with the merchant. Not all products are shown.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / data accuracy
- **Source:** "Shopping with ChatGPT Search" — OpenAI Help Center — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- **Published:** ≈2026-10-28 · **Accessed:** 2026-10-30
- **Excerpt:** > "Keep in mind that not all available products will necessarily be shown (there are a lot of dog costumes out there). We recommend verifying that products meet your specific needs before purchasing."
- **Establishes:** Inclusion is selective. Data errors are expected.
- **Limitations:** None.
- **Related:** CGPT-014
- **Origin:** notes/a-…#A-41 · **Checked:** 2026-10-30

### CGPT-048 — Product results show when a question "suggests shopping intent"
- **Claim:** ChatGPT shows product options with images, details and links when it judges that a question suggests shopping intent.
- **Classification:** VERIFIED FACT (the trigger exists). How intent is detected: undocumented. · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / intent detection
- **Source:** "Shopping with ChatGPT Search" — OpenAI Help Center — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- **Published:** ≈2026-10-31 (page showed "Updated: 8 hours ago") · **Accessed:** 2026-10-31
- **Excerpt:** > "When your question suggests shopping intent (for example, “Help me find costumes for my dog”), ChatGPT can show product options with imagery, product details, and links to sites where you can learn more or purchase."
- **Establishes:** An intent check gates the product-results path. Non-shopping questions take the normal answer path.
- **Limitations:** No classifier, threshold or confidence is described. "Can show" means results are not guaranteed even with shopping intent.
- **Related:** CGPT-011, CGPT-012
- **Origin:** lead, live browser read 2026-10-31 · **Checked:** 2026-10-31

## Plans, models and search behavior

### CGPT-049 — Web search runs on every plan and for logged-out users, within plan usage limits
- **Claim:** OpenAI lists web search on Free, Go, Plus, Pro, Business, Enterprise and Edu, and for signed-out users. Searches count against plan usage limits.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / plans, search availability
- **Source:** "Searching the web with ChatGPT" — OpenAI Help Center — https://help.openai.com/en/articles/9237897-searching-the-web-with-chatgpt
- **Published:** ≈2026-10-20 ("Updated: 11 days ago") · **Accessed:** 2026-10-31
- **Excerpt:** > "Web search is available on ChatGPT Free, Go, Plus, Pro, Business, Enterprise, and Edu. People who are not signed in can also use web search." / > "Searches are subject to your plan’s usage limits."
- **Establishes:** No plan is documented as lacking web search. The search path exists for Free and logged-out users.
- **Limitations:** Per-plan search limits are not stated. Availability says nothing about how often search runs.
- **Related:** CGPT-050, CGPT-052, CGPT-053
- **Origin:** lead, live browser read 2026-10-31 · **Checked:** 2026-10-31

### CGPT-050 — ChatGPT decides when to search; a model update changed that decision
- **Claim:** ChatGPT may search automatically when a question benefits from current information. OpenAI said GPT-5.5 Instant (2026-05-05) improved "when ChatGPT decides to search the web".
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / models, search behavior
- **Source:** "Searching the web with ChatGPT" — OpenAI Help Center — https://help.openai.com/en/articles/9237897-searching-the-web-with-chatgpt ; "ChatGPT release notes" — OpenAI Help Center — https://help.openai.com/en/articles/6825453-chatgpt-release-notes
- **Published:** help ≈2026-10-20; release note dated 2026-05-05 · **Accessed:** 2026-10-31
- **Excerpt:** > "ChatGPT may search the web automatically when your question would benefit from current information." / > "It replaces GPT-5.3 Instant for all ChatGPT users and improves everyday answers across accuracy, clarity and conciseness, image understanding, STEM questions, and when ChatGPT decides to search the web."
- **Establishes:** The search decision is model behavior. It can differ between model versions.
- **Limitations:** No source says models on different plans search at different rates. Users can also start a search manually.
- **Related:** CGPT-049, CGPT-052
- **Origin:** lead, live browser read 2026-10-31 · **Checked:** 2026-10-31

### CGPT-051 — After first results, ChatGPT may send more specific follow-up queries to other providers
- **Claim:** Query rewriting is iterative. ChatGPT reviews the initial results, then may send more specific queries to other search providers.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / retrieval
- **Source:** "Searching the web with ChatGPT" — OpenAI Help Center — https://help.openai.com/en/articles/9237897-searching-the-web-with-chatgpt
- **Published:** ≈2026-10-20 · **Accessed:** 2026-10-31
- **Excerpt:** > "After reviewing the initial results, ChatGPT search may send additional, more specific queries to other search providers, like “CHS-114 conference 2025.”"
- **Establishes:** One prompt can produce several rounds of sub-queries across providers.
- **Limitations:** The example is not a shopping query. Round count and provider order are not stated.
- **Related:** CGPT-002, CGPT-003
- **Origin:** lead, live browser read 2026-10-31 · **Checked:** 2026-10-31

### CGPT-052 — Free and Go run a different default model than paid plans; a mini model is the rate-limit fallback
- **Claim:** Since 2026-10-07, Plus, Pro, Business and Enterprise use GPT-6 Sol in Chat; Free and Go use GPT-6 Luna. Since 2026-07-06, users who hit GPT-5.5 Instant or Auto limits fall back to GPT-5.5 Instant Mini.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / plans, models
- **Source:** "ChatGPT release notes" — OpenAI Help Center — https://help.openai.com/en/articles/6825453-chatgpt-release-notes
- **Published:** entries dated 2026-10-07 and 2026-07-06 · **Accessed:** 2026-10-31
- **Excerpt:** > "Plus, Pro, Business, and Enterprise use GPT-6 Sol; Free and Go use GPT-6 Luna." / > "It replaces GPT-5.3 Instant Mini as the fallback model users reach after hitting their GPT-5.5 Instant or Auto rate limits."
- **Establishes:** The model that answers a shopping prompt depends on the plan and on usage limits.
- **Limitations:** No source says the shopping path or its inputs differ by model. The current fallback model under GPT-6 is not stated.
- **Related:** CGPT-050, CGPT-053, CGPT-054
- **Origin:** lead, live browser read 2026-10-31 · **Checked:** 2026-10-31

### CGPT-053 — The 2026-03-24 shopping update rolled out to all ChatGPT users and names ACP as the product-data protocol
- **Claim:** OpenAI's release note says the shopping improvements rolled out to all ChatGPT users. It says they improve retrieval of product information "from merchants and other providers using the Agentic Commerce Protocol (ACP)".
- **Classification:** VERIFIED FACT (statements). That Shopify Catalog data reaches ChatGPT over ACP is an EVIDENCE-BASED INFERENCE at most: the note does not name Shopify. · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** ChatGPT / plans, protocols
- **Source:** "ChatGPT release notes" — OpenAI Help Center — https://help.openai.com/en/articles/6825453-chatgpt-release-notes
- **Published:** entry dated 2026-03-24 · **Accessed:** 2026-10-31
- **Excerpt:** > "These improvements are rolling out to all ChatGPT users this week." / > "These updates improve how ChatGPT retrieves and presents product information from merchants and other providers using the Agentic Commerce Protocol (ACP)."
- **Establishes:** Product results are not documented as plan-gated. ACP is OpenAI's stated intake protocol for merchant and provider product data.
- **Limitations:** Contradiction: "all ChatGPT users" vs the merchant page's "live for ChatGPT users in the U.S." (CGPT-022). Region scope is unresolved.
- **Related:** CGPT-018, CGPT-022, CGPT-049; report §10 gap 7 (wire format)
- **Origin:** lead, live browser read 2026-10-31 · **Checked:** 2026-10-31

### CGPT-054 — OpenAI documents model gating for reservation search; none for shopping
- **Claim:** Reservation search works only with GPT-5.6 Sol or GPT-5.6 Luna on eligible consumer plans. The shopping help article states no plan or model restriction.
- **Classification:** VERIFIED FACT (both statements). No shopping gating: VERIFIED FACT as absence in fetched OpenAI pages. · **Confidence:** Medium (absence of evidence) · **Tier:** 1
- **Subject / topic:** ChatGPT / models, feature gating
- **Source:** "Searching the web with ChatGPT" — https://help.openai.com/en/articles/9237897-searching-the-web-with-chatgpt ; "Shopping with ChatGPT Search" — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search (OpenAI Help Center)
- **Published:** ≈2026-10-20; ≈2026-10-31 · **Accessed:** 2026-10-31
- **Excerpt:** > "Reservation search is available on eligible consumer plans on web, mobile, and desktop when using GPT-5.6 Sol or GPT-5.6 Luna." / shopping article: > "Available in ChatGPT on mobile and web."
- **Establishes:** OpenAI states model gating where a search feature has it. No such statement exists for shopping.
- **Limitations:** Undocumented gating can still exist. Test by plan (CGPT-T01 condition C5).
- **Related:** CGPT-048, CGPT-049, CGPT-052
- **Origin:** lead, live browser read 2026-10-31 · **Checked:** 2026-10-31
