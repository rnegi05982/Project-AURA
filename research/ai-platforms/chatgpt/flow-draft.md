# ChatGPT product discovery — flow draft (ASCII)

- **Status:** DRAFT for review, 2026-10-31. Colored diagram: `flow.html`. This file holds the evidence tables behind it.
- **Scope:** ChatGPT consumer app, product results (documented for US users).
- **Evidence:** every ID resolves in `evidence/registry/`. Full reasoning: `report.md` §3–§5.

Tags:
- `[D]` documented by OpenAI, Shopify or a cited study (VERIFIED FACT)
- `[I]` follows from documented facts; nobody states it (EVIDENCE-BASED INFERENCE)
- `[H]` plausible but untested (UNVERIFIED HYPOTHESIS)
- `[?]` no source describes it

---

## 1. Main flow

```text
+==============================================================================================+
| 0  USER PROMPT                                                                               |
|    "premium ceramic coffee mug under $30"                                                    |
+==============================================================================================+
                                               |
                                               v
+----------------------------------------------------------------------------------------------+
| 1  INTENT CHECK (made by the plan's model)                                      [D] CGPT-048 |
|    "When your question suggests shopping intent ... ChatGPT can show product options"        |
|    How intent is detected (classifier, threshold): undocumented [?]                          |
|    Model by plan: Free/Go GPT-6 Luna; paid GPT-6 Sol; mini fallback.            [D] CGPT-052 |
|    The model decides whether to search.                                         [D] CGPT-050 |
|    Search + product results: all plans; no model gating stated.       [D] CGPT-049, CGPT-054 |
|    A cheaper model skipping a path: no source [?]. Test: CGPT-T01 C4 vs C5.                  |
|    Product results documented for US users only; none for India.      [D] CGPT-022, CGPT-046 |
+----------------------------------------------------------------------------------------------+
          | shopping intent                                   | no shopping intent
          v                                                   v
          |                                     normal answer (web search optional)
+----------------------------------------------------------------------------------------------+
| 2  QUERY REWRITE                                                      [D] CGPT-002, CGPT-003 |
|    Prompt -> one or more targeted sub-queries.                                               |
|    May add saved memories and approximate location (from IP).         [D] CGPT-003, CGPT-045 |
|    Sub-queries go to partner search providers:                                  [D] CGPT-002 |
|      -> Shopify    lands in P1 (Shopify Catalog search) [I]                                  |
|      -> Microsoft  lands in P3 (Microsoft web index) [I]                                     |
|    After first results, more specific follow-up sub-queries may follow.         [D] CGPT-051 |
|    API study: keyword-style sub-queries; 28% add a brand nobody named.           [D] RES-014 |
+----------------------------------------------------------------------------------------------+
                                               |
                                               v
                           3  CANDIDATE GATHERING - five input paths
          Order and timing undocumented [?]. Side-by-side layout is for reading only.
                                               |
         +------------------+------------------+------------------+------------------+
         |                  |                  |                  |                  |
         v                  v                  v                  v                  v
+----------------+ +----------------+ +----------------+ +----------------+ +----------------+
| P1 FIRST-      | | P2 ACP         | | P3 WEB CRAWL   | | P4 THIRD-      | | P5 MODEL       |
| PARTY          | | PRODUCT FEED   | | + MICROSOFT    | | PARTY DATA     | | PRE-SEARCH     |
| CATALOG        | |                | | SEARCH         | | + REVIEWS      | | ANSWER         |
|                | |                | |                | |                | |                |
| Shopify        | | Approved       | | OAI-SearchBot  | | Unnamed        | | Training-data  |
| Catalog, Etsy. | | partners, or   | | crawl;         | | providers;     | | knowledge,     |
| Shopify as     | | via Stripe,    | | Microsoft      | | public review  | | brand priors   |
| search         | | Salesforce,    | | index;         | | websites       | |                |
| provider [I]   | | Feedonomics    | | OpenAI index   | |                | |                |
|                | |                | | [H]            | |                | |                |
| Reads:         | | Reads:         | | Reads:         | | Reads:         | | Reads:         |
| admin product  | | feed file      | | public pages   | | unknown [?]    | | nothing live   |
| data, Catalog  | | (SFTP / API)   | | + robots.txt   | |                | | (past text)    |
| search signals | |                | |                | |                | |                |
| Shopify store: | | Shopify store: | | Shopify store: | | Shopify store: | | Shopify store: |
| ON by default  | | not used       | | ON by default  | | unknown [?]    | | n/a            |
|                | |                | |                | |                | |                |
| CGPT-002       | | CGPT-018       | | CGPT-002       | | CGPT-012       | | CGPT-012       |
| CGPT-017       | | CGPT-025       | | CGPT-004       | | CGPT-013       | | CGPT-007       |
| SHOP-009       | | CGPT-027       | | SHOP-016       | | CGPT-014       | | RES-015        |
+----------------+ +----------------+ +----------------+ +----------------+ +----------------+
         |                  |                  |                  |                  |
         +------------------+------------------+------------------+------------------+
                                               |
                                               v
+----------------------------------------------------------------------------------------------+
| 4  COMBINE                                                                  [?] undocumented |
|    Merge, de-duplication and conflict rules (feed vs crawl) are not published.               |
|    Shopify Catalog clusters identical items before ChatGPT gets them.           [D] SHOP-024 |
+----------------------------------------------------------------------------------------------+
                                               |
                                               v
+----------------------------------------------------------------------------------------------+
| 5  POLICY FILTER                                                      [D] CGPT-012, CGPT-026 |
|    OpenAI safety standards and prohibited-product rules remove products or sellers.          |
+----------------------------------------------------------------------------------------------+
                                               |
                                               v
+----------------------------------------------------------------------------------------------+
| 6  PRODUCT SELECTION (carousel)                                                 [D] CGPT-011 |
|    Shown when ChatGPT "perceives it to be relevant to your intent".                          |
|    Context: query + Memory + Custom instructions.                                            |
|    Example factors: "available options, price, reviews, and ease of use".                    |
|    Weights shift per query: a stated budget makes price dominant.                            |
|    No formula, weights or candidate count published.                                         |
+----------------------------------------------------------------------------------------------+
                                               |
                                               v
+----------------------------------------------------------------------------------------------+
| 7  PRESENTATION                                                                 [D] CGPT-013 |
|    Model rewrites titles and descriptions, adds labels ("Budget-friendly"),                  |
|    and summarizes reviews from public websites.                                              |
+----------------------------------------------------------------------------------------------+
                                               |
                                               v   (user opens a product)
+----------------------------------------------------------------------------------------------+
| 8  MERCHANT LIST                                                      [D] CGPT-015, CGPT-014 |
|    Sellers of one product ranked by: availability, price, quality,                           |
|    maker or primary seller. "Quality" and "primary seller" are undefined.                    |
|    Headline price = first-ranked merchant. "Best price" = lowest known price.                |
+----------------------------------------------------------------------------------------------+
                                               |
                                               v
+----------------------------------------------------------------------------------------------+
| 9  HAND-OFF                                                           [D] CGPT-022, SHOP-002 |
|    User buys on the merchant site. Shopify: in-app browser (mobile) or new tab (web).        |
|    Order carries ChatGPT referral attribution in Shopify admin.                 [D] SHOP-012 |
+----------------------------------------------------------------------------------------------+

   Beside the answer: one labeled ad unit (Free and Go plans). Separate system;
   OpenAI says ads do not influence steps 1-8.                  [D] CGPT-042, CGPT-043
```

