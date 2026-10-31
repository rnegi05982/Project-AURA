# Registry — SHOP (Shopify)

Schema: `evidence/README.md`. All entries accessed 2026-10-30. Shopify Help Center pages show no dates; "not stated" applies unless noted.

Shopify Catalog: Shopify's cross-merchant product index that syndicates eligible products to AI channels. Agentic Storefronts: Shopify's admin feature that controls which AI channels receive Catalog data.

---

## ChatGPT channel (Agentic Storefronts)

### SHOP-001 — The ChatGPT channel is on by default for eligible stores; opt-out takes up to 7 days
- **Claim:** ChatGPT's access to a store's products through Shopify Catalog is active by default. Merchants remove it in Sales channels > Agentic. Removal can take up to 7 days.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / ChatGPT channel
- **Source:** "Selling on ChatGPT" — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/chatgpt
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "The ChatGPT channel acts as a discovery-focused referrer platform for customers to find your products. It's active by default for eligible stores, but you can remove ChatGPT's access to your products through Shopify Catalog in Sales channels > Agentic in your Shopify admin."
- **Establishes:** Eligible Shopify merchants are already syndicated to ChatGPT unless they opted out.
- **Limitations:** Eligibility defined in SHOP-003 and SHOP-005.
- **Related:** CGPT-017, SHOP-010
- **Origin:** notes/c-…#C-01 · **Checked:** 2026-10-30

### SHOP-002 — ChatGPT is a referrer: checkout happens on the merchant's own Shopify checkout
- **Claim:** ChatGPT users buy on the merchant's online-store checkout, in an in-app browser (mobile) or a new tab (web). The ChatGPT storefront has only a Catalog access setting.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / checkout
- **Source:** "Shopify agentic storefronts" — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts ; "Selling on ChatGPT" — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/chatgpt (Shopify Help Center)
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "ChatGPT is a product discovery channel. Customers using ChatGPT are redirected to buy products in your online store checkout, therefore there's no option to activate or deactivate a ChatGPT direct checkout setting in your Shopify admin."
- **Establishes:** No in-chat checkout for Shopify merchants in ChatGPT. Google AI Mode/Gemini, Copilot and Meta do offer Shopify-powered direct checkout.
- **Limitations:** None.
- **Related:** CGPT-021, CGPT-022
- **Origin:** notes/c-…#C-02 · **Checked:** pending

### SHOP-003 — ChatGPT channel eligibility: sells to US buyers, Catalog-eligible products, three policies
- **Claim:** The store must sell to US customers (it may be based elsewhere). Products must be Catalog-eligible. Terms of service, privacy policy and refund policy must be completed. B2B-only and OpenAI-prohibited products are excluded.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / eligibility
- **Source:** "Selling on ChatGPT" — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/chatgpt
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Your store must sell to customers in the United States, however, your store can be based outside the United States." / > "Ensure that your product descriptions include any relevant legal disclosures in the first 6,000 characters."
- **Establishes:** An India-only store (no US market) is not eligible for the ChatGPT channel.
- **Limitations:** The 6,000-character line implies truncation somewhere; Shopify does not say where.
- **Related:** CGPT-022, SHOP-005
- **Origin:** notes/c-…#C-03 · **Checked:** 2026-10-30 (US sentence)

### SHOP-004 — No fee for ChatGPT sales today; Shopify terms reserve per-channel fees
- **Claim:** Shopify charges no fee for ChatGPT sales beyond payment processing. The Agentic Storefronts terms (updated 2026-10-06) allow Shopify to charge fees for certain channels.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / fees
- **Source:** "Selling on ChatGPT" — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/chatgpt ; "Shopify Agentic Storefronts Supplemental Terms of Service" — https://www.shopify.com/legal/terms-agentic-storefronts
- **Published:** terms updated 2026-10-06 · **Accessed:** 2026-10-30
- **Excerpt:** > "There are no fees associated with selling in ChatGPT. You pay only your standard payment processing fees." / > "For certain Participating Channels, Shopify may, in its discretion, assess a fee on transactions that occur as a result of your participation in Agentic Storefronts."
- **Establishes:** Cost to participate is zero today.
- **Limitations:** Future fees possible.
- **Related:** CGPT-024
- **Origin:** notes/c-…#C-04 · **Checked:** pending

## Shopify Catalog

