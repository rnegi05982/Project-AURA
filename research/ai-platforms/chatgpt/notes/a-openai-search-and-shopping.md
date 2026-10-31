# Agent A: OpenAI's own documentation on ChatGPT search and shopping

- Scope: OpenAI consumer-facing docs (help center, openai.com posts, chatgpt.com/merchants, crawler docs). Topics: search retrieval, product selection, shopping research, ads, personalization, crawlers, agent/Atlas, regions, 2026 changes.
- Research date: 2026-10-30.
- Method:
  - help.openai.com and openai.com return HTTP 403 to WebFetch. I read them in the in-app browser (Claude_Browser) and copied text with `get_page_text` / `document.body.innerText`.
  - developers.openai.com and learn.chatgpt.com: raw Markdown (`.md` twin) fetched with plain `curl`.
  - Superseded versions: Wayback Machine raw snapshots (`id_` URLs) fetched with plain `curl`. Snapshot timestamps are given per finding.
  - Help-center pages show relative dates only ("Updated: 2 days ago"). I convert them to an approximate absolute date relative to 2026-10-30 and mark them "approx.".
  - The browser pane is shared with other agents. Once, the tab showed an unrelated openai.com page; I re-navigated and re-read before quoting.
- Tiers: Tier 1 = OpenAI official docs/blog/help/spec. Tier 3 = press.

---

## 1. Search retrieval

### A-01 ChatGPT search uses third-party search providers plus partner content
- Claim: OpenAI states that ChatGPT search draws on third-party search providers and on content supplied directly by partners.
- Classification: VERIFIED FACT
- Source: Introducing ChatGPT search — OpenAI — https://openai.com/index/introducing-chatgpt-search/
- Published/updated: 2024-10-31; update notes dated 2024-12-16 and 2025-02-05. The page now carries the banner "This post introduced ChatGPT search in 2024."
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "ChatGPT search leverages third-party search providers, as well as content provided directly by our partners, to provide the information users are looking for."
- Establishes: Retrieval is not only an OpenAI-owned index. Partner content (news/data partners) is a separate input.
- Limitations: 2024 launch post. The same paragraph says the search model is "a fine-tuned version of GPT‑4o"; that model detail is outdated (see A-06 and Section 3).

