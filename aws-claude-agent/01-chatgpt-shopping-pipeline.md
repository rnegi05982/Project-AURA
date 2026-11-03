# What happens when a user asks ChatGPT for running shoes

All claims carry an evidence ID from `03-evidence-registry.md` and a classification.
Classifications: **VF** verified fact, **EBI** evidence-based inference, **UH** unverified
hypothesis, **EO** experimentally observed.

A note on what "verified fact" means here. Most of this mechanism is documented only by the vendor
that operates it. "OpenAI states that product results are organic" is a VF. "Product results are
organic" is not — no independent party can audit it. Each claim below is worded so the
classification is honest about which of the two it is.

---

## 0. The short version

ChatGPT does not have one shopping system. It has **three**, and a merchant's product can enter
through any of them:

| Path | What feeds it | Who can use it | Merchant control |
|---|---|---|---|
| **A. Product feed index** | Structured feed ingested by OpenAI (ACP product feed spec) | "Approved partners" only — Shopify is one, acting on behalf of its merchants | High: data quality in Shopify admin |
| **B. Open-web retrieval** | Pages crawled by `OAI-SearchBot` + third-party search providers | Anyone with a crawlable site | Medium: robots.txt, structured data, page content |
| **C. Agentic page reading** | `shopping research` mode reads retail product pages live | Anyone whose pages are reachable and not bot-blocked | Medium: page content, WAF/CDN rules |

For an independent Shopify merchant, **path A is already live and automatic** and is the highest
leverage one, which is the single most counter-intuitive finding in this report. See
`02-shopify-merchant-playbook.md`.

---

## 1. The user types a shopping query

OpenAI's own example query is literally the user's question. The Instant Checkout announcement
says: "When someone asks a shopping question—"best running shoes under $100" or "gifts for a
ceramics lover" — ChatGPT shows the most relevant products from across the web." <sup>`[ACA-CGPT-001]`</sup>
**VF (as stated by OpenAI).**

Two separate things can happen from here, and the distinction matters because the evidence base is
different for each.

### 1a. Default conversational answer with product results
The model decides to retrieve. ChatGPT search "leverages third-party search providers, as well as
content provided directly by our partners" <sup>`[ACA-CGPT-005]`</sup> **VF (as stated, 2024-10-31 — this is
the oldest source in this report and the most likely to be stale; see gaps).**

### 1b. "Shopping research" mode
A distinct product. It "is powered by a version of GPT-5 mini trained with reinforcement learning
specifically for shopping tasks", trained "to read trusted sites, cite reliable sources, and
synthesize information across many sources" <sup>`[ACA-CGPT-002]`</sup> **VF (as stated).** Output is "a
personalized buyer's guide". Results are "organic and based on publicly available retail
sites—reading product pages directly, citing sources, and avoiding low-quality or spammy sites"
<sup>`[ACA-CGPT-002]`</sup> **VF (as stated).**

The operative difference for a merchant: in 1b, an agent fetches and reads **your product page**.
In 1a, a retrieval system consults an **index**. Page-level quality matters in both, but in 1b a
blocked or JS-only page is fatal in a way it is not in 1a.

---

## 2. Candidate generation

### Path A — the product feed index
OpenAI operates an ingestion pipeline for structured merchant feeds. "Merchants provide a secure,
regularly refreshed feed (CSV or JSON) containing key details such as identifiers, descriptions,
pricing, inventory, media, and fulfillment options." <sup>`[ACA-CGPT-003]`</sup> **VF.**

Purpose is explicitly indexing: a feed exists so "ChatGPT accurately indexes and displays your
products with up-to-date price and availability" <sup>`[ACA-CGPT-004]`</sup>, and so "ChatGPT can accurately
surface their products in search and shopping experiences" <sup>`[ACA-CGPT-003]`</sup>. **VF.**

Delivery is a daily full snapshot over SFTP. The documented steps are: review the schema, "Validate
the required fields for every record", "Upload your catalog over SFTP", and keep it current "by
overwriting the same file or shard set with your latest snapshot", with a recommendation of
"uploading a full snapshot at least once a day" <sup>`[ACA-CGPT-006]`</sup>. **VF.**