### SHOP-005 — Catalog eligibility gates: plan, title, image, price, published URL, category exclusions
- **Claim:** Products enter Shopify Catalog if the store is on Starter or higher and not password-protected, and the product has a title, an image, a price above 0, and is not Unlisted or hidden from search engines. Excluded categories and account standing also apply. Merchants cannot opt out of Catalog itself.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / Catalog eligibility
- **Source:** "Requirements for being included in Shopify Catalog" — Shopify Help Center — https://help.shopify.com/en/manual/shopify-catalog/requirements
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Your products can't have Unlisted status or be hidden from search engines." / > "The classification is based on your product information, so it can differ from the product category that you set in your Shopify admin."
- **Establishes:** Hard gates before a product can reach ChatGPT through Catalog. Exclusions include alcohol, tobacco/vaping, CBD, weapons, adult, services, event tickets, live animals and "Uncategorized" products.
- **Limitations:** Account-standing thresholds not published.
- **Related:** SHOP-003
- **Origin:** notes/c-…#C-05 · **Checked:** pending

### SHOP-006 — Catalog syndicates title, description, options, images, price, availability and "other key attributes", continuously updated
- **Claim:** Catalog lists products with title, description, options, images, price, availability and other attributes. It updates continuously. AI channels get no order history or customer database.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / Catalog data
- **Source:** "Shopify Catalog and product discovery for agentic storefronts" — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/products
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "When your products are syndicated to AI channels by Shopify Catalog, the products are listed by default with their title, description, options, images, price, availability, and other key attributes, all structured in a way that AI agents can parse and understand. Shopify Catalog continuously updates your product data, so AI channels receive your latest inventory and prices."
- **Establishes:** The Shopify-admin product record is the data ChatGPT receives via Catalog.
- **Limitations:** Latency of "continuously" not stated. Push vs pull not stated.
- **Related:** CGPT-017, SHOP-007
- **Origin:** notes/c-…#C-06 · **Checked:** pending

### SHOP-007 — Merchants can remap Catalog title and description to metafields; compare-at price maps to UCP `list_price`
- **Claim:** The Catalog Channel mapping page lets merchants source title and description from metafields or Liquid, choose the list price source, and set variant grouping. Product category cannot be remapped.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / Catalog data
- **Source:** "Customizing your product data for Shopify Catalog" — Shopify Help Center — https://help.shopify.com/en/manual/shopify-catalog/mapping
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "You can change the sources for the product title and the product description. You can't map the product category for Shopify Catalog." / > "Shopify Catalog sends an eligible compare-at price through the list_price field in the Universal Commerce Protocol (UCP) Variant specification."
- **Establishes:** A merchant can send AI channels a different title/description from the storefront. Catalog's schema is UCP-shaped.
- **Limitations:** The mapping preview "isn't an exact indicator" of AI display.
- **Related:** SHOP-006, SHOP-014
- **Origin:** notes/c-…#C-07 · **Checked:** pending

