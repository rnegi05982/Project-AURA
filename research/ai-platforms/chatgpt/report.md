# ChatGPT — how it discovers, retrieves and recommends products

- **Research question:** How does ChatGPT discover, retrieve, and recommend products from different e-commerce sources, including Amazon, Shopify stores, Flipkart, and independent merchant websites?
- **Status as of:** 2026-10-30. All sources accessed that day.
- **Evidence:** every claim cites a registry ID. Registry: `evidence/registry/{cgpt,acp,shop,mkt,res}.md`. Raw captures: `notes/`.
- **Reading rule:** "documented" means OpenAI or a partner states it (VERIFIED FACT). "Inference" means it follows from documented facts but no one states it. "Hypothesis" means untested.

---

## 1. Answer

- ChatGPT gets product data from several paths at once. Three are first-party merchant data: Shopify Catalog, Etsy's catalog, and ACP product feeds [CGPT-017, CGPT-018]. Others are third-party structured metadata, web crawl by OAI-SearchBot, partner search providers (Microsoft and Shopify are named), and public reviews [CGPT-002, CGPT-004, CGPT-012, CGPT-013].
- The model's own pre-search knowledge is a documented input to product selection [CGPT-012].
- Product selection is model-judged relevance to the user's intent, using the query plus Memory and Custom instructions. No fixed formula or weights are published [CGPT-011].
- When one product has several sellers, ChatGPT ranks merchants by "factors like availability, price, quality, and whether they are the maker or primary seller" [CGPT-015].
- Paying OpenAI does not buy organic placement, per OpenAI. Ads sit in a separate, labeled unit below the answer [CGPT-010, CGPT-042, CGPT-043].
- Since 2026-03-24 ChatGPT is a discovery surface. Purchases complete on the merchant's own site or app [CGPT-021, CGPT-022, SHOP-002].
- ChatGPT's shopping results are documented as live for US users only [CGPT-022]. No OpenAI source documents shopping results for India [CGPT-046].
- A Shopify store that sells to US buyers is already syndicated to ChatGPT by default through Shopify Catalog [SHOP-001, SHOP-003, CGPT-017].
- Amazon blocks all three OpenAI agents in robots.txt. Flipkart blocks none [MKT-001, MKT-008].
- Retrieval internals (keyword vs semantic vs vector search, index composition, merge logic) are undocumented. Section 10 lists the gaps.

Mechanism, in one line: shopping intent → query rewrite (memory, location) → candidates from catalogs, feeds, provider metadata and crawled pages → policy filter → model-judged selection → merchant list ranked by availability, price, quality, maker/primary seller → hand-off to the merchant's checkout.

---

## 2. Timeline: what changed (read this before trusting any 2025 source)

Many 2025 pages still read as current but are outdated. OpenAI's own 2025 launch post carries no update note [CGPT-016].

| Date | Change | Evidence |
|---|---|---|
| 2024-10-31 | ChatGPT search launches; uses third-party search providers plus partner content | CGPT-001 |
| 2025-09-29 | Instant Checkout + ACP launch (US, Etsy first). Instant Checkout enablement is a merchant-ranking factor | CGPT-016, ACP-001 |
| 2025-11-12 | Amazon adds OAI-SearchBot and ChatGPT-User blocks | MKT-002 |
| 2025-11-24 | Shopping research launches (GPT-5 mini variant) | CGPT-033 |
| 2026-02-09 | Ads test starts in the US (Free and Go plans) | CGPT-043 |
| 2026-03-24 | OpenAI drops standalone Instant Checkout; ACP extended to discovery feeds; Shopify ChatGPT channel goes live; Walmart app | CGPT-018, CGPT-021, SHOP-012, CGPT-041 |
| 2026-04-17 | ACP version 2026-04-17 (push Feed API, carts, MCP binding) | ACP-002, ACP-003 |
| by 2026-05-28 | "Instant Checkout enabled" removed from merchant-ranking factors | CGPT-016 |
| 2026-05 | Shopify rate-limits unsigned bots (Web Bot Auth) | SHOP-019 |
| 2026-07-09 | Apps renamed Plugins; agent mode replaced by ChatGPT Work's cloud browser; Atlas deprecated | CGPT-038, CGPT-036 |
| after 2026-08-05 | Shopping research help article redirects to the general shopping article | CGPT-035 |
| 2026-10-21 | Ads in 89 countries (advertiser side) | CGPT-043 |

---

## 3. Discovery architecture

### 3.1 Product data paths into ChatGPT