**Access is gated.** "Onboarding product feeds in ChatGPT is currently available to approved
partners" <sup>`[ACA-CGPT-006]`</sup>. **VF.** This is the gate that makes path A look closed to a small
merchant and is why most merchant-facing advice online is wrong about it. It is not closed — it is
delegated. Shopify is the approved partner (§5).

Required fields are nine: `item_id`, `title`, `description`, `url`, `brand`, `seller_name`,
`image_url`, `availability`, `price` <sup>`[ACA-CGPT-007]`</sup>. **VF.** Two spec details with direct ranking
consequences:

- `is_eligible_search` defaults to true when omitted, and "Eligibility does not guarantee display."
  <sup>`[ACA-CGPT-007]`</sup> **VF.** Being in the index is necessary, not sufficient.
- Optional attributes are claimed to affect ranking: required fields "ensure correct display of
  price and availability, while recommended attributes—like rich media, reviews, and performance
  signals—improve ranking, relevance, and user trust" <sup>`[ACA-CGPT-003]`</sup>. **VF (as stated).** This is
  the only sentence in OpenAI's documentation that names a category of ranking input. It does not
  say by how much, and no formula is published.

### Path B — open-web retrieval
`OAI-SearchBot` is the crawler whose output governs search visibility. It is "used to surface
websites in search results in ChatGPT's search features", and sites that opt out "will not be shown
in ChatGPT search answers, though can still appear as navigational links" <sup>`[ACA-CGPT-008]`</sup>. **VF.**

Three other agents exist and are commonly confused with it:

| Agent | Function | Blocking it costs you |
|---|---|---|
| `OAI-SearchBot` | Search index for ChatGPT search | Your search visibility |
| `GPTBot` | Model training corpus | Nothing in search — "relates to training only" |
| `ChatGPT-User` | User-triggered fetch (a person asked ChatGPT to open your page) | Live page reads; "robots.txt rules may not apply" |
| `OAI-AdsBot` | Landing-page safety + ad relevance for pages "submitted as ads" | Ad eligibility only |

<sup>`[ACA-CGPT-008]`</sup> **VF.** `ChatGPT-User` "is not used to determine whether content may appear in
Search" — the opt-out lever for search is `OAI-SearchBot` only <sup>`[ACA-CGPT-008]`</sup>. **VF.**
robots.txt changes for search "can take roughly a day to take effect" <sup>`[ACA-CGPT-008]`</sup>. **VF.**

All four publish IP ranges as JSON at `openai.com/<bot>.json`. Observed directly: `searchbot.json`
(created 2026-01-02), `gptbot.json` (2026-09-22), `chatgpt-user.json` (2026-10-27),
`adsbot.json` (2026-05-12). The prefixes are Microsoft Azure ranges (13.x, 20.x, 104.210.x,
172.182.x) <sup>`[ACA-OBS-001]`</sup>. **EO.**

That the `OAI-SearchBot` fleet runs on Azure is consistent with, but does not prove, continued use
of Bing-derived retrieval. **UH.** Do not write "ChatGPT shopping runs on Bing" in any report. The
only sourced statement is the 2024 "third-party search providers" line <sup>`[ACA-CGPT-005]`</sup>.

### Path C — agentic page reading
In shopping research, the model reads product pages directly <sup>`[ACA-CGPT-002]`</sup>. **VF.** Merchants
"who want to ensure they are available to appear in shopping research results can follow the
allowlisting process" <sup>`[ACA-CGPT-002]`</sup>. **VF.**

That allowlisting link resolves to an article about allowlisting ChatGPT's **cloud browser** at the
CDN/WAF layer, using Web Bot Auth (RFC 9421). The browser signs requests with `Signature`,
`Signature-Input`, and `Signature-Agent: "https://chatgpt.com"`, verifiable against keys at
`https://chatgpt.com/.well-known/http-message-signatures-directory`. Cloudflare exposes it as bot
tag `chatgpt-agent`, detection ID `129220581` <sup>`[ACA-CGPT-009]`</sup>. **VF.**

Note the drift: a shopping document points at an enterprise cloud-browser document. Recorded as a
gap in `05`, not papered over.

---

## 3. Ranking

This is the only published ranking statement, and it is narrow but specific. On merchant selection
when the same item is sold in several places:

> "Product results are organic and unsponsored, ranked purely on relevance to the user." …
> "Merchants pay a small fee on completed purchases, but the service is free for users, doesn't
> affect their prices, and doesn't influence ChatGPT's product results. Instant Checkout items are
> not preferred in product results. When ranking multiple merchants that sell the same product,
> ChatGPT considers factors like availability, price, quality, whether a merchant is the primary
> seller, and whether Instant Checkout is enabled, to optimize the user experience."
> <sup>`[ACA-CGPT-001]`</sup> **VF (as stated by OpenAI).**

Read that carefully, because it contains an internal tension OpenAI does not resolve: Instant
Checkout items "are not preferred", yet "whether Instant Checkout is enabled" is a listed ranking
factor. Both sentences are in the same paragraph. The reconciliation is probably that enablement is
a tiebreaker inside relevance rather than a boost, but **no source establishes that**. **UH.**
Recorded in `05`.

What the five named factors mean for a merchant, stated plainly:

| Named factor | Merchant-controllable? | How |
|---|---|---|
| availability | Yes | Accurate stock state; `availability` is the one field where "unknown" is legal but weak |
| price | Yes | Competitiveness against other sellers of the same item |
| quality | Partly | Undefined by OpenAI. Review count/rating are plausible inputs — **UH** |
| whether a merchant is the primary seller | Partly | Brand owner / manufacturer / exclusive seller beats a reseller. Set `brand` and `seller_name` truthfully |
| whether Instant Checkout is enabled | Not yet, for Shopify merchants | See §5 contradiction |

"Quality" is not defined anywhere in OpenAI's documentation. Treat any blog that tells you what it
means as Tier 4.

Separately, there is a measured accuracy objective: a new internal evaluation scores "the
percentage of products in each response that meet the user requirements" <sup>`[ACA-CGPT-002]`</sup>. **VF.**
**EBI:** a model optimized against constraint satisfaction rewards feeds whose attribute fields let
a constraint be checked — size, color, gender, material, price tier. A product with empty
attributes cannot be verified to satisfy "under $100, wide fit, for trail" and is cheaper for the
model to drop than to risk. This is the mechanism-level argument for filling optional fields, and
it is an inference, not a documented rule.

Ads do not change this picture per OpenAI: "Ads in ChatGPT are always clearly labeled and separate
from ChatGPT's answers" and "Advertising does not influence the answers ChatGPT provides"
<sup>`[ACA-CGPT-010]`</sup>. **VF (as stated).**

---

## 4. Rendering and the handoff

Product results render as cards with price, image, availability, and a link out. Purchases either
click through to the retailer, or — for merchants in Instant Checkout — complete inside ChatGPT
<sup>`[ACA-CGPT-001]`</sup>, <sup>`[ACA-CGPT-002]`</sup>. **VF.**

Instant Checkout is the Agentic Commerce Protocol (ACP), co-developed by OpenAI and Stripe,
Apache-2.0 <sup>`[ACA-PROTO-001]`</sup>. **VF.** The flow <sup>`[ACA-CGPT-003]`</sup> **VF**:

1. ChatGPT collects buyer, fulfillment and payment details.
2. ChatGPT calls the merchant's ACP endpoints to create/update a checkout session.
3. OpenAI "prepares a one-time delegated payment request and sets a maximum chargeable amount and
   expiry based on what the user has selected".
4. The merchant's PSP returns a payment token; Stripe's Shared Payment Token is "the first
   Delegated Payment Spec-compatible implementation".
5. The merchant validates, computes tax, screens risk, charges, accepts or declines.
6. ChatGPT shows confirmation or decline.

Crucially: "OpenAI is not the merchant of record in the Agentic Commerce Protocol" and "the actual
checkout state and payment processing occurs on the merchant's systems" <sup>`[ACA-CGPT-003]`</sup>. **VF.**

Being in the feed obliges OpenAI to nothing: "Nothing in these Terms requires OpenAI to use or
surface any Merchant Content" and "OpenAI may remove or decide not to display any Merchant Content
at its sole discretion" <sup>`[ACA-CGPT-011]`</sup>. **VF.** The same terms require that you not block OpenAI
crawlers — including via robots.txt — and that you allowlist OpenAI's signed Web Bot Auth traffic
<sup>`[ACA-CGPT-011]`</sup>. **VF.** So for a feed participant, blocking `OAI-SearchBot` is a terms breach,
not merely a tradeoff.