### SHOP-008 — Shopify lists the product fields "AI platforms or shopping sites" consider, including barcode/GTIN
- **Claim:** Shopify says AI platforms consider title, description, images, type, vendor, collections, tags, barcode and variant options.
- **Classification:** VERIFIED FACT (Shopify's statement). Which fields ChatGPT uses: UNVERIFIED HYPOTHESIS. · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** Shopify / product data
- **Source:** "Optimizing your products for AI platforms" — Shopify Help Center — https://help.shopify.com/en/manual/shopify-catalog/optimizing-products
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Barcode (ISBN, UPC, GTIN, etc.)" / > "Product organization details such as Type, Vendor, Collections, and Tags"
- **Establishes:** Shopify's own data-quality checklist for Catalog.
- **Limitations:** Generic across platforms.
- **Related:** SHOP-009
- **Origin:** notes/c-…#C-08 · **Checked:** pending

### SHOP-009 — Catalog has its own search and "Listing quality" signals; AI channels re-rank
- **Claim:** The Agentic admin page previews raw Shopify Catalog search output. Listing quality uses description completeness, image coverage, verified product reviews, variant completeness and shop policy completeness. Shopify says channels re-rank and relevance also uses popularity, engagement and brand signals.
- **Classification:** VERIFIED FACT (for Shopify Catalog search). Effect on ChatGPT ranking: UNVERIFIED HYPOTHESIS. · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** Shopify / ranking
- **Source:** "Managing agentic storefronts" — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/agentic-home
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Agentic storefronts often re-rank results based on their own logic, so what's displayed in the preview might differ from what customers view in the actual AI experience." / > "Product reviews signal trust and popularity, which can influence how AI channels rank your products. This measurement is calculated only from reviews that are verified by trusted sources."
- **Establishes:** Two ranking layers exist for Shopify products: Catalog search, then ChatGPT's own re-ranking.
- **Limitations:** "Trusted sources" not named. Whether ChatGPT consumes Catalog's order is not stated.
- **Related:** CGPT-011, CGPT-015
- **Origin:** notes/c-…#C-09 · **Checked:** pending

### SHOP-010 — "Allow Shopify to manage for me" auto-enrolls stores in new AI channels
- **Claim:** The default setting activates all channels and enrolls stores in future channels. Hiding a product from all agentic storefronts requires Unlisted status or the `seo.hidden` metafield.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / ChatGPT channel
- **Source:** "Managing agentic storefronts" — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/agentic-home
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Allow Shopify to manage for me is the default behavior for Shopify's agentic storefronts. It means that all channels are active and that Shopify automatically enrolls you in agentic storefronts."
- **Establishes:** Merchants who never opened the setting are enrolled.
- **Limitations:** None.
- **Related:** SHOP-001
- **Origin:** notes/c-…#C-10 · **Checked:** pending

### SHOP-011 — Catalog opt-out does not stop discovery by web crawling
- **Claim:** Removing Catalog access does not stop ChatGPT from finding products by crawling and indexing. Only Unlisted status hides a product everywhere.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / discovery paths
- **Source:** "Shopify Catalog and product discovery for agentic storefronts" — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/products ; "Selling on ChatGPT" — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/chatgpt
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "You can remove Shopify Catalog access for ChatGPT, but your products might still be displayed or referenced by the AI channel through other external discovery and listing methods, such as web crawling and indexing."
- **Establishes:** Two independent paths into ChatGPT: Catalog syndication and open-web crawl.
- **Limitations:** Precedence when they disagree is undocumented.
- **Related:** CGPT-019, SHOP-018
- **Origin:** notes/c-…#C-11 · **Checked:** 2026-10-30 (crawl clause)

### SHOP-012 — The ChatGPT channel went live for Shopify merchants the week of 2026-03-24, with referral attribution
- **Claim:** Shopify says millions of merchants can sell to ChatGPT users from that week. Orders carry ChatGPT referral attribution in the admin.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / ChatGPT channel
- **Source:** "Millions of merchants can sell in AI chats" — Shopify Newsroom — https://www.shopify.com/news/agentic-commerce-momentum
- **Published:** 2026-03-24 · **Accessed:** 2026-10-30
- **Excerpt:** > "Orders flow into the admin with ChatGPT referral attribution, so merchants can see exactly where sales came from."
- **Establishes:** Merchants can measure ChatGPT orders in Shopify admin. Useful as an experiment outcome metric.
- **Limitations:** "Millions" is Shopify's claim.
- **Related:** SHOP-013
- **Origin:** notes/c-…#C-14 · **Checked:** pending

### SHOP-013 — The Agentic admin page shows queries a store ranks for (2026-05-11)
- **Claim:** Shopify added an Agentic admin page that tracks performance across AI channels and shows queries the store ranks for.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / measurement
- **Source:** "A new home for Agentic Storefronts in your admin" — Shopify developer changelog — https://shopify.dev/changelog/a-new-home-for-agentic-storefronts-in-your-admin
- **Published:** 2026-05-11 · **Accessed:** 2026-10-30
- **Excerpt:** > "Your products are automatically accessible to AI channels like ChatGPT, Shop, and Copilot through Shopify Catalog. Now you can track performance across all major AI channels, see which queries you rank for, and get recommendations to improve your product data."
- **Establishes:** A merchant-side measurement surface exists for experiments.
- **Limitations:** Whether "queries you rank for" reflects ChatGPT's ranking or Catalog's is not stated (SHOP-009).
- **Related:** SHOP-009, SHOP-012
- **Origin:** notes/c-…#C-15 · **Checked:** pending

### SHOP-014 — UCP is co-developed by Shopify and Google; OpenAI is not listed; no source says ChatGPT uses UCP
- **Claim:** Shopify announced UCP (Universal Commerce Protocol) with Google on 2026-01-11. ucp.dev lists co-developers and council members; OpenAI is absent. Shopify ties UCP to Google AI Mode/Gemini, not ChatGPT.
- **Classification:** VERIFIED FACT (lists, statements). "ChatGPT does not consume UCP" is an EVIDENCE-BASED INFERENCE from absence. · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** Shopify / protocols
- **Source:** "The agentic commerce platform" — Shopify Newsroom — https://www.shopify.com/news/ai-commerce-at-scale ; https://ucp.dev/
- **Published:** 2026-01-11 · **Accessed:** 2026-10-30
- **Excerpt:** > "We're announcing the Universal Commerce Protocol (UCP), a new open standard co-developed with Google to bring commerce to agents at scale."
- **Establishes:** For ChatGPT, UCP adoption has no documented effect.
- **Limitations:** Catalog's schema is UCP-shaped (SHOP-007), so Catalog data may reach ChatGPT in UCP form. UNVERIFIED.
- **Related:** ACP-006
- **Origin:** notes/c-…#C-16 · **Checked:** pending

### SHOP-015 — Shopify exposes Global and Storefront Catalog MCP endpoints to any agent; some fields are AI-inferred
- **Claim:** Shopify offers `catalog.shopify.com/api/ucp/mcp` (all merchants, clustered by UPID) and `{store}/api/ucp/mcp`. Tools: `search_catalog`, `lookup_catalog`, `get_product`. Shopify generates some fields ("Inferred"). Results support rating filters. Caching is not allowed.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / Catalog API
- **Source:** "About Catalogs" — https://shopify.dev/docs/agents/catalog ; "Global Catalog MCP" — https://shopify.dev/docs/agents/catalog/global-catalog (Shopify.dev)
- **Published:** not stated (references UCP 2026-08-25) · **Accessed:** 2026-10-30
- **Excerpt:** > "Some Global Catalog response fields are generated or enriched by Shopify, and are marked `Inferred` in the reference. These fields might not always be present or might vary in accuracy depending on available product data."
- **Establishes:** Shopify enriches merchant data (attributes, tech specs, top features). Merchants do not fully control what agents see.
- **Limitations:** Docs never name ChatGPT as a consumer of these endpoints.
- **Related:** SHOP-007, SHOP-024
- **Origin:** notes/c-…#C-17 · **Checked:** pending

## Storefront defaults (crawling, structured data)

### SHOP-016 — Shopify's default robots.txt allows all bots, names no OpenAI crawler, and opens with comments addressed to AI agents
- **Claim:** The generated robots.txt has `User-agent: *` / `Allow: /` and no GPTBot, OAI-SearchBot or ChatGPT-User group. It opens with comments pointing agents to `/agents.md` and UCP endpoints, and asking agents to recommend a Shop skill to their user. It disallows cart/checkout AJAX paths with "agents should use UCP/MCP instead".
- **Classification:** VERIFIED FACT (observed on 5 stores by agent C; re-checked on kith.com by lead) · **Confidence:** High · **Tier:** 1 (primary artifact)
- **Subject / topic:** Shopify / crawling
- **Source:** https://kith.com/robots.txt ; https://theme-dawn-demo.myshopify.com/robots.txt ; https://theme-horizon-demo.myshopify.com/robots.txt ; https://www.brooklinen.com/robots.txt ; https://colourpop.com/robots.txt
- **Published:** live file, 2026-10-30 · **Accessed:** 2026-10-30
- **Excerpt:** > "# Shopify storefront. Public product, collection, page, blog, policy, cart, and localized HTML is crawlable." … "User-agent: *" "Allow: /"
- **Establishes:** Default Shopify stores do not block OpenAI crawlers. Shopify uses robots.txt comments to steer agents toward its own interfaces.
- **Limitations:** Comment text is data, not an instruction AURA follows. `grep -ciE 'gptbot|oai-searchbot|chatgpt-user|openai'` = 0 on kith.com.
- **Related:** CGPT-006, SHOP-017, SHOP-018
- **Origin:** notes/c-…#C-18 · **Checked:** 2026-10-30

### SHOP-017 — Stores with a custom robots.txt.liquid do not inherit default changes
- **Claim:** Allbirds, Gymshark and Taylor Stitch serve custom robots.txt files without the new header. Gymshark still disallows `/search` and `/policies/`. None names an OpenAI crawler.
- **Classification:** VERIFIED FACT (observed, 3 stores) · **Confidence:** High · **Tier:** 1 (primary artifact)
- **Subject / topic:** Shopify / crawling
- **Source:** https://www.allbirds.com/robots.txt ; https://www.gymshark.com/robots.txt ; https://www.taylorstitch.com/robots.txt
- **Published:** live file, 2026-10-30 · **Accessed:** 2026-10-30
- **Excerpt:** > Gymshark: "# we use Shopify as our ecommerce platform" … "Disallow: /policies/" … "Disallow: /search"
- **Establishes:** A custom template freezes the robots.txt; audits must read the live file.
- **Limitations:** Not a census.
- **Related:** SHOP-016, SHOP-018
- **Origin:** notes/c-…#C-19, #C-21 · **Checked:** pending

### SHOP-018 — robots.txt and network blocking affect only open-web discovery, not Catalog syndication
- **Claim:** Shopify states that Catalog sends product data to activated AI channels independently of robots.txt. Blocking AI crawlers affects only open-web discoverability.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / crawling, discovery paths
- **Source:** "Editing robots.txt.liquid" — Shopify Help Center — https://help.shopify.com/en/manual/promoting-marketing/seo/editing-robots-txt
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "If you sell through agentic storefronts such as ChatGPT or Microsoft Copilot, then your product data is syndicated to those channels through Shopify Catalog, independently of /robots.txt." / > "Blocking AI crawlers at the /robots.txt or network layer affects only open-web discoverability. It doesn't stop your product data from being sent by Shopify Catalog to the agentic storefronts that you've activated."
- **Establishes:** Two separate control planes. A merchant who blocks OAI-SearchBot still feeds ChatGPT via Catalog.
- **Limitations:** None.
- **Related:** SHOP-011, CGPT-006
- **Origin:** notes/c-…#C-20 · **Checked:** 2026-10-30

### SHOP-019 — Shopify rate-limits unsigned bots hardest (since May 2026), but says LLM indexing needs no signature
- **Claim:** Shopify applies stricter rate limits to bots; unsigned bots get the strictest. Web Bot Auth signing earns higher limits. Shopify says stores can be indexed by LLMs without signatures.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / crawling
- **Source:** "Bots and agents should identify themselves via Web Bot Auth" — Shopify developer changelog — https://shopify.dev/changelog/bots-and-agents-should-identify-themselves-via-web-bot-auth ; "Crawling your store" — https://help.shopify.com/en/manual/promoting-marketing/seo/crawling-your-store
- **Published:** 2026-05-07 (effective 2026-05-30, page metadata) · **Accessed:** 2026-10-30
- **Excerpt:** > "Bots and agents that don't sign their requests are subject to the strictest limits." / > "Your store can be indexed by search engines and large language models (LLMs) without signatures."
- **Establishes:** Merchants have no toggle to block or allow OpenAI bots at the network layer.
- **Limitations:** Whether OpenAI crawlers sign with Web Bot Auth or are exempted is undocumented. ChatGPT Work's cloud browser does sign (CGPT-036).
- **Related:** CGPT-036
- **Origin:** notes/c-…#C-22 · **Checked:** pending

### SHOP-020 — Every Shopify store serves `/agents.md`, `/llms.txt` and `/.well-known/ucp` by default
- **Claim:** Shopify auto-serves agent discovery files and a UCP profile with an MCP endpoint. Shopify calls Catalog the authoritative feed; the files do not replace it.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / agent discovery
- **Source:** "Shopify Catalog and product discovery for agentic storefronts" — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/products ; live https://theme-dawn-demo.myshopify.com/.well-known/ucp
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Shopify Catalog is the authoritative product data feed to your agentic channels. The agent discovery files are separate from Shopify Catalog, and they don't replace any Shopify Catalog capabilities."
- **Establishes:** Each storefront is a UCP endpoint by default.
- **Limitations:** No evidence that ChatGPT reads these files.
- **Related:** SHOP-014, SHOP-023
- **Origin:** notes/c-…#C-23 · **Checked:** pending

### SHOP-021 — The Liquid `structured_data` filter outputs schema.org Product or ProductGroup
- **Claim:** Products without variants output `Product`; with variants, `ProductGroup`.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / structured data
- **Source:** "Liquid filters: structured_data" — Shopify.dev — https://shopify.dev/docs/api/liquid/filters/structured_data
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Product objects are output as a [schema.org `Product`](https://schema.org/Product) if they have no variants, and a [`ProductGroup`](https://schema.org/ProductGroup) if they have one or more variants."
- **Establishes:** Shopify generates product JSON-LD; themes do not hand-write it.
- **Limitations:** No exhaustive field list in the doc.
- **Related:** SHOP-022
- **Origin:** notes/c-…#C-24 · **Checked:** pending

### SHOP-022 — Default Dawn/Horizon JSON-LD includes GTIN, SKU, offers; no ratings, shipping or return policy
- **Claim:** Dawn and Horizon emit `product | structured_data` JSON-LD. Live demo pages show `ProductGroup` with `hasVariant[]` (gtin, sku, offers), brand, category and description. No `aggregateRating`, `review`, `shippingDetails` or `hasMerchantReturnPolicy`.
- **Classification:** VERIFIED FACT (theme source at pinned commits; 2 live pages). Generalisation to all stores: EVIDENCE-BASED INFERENCE. · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** Shopify / structured data
- **Source:** Shopify/dawn @ 05222537 (2026-10-22) `sections/main-product.liquid:749-750` — https://github.com/Shopify/dawn ; Shopify/horizon @ dfad90d8 — https://github.com/Shopify/horizon ; https://theme-dawn-demo.myshopify.com/products/studio-denim
- **Published:** commits 2026-10-22, 2026-10-13 · **Accessed:** 2026-10-30
- **Excerpt:** > `<script type="application/ld+json">` / `{{ product | structured_data }}`
- **Establishes:** Ratings, shipping and return markup require apps or theme edits.
- **Limitations:** No evidence that ChatGPT reads JSON-LD (no OpenAI source mentions schema.org).
- **Related:** SHOP-021, RES-012 (schema.org showed no citation lift in one API study)
- **Origin:** notes/c-…#C-25, #C-26 · **Checked:** pending

### SHOP-023 — Shopify sitemaps now include an "agentic discovery" child sitemap
- **Claim:** The auto-generated sitemap index lists `sitemap_agentic_discovery.xml`, which contains only `/agents.md`.
- **Classification:** VERIFIED FACT (observed) · **Confidence:** High · **Tier:** 1 (primary artifact)
- **Subject / topic:** Shopify / crawling
- **Source:** https://theme-dawn-demo.myshopify.com/sitemap.xml ; https://theme-dawn-demo.myshopify.com/sitemap_agentic_discovery.xml
- **Published:** live file, 2026-10-30 · **Accessed:** 2026-10-30
- **Excerpt:** > `<loc>https://theme-dawn-demo.myshopify.com/sitemap_agentic_discovery.xml</loc>`
- **Establishes:** Live behaviour is ahead of the Help Center sitemap page.
- **Limitations:** No evidence any AI crawler uses it.
- **Related:** SHOP-020
- **Origin:** notes/c-…#C-27 · **Checked:** pending

### SHOP-024 — Shopify Catalog infers categories, extracts attributes and clusters identical items (Dec 2025 launch)
- **Claim:** Shopify's Agentic Storefronts launch post described Catalog enrichment. The same post promised in-chat checkout and listed Perplexity; both are superseded.
- **Classification:** VERIFIED FACT (statements); in-chat checkout and Perplexity listing superseded · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** Shopify / Catalog data
- **Source:** "Introducing Shopify Agentic Storefronts" — Shopify Newsroom — https://www.shopify.com/news/winter-26-edition-agentic-storefronts
- **Published:** 2025-12-10 (now carries a pointer to newer information) · **Accessed:** 2026-10-30
- **Excerpt:** > "It infers categories, extracts attributes, consolidates variants, and clusters identical items so shoppers see only relevant and unique results."
- **Establishes:** Catalog transforms merchant data before AI channels see it.
- **Limitations:** Superseded parts noted above.
- **Related:** SHOP-015, SHOP-002
- **Origin:** notes/c-…#C-29 · **Checked:** pending

## Google AI Mode and Gemini channel

Origin files for this section: `research/ai-platforms/gemini/notes/gc-shopify-and-platforms-to-google.md` (GC-xx).

### SHOP-025 — Google AI Mode and Gemini discover Shopify products through Google Merchant Center, not Shopify Catalog
- **Claim:** Shopify states that product discovery for Google AI Mode and Gemini is powered by Google Merchant Center. Products reach Google through the Google & YouTube sales channel or any other Merchant Center feed. The Google channel has no Shopify Catalog access toggle.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / Google channel
- **Source:** "Selling on Google AI Mode and Gemini" — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google ; "Data sharing and privacy for selling with agentic storefronts" — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/data-privacy
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Product discovery is powered by Google Merchant Center:" / > "For Google AI Mode and Gemini and Meta, product discovery is powered by individual sales channels rather than a Shopify Catalog access setting."
- **Establishes:** The ChatGPT path (Shopify Catalog, SHOP-001) and the Google path (Merchant Center feed) are separate pipes. A Shopify store without a Merchant Center feed has no Shopify-managed discovery path into AI Mode or Gemini.
- **Limitations:** Crawled pages can still reach Google (GOOG-010). Shopify's January 2026 post implied Catalog reached Google; superseded.
- **Related:** SHOP-001, GOOG-010, GOOG-020
- **Origin:** notes/gc-…#GC-01, #GC-15 · **Checked:** 2026-10-31

### SHOP-026 — Google direct checkout is on by default for eligible Shopify stores; opting out keeps discovery
- **Claim:** Shopify-powered direct checkout in AI Mode and Gemini is active by default for eligible stores. Merchants turn it off in Sales channels > Agentic. With checkout off, products stay discoverable via Merchant Center and buyers go to the online store.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / Google checkout
- **Source:** "Selling on Google AI Mode and Gemini" — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "If you opt out of direct checkout with Google AI Mode and Gemini, then your products can still be discovered and included in Google AI Mode and Gemini's search results through Google Merchant Center, but they can't be purchased through a direct checkout."
- **Establishes:** Checkout and discovery are independent switches. Google says checkout is ranking-neutral (GOOG-003).
- **Limitations:** Trade press reports Google emailed Shopify merchants in Sept 2026 that their store "was matched" to Merchant Center (Tier 3).
- **Related:** GOOG-001, GOOG-003
- **Origin:** notes/gc-…#GC-02, #GC-07 · **Checked:** 2026-10-31 (default sentence)

### SHOP-027 — Eligibility: sell to US, Canadian or Australian buyers (store anywhere), valid Merchant Center, Catalog-eligible products, three policies
- **Claim:** The store must sell to customers in the US, Canada or Australia and may be based anywhere. It needs a valid Merchant Center account meeting Google's requirements, products in Merchant Center, Shopify Catalog eligibility, accepted supplemental terms and completed policies. Before a date between 2026-10-19 and 2026-10-30, Shopify required US-based stores selling to US buyers.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / Google eligibility
- **Source:** "Selling on Google AI Mode and Gemini" — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google (earlier text: Wayback 2026-09-21, 2026-10-19)
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "You must sell to customers in the United States, Canada, or Australia."
- **Establishes:** Indian buyers cannot use direct checkout. An India-based store qualifies only for US/CA/AU buyers.
- **Limitations:** Google Search Help still says AI Mode checkout is US-only for buyers (GEM-014); the two conflict for CA/AU.
- **Related:** SHOP-003, GEM-014
- **Origin:** notes/gc-…#GC-03, #GC-06, §2 · **Checked:** 2026-10-31

### SHOP-028 — No Shopify fee for Google direct checkout; several product types unsupported
- **Claim:** Shopify charges no fee beyond payment processing. Subscription-only products, bundles, customizable products and B2B-only products are not supported. Client-side pixels and Google Analytics do not fire in this checkout; local delivery and pickup are unsupported.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / Google checkout
- **Source:** "Selling on Google AI Mode and Gemini" — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "There are no fees associated with selling in Google AI Mode and Gemini's direct checkout." / > "Google Analytics and custom pixels won't fire in Google AI Mode and Gemini's direct checkout."
- **Establishes:** Attribution for Google-checkout orders needs server-side measurement.
- **Limitations:** Google's own UCP exclusion list is broader (used, final-sale, pre-order); which applies to Shopify offers is undocumented.
- **Related:** GOOG-002, SHOP-004
- **Origin:** notes/gc-…#GC-04, #GC-05, #GC-20 · **Checked:** 2026-10-31 (fee sentence)

### SHOP-029 — The Google & YouTube channel is Google's app; it syncs products, shipping and taxes and overwrites any existing feed
- **Claim:** Google develops and supports the Google & YouTube app. It syncs the store domain, online-store products, and shipping and tax settings to Merchant Center, re-syncs on change and within Google's 30-day expiry, and overwrites an existing feed. Google reviews new products in 3–5 business days.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / Merchant Center feed
- **Source:** "Google & YouTube" — Shopify App Store — https://apps.shopify.com/google ; "Syncing your products" — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/marketplaces/google/getting-setup/syncing-products
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "If you already have a product feed set up, then it's overwritten to avoid conflicts between your Shopify store and your Merchant Center account."
- **Establishes:** The feed that drives Google AI discovery for Shopify stores is a Google-owned integration.
- **Limitations:** Sync latency after a change is not stated.
- **Related:** SHOP-025
- **Origin:** notes/gc-…#GC-08, #GC-09 · **Checked:** pending

### SHOP-030 — Shopify → Merchant Center field mapping: barcode → GTIN, vendor → brand (default), General shipping profile only; options must be in English
- **Claim:** GTIN comes from the variant barcode. Products without a GTIN need MPN plus brand, or a "custom product" flag. Google assigns a category if none is set. The channel can send the SEO title and meta description. Only the General shipping profile syncs. Product options must be in English.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / product data
- **Source:** "Google & YouTube channel requirements" — https://help.shopify.com/en/manual/online-sales-channels/marketplaces/google/requirements ; "Syncing your products" — Google Merchant Center Help — https://support.google.com/merchants/answer/13427434?hl=en
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Only shipping rates in your General shipping profile can sync to Google Merchant Center. If you use custom shipping profiles, then rates will sync incorrectly with Google Merchant Center and cause errors." / > "Product options, including variants, need to be in English to sync with Google."
- **Establishes:** Exact Shopify fields that feed Google AI discovery.
- **Limitations:** No full default mapping table is published.
- **Related:** SHOP-008, GOOG-009
- **Origin:** notes/gc-…#GC-10, #GC-11 · **Checked:** pending

### SHOP-031 — Return policy must be set in Merchant Center separately; UCP checkout requires it
- **Claim:** Google's Shopify guide says to set the return policy in Shopify and separately in Merchant Center. Google's UCP checkout requires a Merchant Center return policy with cost, window and link, plus support contact.
- **Classification:** VERIFIED FACT. That the app does not sync return policy is an EVIDENCE-BASED INFERENCE. · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / Merchant Center
- **Source:** "Set up your return policies (for Shopify users)" — Google Merchant Center Help — https://support.google.com/merchants/answer/14232691?hl=en
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Adding your return policy in both locations helps ensure that Google accurately represents your policies in search results and Shopping ads."
- **Establishes:** A manual Merchant Center step that the Shopify app does not cover.
- **Limitations:** None.
- **Related:** GOOG-002
- **Origin:** notes/gc-…#GC-12 · **Checked:** pending

### SHOP-032 — The app auto-opts stores into free listings; India is a supported sync and free-listings country
- **Claim:** Google says the Google & YouTube app automatically opts Shopify stores into free listings. Google's free-listings country list and the app's sync country list both include India (sync languages en, hi).
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / India
- **Source:** "Show your products for free on Google" — https://support.google.com/merchants/answer/13692890?hl=en ; "Syncing your products" — https://support.google.com/merchants/answer/13427434?hl=en
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "When you use the Google & YouTube app on Shopify, you’re automatically opted in to show products from your Shopify store for free on surfaces across Google, such as on the Shopping tab, YouTube, Google Search (.com), Google Images, and Google Lens."
- **Establishes:** An India-only Shopify store can enter Google's AI discovery pipeline (Merchant Center → Shopping Graph → Gemini/AI Mode, GEM-001, GEM-002). It cannot enter ChatGPT's Catalog path (SHOP-003).
- **Limitations:** Shopify's own page still describes free display only for US stores (outdated).
- **Related:** GEM-002, GOOG-017
- **Origin:** notes/gc-…#GC-13, #GC-14, #GC-26 · **Checked:** pending

### SHOP-033 — Google's Shopify addendum: native checkout uses "Shopify's API"; no source says Google reads Shopify Catalog or `/.well-known/ucp`
- **Claim:** Google's Merchant Center addendum for Shopify merchants defines Google Native Checkout as Google using Shopify's API. Item information flows through Shopify's platform or the Google & YouTube app. No Shopify or Google page says Google discovers products via Shopify Catalog or a store's `/.well-known/ucp`; live store profiles do declare a Google Pay handler with gateway `shopify`.
- **Classification:** VERIFIED FACT (addendum text; absence; profile contents) · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopify / Google integration
- **Source:** "Addendum to the Google Merchant Center Terms of Service for Shopify Merchants" — Google — https://developers.google.com/merchant/terms/shopify ; live https://kith.com/.well-known/ucp
- **Published:** addendum last updated 2026-01-06 · **Accessed:** 2026-10-30
- **Excerpt:** > "1.4. "Google Native Checkout" means the checkout process where Google uses Shopify's API to enable the User to complete checkout directly in the Service without displaying a separate checkout layer."
- **Establishes:** Google–Shopify checkout is a platform integration; merchants do not build UCP endpoints.
- **Limitations:** Whether Shopify Payments is required for Google checkout is not stated.
- **Related:** SHOP-020, UCP-004
- **Origin:** notes/gc-…#GC-16, #GC-17 · **Checked:** pending