---

## 2. Path details

Table columns:
- **Reads:** the data point the path uses.
- **Shopify source:** where that data lives in a Shopify store.
- **Default:** what a Shopify store provides with no merchant work.
- **Merchant control:** how a merchant or developer changes it.

### P1 — First-party catalog (Shopify Catalog)

How it reaches ChatGPT:
- Shopify Catalog syndicates admin product data to ChatGPT. It is on by default for eligible stores [D] SHOP-001, SHOP-006, CGPT-017.
- Shopify is also a named search provider for rewritten sub-queries [D] CGPT-002.
- Catalog has its own search, and AI channels re-rank its results [D] SHOP-009.
- So a sub-query sent to Shopify most likely runs a Catalog search; ChatGPT then re-ranks the results [I].
- robots.txt does not affect this path [D] SHOP-018.

#### When a sub-query reaches Shopify

The Shopify sub-query is part of P1, not P3. It searches Shopify's index of admin product data. It does not read the storefront HTML, so robots.txt and theme markup play no part [D] SHOP-006, SHOP-018.

What Shopify's Catalog search uses (documented for Catalog search; ChatGPT's use is [I]):

| Input | What it is | Merchant control | Evidence |
|---|---|---|---|
| Query text vs product data | Free-text or image query matched against listings | Specific titles, descriptions, options | SHOP-034 |
| Availability | Only sale-ready items by default | Keep inventory accurate | SHOP-034 |
| Ships-to, ships-from | Buyer country/region/postal code; merchant origin | Shipping zones that cover the buyer | SHOP-034 |
| Price, relative price tier | Price range; low/medium/high within the category | Price | SHOP-034 |
| Color, Size, Target gender, category | Shopify taxonomy attributes and category IDs | Set the product category and its attributes | SHOP-034 |
| Rating and review count | Minimum rating and review count | Verified review source | SHOP-009, SHOP-034 |
| Media type | Image, video, external video, 3D model | Add media | SHOP-034 |
| Description completeness | Word count | Longer, specific descriptions | SHOP-009 |
| Image coverage | Number of images | More images | SHOP-009 |
| Variant and option completeness | Count, in-stock share, readable names (no acronyms or bare numbers) | Full variants; plain option names | SHOP-009 |
| Policy completeness | Shipping, returns, refund and other policies present | Write all policies | SHOP-009 |
| Popularity, engagement, brand recognition | Accumulated store signals | Indirect only | SHOP-009 |
| Inferred fields | Shopify-written description, attributes, specs, top features | Indirect: better source data | SHOP-015 |