Products in OpenAI's prohibited categories are excluded regardless of feed quality — alcohol,
tobacco/nicotine/vaping, firearms and accessories, prescription-only medication, supplements
marketed for health effects, gambling, adult content, crypto/NFTs, counterfeits, recalled goods,
and more <sup>`[ACA-CGPT-012]`</sup>. **VF.**

---

## 5. Where a Shopify merchant actually sits in this

This is the part that general SEO advice gets wrong.

Shopify is the approved feed partner, and it has already enrolled eligible stores. Shopify Catalog
"is a structured source of product information gathered from eligible products that are sold by
stores on Shopify", consumed by Shop and "select AI platforms, shopping sites, and AI agents"
<sup>`[ACA-SHOP-001]`</sup>. **VF.** It replaces per-channel feed work: you do not need "a separate product
feed for different channels" <sup>`[ACA-SHOP-001]`</sup>. **VF.**

The ChatGPT channel "acts as a discovery-focused referrer platform… It's active by default for
eligible stores" and "You don't need to do anything for your products to be discovered by ChatGPT
through Shopify Catalog" <sup>`[ACA-SHOP-002]`</sup>. **VF.** There are "no fees associated with selling in
ChatGPT. You pay only your standard payment processing fees." <sup>`[ACA-SHOP-002]`</sup> **VF.**

What is sent: "the products are listed by default with their title, description, options, images,
price, availability, and other key attributes, all structured in a way that AI agents can parse and
understand. Shopify Catalog continuously updates your product data" <sup>`[ACA-SHOP-003]`</sup>. **VF.**

What ChatGPT receives is therefore a Shopify-mediated feed, not your HTML. **EBI:** this is why
page-level SEO tactics underperform here and why the Shopify admin fields are the real levers.

Three consequences people get backwards:

1. **robots.txt does not gate it.** "Blocking AI crawlers at the `/robots.txt` or network layer
   affects only open-web discoverability. It doesn't stop your product data from being sent by
   Shopify Catalog to the agentic storefronts that you've activated." <sup>`[ACA-SHOP-004]`</sup> **VF.**
2. **Opting out of Catalog access does not hide you.** "your products might still be displayed or
   referenced by the AI channel through other external discovery and listing methods, such as web
   crawling and indexing" <sup>`[ACA-SHOP-002]`</sup>. **VF.** Only product status **Unlisted** removes a
   product completely — and that also removes it from your sitemap, search engines and your own
   storefront search <sup>`[ACA-SHOP-003]`</sup>. **VF.**
3. **You cannot leave Shopify Catalog.** "You can't opt out of Shopify Catalog itself."
   <sup>`[ACA-SHOP-001]`</sup> **VF.** You can only deny individual channels access.

### Contradiction to carry forward

OpenAI's Instant Checkout post says purchases are live with Etsy sellers "with over a million
Shopify merchants, like Glossier, SKIMS, Spanx and Vuori, coming soon" <sup>`[ACA-CGPT-001]`</sup>. Shopify's
current doc says the opposite for the Shopify path: "ChatGPT is a product discovery channel.
Customers using ChatGPT are redirected to buy products in your online store checkout, therefore
there's no option to activate or deactivate a ChatGPT direct checkout setting in your Shopify
admin" <sup>`[ACA-SHOP-002]`</sup>.

Both are VF as statements by their owners. The most likely reading is sequencing — OpenAI announced
intent, Shopify documents today's state (Shopify doc published 2026-10-21; the OpenAI post carries
no date in the capture). But **no source establishes** that in-ChatGPT checkout for general Shopify
merchants shipped and was then withdrawn, or never shipped. **UH.** Recorded in `05`.

Direct in-channel checkout *does* exist for Shopify merchants on Google AI Mode/Gemini, Microsoft
Copilot and Meta <sup>`[ACA-SHOP-002]`</sup>, <sup>`[ACA-SHOP-005]`</sup>. **VF.** So "whether Instant Checkout is
enabled" as a ChatGPT ranking factor is, for a Shopify merchant today, not a lever they hold.