| # | Path | Who it covers | How a merchant joins | Evidence |
|---|---|---|---|---|
| P1 | Shopify Catalog (Shopify's cross-merchant product index) | Eligible Shopify stores that sell to US buyers | Default-on; nothing to do | CGPT-017, SHOP-001, SHOP-003 |
| P2 | Etsy catalog integration | Etsy sellers | Default | CGPT-017 |
| P3 | ACP product feed, direct to OpenAI | Approved partners (e.g. Target, Best Buy, Wayfair) | Apply at chatgpt.com/merchants; waitlist | CGPT-018, CGPT-025 |
| P4 | ACP feed via a provider | Salesforce, Stripe ACS, Feedonomics clients | Opt-in through the provider | CGPT-018, MKT-017, MKT-019, MKT-020 |
| P5 | Third-party structured metadata | Unnamed providers; supplies prices, descriptions, merchant lists | Not documented | CGPT-012, CGPT-014, CGPT-015 |
| P6 | Web search and crawl | Any site OAI-SearchBot can reach; partner providers Microsoft and Shopify | Allow OAI-SearchBot; no feed needed | CGPT-002, CGPT-004, CGPT-019 |
| P7 | Model knowledge | Brands the model already knows | Not controllable | CGPT-012, RES-015 |
| P8 | Public reviews | Review text on public websites | Not documented | CGPT-013 |

Terms used above:
- ACP (Agentic Commerce Protocol): open spec for product feeds, agent checkout and delegated payment, maintained by OpenAI and Stripe, with Meta on its steering committee [ACP-001].
- OAI-SearchBot: OpenAI's crawler for ChatGPT search. Distinct from GPTBot (training) and ChatGPT-User (user-triggered fetches) [CGPT-006, CGPT-007, CGPT-008].
- Product feed: a file or API push of a merchant's full catalog (one row per variant) to the AI platform.

### 3.2 Request flow

1. **Intent detection.** When a question suggests shopping intent, ChatGPT can show product options with images, details and links [CGPT-011 source].
2. **Query rewriting.** ChatGPT rewrites the question into one or more targeted queries for partner search providers. It may add saved memories and approximate location [CGPT-002, CGPT-003].
3. **Candidate gathering.** Inputs: structured metadata from first- and third-party providers, other third-party content, and the model's pre-search response [CGPT-012]. Crawled pages also count: a feed is optional if ChatGPT already crawls the site [CGPT-019].
4. **Policy filter.** OpenAI safety standards and prohibited-product rules remove items or sellers [CGPT-012, CGPT-026].
5. **Selection.** A product appears in the carousel when ChatGPT "perceives it to be relevant to your intent". Factor weight shifts with the query: a stated budget makes price dominant [CGPT-011].
6. **Presentation.** ChatGPT may rewrite titles and descriptions, add generated labels ("Budget-friendly"), and summarize public reviews [CGPT-013].
7. **Merchant list.** Selecting a product shows merchants ranked by availability, price, quality, maker/primary-seller status. The headline price is the first merchant's price. A "Best price" label marks the lowest known price [CGPT-014, CGPT-015].
8. **Hand-off.** The user buys on the merchant's site or app. For Shopify, checkout opens in an in-app browser (mobile) or a new tab (web) [CGPT-022, SHOP-002]. Approved partners can have a plugin open inline from the product sidebar [CGPT-039].

### 3.3 Other surfaces

- **Plugins (formerly apps).** MCP-based integrations that ChatGPT calls based on their metadata. Walmart, Target, Etsy, Shopee and Allegro run them [CGPT-038, CGPT-040, CGPT-041, MKT-010, MKT-011, MKT-012]. OpenAI says plugins suit larger merchants; most start with feeds [CGPT-040].
- **Cloud browser (ChatGPT Work).** Replaced agent mode. Paid plans only. Signs requests with Web Bot Auth (HTTP message signatures that let a site verify the agent) [CGPT-036]. How it finds or ranks products is undocumented.
- **Site tools.** ChatGPT's implementation of WebMCP (a proposed standard for websites to expose actions to browser agents), desktop app only [CGPT-037].
- **Shopping research.** Launched 2025-11-24, read retailer pages directly and skipped sites that block automation [CGPT-033, CGPT-034]. Its help page now redirects; current status is unknown [CGPT-035].
- **Ads.** One labeled unit below the answer, Free and Go plans, ranked by relevance plus bids [CGPT-043]. Ads Manager product feeds feed ads only, not organic results [CGPT-044].

---

## 4. Retrieval

Documented:
- Query rewriting into targeted sub-queries [CGPT-002].
- Memory and approximate location shape the rewrite [CGPT-003]. A 2026-06-24 model update uses location for shopping queries [CGPT-045].
- Partner search providers: Microsoft and Shopify are the only ones named [CGPT-002]. Shopify acting as a *search provider* is distinct from Shopify Catalog as a data feed.
- OpenAI maintains its own web index, documented for Codex/Work [CGPT-005].

Not documented: keyword vs semantic vs vector retrieval, embedding models, index composition, how provider results merge with feeds, how attribute constraints (material, size, price cap) are parsed.

Independent evidence (API, not the consumer app):
- ChatGPT's API engine splits a question into keyword-style sub-queries, and adds a brand the user did not name to 28% of them [RES-014].
- Every cited page was first retrieved by its own search. Retrieval explains far more citation variance than page features [RES-012].
- Retrieved pages almost never match Google's or Bing's top 10 for the same sub-queries [RES-013]. Tier 3 overlap studies disagree with each other [RES-020].
- A vendor study reports 83% of carousel products match Google Shopping's top 40 [RES-021]. This conflicts with OpenAI naming only Microsoft and Shopify. UNVERIFIED HYPOTHESIS until tested.

---

## 5. Ranking and recommendation

### 5.1 Two documented ranking levels

| Level | What is ranked | Documented factors | Evidence |
|---|---|---|---|
| Product selection | Which products enter the carousel | Relevance to intent; query + Memory + Custom instructions; e.g. "available options, price, reviews, and ease of use"; weights vary by query | CGPT-011, CGPT-012 |
| Merchant list | Which seller is listed first for one product | "availability, price, quality, and whether they are the maker or primary seller" | CGPT-015 |

- "Quality" and "primary seller" are undefined [CGPT-015, MKT-013].
- In 2025 the merchant list also used "whether Instant Checkout is enabled". That factor is gone [CGPT-016].
- OpenAI expects to personalize merchant rankings "even more" [CGPT-015]. The merchant page cites "past interactions" [CGPT-020].

### 5.2 Feed data and ranking

- OpenAI's merchant page: richer data helps products surface "with more accurate information" [CGPT-020].
- One OpenAI guide says recommended attributes "improve ranking". The page is likely stale: it still describes Instant Checkout and a "performance signals" field the current spec lacks [CGPT-032, CGPT-030].
- The current feed spec: "Eligibility does not guarantee display" [CGPT-029].
- The ACP feed RFC puts ranking out of scope [ACP-004].
- Conclusion (EVIDENCE-BASED INFERENCE): a feed or catalog makes a product eligible and keeps its facts current. No source shows that any field raises rank.

### 5.3 What independent research adds

All of it measures API models or mock stores, not ChatGPT's production shopping ranker.

- **Price and ratings:** agents prefer cheaper, better-rated, more-reviewed items, and react to ratings far more than humans do [RES-003, RES-006].
- **Brand priors:** OpenAI models favor known brands and reorder identical products by brand name. Brand acts mainly as a tie-breaker when specs differ [RES-007, RES-015, RES-017]. LLMs favor global over local brands [RES-018].
- **Position:** large and model-specific; flips between model versions [RES-001, RES-004].
- **Content edits:** contested. GEO reports up to 40% gains [RES-009]. C-SEO Bench finds most methods ineffective [RES-010]. Page features explain 2.8% of citation variance in one 2026 API study; schema.org markup showed no lift [RES-012].
- **Volatility:** same-day repeats share 15% of cited pages (API) and Jaccard 0.233 of sources (consumer UI) [RES-014, RES-016]. A vendor reports ~95% of carousel titles appear in under 30% of runs [RES-022]. Inclusion frequency over many runs is the measurable quantity. Single-run position is noise.

### 5.4 Organic vs paid

- OpenAI: product results are "not ads, nor influenced by any OpenAI partnerships" [CGPT-010].
- Ads run on separate systems and advertisers cannot rank responses [CGPT-042].
- Policy rules do affect which links appear: an Indian court order records OpenAI "relying on the USTR" Notorious Markets list (a US government list of marketplaces linked to counterfeiting or piracy), and ChatGPT linking sellers' own sites instead of IndiaMART [MKT-015].

---

## 6. Prices, availability, images, URLs

- Prices come from third-party providers [CGPT-014]. Updates can lag; the lag is not stated.
- Direct feeds: at least daily full snapshots; a missing product survives up to 14 days [CGPT-027].
- Shopify Catalog: "continuously updates" price and inventory; latency not stated [SHOP-006].
- Feed requires a direct image URL per variant and a product URL with the variant selected [CGPT-028].
- OpenAI tells users to confirm price, availability and policies with the merchant [CGPT-047].

---

## 7. Integrations and protocols

### 7.1 ACP
- Founded by OpenAI and Stripe; Meta on the TSC; Apache 2.0; beta [ACP-001].
- Latest version 2026-04-17. It adds a push Feed API: merchants push catalogs to agents [ACP-002, ACP-003].
- In ChatGPT, ACP's role is now discovery intake [CGPT-018]. OpenAI's checkout spec page lags the repo [ACP-005].
- Ranking is out of scope [ACP-004].

### 7.2 OpenAI product feed spec (Stable)
- Nine required fields: `item_id`, `title`, `description`, `url`, `brand`, `seller_name`, `image_url`, `availability`, `price` [CGPT-028].
- Optional: `gtin`, `mpn`, `material`, `dimensions`, `review_count`, `star_rating`, return fields, and more. Full table: `notes/b-openai-commerce-protocols-and-feeds.md` §3.
- SFTP push; parquet preferred; daily; US by default [CGPT-027, CGPT-031].
- Gated: approved partners only [CGPT-025].

### 7.3 UCP and MCP
- UCP (Universal Commerce Protocol) is co-developed by Google and Shopify. OpenAI is not listed. No source says ChatGPT uses UCP [SHOP-014, ACP-006].
- Shopify Catalog's schema is UCP-shaped [SHOP-007], so Catalog data may reach ChatGPT in UCP form. UNVERIFIED: the wire format between Shopify and OpenAI is undocumented.
- MCP appears in three places: commerce plugins connect through the seller's MCP server [CGPT-039]; ACP 2026-04-17 has an MCP binding for checkout [ACP-003]; Shopify exposes Catalog MCP endpoints [SHOP-015]. None is documented as a ChatGPT discovery input.

---

## 8. Structured data

- No OpenAI source mentions schema.org, JSON-LD or Open Graph.
- Shopify's `structured_data` filter outputs `Product` or `ProductGroup` JSON-LD. Default themes include GTIN, SKU and offers, but no ratings, shipping or return policy [SHOP-021, SHOP-022].
- One 2026 API study found schema.org markup had slightly lower citation odds, not higher [RES-012].
- Classification: "ChatGPT reads product JSON-LD" is an UNVERIFIED HYPOTHESIS. For Shopify stores the structured path into ChatGPT is Catalog, not page markup [SHOP-018].

---

## 9. How each source type reaches ChatGPT

| Source | OAI-SearchBot crawl | Catalog / feed | Plugin | Notes | Evidence |
|---|---|---|---|---|---|
| Amazon (.com, .in) | Blocked (since 2025-11-12) | None on record | None | Pages excluded from search answers except navigational links, per OpenAI's rule. Vendor data shows Amazon nearly absent | MKT-001, MKT-002, CGPT-006, RES-022 |
| Flipkart | Allowed (no OpenAI group) | None on record | None | Shopping results not documented for India | MKT-008, CGPT-046 |
| Shopify store selling to US | Allowed by default robots.txt | Shopify Catalog, default-on | Optional | Catalog continues even if crawl is blocked | SHOP-001, SHOP-016, SHOP-018 |
| Shopify store selling only in India | Allowed by default | Not eligible for ChatGPT channel | — | Discovery only via crawl/search | SHOP-003 |
| Independent non-Shopify store | Depends on its robots.txt | Opt-in via Stripe ACS, Feedonomics, Salesforce, or waitlist | Optional | Feed not required if crawled | CGPT-019, MKT-017, MKT-021 |
| Walmart | Allowed | — | Yes (2026-03-24) | Agent terms and MCP gateway (2026-10-21) | MKT-009 |
| Etsy | Allowed | Integrated | Yes (beta) | Says ChatGPT "works well as a discovery channel" | MKT-010 |
| Target | Allowed | ACP discovery feed | Yes | Also tested ads | MKT-011 |
| eBay | Search pages explicitly allowed; GPTBot blocked | None found | None | Bans buy-for-me agents at checkout | MKT-005 |

### The brief's use case: "premium ceramic coffee mug under ₹1,000"

- Shopping results are documented for US users only [CGPT-022]. The feed format targets the US [CGPT-031]. The Shopify ChatGPT channel requires selling to US buyers [SHOP-003].
- EVIDENCE-BASED INFERENCE: an India-located user asking this query is unlikely to get a carousel fed by Shopify Catalog or ACP feeds. The answer more likely comes from web search with citations.
- On that path, crawl access matters. Amazon.in pages are excluded from search answers except navigational links [MKT-001, CGPT-006]. Flipkart pages are crawlable [MKT-008]. Model brand priors favor known brands [RES-015, RES-018].
- This is UNVERIFIED for the consumer app. Test case: `experiments/test-cases/chatgpt-coffee-mug.md`.

---

## 10. Knowledge gaps

1. Which third-party providers supply product metadata, prices and merchant lists [CGPT-012, CGPT-014].
2. Which queries go to Microsoft, Shopify, OpenAI's own index, or Google (if any), and how results merge [CGPT-002, RES-019, RES-021].
3. Retrieval method: keyword, semantic, vector, or hybrid.
4. Weights of any ranking factor; definitions of "quality" and "primary seller" [CGPT-015].
5. Whether product carousels require OAI-SearchBot access, a feed, or either [CGPT-019].
6. Precedence when feed data and crawled data disagree [SHOP-011].
7. Wire format between Shopify Catalog and ChatGPT (ACP, UCP/MCP, or private) [SHOP-014].
8. Whether ChatGPT uses Shopify Catalog's ranking order, inferred fields or ratings [SHOP-009, SHOP-015].
9. Whether ChatGPT reads JSON-LD, `/llms.txt`, `/agents.md` or `/.well-known/ucp` [SHOP-020].
10. Whether consumer product carousels appear in India at all [CGPT-046].
11. Current status of shopping research [CGPT-035].
12. Which model runs ChatGPT search and shopping today (GPT-4o and GPT-5-era models were retired) [CGPT-001].
13. Whether OpenAI crawlers sign with Web Bot Auth or get Shopify rate-limit exemptions [SHOP-019].
14. How the cloud browser finds or ranks products [CGPT-036].

---

## 11. Contradictions and outdated sources

| Topic | Conflict | Resolution |
|---|---|---|
| Merchant ranking | 2025 post lists Instant Checkout as a factor; current help omits it | Current help wins [CGPT-015, CGPT-016] |
| Instant Checkout | Merchant page: "moving away"; plugin docs: beta for select marketplaces | Both true: standalone retired, narrow beta remains [CGPT-021, CGPT-023] |
| Fees | 2025 "small fee"; 2026 "no fees" | 2026 wins [CGPT-024]; Shopify terms reserve future fees [SHOP-004] |
| Feed → ranking | Guide says attributes "improve ranking"; spec says eligibility ≠ display; ACP RFC excludes ranking | Guide likely stale [CGPT-032] |
| Region | Merchant page: US only; consumer help: no region; apps run in Shopee/Allegro markets | "Shopping" = ChatGPT's own product results; plugins are a separate surface (inference) [CGPT-022, MKT-012] |
| Search index | OpenAI names Microsoft, Shopify; press reports Google via SerpApi; vendor finds Google Shopping match; API study finds low overlap with both | Unresolved; test it [CGPT-002, RES-013, RES-019, RES-021] |
| Content optimization | GEO up to 40% vs C-SEO Bench mostly ineffective vs 2.8% variance | Retrieval dominates in the newest study [RES-009, RES-010, RES-012] |
| Shopify docs vs live | Help pages omit the new robots.txt header and agentic sitemap | Live files win [SHOP-016, SHOP-023] |

---

## 12. Shopify implications

Full action list with status and test method: `shopify/chatgpt.md`.

Summary:
- **Confirmed requirements** (to be in ChatGPT via Shopify Catalog): stay Catalog-eligible, sell to US buyers, complete three policies, keep ChatGPT access on, avoid prohibited categories [SHOP-001, SHOP-003, SHOP-005].
- **Evidence-backed improvements:** accurate price and stock, verified reviews, complete product data incl. barcode, own-brand ("maker") listings, crawl access for the open-web path [CGPT-015, SHOP-008, SHOP-009, SHOP-016].
- **Experimental:** Catalog title/description remapping, third-party review coverage, Google Merchant Center presence.
- **No evidence for ChatGPT:** JSON-LD enrichment, llms.txt/agents.md, UCP adoption, a direct OpenAI feed, a ChatGPT plugin for small stores.

---

## 13. Method and limits of this report

- Five research agents gathered sources in parallel on 2026-10-30. Raw captures are in `notes/a-` to `notes/e-`.
- openai.com, help.openai.com and chatgpt.com return HTTP 403 to automated fetches. Those pages were read in a browser. developers.openai.com was fetched as Markdown.
- The lead researcher re-checked load-bearing Tier 1 excerpts on the live pages: the shopping help article, search help article, merchants page, 2026-03-24 post, crawler doc, feed spec, Shopify ChatGPT and robots.txt help pages, kith.com, amazon.in and flipkart.com robots.txt, and the Chen & Koudas paper. Registry `Checked` fields record which entries.
- No ChatGPT queries were run. Every statement about what ChatGPT displays comes from documentation or third-party studies.