Notes:
- Test it: Agentic admin search preview runs a query and shows whether your products reach the Catalog top 10 [D] SHOP-009.
- ChatGPT re-ranks Catalog output. The preview is directional only [D] SHOP-009.
- Which filters and buyer context ChatGPT sends: [?]. Ranking weights: [?] SHOP-034.
- Shopify offers paid promoted placements in Catalog results to enrolled callers [D] SHOP-035. ChatGPT's use is [H]; OpenAI says product results are not ads [D] CGPT-010.

Gate. A product enters only if all of these hold [D] SHOP-003, SHOP-005:
- The store sells to US buyers. The store can be based anywhere.
- Terms of service, privacy policy and refund policy are complete.
- The plan is Starter or higher. The store is not password-protected.
- The product has a title, at least one image, and a price above 0.
- The product is not Unlisted and not hidden from search engines (`seo.hidden`).
- The category is not excluded: alcohol, tobacco/vaping, CBD, weapons, adult, services, tickets, live animals, "Uncategorized".
- The product is not OpenAI-prohibited and not B2B-only.

| Reads | Shopify source | Default | Merchant control | Evidence |
|---|---|---|---|---|
| Title | Product title | Sent | Remap the source to a metafield or Liquid (Catalog > Channel mapping) | SHOP-006, SHOP-007 |
| Description | Product description | Sent | Remap the source. Put legal disclosures in the first 6,000 characters | SHOP-003, SHOP-006, SHOP-007 |
| Options, variants | Product options and variants | Sent | Variant grouping in Channel mapping | SHOP-006, SHOP-007 |
| Images | Product media | Sent | Add an image per variant | SHOP-006 |
| Price | Variant price | Sent; updated continuously | Edit the price | SHOP-006 |
| List price | Compare-at price, sent as UCP `list_price` | Sent when eligible | Pick the list-price source in Channel mapping | SHOP-007 |
| Availability | Inventory | Sent; updated continuously | Keep inventory tracking accurate | SHOP-006 |
| Barcode (GTIN, UPC, EAN, ISBN) | Variant barcode | Used if filled | Fill it per variant | SHOP-008 |
| Type, vendor, collections, tags | Product organization fields | Used if filled | Fill them. Set vendor to the maker's brand | SHOP-008 |
| Category | Catalog's own classification of the product info | Catalog infers it; it can differ from the admin category | No remap. Clear product info steers it [I] | SHOP-005, SHOP-007, SHOP-024 |
| Attributes, tech specs | Generated by Shopify, marked "Inferred" | Generated | No direct control. Accuracy follows the source data | SHOP-015, SHOP-024 |
| Product rating and review count | Reviews "verified by trusted sources" | None until a verified source exists | Use a review source that Shopify counts as verified | SHOP-009 |
| Shop policies | Settings > Policies | Empty until written | Complete all three | SHOP-003, SHOP-009 |
| Popularity, engagement, brand recognition | Accumulated store activity | Accrues over time | Indirect only | SHOP-009 |