### The second, parallel protocol

Separate from ACP, Shopify stores expose the **Universal Commerce Protocol** (UCP) — backed by
Google, Shopify, Etsy, Wayfair, Target, Walmart, Amazon, Microsoft, Meta, Salesforce and Stripe
<sup>`[ACA-PROTO-002]`</sup>. **VF.** Observed live on a Shopify store: `/.well-known/ucp` returns a profile
advertising version `2026-08-25`, an MCP endpoint at `/api/ucp/mcp`, and capabilities for cart,
checkout, fulfillment, discount, buyer consent and order <sup>`[ACA-OBS-002]`</sup>. **EO.**

Shopify also runs a cross-merchant **Global Catalog** MCP: "Use Global Catalog MCP when your agent
needs to discover products across multiple Shopify merchants — for example, comparison shopping,
cross-merchant discovery, or recommendations not tied to a specific store." <sup>`[ACA-SHOP-006]`</sup> **VF.**
Tools are `search_catalog`, `lookup_catalog` and `get_product`, reached at `/api/ucp/mcp`, which
"requires an agent profile" <sup>`[ACA-SHOP-006]`</sup>. **VF.** (The full host for the global endpoint is
rendered client-side and is not in my raw capture — treat `catalog.shopify.com` as
`[paraphrase]`.)

The retrieval design is stated explicitly, and it matters more than the tool names: "Results are
clustered by Universal Product ID (UPID) and include offers from multiple merchants."
<sup>`[ACA-SHOP-006]`</sup> **VF.** Also: "Multiple IDs that resolve to the same product are grouped into a
single product in the response." <sup>`[ACA-SHOP-006]`</sup> **VF.**

So cross-merchant competition is a first-class concept in the retrieval layer: offers for one UPID
are gathered, then an agent chooses among them — exactly the situation OpenAI's ranking paragraph
describes. How Shopify derives a UPID is **not documented**; whether GTIN/barcode is an input is
**UH** and is experiment E-3 in `05`.

Search filters include `available`, `ships_to`, `ships_from`, `price`, `condition`, `rating` (with
`min` and `min_count`), `price_tier`, `media` type, `categories`, and `attributes`: "Filter by
Shopify taxonomy attributes. Supported names are `Color`, `Size`, and `Target gender`. Entries
combine with AND logic." <sup>`[ACA-SHOP-006]`</sup> **VF.**

**EBI, and the most actionable inference in this report:** those filter names are a concrete,
published list of the attributes on which an agent can *exclude* you. A product with no color, no
size, no rating and no shipping country is unreachable by a filtered query regardless of how good
its description is. Optimising for filterability is more tractable than optimising for "relevance".

Shopify marks some catalog fields as `Inferred` — `description`, `options`,
`metadata.attributes`, `tech_specs`, `top_features`, `unique_selling_points`,
`variants[].condition` — and says to treat them as "discovery and merchandising signals, not as
merchant-authored source text" <sup>`[ACA-SHOP-006]`</sup>. **VF.** **EBI:** Shopify is generating structured
attributes from your prose. Prose that states specs explicitly produces better inferred attributes
than prose that gestures at them.

---

## 6. End-to-end, as one sequence

For a Shopify merchant, "best running shoes under $100":

1. User asks. Model routes to retrieval (or the user picks shopping research).
2. **Candidates**: feed index (your data, via Shopify Catalog → OpenAI) ∪ open-web retrieval
   (`OAI-SearchBot` index) ∪ live page reads (shopping research).
3. **Hard filters**: price ≤ 100; `availability` in stock; category match; not an OpenAI-prohibited
   product; `is_eligible_search` not false.
4. **Ranking**: relevance, then — among sellers of the same item — availability, price, quality,
   primary-seller status, Instant Checkout. Attribute completeness feeds the constraint-satisfaction
   objective (**EBI**).
5. **Render**: product cards with price/image/availability, citations to the pages read.
6. **Checkout**: for Shopify merchants on ChatGPT today, click out to your own checkout.

The merchant-controllable surface, in descending leverage, is in
`02-shopify-merchant-playbook.md`.
