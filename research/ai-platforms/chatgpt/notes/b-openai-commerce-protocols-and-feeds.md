# B — OpenAI merchant integrations, commerce protocols, product feeds

- Agent: B (AURA research)
- Scope: Instant Checkout status; ACP (Agentic Commerce Protocol, the OpenAI/Stripe open spec for agent checkout, payments and feeds); OpenAI Product Feed Spec; merchant onboarding; merchant-ranking statements; ChatGPT apps/plugins for commerce; ACP vs UCP.
- Research date: 2026-10-30 (all pages accessed 2026-10-30).
- Method:
  - `curl` of Markdown twins on developers.openai.com (`/commerce/llms-full.txt`, `/plugins` export via `/apps-sdk/llms-full.txt`, `.md` pages).
  - `curl` of raw files from GitHub; shallow `git clone` of the ACP and UCP repos; GitHub REST API for commits, tags, releases.
  - WebFetch for Stripe, Shopify, agenticcommerce.dev, ucp.dev, press.
  - In-app browser pane (`document.body.innerText`) for openai.com, help.openai.com and chatgpt.com. WebFetch and curl get HTTP 403 there. No CAPTCHA was shown or solved.
- Terms used below:
  - PSP (payment service provider, e.g. Stripe, Adyen).
  - TSC (Technical Steering Committee, ACP's governing body).
  - SPT (Shared Payment Token, Stripe's scoped one-time payment credential).
  - SFTP (SSH File Transfer Protocol, the feed upload channel).
  - Plugin (ChatGPT): the 2026 name for an MCP-based ChatGPT app.

---

## 2. Findings

### B-01 Instant Checkout launched 2025-09-29 (US, Etsy first); Shopify merchants added 2025-11-20
- Claim: Instant Checkout launched for US users with US Etsy sellers. Shopify merchants followed on 2025-11-20. Launch scope was single-item purchases.
- Classification: VERIFIED FACT
- Source: Buy it in ChatGPT: Instant Checkout and the Agentic Commerce Protocol — OpenAI — https://openai.com/index/buy-it-in-chatgpt/ ; ChatGPT release notes — OpenAI Help Center — https://help.openai.com/en/articles/6825453-chatgpt-release-notes
- Published/updated: 2025-09-29 (blog, no update note shown); release-notes entry dated 2025-11-20
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "U.S. ChatGPT Plus, Pro, and Free users can now buy directly from U.S. Etsy sellers right in chat, with over a million Shopify merchants, like Glossier, SKIMS, Spanx and Vuori, coming soon. Today, Instant Checkout supports single-item purchases. Next, we’ll add multi-item carts and expand merchants and regions."
- Excerpt (release notes, November 20, 2025): > "You can now find and buy from Shopify merchants starting with Spanx, Skims, and Glossier through Instant Checkout in ChatGPT." … "Instant Checkout is available for logged in Plus, Pro, and Free users in the US."
- Establishes: The 2025 baseline: US-only, Etsy then Shopify, in-chat purchase.
- Limitations: The blog is historical. It carries no update banner despite the 2026 change (see B-03, B-25).

### B-02 2026-03-24: OpenAI drops the initial Instant Checkout and lets merchants use their own checkout
- Claim: OpenAI stated the first Instant Checkout lacked flexibility. Merchants now use their own checkout. OpenAI focuses on product discovery.
- Classification: VERIFIED FACT
- Source: Powering Product Discovery in ChatGPT — OpenAI — https://openai.com/index/powering-product-discovery-in-chatgpt/
- Published/updated: 2026-03-24
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "We’ve found that the initial version of Instant Checkout did not offer the level of flexibility that we aspire to provide, so we’re allowing merchants to use their own checkout experiences while we focus our efforts on product discovery."
- Establishes: The primary-source date and wording of the scale-back.
- Limitations: The post gives no shutdown date for existing Etsy/Shopify Instant Checkout. Adweek (Tier 3, https://www.adweek.com/commerce/openais-chatgpt-is-making-a-big-change-to-its-commerce-strategy/) quotes the same sentence and says "ChatGPT has since gotten rid of that feature."

### B-03 Current merchant page: "moving away from a standalone Instant Checkout"; shopping live in the US only
- Claim: Today, purchases complete on merchant-owned sites or apps. Shopping is live only for US users.
- Classification: VERIFIED FACT
- Source: Power product discovery in ChatGPT — OpenAI — https://chatgpt.com/merchants (served at https://chatgpt.com/merchants/)
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "We’re moving away from a standalone Instant Checkout experience in ChatGPT and prioritizing better shopping discovery and merchant-owned checkout experiences. Users can discover and evaluate products in ChatGPT, but purchases are completed on merchant-owned websites or apps."
- Excerpt: > "Shopping is currently live for ChatGPT users in the U.S. We’re building a merchant platform for self-serve data integration later this year, and plan to expand to more merchants and regions over time."
- Establishes: Current (2026-10-30) status of in-chat purchase and geography.
- Limitations: "later this year" is undated. Probably 2026; that is an inference.

### B-04 The Instant Checkout help article no longer exists
- Claim: The help-center article on Instant Checkout returns a "page doesn't exist" screen.
- Classification: VERIFIED FACT (observation); the retirement reason is an EVIDENCE-BASED INFERENCE from B-02/B-03.
- Source: Instant Checkout — OpenAI Help Center — https://help.openai.com/en/articles/12440090-instant-checkout
- Published/updated: n/a (page removed)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "UH OH. THAT PAGE DOESN'T EXIST."
- Establishes: OpenAI removed the consumer Instant Checkout documentation.
- Limitations: The removal date is unknown. A Wayback snapshot could not be fetched (see §6).

### B-05 Residual: "Instant Checkout" / ChatGPT payment sheet still exists in beta for "select marketplace partners"
- Claim: Plugin docs still describe a beta in-ChatGPT checkout for select marketplaces. External checkout is the required default.
- Classification: VERIFIED FACT (as documented); who the partners are is not stated.
- Source: Plugin guidelines and Checkout API reference — OpenAI Developers — https://developers.openai.com/plugins/plugin-guidelines.md ; https://developers.openai.com/plugins/build/monetization.md (read via https://developers.openai.com/apps-sdk/llms-full.txt)
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (guidelines): > "Instant Checkout, which is currently in beta, is currently available only to select marketplace partners and may expand to additional marketplaces and retailers over time."
- Excerpt (checkout reference; markdown bold removed): > "We’re also enabling embedded checkout with the ChatGPT payment sheet for select marketplace partners (beta), with plans to extend access to more marketplaces and physical-goods retailers over time."
- Excerpt: > "Checkout with the ChatGPT payment sheet is limited to select marketplaces today and is not available to all users."
- Establishes: In-chat payment survives as a narrow, plugin-based beta. It is not fully retired.
- Limitations: The partners are not named. This conflicts in tone with B-03 (see §4).

### B-06 Fees: "small fee" (2025) → "no fees" (2026)
- Claim: The 2025 model charged merchants a fee per completed purchase. The current page states no fees on purchases that start in ChatGPT.
- Classification: VERIFIED FACT
- Source: https://openai.com/index/buy-it-in-chatgpt/ (2025-09-29); https://chatgpt.com/merchants (current)
- Published/updated: 2025-09-29; current page not dated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (2025): > "Merchants pay a small fee on completed purchases, but the service is free for users, doesn’t affect their prices, and doesn’t influence ChatGPT’s product results."
- Excerpt (current): > "There are no fees on purchases that start in ChatGPT."
- Excerpt (current): > "Send shoppers to your site or app by default, with no fees for purchases made on your site or app."
- Establishes: The fee model was superseded.
- Limitations: The 2025 fee rate was never stated in a fetched primary source.

### B-07 ACP maintainers, governance and license: OpenAI + Stripe founders; Meta added 2026-04-24; Apache 2.0; beta
- Claim: OpenAI and Stripe are Founding Maintainers. Meta holds TSC seat 3. The license is Apache 2.0. The status is beta.
- Classification: VERIFIED FACT
- Source: README.md, MAINTAINERS.md, docs/governance.md, changelog/unreleased/add-meta-tsc-member.md — agentic-commerce-protocol GitHub org — https://github.com/agentic-commerce-protocol/agentic-commerce-protocol (raw files via raw.githubusercontent.com, main branch)
- Published/updated: Meta TSC commit 2026-04-24T16:44:27Z ("ADMIN: Add Meta as TSC member (#236)")
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (README): > "The specification is [maintained](MAINTAINERS.md) by **OpenAI** and **Stripe** and is currently in `beta`."
- Excerpt (MAINTAINERS.md): > "## Lead maintainers\n\n- OpenAI\n- Stripe\n- Meta"
- Excerpt (governance.md table): > "| 1    | OpenAI      | aravindrao-openai |" / "| 2    | Stripe      | prasad-stripe     |" / "| 3    | Meta        | lhwa              |"
- Excerpt (governance.md): > "The TSC has up to 7 seats. Each seat is held by one organization, including OpenAI and Stripe."
- Excerpt (governance.md): > "the Founding Maintainers (OpenAI and Stripe) reserve a limited veto authority over TSC decisions."
- Excerpt (governance.md): > "The Founding Maintainers recognize the long-term goal of transitioning ACP governance to a neutral foundation, similar to models used by the Linux Foundation or OpenJS Foundation."
- Excerpt (README): > "Licensed under the [Apache 2.0 License](LICENSE)."
- Excerpt (agenticcommerce.dev): > "ACP is open source and community-designed under the Apache 2.0 license."
- Establishes: Governance and licensing as of today.
- Limitations: The README text still says "maintained by OpenAI and Stripe" only. A CLA is required for contributions.

### B-08 ACP versions: five dated releases; latest stable 2026-04-17; no GitHub releases; last commit 2026-07-18
- Claim: ACP uses date versions 2025-09-29, 2025-12-12, 2026-01-16, 2026-01-30 and 2026-04-17. 2026-04-17 is latest stable. The repo has no tags or GitHub releases. The last commit to main is 2026-07-18.
- Classification: VERIFIED FACT
- Source: README.md, changelog/*.md — https://github.com/agentic-commerce-protocol/agentic-commerce-protocol ; GitHub API `/releases`, `/tags`, `/commits`
- Published/updated: changelog 2026-04-17 committed 2026-04-17T21:48:30Z ("RELEASE: 2026-04-17 (#227)"); latest commit 2026-07-18T04:51:51Z ("SEP: Optional product URL on checkout Item (#281)")
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (README): > "ACP uses **date-based versioning** in `YYYY-MM-DD` format. Each version represents a complete snapshot of the specification at that point in time."
- Excerpt (README tree): > "├── 2025-09-29/              # Initial release" … "├── 2025-12-12/              # Fulfillment enhancements" … "├── 2026-01-16/              # Capability negotiation" … "├── 2026-01-30/              # Extensions, discounts, payment handlers" … "├── 2026-04-17/              # Cart, feed, orders, authentication, and MCP"
- Excerpt (changelog 2026-04-17): > "This release promotes the accumulated unreleased ACP changes since 2026-01-30."
- Establishes: Version history and current version.
- Limitations: GitHub API returned empty arrays for `/releases` and `/tags`. No commits after 2026-07-18 is an observation. Reduced activity is only an inference.

### B-09 ACP 2026-04-17 components: checkout, delegate payment, delegate authentication, cart, feed (push), orders, discovery, MCP binding
- Claim: 2026-04-17 adds an agent-hosted Feed API, carts, native orders, 3DS delegate authentication, `/.well-known/acp.json` discovery and an MCP transport binding.
- Classification: VERIFIED FACT
- Source: changelog/2026-04-17.md; spec/2026-04-17/openapi/*.yaml — https://github.com/agentic-commerce-protocol/agentic-commerce-protocol
- Published/updated: 2026-04-17
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "These endpoints are hosted by Agents and called by merchants. The Feed API is a push model: merchants push product catalog metadata and product records to Agents, rather than Agents pulling catalog data from merchant-hosted endpoints."
- Excerpt: > "**Added** -- Model Context Protocol (MCP) transport binding for ACP checkout operations."
- Excerpt: > "**`/.well-known/acp.json`** -- A static, publicly accessible JSON document served at the origin\n  root per RFC 8615."
- Establishes: The protocol's component set. Spec files: `openapi.agentic_checkout.yaml`, `openapi.agentic_checkout_webhook.yaml`, `openapi.cart.yaml`, `openapi.delegate_authentication.yaml`, `openapi.delegate_payment.yaml`, `openapi.feed.yaml`, `openrpc.agentic_checkout.json`.
- Limitations: ACP Feed API paths are `/feeds`, `/feeds/{id}`, `/feeds/{id}/products`. OpenAI's own API docs use `/product_feeds/...` (see §4).

### B-10 ACP Product Feeds RFC: feed = discovery data surface; ranking is explicitly out of scope
- Claim: The ACP feed RFC defines data, not ranking. Agents build their own retrieval layer.
- Classification: VERIFIED FACT
- Source: rfcs/rfc.product_feeds.md — https://raw.githubusercontent.com/agentic-commerce-protocol/agentic-commerce-protocol/main/rfcs/rfc.product_feeds.md
- Published/updated: "**Status:** Proposal", "**Version:** unreleased"
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "- **Search or ranking algorithms**: This RFC defines the data surface, not how\n  agents rank products or personalize recommendations."
- Excerpt: > "Search APIs embed ranking, personalization, query syntax, and business rules\nthat vary widely by merchant. Feeds are simpler and more interoperable: they let\nagents build their own retrieval layer while merchants keep control over source\ncatalog data."
- Excerpt: > "Product feeds are a discovery and merchandising surface. Checkout remains the\nauthoritative surface for pricing, taxes, fulfillment, payment, policy checks,\nand order creation."
- Establishes: At protocol level, ranking is the agent's private logic.
- Limitations: RFC status is "Proposal". The 2026-04-17 `schema.feed.json` has no review, popularity or return-rate fields (Product: `id`, `title`, `description`, `url`, `media`, `variants`; Variant adds price, availability, categories, seller, `marketplace`, etc.).

### B-11 PSPs: Stripe SPT first; OpenAI docs list `stripe`, `adyen`, `braintree`; ACP schema enum lists `stripe`, `adyen`
- Claim: Stripe's SPT is the first Delegated Payment implementation. OpenAI's checkout docs name three processors. The ACP 2026-04-17 schema enum names two.
- Classification: VERIFIED FACT
- Source: OpenAI commerce docs (Key concepts; Agentic Checkout Spec) — https://developers.openai.com/commerce/llms-full.txt ; ACP changelog/2026-01-16.md and spec/2026-04-17/json-schema/schema.agentic_checkout.json ; https://www.agenticcommerce.dev
- Published/updated: not stated (OpenAI docs); 2026-01-16 (ACP)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (OpenAI): > "[Stripe’s Shared Payment Token](https://docs.stripe.com/agentic-commerce) is the first Delegated Payment Spec-compatible implementation, with more PSPs coming soon."
- Excerpt (OpenAI checkout spec, PaymentProvider): > "String value representing payment processor. Possible values are: `stripe` `adyen` `braintree`"
- Excerpt (ACP 2026-01-16): > "Added `adyen` to the provider enum for both `PaymentProvider` and `AuthenticationProvider`"
- Excerpt (agenticcommerce.dev): > "Stripe is the first compatible PSP with its Shared Payment Token."
- Establishes: The documented PSP set.
- Limitations: The 2026-01-30 payment-handlers framework uses a free-string `psp` field. An enum is therefore not a list of live partners.

### B-12 OpenAI's Agentic Checkout Spec page is on the deprecated 2025-09 shape
- Claim: OpenAI's checkout docs still use `fulfillment_address` and API-Version examples `2025-09-12`/`2025-09-29`. ACP renamed the field and deprecated 2025-09-29 in 2025-12-12.
- Classification: VERIFIED FACT (text comparison); "not maintained since the pivot" is an EVIDENCE-BASED INFERENCE.
- Source: https://developers.openai.com/commerce/llms-full.txt (Agentic Checkout Spec); ACP changelog/2025-12-12.md
- Published/updated: not stated (OpenAI); 2025-12-12 (ACP)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (ACP 2025-12-12): > "#### 1. Renamed `fulfillment_address` to `fulfillment_details`" … "- Previous version `2025-09-29` is deprecated"
- Excerpt (OpenAI checkout spec header table): > "| API-Version     | API version                                               | 2025-09-12                                      |"
- Establishes: OpenAI's checkout page and current ACP disagree. Count in the export: `fulfillment_address` 11 times, `fulfillment_details` 0 times.
- Limitations: OpenAI may accept several versions. No OpenAI statement on supported versions was found.

### B-13 2026-03-24: ACP extended to discovery; named retailers; Salesforce and Stripe as delivery paths
- Claim: ACP now carries product feeds and promotions for discovery. Named retailers integrated. Feeds can arrive via Salesforce or Stripe.
- Classification: VERIFIED FACT
- Source: https://openai.com/index/powering-product-discovery-in-chatgpt/ ; release notes entry "March 24, 2026 — Shopping updates in ChatGPT" — https://help.openai.com/en/articles/6825453-chatgpt-release-notes
- Published/updated: 2026-03-24
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Through ACP, merchants share product feeds and promotions so their catalogs are fully represented in ChatGPT. We support multiple delivery paths, including through third-party providers like Salesforce and Stripe, so merchants can participate with the systems they already use. Over time, ACP will serve as a foundation for broader AI-native commerce experiences, including personalization, local availability, and ETAs."
- Excerpt: > "Already, leading retailers including Target, Sephora, Nordstrom, Lowe’s, Best Buy, The Home Depot, and Wayfair have integrated into ACP for discovery."
- Excerpt (release notes): > "These updates improve how ChatGPT retrieves and presents product information from merchants and other providers using the Agentic Commerce Protocol (ACP)."
- Establishes: ACP's primary role in ChatGPT is now discovery data intake.
- Limitations: "integrated into ACP for discovery" does not say the retailers use the ACP Feed API or OpenAI SFTP.

### B-14 Shopify and Etsy catalogs are already integrated; Shopify checkout runs in an in-app browser
- Claim: Shopify products reach ChatGPT through Shopify Catalog. Etsy catalogs are also integrated. Shopify buyers pay on the merchant's own checkout in an in-app browser.
- Classification: VERIFIED FACT
- Source: https://chatgpt.com/merchants ; https://openai.com/index/powering-product-discovery-in-chatgpt/ ; ChatGPT (Agentic storefronts) — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/chatgpt
- Published/updated: not stated (merchants page, Shopify page); 2026-03-24 (blog)
- Accessed: 2026-10-30
- Tier: 1 (OpenAI); 1 (Shopify, partner primary)
- Excerpt (OpenAI merchants): > "If you’ve already applied, you’re on the waitlist. If you sell through Shopify or Etsy, your catalog is already integrated, and no additional setup or application is required."
- Excerpt (OpenAI blog, Shopify quote): > "They can complete purchases on the merchant's online store through an in-app browser, so everything happens seamlessly, with the merchant's brand front and center."
- Excerpt (Shopify help, via WebFetch quote extraction): > "ChatGPT users complete their purchase on your online store checkout in a ChatGPT in-app browser"
- Excerpt (Shopify help, via WebFetch quote extraction): > "Your store must sell to customers in the United States, however, your store can be based outside the United States."
- Excerpt (Shopify help, via WebFetch quote extraction): > "There are no fees associated with selling in ChatGPT. You pay only your standard payment processing fees."
- Establishes: The largest merchant path needs no OpenAI feed.
- Limitations: The Shopify excerpts came through WebFetch quote extraction, not a raw file.

### B-15 A feed is not required to appear in ChatGPT product results
- Claim: OpenAI says merchants do not need a feed if ChatGPT crawls the site. Feeds add control and freshness.
- Classification: VERIFIED FACT
- Source: https://chatgpt.com/merchants (FAQ); Shopping with ChatGPT Search — OpenAI Help Center — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- Published/updated: merchants page not stated; help article "Updated: 2 days ago" as rendered 2026-10-30 (≈ 2026-10-28)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Do I need a product feed if ChatGPT already crawls my site?\n\nNo, but feeds give you greater control over how your products appear, helping ensure more accurate and up-to-date information."
- Excerpt (help): > "Structured metadata from first-party and third-party providers (e.g., price, product description) and other third-party content."
- Establishes: Product results draw on crawl, third-party providers and first-party feeds.
- Limitations: The source mix and weighting are not disclosed.

### B-16 Product Feed Spec (Stable): delivery, formats, cadence, retention
- Claim: Feeds are full snapshots pushed by SFTP. Parquet is preferred. Cadence is at least daily. Missing products persist up to 14 days.
- Classification: VERIFIED FACT
- Source: File upload Overview — OpenAI Developers — https://developers.openai.com/commerce/specs/file-upload/overview.md (in llms-full.txt)
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "| Delivery model     | Push feeds to OpenAI via SFTP."
- Excerpt: > "| Formats            | Prefer `parquet` (ideally with `ztsd` compression). `jsonl.gz`, `csv.gz`, and `tsv.gz` are also supported."
- Excerpt: > "- **Full snapshot feed**: a complete catalog export treated as the source of truth.\n- **Recommended cadence**: at least daily."
- Excerpt: > "A product is not deleted immediately when missing from a processed snapshot.\nOpenAI retains its most recently processed record for up to 14 days."
- Excerpt: > "| Shard sizing       | Up to 500k items per shard is recommended; target shard files under ~500MB"
- Establishes: Ingestion mechanics.
- Limitations: "ztsd" is sic in source (presumably zstd). The merchants FAQ also cites "SFTP, APIs, and leading commerce platforms and feed providers". The Stable spec documents only SFTP for product upload. The API is read-only for products and read/upsert for promotions.

### B-17 Product Feed Spec (Stable): nine required fields; one row per item/variant; defaults
- Claim: The Stable spec requires nine fields per row. Search defaults on, checkout off, Ads off.
- Classification: VERIFIED FACT
- Source: Products (file upload) — OpenAI Developers — https://developers.openai.com/commerce/specs/file-upload/products.md
- Published/updated: not stated. The page labels this schema "Stable". A "Draft" view exists "for planning and feedback only".
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Submit one row per purchasable item or variant. Include the nine required\nfields in [Basic product data](#basic-product-data), then add the optional data\nthat describes your products. Ads and checkout have separate requirements."
- Excerpt: > "This JSONL record describes one item. Search defaults to enabled and checkout\nto disabled. Ads defaults to disabled unless your feed has an Ads default configured."
- Excerpt (HTML view selector): > "Use Stable for supported file upload integrations. This schema is expected\n    to remain the supported file upload path for the foreseeable future."
- Establishes: Spec version label = "Stable" (no number or date). The full field table is in §3.
- Limitations: Draft content was not captured; see §5.

### B-18 Eligibility flags: `is_eligible_search` / `is_eligible_checkout` (aliases `enable_search` / `enable_checkout`)
- Claim: `enable_search`/`enable_checkout` are now legacy aliases. Search eligibility does not guarantee display. Checkout needs separate onboarding.
- Classification: VERIFIED FACT
- Source: https://developers.openai.com/commerce/specs/file-upload/products.md
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "`true` enables search eligibility; `false` disables it and checkout eligibility. Omitted or empty: `true`. Eligibility does not guarantee display."
- Excerpt: > "`true` opts in only when search eligibility is also `true` and checkout is enabled for the integration. Omitted, empty, or `false`: disabled. Search set to `false` overrides this flag."
- Excerpt: > "Existing aliases remain accepted: `id` or `sku` for `item_id`, `item_group_id`\nfor `group_id`, `enable_search` for `is_eligible_search`, `enable_checkout` for\n`is_eligible_checkout`, `is_eligible_ads` for `is_ads_eligible`, and\n`return_window` for `return_deadline_in_days`."
- Excerpt: > "Checkout requires a separately enabled integration. Setting an eligibility flag\ndoes not complete checkout onboarding."
- Establishes: Flag semantics and the rename.
- Limitations: The spec says "the `enable_` flags win over their `is_eligible_` names". New feeds that send both may be surprised.

### B-19 Ranking-relevant fields in the current spec: reviews yes; popularity / return-rate no
- Claim: The current OpenAI spec carries `review_count`, `star_rating`, and setup-gated store ratings. Return policy fields exist. No popularity or return-rate field exists. The old `/commerce/specs/feed` URL redirects to the new spec.
- Classification: VERIFIED FACT (field existence; redirect). Use of these fields in ranking: UNVERIFIED HYPOTHESIS.
- Source: https://developers.openai.com/commerce/specs/file-upload/products.md ; HTTP 301 from https://developers.openai.com/commerce/specs/feed to https://developers.openai.com/commerce/specs/file-upload/products
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Raw review entries and question-and-answer lists are not part of this discovery\ncontract. Store aggregates have a separate scope and require the setup in the\nnext section."
- Excerpt: > "These optional fields require an integration configured to carry them. Confirm\nsupport during onboarding before relying on them; adding these columns alone\nto a standard OpenAI-format upload does not enable them."
- Establishes: The current field inventory. A `grep` of the full commerce export for `popularity_score`, `return_rate` and `q_and_a` returned nothing.
- Limitations: The 2025 field list could not be re-fetched (Wayback blocked). Its supersession is shown by the 301 redirect and absent fields only.

### B-20 OpenAI doc claim: recommended attributes "improve ranking" (likely stale wording)
- Claim: The Key concepts guide says reviews and "performance signals" improve ranking. It also says feeds are "CSV or JSON".
- Classification: VERIFIED FACT (statement exists). That the wording predates the current spec is an EVIDENCE-BASED INFERENCE.
- Source: Key concepts — OpenAI Developers — https://developers.openai.com/commerce/guides/key-concepts.md
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Required fields ensure correct display of price and availability, while recommended attributes—like rich media, reviews, and performance signals—improve ranking, relevance, and user trust."
- Excerpt: > "Merchants provide a secure, regularly refreshed feed (CSV or JSON) containing key details such as identifiers, descriptions, pricing, inventory, media, and fulfillment options."
- Establishes: OpenAI's only explicit doc statement linking feed attributes to ranking.
- Limitations: The current spec has no "performance signals" field and prefers parquet. The page also opens "Supporting Instant Checkout in ChatGPT requires a merchant to implement three flows." Both point to unrevised 2025 text.

### B-21 Merchants page: richer data → "better placement in results"; matching uses preferences and past interactions
- Claim: OpenAI markets feeds as improving placement and personalized matching.
- Classification: VERIFIED FACT (statement). The mechanism is not described.
- Source: https://chatgpt.com/merchants
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Get better placement in results\n\nRicher data helps your products surface with more accurate information when shoppers compare options."
- Excerpt: > "ChatGPT helps match your products to people based on shopper preferences and past interactions."
- Excerpt: > "Make more of your catalog available to appear across ChatGPT results."
- Establishes: The vendor claim of a feed–placement link.
- Limitations: Marketing copy. The "placement" sentence ties benefit to "more accurate information", not to a ranking boost.

### B-22 Market scope in the feed: US default; format represents US, CA, MX
- Claim: Standard uploads target the US. Other markets need OpenAI-confirmed setup.
- Classification: VERIFIED FACT
- Source: https://developers.openai.com/commerce/specs/file-upload/products.md
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "The standard OpenAI-format upload currently targets the US. Row-level market\ncolumns do not change that default. Use additional markets only after OpenAI\nconfirms the integration and its allowed countries and currencies."
- Excerpt: > "the shared format currently represents `US`, `CA`, and `MX`. Standard uploads use `[\"US\"]` regardless of this column."
- Establishes: Discovery feeds are US-first, matching B-03.
- Limitations: Whether CA/MX are live for shopping is not stated.

### B-23 One feed schema now serves organic discovery, checkout and Ads; organic results are stated to be ad-independent
- Claim: The same product file powers Ads via `is_ads_eligible`, independent of search eligibility. OpenAI states product results are not ads.
- Classification: VERIFIED FACT
- Source: https://developers.openai.com/commerce/specs/file-upload/products.md ; Product Feeds (Ads) — https://developers.openai.com/ads/product-feeds.md ; https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search ; A milestone in expanding access to AI — OpenAI — https://openai.com/index/expanding-access-to-ai-with-chatgpt-ads/
- Published/updated: Ads blog 2026-08-31; others not stated / ≈2026-10-28
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (spec): > "Set `true` for products Ads should process. `false` explicitly opts out in the OpenAI format. Omitted or empty: disabled unless a feed-level Ads default applies. Independent of search eligibility."
- Excerpt (Ads guide): > "Use product feeds to create ads from your catalog."
- Excerpt (help): > "Product results are selected independently by ChatGPT and are not ads, nor influenced by any OpenAI partnerships. Ads are separate from product results, and you can learn more about ads in ChatGPT."
- Excerpt (Ads blog): > "Ads in ChatGPT are always clearly labeled and separate from ChatGPT’s answers. Advertising does not influence the answers ChatGPT provides."
- Establishes: Ads and organic share a schema but are declared separate.
- Limitations: The separation is a policy statement and cannot be externally verified.

### B-24 2025 ranking statement: Instant Checkout enablement WAS a merchant-ordering factor
- Claim: In 2025, OpenAI listed Instant Checkout enablement among merchant-ranking factors. It also said Instant Checkout items were not preferred in product results.
- Classification: VERIFIED FACT (historical statement)
- Source: https://openai.com/index/buy-it-in-chatgpt/ ; release notes (September 29, 2025 entry) — https://help.openai.com/en/articles/6825453-chatgpt-release-notes
- Published/updated: 2025-09-29
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Product results are organic and unsponsored, ranked purely on relevance to the user."
- Excerpt: > "Instant Checkout items are not preferred in product results. When ranking multiple merchants that sell the same product, ChatGPT considers factors like availability, price, quality, whether a merchant is the primary seller, and whether Instant Checkout is enabled, to optimize the user experience."
- Excerpt (release notes): > "Choose an item and ChatGPT shows where to buy, ranking merchants by factors like inventory, price, quality, primary seller status, and Instant Checkout availability."
- Establishes: Two levels existed: product results (no checkout preference) and merchant list (checkout a factor).
- Limitations: Superseded by B-25. The blog was not annotated.

### B-25 Current ranking statement: merchants ordered by availability, price, quality, maker/primary seller — Instant Checkout no longer listed
- Claim: The current help article lists four merchant-ranking factors. It omits Instant Checkout and anticipates more personalization.
- Classification: VERIFIED FACT
- Source: Shopping with ChatGPT Search — OpenAI Help Center — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- Published/updated: "Updated: 2 days ago" as rendered 2026-10-30 (≈ 2026-10-28)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "When you select a product, ChatGPT may show a list of merchants offering it. This list is generated by ChatGPT based on merchant and product metadata from third-party providers or directly from the merchants themselves. Merchants are ranked based on factors like availability, price, quality, and whether they are the maker or primary seller of that item. We expect this to evolve as we continue to improve the shopping experience, such as by personalizing merchant rankings even more to user preferences."
- Excerpt: > "Prices shown in ChatGPT’s initial response typically reflect the price from the first merchant listed, which may not be the lowest available price. ChatGPT works to highlight the lowest priced option it is aware of in the product detail page and merchant rankings. When more than one merchant offers the product, that option may have a “Best price” label."
- Establishes: Today's authoritative answer to research question 5.
- Limitations: "factors like" means the list is non-exhaustive. Weights are not disclosed.

### B-26 Current product-selection statement (carousel)
- Claim: Product inclusion depends on perceived relevance to intent plus user context and structured metadata.
- Classification: VERIFIED FACT
- Source: https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- Published/updated: ≈ 2026-10-28
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "A product appears in the carousel when ChatGPT perceives it to be relevant to your intent. It considers your query and context (such as Memory or Custom instructions)."
- Excerpt: > "Keep in mind that not all available products will necessarily be shown (there are a lot of dog costumes out there)."
- Excerpt: > "ChatGPT may generate simplified product titles and descriptions based on information it receives from third-party providers to make results easier to read, since merchants often use varying titles and descriptions for the same product."
- Establishes: Personal context affects product inclusion. Displayed titles may be model-rewritten.
- Limitations: Agent A's scope likely covers this in more depth.

### B-27 Merchant onboarding: application form, waitlist, no published approval criteria
- Claim: Merchants apply through a form at chatgpt.com/merchants. Applicants join a waitlist. The form asks for country, website, categories and SKU count. A self-serve portal is planned.
- Classification: VERIFIED FACT
- Source: https://chatgpt.com/merchants ; Get Started — https://developers.openai.com/commerce/guides/get-started.md
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (Get Started): > "Onboarding product feeds in ChatGPT is currently available to approved\n  partners. To apply for access, fill out this form \n  [here](https://chatgpt.com/merchants)"
- Excerpt (merchants): > "Merchants can apply to share product data and participate in shopping experiences in ChatGPT, including integrating your feed so your products can appear in results."
- Excerpt (merchants FAQ): > "We’re accelerating onboarding of partners, and aim to have a self-service merchant portal later this year."
- Establishes: Form fields seen: First name, Last name, Work title, LinkedIn, Work email, Company, Headquarter country, merchant website, Primary Product Categories (Arts, Media & Learning; Automotive; Beauty; Fitness, Health & Wellness; Electronics & Appliances; Fashion, Jewelry & Accessories; Home, Garden & Improvement; Baby, Kids & Toys; Pet Care; Food & Beverage; Travel; Other), interest, feed readiness, feed size (0–1M … 100M+).
- Limitations: No approval criteria, SLA or PSP requirement is published. The HQ-country list is global, but shopping is US-only (B-03).

### B-28 Prohibited products (feeds) and prohibited goods (plugins)
- Claim: OpenAI publishes a prohibited-products policy for feeds. It can remove products or ban sellers from being surfaced.
- Classification: VERIFIED FACT
- Source: https://developers.openai.com/commerce/guides/get-started.md ; https://developers.openai.com/plugins/plugin-guidelines.md
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Prohibited products include, but are not limited to, those that involve adult content, age-restricted products (for example, alcohol, nicotine, gambling), harmful or dangerous materials, weapons, prescription-only medications, unlicensed financial products, legally restricted goods, illegal activities, or deceptive practices."
- Excerpt: > "OpenAI may take corrective actions such as removing a product or banning a seller from being surfaced in ChatGPT if these policies are violated."
- Establishes: A policy-level eligibility filter before any ranking.
- Limitations: The plugin list (adult, gambling, Rx, illicit goods, malware/surveillance, extremist merchandise, etc.) is longer than the feed list.

### B-29 Apps SDK → Plugins; App Directory → Plugin Directory (2026-07-09)
- Claim: OpenAI replaced the App Directory with a Plugin Directory. The Apps SDK docs URL now redirects to `/plugins`.
- Classification: VERIFIED FACT
- Source: ChatGPT release notes (July 9, 2026 and December 18, 2025 entries) — https://help.openai.com/en/articles/6825453-chatgpt-release-notes ; HTTP 301 https://developers.openai.com/apps-sdk → https://developers.openai.com/plugins
- Published/updated: 2026-07-09
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "We’re also replacing the App Directory with the Plugin Directory. Existing app connections are unaffected. Plugins can package skills, apps, and app templates for specific workflows, and are available from ChatGPT on web and desktop, including Work and Codex."
- Excerpt (Dec 18, 2025): > "You can now browse and add approved apps in the new app directory."
- Establishes: "Apps in ChatGPT" research should now target the Plugins docs.
- Limitations: The commerce pages (B-02, B-30) still say "apps".

### B-30 Commerce plugins: feed first, then an MCP plugin can open inline for checkout from the product sidebar
- Claim: A "product checkout conversion" plugin contract exists. ChatGPT can open a seller's plugin from the product entity sidebar instead of linking out. It requires a feed first.
- Classification: VERIFIED FACT
- Source: Product checkout conversion spec — OpenAI Developers — https://developers.openai.com/plugins/guides/product-checkout-conversion-spec.md
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Product checkout conversion plugins in ChatGPT are currently in beta and being\n  tested with approved partners."
- Excerpt: > "Once partners provide us with a product feed for search, we can connect their\nMCP servers for bottom-of-funnel conversion actions."
- Excerpt: > "When users search for products, the product entity sidebar can show **Open**\nbuttons for sellers. If a seller has a plugin, ChatGPT can open that plugin\ninline for checkout instead of punching out to an external website."
- Excerpt: > "It doesn't generate a description or use another merchant's description or images."
- Establishes: The concrete 2026 replacement for Instant Checkout: feed → merchant list → "Open" → plugin with `checkout_session` tool (`ui://widget/checkout-session.html`).
- Limitations: Beta; approved partners only. It does not say whether having a plugin changes merchant order.

### B-31 Plugin commerce rules: physical goods only; external checkout default; no ChatGPT-specific surcharges
- Claim: Plugins may sell only physical goods. Default checkout is external. Saved-payment-method checkout is allowed. The payment sheet is private beta.
- Classification: VERIFIED FACT
- Source: https://developers.openai.com/plugins/plugin-guidelines.md ; https://developers.openai.com/plugins/build/monetization.md
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Currently, plugins may conduct commerce only for physical goods. Selling digital products or services—including subscriptions, digital content, tokens, or credits—is not allowed, whether offered directly or indirectly (for example, through freemium upsells)."
- Excerpt: > "Plugins should use external checkout, directing users to complete purchases on your own domain."
- Excerpt: > "Plugins must not apply ChatGPT-specific fees, surcharges, or other pricing that penalizes users for accessing a service through ChatGPT."
- Excerpt: > "Plugin developers can build a checkout flow in optional UI that allows customers to use payment methods already saved with the merchant. This flow can only display saved payment methods and cannot collect new payment method credentials from customers."
- Establishes: Rules for retailer apps today.
- Limitations: None.

### B-32 How plugins are surfaced: tool metadata drives invocation; enhanced distribution is not requestable
- Claim: ChatGPT picks a plugin's tools from metadata. Directory placement and proactive suggestions are discretionary. Feeds are the default merchant path; apps are optional.
- Classification: VERIFIED FACT
- Source: Optimize Metadata — https://developers.openai.com/plugins/guides/optimize-metadata.md ; Remote MCP server review requirements / Plugin guidelines — https://developers.openai.com/plugins/deploy/app-review.md , https://developers.openai.com/plugins/plugin-guidelines.md ; https://chatgpt.com/merchants
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "ChatGPT and Codex decide when to call your tool based on the metadata you\nprovide."
- Excerpt: > "Plugins that demonstrate strong real-world utility and high user satisfaction may be eligible for enhanced distribution opportunities—such as directory placement or proactive suggestions—but few plugins will receive enhanced distribution at publication. Developers cannot request enhanced distribution."
- Excerpt (merchants FAQ): > "Most merchants start with product feeds, which power how products appear in ChatGPT. Apps are optional and are best suited for larger merchants who want more control over the shopping and purchase experience."
- Establishes: Plugin discovery is model-driven tool selection plus editorial distribution.
- Limitations: The selection algorithm is not disclosed.

### B-33 Retailer app example: Walmart in-ChatGPT app (2026-03-24)
- Claim: Walmart launched an in-ChatGPT app with account linking, loyalty and Walmart payments.
- Classification: VERIFIED FACT
- Source: https://openai.com/index/powering-product-discovery-in-chatgpt/
- Published/updated: 2026-03-24
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Today, we are excited to share that Walmart is introducing an in-ChatGPT app experience that takes users from discovery in ChatGPT into a tailored Walmart environment that supports account linking, loyalty and Walmart payments. This new experience is now available in web browsers, with app access in iOS and Android to follow shortly."
- Establishes: A named retailer app.
- Limitations: Other retailer apps were not verified from primary sources in this pass.

### B-34 ACP vs UCP: no OpenAI or ACP-repo statement found; Stripe and Meta sit on both governance bodies
- Claim: No fetched OpenAI page, OpenAI doc export or ACP repo file mentions UCP. The UCP repo does not mention ACP or OpenAI. Stripe (ACP founder) is on UCP's Tech and Governing Councils. Meta joined ACP's TSC and UCP's Tech Council on the same date.
- Classification: VERIFIED FACT (absence in fetched corpus; council memberships). "Stripe hedges across both" is an EVIDENCE-BASED INFERENCE.
- Source: ACP repo clone (grep for `UCP|universal commerce`: 0 hits); OpenAI `commerce/llms-full.txt`, plugins export, Ads feed guide (0 hits); UCP repo clone `docs/documentation/announcements.md` — https://github.com/Universal-Commerce-Protocol/ucp ; Universal Commerce Protocol — Stripe Docs — https://docs.stripe.com/agentic-commerce/protocols/ucp.md ; Sell products through agents — Stripe Docs — https://docs.stripe.com/agentic-commerce/sellers/use-cases/retail.md
- Published/updated: UCP announcements 2026-04-24 and 2026-04-28; UCP repo last commit 2026-10-29; Stripe pages not dated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (UCP): > "The Tech Council has expanded its seats to 16, welcoming five new members:" … "- James Andersen (Meta)" … "- Prasad Wangikar (Stripe)"
- Excerpt (UCP): > "Stripe has joined the UCP Governing Council as a new member, joining existing permanent members Google and Shopify."
- Excerpt (Stripe): > "The [Universal Commerce Protocol](https://ucp.dev) (UCP) is an open standard that lets different participants in commerce transactions interoperate, with support for checkout, identity linking, order tracking, and secure payment token exchange (Stripe is a member of the UCP Tech Council)."
- Excerpt (Stripe retail table): > "| [Use your own checkout](https://docs.stripe.com/agentic-commerce/sellers/use-cases/retail/ucp.md) | Run your own Universal Commerce Protocol checkout and accept payments with the Stripe Payments handler. |"
- Establishes: Research question 7 has no first-party interoperability statement. The maintainer overlap is documented.
- Limitations: OpenAI is not listed on UCP councils in the fetched announcements. None of Stripe's fetched agentic-commerce pages names ACP or ChatGPT.

### B-35 Stripe's own catalog feed (not OpenAI's) includes `popularity_score` and says agents "rank" products
- Claim: Stripe's Agentic Commerce Suite feed has a recommended `popularity_score` and a `disable_checkout` flag. Stripe syndicates it to unnamed agents.
- Classification: VERIFIED FACT (Stripe doc). Any link to ChatGPT ranking: UNVERIFIED HYPOTHESIS.
- Source: Catalogue feed — Stripe Docs — https://docs.stripe.com/agentic-commerce/concepts/catalog-feed.md
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1 (Stripe), but not an OpenAI source
- Excerpt: > "Discovery-only products follow the same feed processing rules as other products. Agents can index, search, and rank them. The only difference is that the purchase action redirects to your site instead of starting an in-agent checkout session."
- Excerpt: > "These fields are optional but recommended. They improve discovery, ranking and personalisation across agentic interfaces."
- Establishes: Ranking-signal fields that OpenAI's spec dropped survive in a feed provider's spec. OpenAI names Stripe as a delivery path (B-13).
- Limitations: Stripe states it converts feeds "to the format each agent requires". OpenAI's spec has no `popularity_score`, so the field likely does not reach ChatGPT as-is (inference).

---

## 3. Product Feed Spec fields (OpenAI file upload, "Stable" view)

Source: https://developers.openai.com/commerce/specs/file-upload/products.md, accessed 2026-10-30. Version label: "Stable" (no number or date). The Requirement column is copied verbatim. Notes are condensed from the spec's description column.

| Field | Requirement (verbatim) | Notes (from spec) |
|---|---|---|
| `item_id` | Required | Stable ID per item/variant; never reuse. Alias `id`/`sku`. |
| `title` | Required | Include selected variant; aim ≤150 chars. |
| `description` | Required | Factual, plain text; aim ≤5,000 chars. |
| `url` | Required | PDP with variant selected; stable. |
| `brand` | Required | As shown on product page. |
| `seller_name` | Required | Seller supplying the offer; required on each row. |
| `image_url` | Required | Direct JPEG/PNG of this variant. |
| `availability` | Required | `in_stock`, `out_of_stock`, `pre_order`, `backorder`, `unknown`; bad value rejects row. |
| `price` | Required | `79.99 USD` format, major units. |
| `is_eligible_search` | Optional | Default `true`; `false` also disables checkout; "Eligibility does not guarantee display." Alias `enable_search`. |
| `group_id` | Conditionally required for variants | Parent listing ID; alias `item_group_id`. |
| `listing_has_variations` | Conditionally required for variants | `true` on every variant row. |
| `variant_dict` | Conditionally required for variants | Option name → value map. |
| `offer_id` | Optional | Stable offer ID; "Never include price in an offer ID." |
| `gtin` | Optional | 8/12/13/14 digits with valid check digit. |
| `mpn` | Optional | Submit with `brand`; don't invent. |
| `condition` | Optional | `new`, `refurbished`, `used`; omitted may be treated as `new`. |
| `product_category` | Optional | Merchant path, `>`-separated. |
| `material` | Optional | Principal materials. |
| `color` | Optional | Selected color. |
| `size` | Optional | Selected size label. |
| `gender` | Optional | `male`, `female`, `unisex`. |
| `age_group` | Optional | `newborn` … `adult`; not a purchase-age restriction. |
| `dimensions` | Optional | Object with ≥2 axes + `unit`; overrides separate fields. |
| `length` / `width` / `height` | Optional | Legacy separate axes; need `dimensions_unit`. |
| `dimensions_unit` | Conditionally required with separate dimensions | `in`, `cm`, `ft`, `m`, `mm`. |
| `weight` | Optional | Net weight; needs `item_weight_unit`. |
| `item_weight_unit` | Conditionally required with `weight` | `g`, `kg`, `oz`, `lb`. |
| `additional_image_urls` | Optional | Array (JSONL) or comma string (CSV). |
| `sale_price` | Optional | Must be > 0 and < `price`, same currency. |
| `seller_url` | Optional | Seller storefront/profile page. |
| `shipping_price` | Optional | Omitted = unknown, not free. |
| `shipping` | Optional; requires feed-specific setup | Tuple `country:region:service_class:price`. |
| `accepts_returns` | Optional | Boolean; policy URL does not set it. |
| `return_deadline_in_days` | Optional | Only with `accepts_returns=true`. Alias `return_window`. |
| `return_policy` | Optional | Public policy URL. |
| `review_count` | Optional | Product reviews only; exclude store reviews. |
| `star_rating` | Optional | 0–5, two decimals; pair with `review_count`. |
| `marketplace_seller` | Conditionally required for third-party marketplace offers; requires setup | Marketplace where checkout occurs. |
| `size_system` | Optional; requires setup | `US`, `UK`, `EU`, … |
| `store_review_count` | Optional; requires setup | Store/seller review count. |
| `store_star_rating` | Optional; requires setup | Store average 0–5. |
| `accepts_exchanges` | Optional; requires setup | Boolean. |
| `is_digital` | Optional; requires setup | Boolean. |
| `target_countries` | Optional; requires market setup | Format represents `US`, `CA`, `MX`; standard uploads use `["US"]`. |
| `store_country` | Optional; requires market setup | Standard uploads use `US`. |
| `is_ads_eligible` | Conditionally required for Ads processing | Independent of search eligibility. Alias `is_eligible_ads`. |
| `ads_metadata` | Optional for Ads | Configured filter keys only. |
| `is_eligible_checkout` | Conditionally required to opt into checkout | Needs search `true` + checkout enabled for integration. Alias `enable_checkout`. |
| `seller_privacy_policy` | Conditionally required for checkout | URL. |
| `seller_tos` | Conditionally required for checkout | URL. |

Accepted formats: `parquet` (preferred), `jsonl.gz`, `csv.gz`, `tsv.gz`; UTF-8. Delivery: SFTP push, full snapshot. Cadence: "at least daily". Retention of missing items: up to 14 days. Legacy `Custom_variant{1,2,3}_category/_option` pairs are still accepted.

Related schemas (not the file format):
- OpenAI Feed API (read): `GET/POST /product_feeds`, `GET /product_feeds/{id}/products`, `GET/PATCH /product_feeds/{id}/promotions`. Product requires `id`, `variants`; Variant requires `id`, `title`.
- ACP 2026-04-17 `schema.feed.json`: same nested Product/Variant model plus `Variant.marketplace`. Paths `/feeds`, `/feeds/{id}`, `/feeds/{id}/products` (incl. `PATCH`).

---

## 4. Contradictions and superseded information

1. **Merchant-ranking factor.** The 2025 blog and 2025-09-29 release notes list "whether Instant Checkout is enabled" (B-24). The current help article omits it (B-25). The 2025 blog has no update note. Treat B-24 as superseded.
2. **Is Instant Checkout gone?** The merchants page says OpenAI is "moving away from a standalone Instant Checkout" and the help article is removed (B-03, B-04). Plugin docs still describe "Instant Checkout, which is currently in beta" for "select marketplace partners" (B-05). Press saying it is "gone" overstates the primary record.
3. **Stale OpenAI commerce guides.** Key concepts still says "Supporting Instant Checkout in ChatGPT requires a merchant to implement three flows". It cites "performance signals" and "CSV or JSON" feeds (B-20). The current spec has no performance-signal fields and prefers parquet (B-16, B-19).
4. **Checkout spec version drift.** OpenAI's Agentic Checkout Spec uses `fulfillment_address` and 2025-09 API-Version examples. ACP deprecated both in 2025-12-12 (B-12). OpenAI's PSP enum includes `braintree`; ACP 2026-04-17 enum has `stripe`, `adyen` (B-11).
5. **Feed API path mismatch.** OpenAI documents `/product_feeds/...` with products read-only (updates via SFTP). ACP 2026-04-17 defines `/feeds/...` with `PATCH /feeds/{id}/products` (B-09, §3).
6. **Fees.** "Merchants pay a small fee on completed purchases" (2025) vs "There are no fees on purchases that start in ChatGPT" (current) (B-06).
7. **Maintainer list.** The ACP README says "maintained by OpenAI and Stripe". MAINTAINERS.md and governance.md add Meta (B-07).
8. **Feed delivery channels.** The merchants FAQ says "SFTP, APIs, and leading commerce platforms and feed providers". The Stable spec documents SFTP only for product upload. The March 2026 post names Salesforce and Stripe (B-13, B-16).
9. **Old feed spec.** `https://developers.openai.com/commerce/specs/feed` now 301-redirects to the file-upload Products spec. 2025-era field names (`enable_search`, `enable_checkout`) survive only as aliases (B-18, B-19).
10. **Rollout wording (minor).** The March 24 blog says "all ChatGPT free, Go, Plus, and Pro users". The release note says "all ChatGPT users this week".

---

## 5. Knowledge gaps

- Which "select marketplace partners" use the beta Instant Checkout / payment sheet today. Whether Etsy in-chat checkout still runs.
- No OpenAI shutdown date for 2025 Instant Checkout merchants (only the 2026-03-24 announcement).
- Weights of merchant-ranking factors. Whether a checkout-capable plugin affects merchant order.
- Whether `review_count`, `star_rating` or store ratings feed ranking. OpenAI states no field-level use.
- Content of the Product Feed Spec "Draft" view. It renders client-side; static HTML and `.md?version=draft` returned Stable text.
- The full 2025 Product Feed Spec field list (e.g. popularity/return-rate fields). Not re-fetchable here.
- Whether OpenAI implements ACP 2026-04-17 (`/feeds`, carts, MCP binding) or only its own `/product_feeds` API.
- OpenAI's position on UCP. No statement found.
- Approval criteria, SLA and timing for merchant applications. The self-serve portal date is only "later this year".
- Whether CA/MX shopping is live; the feed format supports them.
- Press claims not verified in this pass: The Information (shelving report), Forrester ("~30 Shopify merchants live"), CNBC. Not fetched.

---

## 6. Unfetched sources

| URL | Attempt | Result | Alternate used |
|---|---|---|---|
| https://openai.com/index/buy-it-in-chatgpt/ | WebFetch; curl | 403 | In-app browser pane: fetched |
| https://openai.com/index/powering-product-discovery-in-chatgpt/ | curl | 403 (bot challenge page) | In-app browser pane: fetched |
| https://chatgpt.com/merchants | WebFetch | 403 | In-app browser pane: fetched |
| https://help.openai.com/en/articles/12440090-instant-checkout | WebFetch | 403 | Browser pane: page renders "THAT PAGE DOESN'T EXIST" |
| https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search | WebFetch | 403 | Browser pane: fetched |
| https://help.openai.com/en/articles/6825453-chatgpt-release-notes | (not tried via WebFetch) | — | Browser pane: fetched |
| https://web.archive.org/web/2026/https://openai.com/index/buy-it-in-chatgpt/ | WebFetch | "unable to fetch from web.archive.org" | none |
| https://searchengineland.com/chatgpt-instant-checkout-plan-change-471033 | WebFetch | 403 | Adweek and Lumio (Tier 3) used only to locate the primary post |
| https://developers.openai.com/commerce/specs/file-upload/products?version=draft | curl (HTML and .md) | 200, but Draft content not distinguishable | none |
| https://www.cnbc.com/2026/03/24/openai-revamps-shopping-experience-in-chatgpt-after-instant-checkout.html ; https://www.forrester.com/blogs/what-it-means-that-the-leader-in-agentic-commerce-just-pulled-back/ | not fetched | — | — |

---

## 7. Source list

| # | Title | Publisher | URL | Date | Tier | Method |
|---|---|---|---|---|---|---|
| 1 | Buy it in ChatGPT: Instant Checkout and the Agentic Commerce Protocol | OpenAI | https://openai.com/index/buy-it-in-chatgpt/ | 2025-09-29 | 1 | browser pane |
| 2 | Powering Product Discovery in ChatGPT | OpenAI | https://openai.com/index/powering-product-discovery-in-chatgpt/ | 2026-03-24 | 1 | browser pane |
| 3 | A milestone in expanding access to AI (ChatGPT Ads) | OpenAI | https://openai.com/index/expanding-access-to-ai-with-chatgpt-ads/ | 2026-08-31 | 1 | browser pane |
| 4 | Power product discovery in ChatGPT (merchants) | OpenAI | https://chatgpt.com/merchants | not stated | 1 | browser pane |
| 5 | Shopping with ChatGPT Search | OpenAI Help Center | https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search | "Updated: 2 days ago" (≈2026-10-28) | 1 | browser pane |
| 6 | ChatGPT release notes | OpenAI Help Center | https://help.openai.com/en/articles/6825453-chatgpt-release-notes | "Updated: 16 hours ago" | 1 | browser pane |
| 7 | Instant Checkout (removed) | OpenAI Help Center | https://help.openai.com/en/articles/12440090-instant-checkout | n/a | 1 | browser pane |
| 8 | Agentic Commerce — full documentation | OpenAI Developers | https://developers.openai.com/commerce/llms-full.txt (+ /commerce/llms.txt, /commerce/specs/file-upload/products.md, /commerce/guides/get-started.md) | not stated | 1 | curl |
| 9 | Plugins — full documentation | OpenAI Developers | https://developers.openai.com/apps-sdk/llms-full.txt (serves Plugins docs) | not stated | 1 | curl |
| 10 | Product Feeds (Ads) | OpenAI Developers | https://developers.openai.com/ads/product-feeds.md | not stated | 1 | curl |
| 11 | ACP README, MAINTAINERS, governance, changelogs, RFCs, specs | agentic-commerce-protocol (GitHub) | https://github.com/agentic-commerce-protocol/agentic-commerce-protocol | last commit 2026-07-18 | 1 | raw files, git clone, GitHub API |
| 12 | Agentic Commerce Protocol (site) | Stripe/OpenAI | https://www.agenticcommerce.dev ; https://www.agenticcommerce.dev/docs | not stated | 1 | WebFetch |
| 13 | Agentic commerce; UCP; Catalogue feed; Retail; How ACS works | Stripe Docs | https://docs.stripe.com/agentic-commerce.md ; …/protocols/ucp.md ; …/concepts/catalog-feed.md ; …/sellers/use-cases/retail.md ; …/retail/how-it-works.md | not stated | 1 | curl |
| 14 | ChatGPT (Agentic storefronts) | Shopify Help Center | https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/chatgpt | not stated | 1 (partner) | WebFetch |
| 15 | UCP repo (announcements) | Universal-Commerce-Protocol (GitHub) | https://github.com/Universal-Commerce-Protocol/ucp | last commit 2026-10-29 | 1 | git clone |
| 16 | ucp.dev home | UCP Authors | https://ucp.dev | not stated | 1 | WebFetch |
| 17 | OpenAI's ChatGPT is making a big change to its commerce strategy | Adweek | https://www.adweek.com/commerce/openais-chatgpt-is-making-a-big-change-to-its-commerce-strategy/ | not stated on page | 3 | WebFetch |
| 18 | ChatGPT product discovery: how OpenAI killed Instant Checkout | Lumio (blog) | https://www.heylumio.ai/blog/openai-product-discovery-chatgpt | 2026-04-11 (upd. 2026-05-01) | 3 | WebFetch (locator only) |