Notes:
- Not sent: order history and customer data [D] SHOP-006.
- Catalog's "Listing quality" score uses description completeness, image coverage, verified reviews, variant completeness and policy completeness [D] SHOP-009.
- Rating, popularity and engagement are Catalog search signals. ChatGPT's use of them is [H] SHOP-009.
- Store off switch: Sales channels > Agentic > ChatGPT. Removal takes up to 7 days [D] SHOP-001.
- Product off switch: Unlisted status or `seo.hidden` [D] SHOP-010.
- Unknown [?]: the wire format, sync latency, and whether ChatGPT uses Catalog's order or inferred fields (`report.md` §10, gaps 7–8).

### P2 — ACP product feed

How it reaches ChatGPT:
- The merchant, or a provider (Salesforce, Stripe, Feedonomics), pushes a full-catalog feed [D] CGPT-018, MKT-017, MKT-019, MKT-020.
- File upload uses SFTP, parquet preferred, a full snapshot at least daily [D] CGPT-027.
- ACP 2026-04-17 adds a push Feed API [D] ACP-003.
- Gate: approved partners only, by application and waitlist [D] CGPT-025. Standard uploads target the US [D] CGPT-031.

Shopify:
- Not used. OpenAI says Shopify catalogs are integrated with "no additional setup or application" [D] CGPT-017.
- AURA found no Shopify-native ACP feed export [?].
- Read the table as OpenAI's product data model. Whether Catalog fills the same fields is [?].

| OpenAI feed field | Requirement | Shopify equivalent (AURA mapping [I]) | In a default Shopify store |
|---|---|---|---|
| `item_id` | Required | Variant ID or SKU | Yes (ID) |
| `title` | Required | Product title + variant title | Yes |
| `description` | Required | Product description | If written |
| `url` | Required | Product URL with `?variant=` | Yes |
| `brand` | Required | Vendor | If set |
| `seller_name` | Required | Store name | Yes |
| `image_url` | Required | Variant image | If uploaded |
| `availability` | Required | Inventory status | Yes |
| `price` | Required | Variant price (compare-at price when a sale is on) | Yes |
| `sale_price` | Optional | Variant price when a compare-at price is set | If set |
| `gtin` | Optional | Variant barcode | If filled |
| `mpn` | Optional | No core field; needs a metafield | No |
| `product_category` | Optional | Product category | If set |
| `material`, `color`, `size` | Optional | Variant options or category metafields | If set |
| `dimensions`, `weight` | Optional | Variant weight; dimensions need a metafield | Weight only |
| `return_policy`, `accepts_returns`, `return_deadline_in_days` | Optional | Refund policy page; no structured fields | Policy URL only |
| `review_count`, `star_rating` | Optional | Review app data | No |
| `is_eligible_search` | Optional, default `true` | — | — |

Feed notes:
- "Eligibility does not guarantee display" [D] CGPT-029.
- The ACP feed RFC puts ranking out of scope [D] ACP-004.
- The spec has review fields but no popularity or return-rate field [D] CGPT-030.
- Full field list: `notes/b-openai-commerce-protocols-and-feeds.md` §3 [D] CGPT-028.

### P3 — Web crawl and Microsoft search