### A-02 The current help article names Microsoft and Shopify as search providers (Bing named explicitly in the 2025 version)
- Claim: ChatGPT search "sometimes partners with other search providers" and rewrites the user query into targeted queries sent to them. The privacy-policy list for those providers is Microsoft and Shopify.
- Classification: VERIFIED FACT (providers listed); EVIDENCE-BASED INFERENCE that Microsoft = Bing in the current version (the 2025 version said "Bing" explicitly; the current version says only "Microsoft privacy statement").
- Source: Searching the web with ChatGPT — OpenAI Help Center — https://help.openai.com/en/articles/9237897-searching-the-web-with-chatgpt
- Published/updated: "Updated: 10 days ago" (approx. 2026-10-20)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "To provide relevant responses to your questions, ChatGPT search sometimes partners with other search providers. When it does, ChatGPT search typically rewrites your query into one or more targeted queries that it sends those providers."
- Excerpt: > "For more information about how search providers may process queries, review their privacy policies:" followed by links "Microsoft privacy statement" (https://www.microsoft.com/en-us/privacy/privacystatement) and "Shopify privacy policy" (https://www.shopify.com/legal/privacy).
- Prior version (Wayback snapshot 2025-10-14, https://web.archive.org/web/20251014133746/https://help.openai.com/en/articles/9237897): > "Bing (Microsoft’s privacy policy)" and > "Shopify (Shopify’s privacy policy)"
- Establishes: OpenAI's own docs identify Microsoft (Bing) and Shopify as external search providers. Shopify's presence is consistent with Shopify Catalog feeding product results (A-19).
- Limitations: The page does not say which queries go to which provider, or how provider results are ranked or merged.

### A-03 Query rewriting uses approximate location and, if enabled, saved memories; IP and account data are not shared
- Claim: ChatGPT may add IP-derived general location and saved memories to rewritten search queries. It does not send the IP address or account information to third-party providers.
- Classification: VERIFIED FACT
- Source: Searching the web with ChatGPT — OpenAI Help Center — https://help.openai.com/en/articles/9237897-searching-the-web-with-chatgpt
- Published/updated: approx. 2026-10-20
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "If memory is enabled, ChatGPT may use relevant saved memories when rewriting a search query. For example, if you have shared that you are vegan and live in San Francisco, ChatGPT may search for “good vegan restaurants San Francisco” when you ask for nearby restaurants you might like."
- Excerpt: > "ChatGPT does not share the IP address itself, or any of your ChatGPT account information, with third-party search providers in order to run the search."
- Establishes: Personal context enters retrieval at the query-rewrite step, before results come back.
- Limitations: The example is restaurants, not products. The page does not state that product queries are rewritten the same way (inference only).

### A-04 Site inclusion in search: OAI-SearchBot access is the stated eligibility condition; ranking uses "multiple factors"
- Claim: OpenAI gives one eligibility condition (allow OAI-SearchBot and its IPs) and says placement is not guaranteed.
- Classification: VERIFIED FACT
- Source: Searching the web with ChatGPT — OpenAI Help Center — https://help.openai.com/en/articles/9237897-searching-the-web-with-chatgpt
- Published/updated: approx. 2026-10-20
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "ChatGPT ranks search results using multiple factors intended to help users find relevant, reliable information. Placement is not guaranteed."
- Excerpt: > "To make a website eligible for inclusion, allow OAI-Searchbot to crawl the site and confirm that the website host or content delivery network allows traffic from OpenAI’s published searchbot IP addresses."
- Establishes: OAI-SearchBot crawl access is the documented gate for web-result eligibility.
- Limitations: The ranking factors are not listed.

### A-05 OpenAI describes a "first-party web search tool" and an "OpenAI-maintained index" (Codex/Work docs)
- Claim: OpenAI's ChatGPT Work/Codex docs call web search first-party and describe a cached mode that uses an OpenAI-maintained index.
- Classification: VERIFIED FACT for the Codex/Work context. EVIDENCE-BASED INFERENCE that OpenAI operates its own web index. UNVERIFIED that consumer ChatGPT search uses the same index.
- Source: Web search — ChatGPT docs (learn.chatgpt.com) — https://learn.chatgpt.com/docs/web-search.md
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "ChatGPT includes a first-party web search tool. Treat all web results as untrusted input."
- Excerpt: > "For local Codex chats, Codex enables cached search by default. Cached mode uses an OpenAI-maintained index instead of fetching arbitrary pages live, which lowers—but doesn't remove—prompt injection risk."
- Establishes: An OpenAI-maintained index exists. This is consistent with OAI-SearchBot crawling (A-07).
- Limitations: The index statement is scoped to Codex local chats. It does not say how consumer search mixes this index with third-party providers (A-01, A-02).

### A-06 The 2024 statement on the search model is outdated
- Claim: The launch post names a fine-tuned GPT-4o as the search model. GPT-4o was retired from ChatGPT on 2026-02-13.
- Classification: VERIFIED FACT (both statements); EVIDENCE-BASED INFERENCE that the 2024 model statement no longer describes current search.
- Source 1: Introducing ChatGPT search — OpenAI — https://openai.com/index/introducing-chatgpt-search/ (2024-10-31)
- Source 2: ChatGPT release notes — OpenAI Help Center — https://help.openai.com/en/articles/6825453-chatgpt-release-notes (entry dated 2026-02-13)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (1): > "The search model is a fine-tuned version of GPT‑4o, post-trained using novel synthetic data generation techniques, including distilling outputs from OpenAI o1‑preview."
- Excerpt (2): > "As previously announced, we have retired GPT-4o, GPT-4.1, GPT-4.1 mini, and OpenAI o4-mini from ChatGPT."
- Establishes: Do not cite the GPT-4o search model as current.
- Limitations: No current OpenAI page found that names the current search model.

---

## 2. Crawlers and agent identification

### A-07 OAI-SearchBot: search crawler; opt-out removes a site from search answers, but navigational links may remain
- Claim: OAI-SearchBot surfaces sites in ChatGPT search. Blocking it removes the site from search answers but not from navigational links. robots.txt changes take ~24 hours.
- Classification: VERIFIED FACT
- Source: Overview of OpenAI Crawlers — OpenAI Developers — https://developers.openai.com/api/docs/bots (Markdown twin: https://developers.openai.com/api/docs/bots.md). platform.openai.com/docs/bots returns 301 to this URL.
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "OAI-SearchBot is for search. OAI-SearchBot is used to surface websites in search results in ChatGPT's search features. Sites that are opted out of OAI-SearchBot will not be shown in ChatGPT search answers, though can still appear as navigational links. To help ensure your site appears in search results, we recommend allowing OAI-SearchBot in your site’s robots.txt file and allowing requests from our published IP ranges below."
- Excerpt: > "For search results, please note it can take ~24 hours from a site’s robots.txt update for our systems to adjust."
- Establishes: OAI-SearchBot is the documented crawler for search inclusion. Current UA example: `OAI-SearchBot/1.4`.
- Limitations: The doc does not mention shopping or product results. It does not say whether product carousels depend on OAI-SearchBot.

### A-08 GPTBot: training crawler; settings are independent of OAI-SearchBot; one crawl may serve both
- Claim: GPTBot collects training data. Disallowing it does not affect search. If both bots are allowed, OpenAI may reuse one crawl for both purposes.
- Classification: VERIFIED FACT
- Source: Overview of OpenAI Crawlers — OpenAI Developers — https://developers.openai.com/api/docs/bots.md
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Each setting is independent of the others – for example, a webmaster can allow OAI-SearchBot in order to appear in search results while disallowing GPTBot to indicate that crawled content should not be used for training OpenAI’s generative AI foundation models. If your site has allowed both bots, we may use the results from just one crawl for both use cases to avoid duplicative crawling."
- Excerpt: > "GPTBot is used to make our generative AI foundation models more useful and safe. It is used to crawl content that may be used in training our generative AI foundation models. Disallowing GPTBot indicates a site’s content should not be used in training generative AI foundation models."
- Establishes: GPTBot opt-out has no documented effect on search or shopping visibility.
- Limitations: None material.

### A-09 ChatGPT-User: user-initiated fetches; "robots.txt rules may not apply"; not used for search inclusion
- Claim: ChatGPT-User fetches pages when a user's request triggers it. OpenAI says robots.txt may not apply to it. It does not decide search inclusion.
- Classification: VERIFIED FACT
- Source: Overview of OpenAI Crawlers — OpenAI Developers — https://developers.openai.com/api/docs/bots.md
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "ChatGPT-User is not used for crawling the web in an automatic fashion. Because these actions are initiated by a user, robots.txt rules may not apply. ChatGPT-User is not used to determine whether content may appear in Search. Please use OAI-SearchBot in robots.txt for managing Search opt outs and automatic crawl."
- Establishes: Blocking ChatGPT-User in robots.txt is not a documented way to control search or shopping visibility. robots.txt compliance for ChatGPT-User is not guaranteed.
- Limitations: I could not read a 2025 version of this page to date the wording change. The platform.openai.com Wayback snapshot (2025-11-11) is a JS shell with no text.

### A-10 OAI-AdsBot (new crawler for ads landing pages)
- Claim: OAI-AdsBot visits only pages submitted as ads. It checks policy compliance and may use page content for ad relevance. Its data is not used for training.
- Classification: VERIFIED FACT
- Source: Overview of OpenAI Crawlers — OpenAI Developers — https://developers.openai.com/api/docs/bots.md
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "OAI-AdsBot is used to validate the safety of web pages submitted as ads on ChatGPT. When you submit an ad, OpenAI may visit the landing page to ensure it complies with our policies. We may also use content from the landing page to determine when it's most relevant to show the ad to users. OAI-AdsBot only visits pages submitted as ads, and the data collected by OAI-AdsBot is not used to train generative AI foundation models."
- Establishes: Ad relevance uses landing-page content. This crawler is separate from organic search crawling.
- Limitations: None material.

### A-11 IP ranges are published per bot
- Claim: OpenAI publishes JSON IP lists for each bot.
- Classification: VERIFIED FACT
- Source: Overview of OpenAI Crawlers — https://developers.openai.com/api/docs/bots.md ; plus https://openai.com/searchbot.json (fetched; HTTP 200; field `"creationTime": "2026-01-02T11:00:00.000000"`)
- Published/updated: searchbot.json creationTime 2026-01-02
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Published IP addresses: https://openai.com/searchbot.json" (also `adsbot.json`, `gptbot.json`, `chatgpt-user.json` listed for the other bots)
- Establishes: Bot traffic can be verified by IP for all four agents.
- Limitations: I fetched only searchbot.json.

### A-12 Cloud browser (agent) traffic is signed with Web Bot Auth (RFC 9421), not a robots.txt user agent
- Claim: ChatGPT Work's cloud browser signs requests with HTTP Message Signatures. CDNs list it as "ChatGPT Agent".
- Classification: VERIFIED FACT
- Source: ChatGPT Work's Cloud browser allowlisting — OpenAI Help Center — https://help.openai.com/en/articles/11845367-chatgpt-works-cloud-browser-allowlisting (old slug `11845367-chatgpt-agent-allowlisting` redirects here)
- Published/updated: "Updated: 11 days ago" (approx. 2026-10-19)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "ChatGPT Work's Cloud browser uses Web Bot Auth to sign outbound HTTP requests, allowing website operators to verify that requests genuinely originate from ChatGPT."
- Excerpt: > A Signature-Agent header set to "https://chatgpt.com".
- Establishes: Agent browsing is identified by signature, separately from the four robots.txt agents.
- Limitations: The page also says "at launch, Cloud browser cannot sign in to websites or complete payments." This conflicts with A-36 (see Section 3).

---

## 3. Product results in ChatGPT (shopping)

### A-13 Product results are "not ads, nor influenced by any OpenAI partnerships"
- Claim: OpenAI states that organic product results are selected independently and are separate from ads.
- Classification: VERIFIED FACT (OpenAI's stated policy; the mechanism is not independently verifiable)
- Source: Shopping with ChatGPT Search — OpenAI Help Center — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search (old slug `...-improved-shopping-results-from-chatgpt-search` redirects here)
- Published/updated: "Updated: 2 days ago" (approx. 2026-10-28)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Product results are selected independently by ChatGPT and are not ads, nor influenced by any OpenAI partnerships. Ads are separate from product results, and you can learn more about ads in ChatGPT."
- Establishes: The stated policy is that payment, partnerships and ads do not rank organic product results.
- Limitations: This is a policy statement. No audit or mechanism is published.

### A-14 Product selection = perceived relevance to intent, using query + context (Memory, Custom instructions)
- Claim: A product appears when ChatGPT judges it relevant to user intent. Factors include availability, price, reviews, and stated preferences. Their weight depends on the query.
- Classification: VERIFIED FACT
- Source: Shopping with ChatGPT Search — OpenAI Help Center — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- Published/updated: approx. 2026-10-28
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "A product appears in the carousel when ChatGPT perceives it to be relevant to your intent. It considers your query and context (such as Memory or Custom instructions)."
- Excerpt: > "For example, if you ask for goofy dog costumes, ChatGPT may consider available options, price, reviews, and ease of use, as well as any other context you provide. If you’ve said you dislike clowns, it may leave out clown costumes."
- Excerpt: > "Depending on your needs, some of these factors will be more relevant than others. For example, if you specify a budget of $30, ChatGPT will focus more on price, whereas if price isn’t mentioned, it may focus on other aspects instead."
- Establishes: Selection is model-judged and query-dependent. There is no fixed weighting.
- Limitations: No numeric weights, thresholds, or candidate-set size are disclosed.

### A-15 Three named inputs to product selection
- Claim: OpenAI lists three inputs: structured metadata from first- and third-party providers plus other third-party content; the model's own pre-search response; safety standards and product policies.
- Classification: VERIFIED FACT
- Source: Shopping with ChatGPT Search — OpenAI Help Center — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- Published/updated: approx. 2026-10-28 (same three bullets present in Wayback snapshots 2025-10-28 and 2026-05-28)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Structured metadata from first-party and third-party providers (e.g., price, product description) and other third-party content."
- Excerpt: > "Model responses generated by ChatGPT before it considers any new search results."
- Excerpt: > "OpenAI safety standards and product policies."
- Establishes: The model's prior (pre-search) answer is an explicit input to product selection, alongside feed and third-party metadata.
- Limitations: "First-party" is not defined. Inference: it means merchant-supplied feeds (consistent with A-18 and A-19).

### A-16 Titles, feature labels and review summaries are model-generated; reviews are not verified
- Claim: ChatGPT may rewrite product titles and descriptions, generate labels such as "Budget-friendly", and summarize public reviews.
- Classification: VERIFIED FACT
- Source: Shopping with ChatGPT Search — OpenAI Help Center — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- Published/updated: approx. 2026-10-28
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "ChatGPT may generate simplified product titles and descriptions based on information it receives from third-party providers to make results easier to read, since merchants often use varying titles and descriptions for the same product."
- Excerpt: > "These model-generated summaries are based on reviews from public websites and are intended to highlight common user likes and dislikes about a product. Reviews and ratings are not verified by OpenAI."
- Establishes: Displayed product text is not a verbatim copy of merchant data. Review signals come from public websites.
- Limitations: The page does not name which review sources are used.

### A-17 Prices come from third-party providers; the initial price is the first-listed merchant's, not necessarily the lowest
- Claim: The headline price is the first merchant's price. A "Best price" label marks the lowest price ChatGPT knows. Updates can lag.
- Classification: VERIFIED FACT
- Source: Shopping with ChatGPT Search — OpenAI Help Center — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- Published/updated: approx. 2026-10-28
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Prices shown in ChatGPT’s initial response typically reflect the price from the first merchant listed, which may not be the lowest available price. ChatGPT works to highlight the lowest priced option it is aware of in the product detail page and merchant rankings. When more than one merchant offers the product, that option may have a “Best price” label."
- Excerpt: > "When merchants update their pricing or shipping terms, there may be some delay before it is reflected in the information you see."
- Establishes: Merchant rank 1 decides the headline price. Price freshness depends on the data pipeline.
- Limitations: The lag duration is not stated.

### A-18 Merchant list ordering: availability, price, quality, maker/primary seller. The Instant Checkout factor was removed in 2026.
- Claim: For one product, merchants are ranked by availability, price, quality, and whether the merchant is the maker or primary seller. The October 2025 version also listed "whether Instant Checkout is enabled". That factor is absent by 2026-05-28.
- Classification: VERIFIED FACT (both versions quoted); EVIDENCE-BASED INFERENCE that Instant Checkout no longer affects merchant order.
- Source: Shopping with ChatGPT Search — OpenAI Help Center — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- Published/updated: current approx. 2026-10-28. Prior versions: Wayback 2025-10-28 (https://web.archive.org/web/20251028124133/https://help.openai.com/en/articles/11128490-improved-shopping-results-from-chatgpt-search) and 2026-05-28.
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (current): > "This list is generated by ChatGPT based on merchant and product metadata from third-party providers or directly from the merchants themselves. Merchants are ranked based on factors like availability, price, quality, and whether they are the maker or primary seller of that item. We expect this to evolve as we continue to improve the shopping experience, such as by personalizing merchant rankings even more to user preferences."
- Excerpt (2025-10-28 snapshot): > "Merchants are ranked based on factors like availability, price, quality, whether they are the maker or primary seller of that item, and whether Instant Checkout is enabled."
- Establishes: The current merchant-ranking factors are documented. Payment integration was a ranking factor in 2025 and is no longer listed.
- Limitations: "Quality" is not defined. "personalizing merchant rankings even more" implies some personalization already applies, but the extent is not stated.

### A-19 Product data pipelines: Shopify Catalog, direct feeds, ACP (discovery), third-party delivery (Salesforce, Stripe)
- Claim: Shopify merchants are integrated through Shopify Catalog with no merchant work. Other merchants can send direct feeds. In March 2026, ACP was extended to product discovery (feeds and promotions), with Salesforce and Stripe as delivery paths. Named retailers are integrated.
- Classification: VERIFIED FACT
- Source 1: Powering Product Discovery in ChatGPT — OpenAI — https://openai.com/index/powering-product-discovery-in-chatgpt/
- Source 2: Shopping with ChatGPT Search — OpenAI Help Center — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- Published/updated: Source 1 2026-03-24; Source 2 approx. 2026-10-28
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (1): > "Through ACP, merchants share product feeds and promotions so their catalogs are fully represented in ChatGPT. We support multiple delivery paths, including through third-party providers like Salesforce and Stripe, so merchants can participate with the systems they already use. Over time, ACP will serve as a foundation for broader AI-native commerce experiences, including personalization, local availability, and ETAs."
- Excerpt (1): > "Already, leading retailers including Target, Sephora, Nordstrom, Lowe’s, Best Buy, The Home Depot, and Wayfair have integrated into ACP for discovery."
- Excerpt (2): > "For merchants on Shopify, product data is already integrated into ChatGPT through Shopify Catalog, helping products appear more accurately and completely in relevant user conversations. No additional work is required from individual merchants."
- Establishes: The main structured inputs to A-15 are merchant feeds via ACP, Shopify Catalog, and third-party feed providers.
- Limitations: OpenAI does not say how feed data and crawled data are reconciled when they conflict.

### A-20 Merchant page: feeds give "control" and "better placement"; crawling is an alternative; Etsy and Shopify are pre-integrated
- Claim: OpenAI's merchant page says a feed is optional because ChatGPT also crawls sites. It says richer feed data helps products surface. Matching uses shopper preferences and past interactions.
- Classification: VERIFIED FACT
- Source: Power product discovery in ChatGPT — OpenAI (chatgpt.com) — https://chatgpt.com/merchants/
- Published/updated: not stated (footer "OpenAI © 2015–2026"; text refers to "later this year")
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Do I need a product feed if ChatGPT already crawls my site?" / > "No, but feeds give you greater control over how your products appear, helping ensure more accurate and up-to-date information."
- Excerpt: > "Get better placement in results" / > "Richer data helps your products surface with more accurate information when shoppers compare options."
- Excerpt: > "ChatGPT helps match your products to people based on shopper preferences and past interactions."
- Excerpt: > "If you sell through Shopify or Etsy, your catalog is already integrated, and no additional setup or application is required."
- Establishes: Both crawling and feeds are product inputs. Data completeness affects placement, per OpenAI.
- Limitations: Marketing page. "Better placement" is not quantified. The page is undated.

### A-21 Developer docs: recommended feed attributes "improve ranking"
- Claim: OpenAI's commerce docs say recommended attributes (rich media, reviews, performance signals) improve ranking and relevance.
- Classification: VERIFIED FACT
- Source: Key concepts — OpenAI Developers (Agentic Commerce) — https://developers.openai.com/commerce/guides/key-concepts.md
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Required fields ensure correct display of price and availability, while recommended attributes—like rich media, reviews, and performance signals—improve ranking, relevance, and user trust."
- Establishes: Feed attribute completeness is a documented ranking input.
- Limitations: The page opens with "Supporting Instant Checkout in ChatGPT requires a merchant to implement three flows." That framing is outdated (A-24). "Performance signals" is not defined here. Detailed ACP feed coverage belongs to another agent's scope.

### A-22 Product feeds uploaded through Ads Manager serve ads only, not organic results (beta)
- Claim: Ads Manager product feeds make products eligible for ads only. They do not enter organic ChatGPT results during the beta.
- Classification: VERIFIED FACT
- Source: Create Campaigns from Product Feeds — OpenAI Help Center — https://help.openai.com/en/articles/20001268-create-campaigns-from-product-feeds
- Published/updated: "Updated: 3 days ago" (approx. 2026-10-27)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Products from your feed will only be eligible for use in ads during this beta. They will not appear in organic ChatGPT conversations, though we may offer that capability in the future"
- Excerpt: > "Product ads use formats designed specifically for showcasing items from your catalog, featuring details such as product images, titles, stars, prices, sales prices, and your brand"
- Establishes: Ads feeds and organic discovery feeds are separate pipelines, per OpenAI.
- Limitations: "During this beta" means the separation may change.

---

## 4. Instant Checkout (2025) and its 2026 retreat

### A-23 Sept 2025 launch: Instant Checkout "not preferred in product results" but was a merchant-ranking factor
- Claim: At launch, OpenAI said product results are organic and ranked on relevance. Instant Checkout items are not preferred, but Instant Checkout status was a factor when ranking merchants for the same product. Merchants paid a fee.
- Classification: VERIFIED FACT (as of 2025-09-29); superseded in part (A-18, A-24)
- Source: Buy it in ChatGPT: Instant Checkout and the Agentic Commerce Protocol — OpenAI — https://openai.com/index/buy-it-in-chatgpt/
- Published/updated: 2025-09-29 (no update note on the page as of 2026-10-30)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Product results are organic and unsponsored, ranked purely on relevance to the user."
- Excerpt: > "Merchants pay a small fee on completed purchases, but the service is free for users, doesn’t affect their prices, and doesn’t influence ChatGPT’s product results. Instant Checkout items are not preferred in product results. When ranking multiple merchants that sell the same product, ChatGPT considers factors like availability, price, quality, whether a merchant is the primary seller, and whether Instant Checkout is enabled, to optimize the user experience."
- Establishes: OpenAI separated product ranking (no checkout preference) from merchant ranking (checkout considered).
- Limitations: The page is not annotated with the 2026 change. It reads as current but is not.

### A-24 2026: OpenAI is "moving away from a standalone Instant Checkout"; purchases complete on merchant sites
- Claim: In March 2026 OpenAI let merchants use their own checkout and refocused on discovery. The merchant page now says purchases complete on merchant-owned sites or apps. The Instant Checkout help article returns 404.
- Classification: VERIFIED FACT (statements and 404). EVIDENCE-BASED INFERENCE that the help article was removed between 2026-02-10 and 2026-04-07, from Wayback: 200 on 2026-02-10, 404 on 2026-04-07.
- Source 1: Powering Product Discovery in ChatGPT — OpenAI — https://openai.com/index/powering-product-discovery-in-chatgpt/ (2026-03-24)
- Source 2: Power product discovery in ChatGPT — OpenAI — https://chatgpt.com/merchants/ (undated)
- Source 3: https://help.openai.com/en/articles/12440090-instant-checkout — live page shows "UH OH. THAT PAGE DOESN'T EXIST." Wayback snapshot 2026-02-10 of `12440090-instant-checkout-buy-directly-from-merchants-through-chatgpt` was readable.
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (1): > "We’ve found that the initial version of Instant Checkout did not offer the level of flexibility that we aspire to provide, so we’re allowing merchants to use their own checkout experiences while we focus our efforts on product discovery."
- Excerpt (2): > "We’re moving away from a standalone Instant Checkout experience in ChatGPT and prioritizing better shopping discovery and merchant-owned checkout experiences. Users can discover and evaluate products in ChatGPT, but purchases are completed on merchant-owned websites or apps."
- Excerpt (2): > "There are no fees on purchases that start in ChatGPT."
- Excerpt (3, Wayback 2026-02-10): > "Merchant rankings, within the same product, consider inventory, price, seller type, and Instant Checkout availability."
- Establishes: The current state is discovery in ChatGPT and checkout on the merchant's site. Deeper integration goes through ChatGPT apps (Walmart example in Source 1). The fee-based checkout model is gone, per the merchant page.
- Limitations: OpenAI does not give an end date for Instant Checkout. Source 1 says "allowing merchants to use their own checkout"; it does not say Instant Checkout was switched off.

---

## 5. Shopping research

### A-25 Launch, model, and plans
- Claim: Shopping research launched 2025-11-24 for logged-in Free, Go, Plus and Pro users on mobile and web. It runs on a GPT-5 mini variant trained with reinforcement learning for shopping.
- Classification: VERIFIED FACT
- Source: Introducing shopping research in ChatGPT — OpenAI — https://openai.com/index/chatgpt-shopping-research/
- Published/updated: 2025-11-24
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Shopping research is powered by a version of GPT‑5 mini trained with reinforcement learning specifically for shopping tasks. We trained it to read trusted sites, cite reliable sources, and synthesize information across many sources to produce high-quality product research."
- Excerpt: > "*Shopping research is a mini model post-trained on GPT‑5‑Thinking‑mini."
- Excerpt: > "Shopping research is starting to roll out today on mobile and web for logged-in ChatGPT users on Free, Go, Plus, and Pro plans."
- Establishes: A separate, shopping-specific model, distinct from the default chat model.
- Limitations: GPT-5-era models were later retired from ChatGPT (release notes, 2026-02-13). The page does not say whether shopping research was re-based. See A-28 for its current status.

### A-26 Sources and priorities: organic, public retail sites, read product pages directly, avoid low-quality/spammy sites
- Claim: Shopping research reads retailer product pages directly, cites sources, avoids low-quality and spammy sites, and says results are organic. Merchants "ensure" eligibility through an allowlisting process.
- Classification: VERIFIED FACT
- Source: Introducing shopping research in ChatGPT — OpenAI — https://openai.com/index/chatgpt-shopping-research/
- Published/updated: 2025-11-24
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Your chats are never shared with retailers. Results are organic and based on publicly available retail sites—reading product pages directly, citing sources, and avoiding low-quality or spammy sites. Merchants who want to ensure they are available to appear in shopping research results can follow the allowlisting process here."
- Excerpt: > "In the background it looks across the internet for up-to-date information like price, availability, reviews, specs, and images, and brings options back to you as it goes."
- Establishes: Merchant inclusion depends on the agent being able to fetch pages. The "allowlisting process" is bot-management allowlisting, not a paid listing.
- Limitations: The "here" link now resolves to "ChatGPT Work's Cloud browser allowlisting" (A-12). The link target changed after launch.

### A-27 Superseded help article (Aug 2026 snapshot): ACP merchant data was an input; sites that block automation were skipped
- Claim: Before its removal, the help article listed ACP merchant data, public product information, and other retail sources. It said blocked retailers are skipped.
- Classification: VERIFIED FACT (as of the snapshot); status now superseded (A-28)
- Source: Using shopping research in ChatGPT — OpenAI Help Center — Wayback snapshot 2026-08-05: https://web.archive.org/web/20260805232131/https://help.openai.com/en/articles/12911370-using-shopping-research-in-chatgpt
- Published/updated: snapshot shows "Updated: 6 days ago" (approx. 2026-07-30)
- Accessed: 2026-10-30
- Tier: 1 (archived)
- Excerpt: > "merchant product data provided through the Agentic Commerce Protocol (ACP)" / > "publicly available product information" / > "other relevant retail sources"
- Excerpt: > "In addition, some retailers block automated access to their sites.When this happens, shopping research will either skip those sources or rely on other sites with similar products."
- Excerpt: > "Shopping research may use ChatGPT memory to better tailor recommendations, but you can turn memory off or clear it at any time your personalization settings."
- Establishes: Blocking automated access led to exclusion or substitution in shopping research.
- Limitations: Archived copy. It may not reflect current behavior.

### A-28 The shopping research help article now redirects to the general shopping article
- Claim: Both the article ID and its full slug redirect to "Shopping with ChatGPT Search", which does not mention shopping research. A help-center search for "shopping" does not list it.
- Classification: VERIFIED FACT (the redirect). UNVERIFIED HYPOTHESIS that the feature itself was retired or merged into standard shopping.
- Source: https://help.openai.com/en/articles/12911370-using-shopping-research-in-chatgpt → https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search (observed 2026-10-30)
- Published/updated: redirect observed 2026-10-30. Wayback still shows the article live on 2026-08-05.
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: [no text: redirect observed in browser; `location.href` = https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search]
- Establishes: OpenAI no longer maintains a separate help page for shopping research.
- Limitations: The release notes contain no retirement entry for shopping research. Pulse, a shopping-research surface, was sunset 2026-06-17 (release notes).

---

## 6. Ads in ChatGPT

### A-29 OpenAI policy: ads do not influence answers; ads run on separate systems; advertisers cannot rank responses
- Claim: OpenAI says ads do not influence answers, run on systems separate from the chat model, and are labeled.
- Classification: VERIFIED FACT (stated policy)
- Source 1: Ads in ChatGPT — OpenAI Help Center — https://help.openai.com/en/articles/20001047-ads-in-chatgpt
- Source 2: Our approach to advertising and expanding access to ChatGPT — OpenAI (author Fidji Simo) — https://openai.com/index/our-approach-to-advertising-and-expanding-access/
- Published/updated: Source 1 "Updated: 2 days ago" (approx. 2026-10-28); Source 2 2026-01-16
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (1): > "No. Ads do not influence ChatGPT’s answers. Ads run on separate systems from our chat model, and advertisers have no ability to shape, rank, or alter ChatGPT’s responses. Ads are separate and clearly labeled."
- Excerpt (2): > "Answer independence: Ads do not influence the answers ChatGPT gives you. Answers are optimized based on what’s most helpful to you. Ads are always separate and clearly labeled."
- Establishes: The stated design separates ads from answers, and (with A-13) from organic product results.
- Limitations: Policy statement only. No technical audit is published.

### A-30 Placement and labeling: one ad unit below a response; multi-image ads during image generation (test)
- Claim: Ads appear below a response, labeled as sponsored. A multi-image format is being tested during image generation.
- Classification: VERIFIED FACT
- Source: Ads in ChatGPT — OpenAI Help Center — https://help.openai.com/en/articles/20001047-ads-in-chatgpt ; ChatGPT release notes 2026-02-09 — https://help.openai.com/en/articles/6825453-chatgpt-release-notes
- Published/updated: approx. 2026-10-28; 2026-02-09
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "You will see one ad unit that may contain one or multiple images below a ChatGPT response. We are also testing a multi-image visual ad format that will appear during image generation in ChatGPT."
- Excerpt (release notes 2026-02-09): > "When you see an ad, they are always clearly labeled as sponsored and visually separated from the organic answer."
- Establishes: Ads do not appear inside product carousels, per the documented placements.
- Limitations: Product-feed ads (A-22) show product images, stars and prices. They look similar to organic product cards but are placed in the ad unit.

### A-31 Ad selection and ranking: relevance plus advertiser bids; conversation context; optional personalization
- Claim: The ad system uses conversation context, the ad's landing page and copy, advertiser context hints and targeting, and (if enabled) wider ChatGPT signals. Ranking combines relevance and bids.
- Classification: VERIFIED FACT
- Source: Ads in ChatGPT — OpenAI Help Center — https://help.openai.com/en/articles/20001047-ads-in-chatgpt
- Published/updated: approx. 2026-10-28
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "If there are multiple eligible ads, we consider a combination of factors, including relevance and advertiser bids when deciding which ad to show first."
- Excerpt: > "If you have Personalized Ads enabled, starting in February 2026 this can also include:" / > "Past chats and memory"
- Establishes: Ads are an auction-plus-relevance system that is separate from organic ranking.
- Limitations: Weights are not disclosed.

### A-32 Plans and exclusions
- Claim: Ads appear only on Free and Go. They are not shown on Plus, Pro, Business, Enterprise or Edu, to users identified as under 18, near sensitive topics, or in Temporary Chats. Free users can switch to an ads-free mode with lower limits.
- Classification: VERIFIED FACT
- Source: Ads in ChatGPT — OpenAI Help Center — https://help.openai.com/en/articles/20001047-ads-in-chatgpt
- Published/updated: approx. 2026-10-28
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Ads may appear for users on the Free and Go plans. Plus, Pro, Business, Enterprise, and Edu accounts will not have ads. We do not show ads to accounts identified as belonging to people under 18."
- Excerpt: > "No. Ads are not eligible to appear near sensitive topics, including personal health, mental health, or politics."
- Excerpt: > "Temporary Chats will not show ads."
- Establishes: Ad exposure depends on plan.
- Limitations: The 2026-10-21 blog lists only "Plus, Pro, and Enterprise" as ad-free (Section 3).

### A-33 Regional rollout of ads (2026) and the India status
- Claim: Ads testing began in the U.S. on 2026-02-09. Canada, Australia and New Zealand followed (release notes 2026-04-16), then the UK, Mexico, Brazil, Japan and South Korea, Europe, Southeast Asia and Taiwan, and 26 more countries, for 89 total by 2026-10-21. Advertiser self-service opened in India on 2026-08-31. No OpenAI page I fetched says that users in India see ads.
- Classification: VERIFIED FACT (dates and statements). EVIDENCE-BASED INFERENCE: the "89 countries" figure and the Ads Manager list are advertiser-side availability. User-side ad display in India is not stated.
- Sources:
  - Testing ads in ChatGPT — OpenAI — https://openai.com/index/testing-ads-in-chatgpt/ (originally 2026-02-09; updates 2026-03-26, 2026-05-07, 2026-08-11)
  - ChatGPT Ads expands to 26 new countries… — OpenAI — https://openai.com/index/chatgpt-ads-expands-26-new-countries/ (2026-10-21)
  - A milestone in expanding access to AI — OpenAI — https://openai.com/index/expanding-access-to-ai-with-chatgpt-ads/ (2026-08-31)
  - Ads Manager Availability — OpenAI Help Center — https://help.openai.com/en/articles/20001245-ads-manager-availability ("Updated: 3 days ago", approx. 2026-10-27); India listed "Available"
  - ChatGPT release notes — https://help.openai.com/en/articles/6825453-chatgpt-release-notes
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Today, we’re expanding ChatGPT Ads to 26 additional countries, extending availability to 89 countries worldwide."
- Excerpt: > "Starting later today, advertisers can purchase ChatGPT ads directly via Ads Manager across India, Europe, the Middle East, and North Africa."
- Excerpt (help): > "For current advertiser availability by country, see Ads Manager Availability. Availability may continue to evolve as testing expands."
- Excerpt (release notes 2026-04-16): > "We're beginning to roll out ads for users on Free and Go plans in Australia, New Zealand, and Canada."
- Establishes: Ads moved from a U.S. test to a multi-country program in 2026. India is an advertiser self-service market.
- Limitations: UK dates conflict (release notes 2026-06-04 vs blog 2026-08-11; Section 3). No user-side country list was found.

### A-34 Other ad formats: Sponsored Agents (alpha) and "Ask ChatGPT" about an ad
- Claim: Sponsored Agents let users chat with an AI representative of a business, opened from an ad. Selected advertisers only. By default ChatGPT cannot see the ad; a user can share it, and OpenAI says advertisers do not influence the answers about it.
- Classification: VERIFIED FACT
- Source: Sponsored Agents in ChatGPT Ads — OpenAI Help Center — https://help.openai.com/en/articles/20001524-sponsored-agents-in-chatgpt-ads (approx. 2026-10-27); Ads in ChatGPT — https://help.openai.com/en/articles/20001047-ads-in-chatgpt
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Sponsored Agents are an advertising format that lets people chat with an AI representative of a business in ChatGPT. People can open a conversation from an ad to ask questions about the business’s products or services."
- Excerpt: > "Advertisers do not influence ChatGPT’s responses about ads that are shared in the chat."
- Establishes: Conversational ad formats exist next to organic shopping.
- Limitations: Limited alpha. No placement details.

---

## 7. Personalization

### A-35 Memory, custom instructions, past chats and location shape product results
- Claim: Product selection uses Memory and Custom instructions. Shopping research used memory. Merchant rankings are expected to be personalized "even more". The merchant page cites "past interactions". GPT-5.5 Instant uses location context for shopping queries.
- Classification: VERIFIED FACT
- Sources:
  - Shopping with ChatGPT Search — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search (approx. 2026-10-28)
  - Introducing shopping research in ChatGPT — https://openai.com/index/chatgpt-shopping-research/ (2025-11-24)
  - Power product discovery in ChatGPT — https://chatgpt.com/merchants/ (undated)
  - ChatGPT release notes, entry 2026-06-24 — https://help.openai.com/en/articles/6825453-chatgpt-release-notes
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "It considers your query and context (such as Memory or Custom instructions)."
- Excerpt: > "If you have memory turned on, the research can be tailored even further. For example, if ChatGPT knows that you’re into gaming, it can factor that in when helping you find a new laptop."
- Excerpt (2026-06-24): > "Shopping and local business queries should also feel more useful. The model makes better use of location context to surface relevant nearby options and can bring together product recommendations, business information, and images more coherently when those elements are helpful."
- Establishes: The same query can return different products for different users.
- Limitations: OpenAI does not quantify the personalization effect. Ads personalization is a separate control (A-31).

---

## 8. Agent mode, cloud browser, Atlas

### A-36 "ChatGPT agent is no longer available"; ChatGPT Work's cloud browser replaces it
- Claim: Agent mode is discontinued. Browser tasks now run in ChatGPT Work's cloud browser (paid plans except Free and Go). It asks for confirmation before payments. Sites can block it.
- Classification: VERIFIED FACT
- Source 1: ChatGPT agent — OpenAI Help Center — https://help.openai.com/en/articles/11752874-chatgpt-agent ("Updated: 3 days ago", approx. 2026-10-27)
- Source 2: Using cloud browser in ChatGPT — OpenAI Help Center — https://help.openai.com/en/articles/20001280-using-cloud-browser-in-chatgpt (approx. 2026-10-28)
- Source 3: ChatGPT release notes (2026-07-09 "Introducing ChatGPT Work"; 2026-08-25 signed-in websites)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (1): > "ChatGPT agent is no longer available. Use ChatGPT Work for longer, multi-step tasks and finished deliverables. For supported browser workflows, see Using cloud browser in ChatGPT."
- Excerpt (2): > "Cloud browser is available in ChatGPT Work on paid ChatGPT plans in supported regions, excluding Free and Go."
- Excerpt (2): > "Find flights that match your plans, or compare product availability and local stock."
- Excerpt (2): > "ChatGPT is designed to request confirmation before actions that could be hard to reverse or create a financial, legal, account, or other real-world commitment, such as confirming a booking or making a payment."
- Excerpt (2): > "These restrictions are set by the website, not by ChatGPT."
- Establishes: Agentic shopping now happens in the cloud browser of ChatGPT Work, not in agent mode.
- Limitations: No OpenAI doc says how the cloud browser finds or ranks products (gap). Source 1 still contains legacy text ("Agent mode is currently available on Pro, Plus, Business, Enterprise, and Edu plans…").

### A-37 Atlas browser retired (stop date 2026-08-09)
- Claim: OpenAI deprecated Atlas on 2026-07-09 and scheduled it to stop working on 2026-08-09. The help center says it "has been retired".
- Classification: VERIFIED FACT
- Source 1: ChatGPT release notes, entry 2026-07-09 — https://help.openai.com/en/articles/6825453-chatgpt-release-notes
- Source 2: ChatGPT Atlas retirement — OpenAI Help Center — https://help.openai.com/en/articles/20001371-chatgpt-atlas-retirement ("Updated: 7 days ago", approx. 2026-10-23)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (1): > "We’re deprecating Atlas as we bring browser-based agentic capabilities into ChatGPT and Codex. Atlas is scheduled to stop working on August 9, 2026."
- Excerpt (2): > "ChatGPT Atlas has been retired and no longer receives updates."
- Establishes: Atlas is not a current shopping surface. Its successor is the ChatGPT desktop app's built-in browser.
- Limitations: None.

### A-38 Site tools (WebMCP) let websites expose actions to the agent in the desktop built-in browser
- Claim: ChatGPT implements the proposed WebMCP standard ("site tools"). Websites can offer predefined actions to ChatGPT Work and Codex in the desktop app's built-in browser.
- Classification: VERIFIED FACT
- Source: Site tools — ChatGPT docs — https://learn.chatgpt.com/docs/webmcp.md ; release notes 2026-08-31
- Published/updated: not stated; release note 2026-08-31
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Site tools are ChatGPT's implementation of the proposed [WebMCP standard](https://webmachinelearning.github.io/webmcp/). With WebMCP, a website can offer useful actions directly to an agent alongside the interface people already use."
- Establishes: This is a documented, non-crawl channel through which a site can expose functions to ChatGPT's agent.
- Limitations: Shopping is not documented as a use case. Desktop app only.

---

## 9. Regions and accuracy

### A-39 Shopping is "currently live" in the U.S. per the merchant page; consumer docs give no region limit
- Claim: The merchant page says shopping is live for U.S. users. The consumer help article says only "mobile and web". The March 2026 rollout says "all ChatGPT free, Go, Plus, and Pro users" with no region named.
- Classification: VERIFIED FACT (each statement). The scope of "shopping" in the merchant page is ambiguous; see Section 3.
- Sources: https://chatgpt.com/merchants/ ; https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search ; https://openai.com/index/powering-product-discovery-in-chatgpt/
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Shopping is currently live for ChatGPT users in the U.S. We’re building a merchant platform for self-serve data integration later this year, and plan to expand to more merchants and regions over time."
- Excerpt: > "Shopping is currently live in the U.S. and will expand to additional regions over time."
- Excerpt: > "Available in ChatGPT on mobile and web."
- Establishes: OpenAI's only explicit region statement for shopping is U.S.-only. India is not named.
- Limitations: Undated page. "Shopping" may mean the merchant-feed program rather than all product carousels (inference).

### A-40 India: OpenAI primary sources found cover ads and plans, not consumer shopping; press reports a UPI pilot
- Claim: No OpenAI page I fetched documents ChatGPT shopping availability in India. India appears only for advertiser self-service (A-33) and ChatGPT Go. Press (Tier 3) reported an NPCI/Razorpay pilot with OpenAI in October 2025.
- Classification: VERIFIED FACT (absence in the fetched sources; Tier 3 report content). UNVERIFIED HYPOTHESIS for any India shopping availability.
- Source: India pilots AI chatbot-led e-commerce… — TechCrunch (Jagmeet Singh) — https://techcrunch.com/2025/10/09/india-pilots-ai-chatbot-led-e-commerce-with-chatgpt-gemini-claude-in-the-mix/
- Published/updated: 2025-10-09
- Accessed: 2026-10-30
- Tier: 3
- Excerpt: > "partnered with OpenAI and fintech firm Razorpay to enable consumers to shop and pay directly through ChatGPT."
- Excerpt: > "Tata Group-owned online grocer BigBasket and telecom operator Vi are the initial merchant partners for the new pilot"
- Establishes: Only that a pilot was reported. No OpenAI confirmation was found.
- Limitations: WebFetch summarizer output. Text is quoted as returned but not checked against raw HTML. Tier 3.

### A-41 Accuracy disclaimers on price, availability and search results
- Claim: OpenAI tells users to confirm final price, taxes, shipping, availability and return policy with the merchant. It says search results can be incomplete or outdated.
- Classification: VERIFIED FACT
- Sources: https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search ; https://help.openai.com/en/articles/9237897-searching-the-web-with-chatgpt ; https://openai.com/index/chatgpt-shopping-research/
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Search results and citations can be incomplete, outdated, or incorrect."
- Excerpt: > "Shopping research might make mistakes about product details like price and availability, and we encourage you to visit the merchant site for the most accurate details."
- Excerpt: > "Keep in mind that not all available products will necessarily be shown (there are a lot of dog costumes out there)."
- Establishes: OpenAI does not guarantee the accuracy or completeness of product listings.
- Limitations: None.

---

## 10. 2026 changes to shopping (timeline)

### A-42 Dated 2026 shopping changes from release notes and posts
- Claim: The dated OpenAI record of 2026 shopping changes is below.
- Classification: VERIFIED FACT (each line is quoted or directly stated by the cited source)
- Source: ChatGPT release notes — OpenAI Help Center — https://help.openai.com/en/articles/6825453-chatgpt-release-notes ("Updated: 16 hours ago"); plus the posts cited
- Accessed: 2026-10-30
- Tier: 1
- Timeline:
  - 2026-01-26: > "We’ve improved search responses in ChatGPT Voice to deliver more complete, up-to-date answers, including better access to shopping results."
  - 2026-02-09: ads test starts in the U.S. (A-33).
  - 2026-03-24: > "These updates improve how ChatGPT retrieves and presents product information from merchants and other providers using the Agentic Commerce Protocol (ACP)." Same day: Instant Checkout de-emphasized; Walmart app (A-24).
  - Between 2026-02-10 and 2026-04-07: Instant Checkout help article removed (Wayback; A-24).
  - Between 2025-10-28 and 2026-05-28: "Instant Checkout is enabled" dropped from merchant-ranking factors (A-18).
  - 2026-06-17: Pulse sunset (shopping research was offered in Pulse): > "Pulse is being sunset as proactive updates move into scheduled tasks."
  - 2026-06-24: GPT-5.5 Instant update for shopping and local queries (A-35).
  - 2026-07-09: ChatGPT Work introduced; Atlas deprecation (A-36, A-37).
  - After 2026-08-05: shopping research help article redirected (A-28).
  - 2026-10-01: > "Virtually try on clothing and accessories: A “Try on” button will appear on product listings for clothes and accessories in ChatGPT." and > "Save your finds: Save any product to Favorites or create a folder to organize your finds in your ChatGPT Library."
  - 2026-10-21: ads in 89 countries (A-33). 2026-10-26: multi-image ad format open beta in Ads Manager (help article 20001212).
- Establishes: 2026 moved shopping from "buy in chat" to "discover in chat, buy on merchant site". It added ads, visual features and ACP-based discovery feeds. It retired agent mode and Atlas.
- Limitations: The exact dates for agent-mode removal and the shopping research redirect are not documented.

---

## Contradictions and superseded information

1. **Instant Checkout as a merchant-ranking factor.** The buy-it-in-chatgpt post (2025-09-29) and the 2025 help versions list "whether Instant Checkout is enabled". The current help article omits it (A-18). The 2025 post carries no update note, so it reads as current but is outdated.
2. **Instant Checkout status.** The merchant FAQ says "moving away from a standalone Instant Checkout". The commerce "Key concepts" doc still opens "Supporting Instant Checkout in ChatGPT requires…" (A-21). The developer doc looks outdated relative to the merchant page.
3. **Shopping region.** chatgpt.com/merchants: "Shopping is currently live … in the U.S." The help article ("Available in ChatGPT on mobile and web") and the 2026-03-24 post ("all ChatGPT free, Go, Plus, and Pro users") name no region. Unresolved.
4. **UK ads date.** Release notes place "Rolling out ads in the UK" under 2026-06-04. testing-ads-in-chatgpt says the UK pilot was planned on 2026-05-07 and "launched" on 2026-08-11. Possibly user rollout vs advertiser launch; unverified.
5. **Ad-free plans list.** The help center lists Plus, Pro, Business, Enterprise and Edu as ad-free. The 2026-10-21 post says "Plus, Pro, and Enterprise subscriptions will remain ad-free" (omits Business and Edu). Likely an omission, not a policy change (inference).
6. **ChatGPT agent page.** It opens with "ChatGPT agent is no longer available" but keeps "Agent mode is currently available on Pro, Plus, Business, Enterprise, and Edu plans…". Legacy body text.
7. **Cloud browser sign-in.** The allowlisting article says "at launch, Cloud browser cannot sign in to websites or complete payments." The cloud-browser article and release notes (2026-08-25) document sign-in support. The allowlisting sentence is stale or launch-scoped.
8. **Shopping research link target.** The 2025-11-24 post's "allowlisting process here" link now opens "ChatGPT Work's Cloud browser allowlisting", a different product name.
9. **Search model.** "fine-tuned version of GPT‑4o" (2024) vs GPT-4o retirement from ChatGPT (2026-02-13). Outdated (A-06).
10. **Bing naming.** The 2025 help article listed "Bing (Microsoft’s privacy policy)". The current article lists "Microsoft privacy statement". Wording change only; the provider set (Microsoft, Shopify) is unchanged.
11. **Shopping research sources.** The launch post says "based on publicly available retail sites". The 2026 help snapshot adds "merchant product data provided through the Agentic Commerce Protocol (ACP)". This is an evolution, not a conflict.

## Knowledge gaps

- Which share of queries go to Microsoft/Bing vs Shopify vs OpenAI's own index, and how their results are merged.
- Whether product carousels need OAI-SearchBot access, feed participation, or both. Only the merchant FAQ's "No, but feeds give you greater control" touches this.
- Definitions of "quality" (merchant ranking) and "performance signals" (feed attributes).
- Current status of shopping research as a feature: retired, merged, or only undocumented.
- Exact date when Instant Checkout stopped processing orders, if it did.
- Whether consumer product results (carousels) are available in India. No OpenAI statement found.
- Whether users in India see ads. Only advertiser self-service in India is documented.
- How the cloud browser (ChatGPT Work) discovers or ranks products during agentic shopping.
- Whether ChatGPT-User obeyed robots.txt in earlier versions of the bots doc. The 2025 archive is a JS shell with no text.
- Current model behind ChatGPT search and shopping (after GPT-4o and GPT-5 mini era models were retired).

## Unfetched sources

| URL | Error | Workaround |
|---|---|---|
| https://openai.com/index/introducing-chatgpt-search/ (and all openai.com posts) | WebFetch HTTP 403 | Read live in the in-app browser |
| https://help.openai.com/... (all help articles) | WebFetch HTTP 403 | Read live in the in-app browser |
| https://help.openai.com/en/articles/12440090-instant-checkout | Live page: "THAT PAGE DOESN'T EXIST" (404) | Wayback snapshot 2026-02-10 |
| https://developers.openai.com/ads/openai-geotargets.csv | HTTP 403 Cloudflare challenge (ads.openai.com) | Not bypassed; country targeting list not verified |
| https://web.archive.org/web/20251111230644/https://platform.openai.com/docs/bots | Snapshot is a JS shell (no doc text) | None; historical ChatGPT-User wording not verified |
| Wayback CDX for chatgpt.com/merchants | Internet Archive "Temporarily Offline" | None; merchant page history not checked |
| curl with a browser User-Agent | Blocked by the session's permission classifier ("Bot Check Circumvention") | Not retried; used plain curl and the in-app browser |

## Source list

| Title | Publisher | URL | Date |
|---|---|---|---|
| Introducing ChatGPT search | OpenAI | https://openai.com/index/introducing-chatgpt-search/ | 2024-10-31 (updates 2024-12-16, 2025-02-05) |
| Introducing shopping research in ChatGPT | OpenAI | https://openai.com/index/chatgpt-shopping-research/ | 2025-11-24 |
| Buy it in ChatGPT: Instant Checkout and the Agentic Commerce Protocol | OpenAI | https://openai.com/index/buy-it-in-chatgpt/ | 2025-09-29 |
| Powering Product Discovery in ChatGPT | OpenAI | https://openai.com/index/powering-product-discovery-in-chatgpt/ | 2026-03-24 |
| Our approach to advertising and expanding access to ChatGPT | OpenAI (Fidji Simo) | https://openai.com/index/our-approach-to-advertising-and-expanding-access/ | 2026-01-16 |
| Testing ads in ChatGPT | OpenAI | https://openai.com/index/testing-ads-in-chatgpt/ | 2026-02-09 (updated 2026-08-11) |
| A milestone in expanding access to AI | OpenAI | https://openai.com/index/expanding-access-to-ai-with-chatgpt-ads/ | 2026-08-31 |
| ChatGPT Ads expands to 26 new countries… | OpenAI | https://openai.com/index/chatgpt-ads-expands-26-new-countries/ | 2026-10-21 |
| Shopping with ChatGPT Search | OpenAI Help Center | https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search | approx. 2026-10-28 |
| Shopping help, archived versions | OpenAI Help Center via Wayback | https://web.archive.org/web/20251028124133/https://help.openai.com/en/articles/11128490-improved-shopping-results-from-chatgpt-search ; …/20260528132616/… | 2025-10-28; 2026-05-28 |
| Searching the web with ChatGPT | OpenAI Help Center | https://help.openai.com/en/articles/9237897-searching-the-web-with-chatgpt | approx. 2026-10-20 |
| ChatGPT search (archived) | OpenAI Help Center via Wayback | https://web.archive.org/web/20251014133746/https://help.openai.com/en/articles/9237897 | 2025-10-14 snapshot |
| Using shopping research in ChatGPT (archived) | OpenAI Help Center via Wayback | https://web.archive.org/web/20260805232131/https://help.openai.com/en/articles/12911370-using-shopping-research-in-chatgpt | 2026-08-05 snapshot |
| Instant Checkout: Buy Directly from Merchants through ChatGPT (archived) | OpenAI Help Center via Wayback | https://web.archive.org/web/20260210072037/https://help.openai.com/en/articles/12440090-instant-checkout-buy-directly-from-merchants-through-chatgpt | 2026-02-10 snapshot |
| Ads in ChatGPT | OpenAI Help Center | https://help.openai.com/en/articles/20001047-ads-in-chatgpt | approx. 2026-10-28 |
| Ads Manager Availability | OpenAI Help Center | https://help.openai.com/en/articles/20001245-ads-manager-availability | approx. 2026-10-27 |
| Create Campaigns from Product Feeds | OpenAI Help Center | https://help.openai.com/en/articles/20001268-create-campaigns-from-product-feeds | approx. 2026-10-27 |
| Creating ads for ChatGPT Ads | OpenAI Help Center | https://help.openai.com/en/articles/20001212-creating-ads-for-chatgpt-ads | approx. 2026-10-29 |
| Sponsored Agents in ChatGPT Ads | OpenAI Help Center | https://help.openai.com/en/articles/20001524-sponsored-agents-in-chatgpt-ads | approx. 2026-10-27 |
| Shopping from Shopify merchants in ChatGPT | OpenAI Help Center | https://help.openai.com/en/articles/20001241-shopping-from-shopify-merchants-in-chatgpt | approx. 2026-10-20 |
| ChatGPT agent | OpenAI Help Center | https://help.openai.com/en/articles/11752874-chatgpt-agent | approx. 2026-10-27 |
| ChatGPT agent – release notes | OpenAI Help Center | https://help.openai.com/en/articles/11794368-chatgpt-agent-release-notes | approx. 2026-10-19 |
| Using cloud browser in ChatGPT | OpenAI Help Center | https://help.openai.com/en/articles/20001280-using-cloud-browser-in-chatgpt | approx. 2026-10-28 |
| ChatGPT Work's Cloud browser allowlisting | OpenAI Help Center | https://help.openai.com/en/articles/11845367-chatgpt-works-cloud-browser-allowlisting | approx. 2026-10-19 |
| ChatGPT Atlas retirement | OpenAI Help Center | https://help.openai.com/en/articles/20001371-chatgpt-atlas-retirement | approx. 2026-10-23 |
| ChatGPT release notes | OpenAI Help Center | https://help.openai.com/en/articles/6825453-chatgpt-release-notes | updated approx. 2026-10-29 |
| Power product discovery in ChatGPT (merchants) | OpenAI | https://chatgpt.com/merchants/ | not stated |
| Overview of OpenAI Crawlers | OpenAI Developers | https://developers.openai.com/api/docs/bots (.md) | not stated |
| searchbot.json | OpenAI | https://openai.com/searchbot.json | creationTime 2026-01-02 |
| Key concepts / Get Started (Agentic Commerce) | OpenAI Developers | https://developers.openai.com/commerce/guides/key-concepts.md ; https://developers.openai.com/commerce/guides/get-started.md | not stated |
| Location Targeting / Product Feeds (Ads) | OpenAI Developers | https://developers.openai.com/ads/location-targeting.md ; https://developers.openai.com/ads/product-feeds.md | not stated |
| Web search / Browser / Site tools | ChatGPT docs | https://learn.chatgpt.com/docs/web-search.md ; https://learn.chatgpt.com/docs/browser.md ; https://learn.chatgpt.com/docs/webmcp.md | not stated |
| India pilots AI chatbot-led e-commerce… | TechCrunch (Tier 3) | https://techcrunch.com/2025/10/09/india-pilots-ai-chatbot-led-e-commerce-with-chatgpt-gemini-claude-in-the-mix/ | 2025-10-09 |