How it reaches ChatGPT:
- OAI-SearchBot crawls sites for ChatGPT search. Allowing it is OpenAI's one stated eligibility condition [D] CGPT-004, CGPT-006.
- Rewritten sub-queries go to Microsoft as a partner search provider [D] CGPT-002. They most likely hit Microsoft's web index [I].
- Microsoft's crawler and index are not yet researched. They belong to the Copilot phase [?].
- Sub-queries to Shopify belong to P1, not here.
- OpenAI keeps its own web index. It is documented for Codex and Work only; consumer use is [H] CGPT-005.
- ChatGPT-User fetches a page when a user's request triggers it. It does not decide inclusion [D] CGPT-008.
- A feed is not required if ChatGPT already crawls the site [D] CGPT-019.

| Reads | Shopify default | Merchant control | Evidence |
|---|---|---|---|
| robots.txt rules for OAI-SearchBot | `User-agent: *` / `Allow: /`; no OpenAI group | Edit the `robots.txt.liquid` template. A custom file stops inheriting Shopify's updates | SHOP-016, SHOP-017 |
| Network access from OpenAI's searchbot IPs | Shopify rate-limits bots; unsigned bots get the strictest limits. Shopify says LLM indexing needs no signature | No merchant setting documented [?] | CGPT-004, SHOP-019 |
| Product page HTML: title, price, stock, description | Rendered by the theme | Theme code | What OAI-SearchBot extracts: [?] |
| Product JSON-LD | `Product` or `ProductGroup`: brand, category, description, GTIN, SKU, offers. No rating, review, shipping or return markup | Theme code or an app | SHOP-021, SHOP-022. ChatGPT use: [H]. No lift in one API study: RES-012 |
| `/llms.txt`, `/agents.md`, `/.well-known/ucp` | Served by default | Not documented | SHOP-020. ChatGPT use: [H] |
| Sitemap | Auto-generated; includes `sitemap_agentic_discovery.xml` | Not documented | SHOP-023. OpenAI use: [?] |
| Pages on other sites (reviews, comparisons) | — | Earn coverage | RES-011 |

Notes:
- Blocking OAI-SearchBot removes the site from answers within ~24 h. It can still appear as a navigational link [D] CGPT-006.
- Blocking GPTBot does not affect this path [D] CGPT-007.
- API study: every cited page was first retrieved by search [D] RES-012.
- Same study: retrieval explained 32% of within-site citation variance; 14 page features explained 2.8% [D] RES-012.
- API study: for "best X" queries, 93.5% of citations were third-party media [D] RES-011.

### P4 — Third-party metadata and reviews

How it reaches ChatGPT:
- OpenAI input: "Structured metadata from first-party and third-party providers (e.g., price, product description) and other third-party content" [D] CGPT-012.
- Displayed prices come from third-party providers [D] CGPT-014.
- The merchant list uses metadata "from third-party providers or directly from the merchants themselves" [D] CGPT-015.
- Review summaries use "reviews from public websites". OpenAI does not verify them [D] CGPT-013.
- OpenAI names no metadata provider [?].

| Reads | Likely origin | Shopify default | Merchant control | Evidence |
|---|---|---|---|---|
| Price, description, merchant list | Unnamed providers | Unknown [?] | Unknown | CGPT-012, CGPT-014, CGPT-015 |
| Google Shopping listing, if Google is a provider [H] | Merchant Center feed | Not part of Catalog. Needs the Google & YouTube app or another feed | Install the app; keep products approved | SHOP-025, SHOP-029, RES-021 |
| Review text and ratings | Public review websites | No review markup in default theme JSON-LD | Review app; earn third-party reviews | CGPT-013, SHOP-022 |

Google as a provider is [H]. The evidence is Tier 3 only:
- A vendor study matched 83% of 43,000+ carousel products to Google Shopping's top 40, vs 11% for Bing. RES-021.
- Press reported OpenAI partially used Google results via SerpApi (Aug 2025). RES-019.
- OpenAI names Microsoft and Shopify, not Google [D] CGPT-002.

### P5 — Model pre-search answer

How it reaches ChatGPT:
- OpenAI input: "Model responses generated by ChatGPT before it considers any new search results" [D] CGPT-012.
- It reads nothing from the store at query time [I].
- The knowledge comes from training data [I]. GPTBot collects OpenAI's training data [D] CGPT-007.

| Reads | Shopify default | Merchant control | Evidence |
|---|---|---|---|
| Past web text about the brand and products (training data) | robots.txt allows GPTBot (no OpenAI group) | Block GPTBot in `robots.txt.liquid`. This opts out of future training only; search is unaffected | SHOP-016, CGPT-007 |

Research on this path (API models, not the consumer app):
- Models reorder identical products by brand name [D] RES-015.
- 47% of citations came from sites the model named without searching [D] RES-015.
- With identical specs, a known brand won every trial. A rating edge under 0.1 star removed that advantage [D] RES-017.
- LLMs favor global brands over local brands [D] RES-018.
- No per-query merchant lever exists. Brand presence in public text builds the prior over time [I].

---

## 3. After combine: what decides, and which Shopify data feeds it

| Step | What decides | Shopify data that feeds it | Evidence |
|---|---|---|---|
| 5 Policy filter | OpenAI prohibited products; seller bans | Product type and content; Catalog category exclusions | CGPT-026, SHOP-005 |
| 6 Selection | Relevance to intent. Example factors: options, price, reviews, ease of use | Variant options, price, verified reviews, description detail | CGPT-011 |
| 7 Presentation | Model-written titles, labels, review summaries | None directly. Source data shapes the output | CGPT-013 |
| 8 Merchant list | Availability, price, quality, maker or primary seller | Inventory accuracy, price, vendor set to own brand. "Quality" is undefined | CGPT-014, CGPT-015 |
| 9 Hand-off | Merchant checkout | Online-store checkout; referral attribution in admin | SHOP-002, SHOP-012 |

The merchant list matters when several stores sell one product. The first-ranked merchant sets the headline price [D] CGPT-014.

---

## 4. Where this draft differs from the requested outline

1. **Intent check (step 1).** OpenAI documents the trigger, not the classifier [D] CGPT-048. A US-only note was added [D] CGPT-022.
2. **"In parallel" (step 3).** OpenAI lists the inputs, not their order or timing. The side-by-side layout is not a claim [?].
3. **Path 1 name.** "Provider metadata" became "first-party catalog". OpenAI splits providers into first-party and third-party [D] CGPT-012. P4 is the third-party half.
4. **Partner search split by provider (review fix).** Shopify sub-queries land in P1 (Catalog search). Microsoft sub-queries land in P3 [D] CGPT-002; landing points [I].
5. **P4 includes public reviews.** OpenAI groups them as "other third-party content" [D] CGPT-012, CGPT-013.
6. **Steps after "combine".** Four documented steps were added: policy filter, presentation, merchant list, hand-off. The merchant list has its own ranking factors [D] CGPT-015.

---

## 5. Model and plan

- Free and Go use GPT-6 Luna; Plus, Pro, Business and Enterprise use GPT-6 Sol. A mini model takes over after rate limits [D] CGPT-052.
- Web search runs on every plan and for logged-out users, within usage limits [D] CGPT-049.
- The 2026-03-24 shopping update reached "all ChatGPT users" [D] CGPT-053.
- OpenAI states model gating where it exists, e.g. reservation search. It states none for shopping [D] CGPT-054.
- The model decides whether to search. OpenAI says a model update changed that decision [D] CGPT-050.
- So every plan has the same documented paths. How often each path fires can differ by model [I].
- A cheaper model skipping partner search: no source [?]. Test: CGPT-T01 condition C5 vs C4.
- Memory feeds the rewrite only when enabled [D] CGPT-003. Logged-out users have no saved memories to add [I].

---

## 6. India note

- No step above is documented for India-located users [D] CGPT-046.
- P1 needs US selling [D] SHOP-003. P2 targets the US [D] CGPT-031.
- An India-only store can reach ChatGPT through P3–P5 at most [I].
- Test: `experiments/test-cases/chatgpt-coffee-mug.md`.
