# Evidence registry — aws-claude-agent

Self-contained registry for this folder only. Does not share ID space with
`/evidence/evidence-registry.md`, and I did not read or modify that file — the user scoped this
track as independent, so the tier scheme below is declared locally rather than inherited.

**All sources accessed 2026-10-30.** Re-fetch before **2027-01-28** (90-day rule, `/CLAUDE.md`).

## Tiers

| Tier | Meaning |
|---|---|
| 1 | The platform's own normative artefact: spec, developer docs, policy, terms, help centre, robots/IP file |
| 2 | The platform's own announcement or marketing (true as a statement of intent, not a spec) |
| 3 | A second platform's documentation describing the first (e.g. Shopify describing ChatGPT) |
| 4 | Press, SEO blogs, vendor content marketing. Raises questions only. **No Tier 4 source is cited in `01` or `02`.** |

## Excerpt fidelity

This column is load-bearing and is the honest part of this registry.

- **byte** — raw bytes saved in `notes/raw/`; every quotation grep-verified against that file.
- **byte (reader)** — raw markdown saved, obtained via the `r.jina.ai` text-extraction proxy
  because the origin returns 403 to non-browser clients. Quotations grep-verified against the saved
  file. One remove from the origin's own bytes; the proxy could in principle alter text.
- **rendered** — content reached me only through a JS-rendering fetch tool that summarises. Quotes
  from these are `[paraphrase]` and are **not** used as the sole support for any claim in `01`/`02`.
- **observed** — I executed the request and read the response myself.

## ID prefixes

`ACA-CGPT-###` OpenAI/ChatGPT · `ACA-SHOP-###` Shopify · `ACA-PROTO-###` protocol bodies ·
`ACA-OBS-###` my own observations.

---

## OpenAI / ChatGPT

### ACA-CGPT-001
- **Source:** "Buy it in ChatGPT" — https://openai.com/index/buy-it-in-chatgpt/
- **Tier:** 2 · **Fidelity:** byte (reader) · `notes/raw/oai-buy-it-in-chatgpt.md`
- **Published:** no date in capture. Origin returns 403 to non-browser clients. **Date unknown —
  do not cite a date.**
- **Excerpt (verbatim):** "When someone asks a shopping question—"best running shoes under $100" or
  "gifts for a ceramics lover" — ChatGPT shows the most relevant products from across the web.
  Product results are organic and unsponsored, ranked purely on relevance to the user."
- **Excerpt (verbatim):** "Merchants pay a small fee on completed purchases, but the service is free
  for users, doesn't affect their prices, and doesn't influence ChatGPT's product results. Instant
  Checkout items are not preferred in product results. When ranking multiple merchants that sell the
  same product, ChatGPT considers factors like availability, price, quality, whether a merchant is
  the primary seller, and whether Instant Checkout is enabled, to optimize the user experience."
- **Excerpt (verbatim):** "U.S. ChatGPT Plus, Pro, and Free users can now buy directly from U.S.
  Etsy sellers right in chat, with over a million Shopify merchants, like Glossier, SKIMS, Spanx and
  Vuori, coming soon. Today, Instant Checkout supports single-item purchases."
- **Supports:** the only published ranking-factor list; organic/unsponsored claim; fee model;
  Etsy-live / Shopify-pending status.
- **Contradiction:** the Shopify-merchant checkout claim conflicts with `ACA-SHOP-002`. See `05`.

### ACA-CGPT-002
- **Source:** "Shopping research" — https://openai.com/index/chatgpt-shopping-research/
- **Tier:** 2 · **Fidelity:** byte (reader) · `notes/raw/oai-shopping-research.md`
- **Published:** no date in capture.
- **Excerpt (verbatim):** "Shopping research is powered by a version of GPT-5 mini trained with
  reinforcement learning specifically for shopping tasks. We trained it to read trusted sites, cite
  reliable sources, and synthesize information across many sources to produce high-quality product
  research."
- **Excerpt (verbatim):** "Your chats are never shared with retailers. Results are organic and based
  on publicly available retail sites—reading product pages directly, citing sources, and avoiding
  low-quality or spammy sites. Merchants who want to ensure they are available to appear in shopping
  research results can follow the allowlisting process here"
- **Excerpt (verbatim):** "Shopping research might make mistakes about product details like price
  and availability, and we encourage you to visit the merchant site for the most accurate details."
- **Supports:** path C (live page reading); allowlisting as the merchant lever; the accuracy caveat.
- **Note:** the "here" link targets `ACA-CGPT-009`, which is a cloud-browser document. See `05`.

### ACA-CGPT-003
- **Source:** Key concepts, ACP — https://developers.openai.com/commerce/guides/key-concepts
- **Tier:** 1 · **Fidelity:** byte · `notes/raw/oai-key-concepts.md`
- **Excerpt (verbatim):** "Merchants provide a secure, regularly refreshed feed (CSV or JSON)
  containing key details such as identifiers, descriptions, pricing, inventory, media, and
  fulfillment options."
- **Excerpt (verbatim):** "Required fields ensure correct display of price and availability, while
  recommended attributes—like rich media, reviews, and performance signals—improve ranking,
  relevance, and user trust."
- **Excerpt (verbatim):** "define how merchants share structured product data with OpenAI so ChatGPT
  can accurately surface their products in search and shopping experiences."
- **Excerpt (verbatim):** "OpenAI is not the merchant of record in the Agentic Commerce Protocol."
- **Excerpt (verbatim):** "the actual checkout state and payment processing occurs on the merchant's
  systems."
- **Supports:** feed as the indexing mechanism; the only OpenAI statement naming ranking inputs; the
  six-step ACP flow; merchant-of-record position.

### ACA-CGPT-004
- **Source:** Commerce docs index — https://developers.openai.com/commerce/
- **Tier:** 1 · **Fidelity:** rendered (index page only; its child pages are byte-captured)
- **Excerpt `[paraphrase]`:** a feed exists so "ChatGPT accurately indexes and displays your products
  with up-to-date price and availability".
- **Supports:** nothing on its own. Used only for navigation; the substantive claims sit on
  `ACA-CGPT-003`, `-006`, `-007`.

### ACA-CGPT-005
- **Source:** "Introducing ChatGPT search" — https://openai.com/index/introducing-chatgpt-search/
- **Tier:** 2 · **Fidelity:** rendered · **Published:** 2024-10-31 (updates 2024-12-16, 2025-02-05)
- **Excerpt `[paraphrase]`:** search "leverages third-party search providers, as well as content
  provided directly by our partners"; "Any website or publisher can choose to appear in ChatGPT
  search."
- **Supports:** that a third-party retrieval layer existed in 2024.
- **Staleness warning:** two years old and predates every shopping feature in this report. Do not
  use it to describe today's retrieval stack. It is the sole basis for any Bing-adjacency reading,
  which is why that reading is **UH**.

### ACA-CGPT-006
- **Source:** Get started, commerce — https://developers.openai.com/commerce/guides/get-started
- **Tier:** 1 · **Fidelity:** byte · `notes/raw/oai-get-started.md`
- **Excerpt (verbatim):** "currently available to approved partners"
- **Excerpt (verbatim):** "Upload your catalog over SFTP."
- **Excerpt (verbatim):** "uploading a full snapshot at least once a day"
- **Supports:** the feed gate (and therefore why Shopify, not the merchant, is the integrator);
  SFTP delivery; daily snapshot cadence.

### ACA-CGPT-007
- **Source:** Product feed schema (file upload) —
  https://developers.openai.com/commerce/specs/file-upload/products
- **Tier:** 1 · **Fidelity:** byte · `notes/raw/oai-feed-products.md` (37.9 KB — the full field
  reference)
- **Required fields:** `item_id`, `title`, `description`, `url`, `brand`, `seller_name`,
  `image_url`, `availability`, `price`.
- **Excerpt (verbatim):** availability accepts `in_stock`, `out_of_stock`, `pre_order`, `backorder`,
  `unknown`; "Omitted, empty, or unrecognized values reject the row."
- **Excerpt (verbatim):** GTIN must be "exactly 8, 12, 13, or 14 digits, including a valid check
  digit".
- **Excerpt (verbatim):** `is_eligible_search` — "Eligibility does not guarantee display."
- **Also records:** variant grouping (`group_id`, `listing_has_variations`, `variant_dict`);
  `review_count`/`star_rating`; `condition`, `color`, `size`, `gender`, `age_group`,
  `product_category`; `sale_price` must be "strictly less than `price`"; title ≤150 chars,
  description ≤5,000; `shipping_price` — "Omitted or empty means unknown, not free shipping";
  checkout flags `is_eligible_checkout`, `seller_privacy_policy`, `seller_tos`.
- **Negative finding (important):** the schema **never references schema.org or Google Merchant
  Center**. The feed is its own vocabulary. This is why structured-data advice is classified
  separately from feed advice in `02`.

### ACA-CGPT-008
- **Source:** Crawlers and user agents — https://developers.openai.com/api/docs/bots
  (redirected from `platform.openai.com/docs/bots`)
- **Tier:** 1 · **Fidelity:** byte · `notes/raw/oai-bots.md`
- **Excerpts (verbatim):** `OAI-SearchBot` "used to surface websites in search results in ChatGPT's
  search features"; opted-out sites "will not be shown in ChatGPT search answers, though can still
  appear as navigational links"; `GPTBot` disallow signals content "should not be used in training
  generative AI foundation models"; `ChatGPT-User` "is not used to determine whether content may
  appear in Search" and "robots.txt rules may not apply"; `OAI-AdsBot` visits pages "submitted as
  ads on ChatGPT".
- **Supports:** the four-agent table and the cost of blocking each; the ~1-day robots propagation.

### ACA-CGPT-009
- **Source:** "ChatGPT Work's Cloud browser allowlisting" — requested as
  `https://help.openai.com/en/articles/11845367-chatgpt-agent-allowlisting`, **final URL**
  `.../11845367-chatgpt-works-cloud-browser-allowlisting`
- **Tier:** 1 · **Fidelity:** byte (reader) · `notes/raw/oai-allowlisting.md`
- **Excerpts (verbatim-verified):** `Signature-Agent` header; Cloudflare detection ID `129220581`;
  key directory `https://chatgpt.com/.well-known/http-message-signatures-directory`; RFC 9421;
  per-vendor steps for Cloudflare, Akamai, HUMAN Sightline, Vercel.
- **Supports:** WAF/CDN allowlisting mechanics (playbook action 9).
- **Defect recorded:** this is the target of the shopping-research "allowlisting process" link
  (`ACA-CGPT-002`) but is written for ChatGPT Work's cloud browser. The redirect slug changed under
  the same article ID. Treat the shopping-research → allowlisting mapping as **unresolved**; see `05`.

### ACA-CGPT-010
- **Source:** ChatGPT ads announcement —
  https://openai.com/index/expanding-access-to-ai-with-chatgpt-ads/
- **Tier:** 2 · **Fidelity:** rendered · **Published:** no date in capture
- **Excerpt `[paraphrase]`:** "Ads in ChatGPT are always clearly labeled and separate from ChatGPT's
  answers"; "Advertising does not influence the answers ChatGPT provides."
- **Supports:** only the negative claim that ads are stated not to affect organic answers. Marked
  `[paraphrase]`; corroborated independently by `ACA-CGPT-001` ("organic and unsponsored"), which is
  byte-verified.

### ACA-CGPT-011
- **Source:** Merchant Feed Terms of Service —
  https://openai.com/policies/merchant-feed-terms-of-service/
- **Tier:** 1 · **Fidelity:** byte (reader) · `notes/raw/oai-merchant-feed-tos.md`
- **Excerpt (verbatim, grep-verified):** "Nothing in these Terms requires OpenAI to use or surface
  any Merchant Content"
- **Also records:** merchant may not block OpenAI crawlers including via robots.txt; must allowlist
  OpenAI's signed Web Bot Auth traffic; TDM reservations "will have no effect with respect to OpenAI
  or its Affiliates"; feed content "does not constitute Confidential Information"; OpenAI "may
  access the Merchant Content for purposes of a search index"; warranty that pricing "is and will
  remain complete, correct and current"; changes effective "at least 15 days after being posted".
- **Supports:** no-guarantee-of-display; the robots-blocking conflict for feed participants.
- **Caveat:** summarised, not legal advice. Full text in the capture.

### ACA-CGPT-012
- **Source:** Commerce policies — https://openai.com/policies/commerce-policies/
- **Tier:** 1 · **Fidelity:** byte (reader) · `notes/raw/oai-commerce-policies.md`
- **Supports:** prohibited product categories; "truthful listings and imagery"; OpenAI reserves "the
  right to remove product listings or restrict merchant participation in these experiences for any
  reason". Cited by Shopify at `ACA-SHOP-002`.
- **Negative finding:** contains **no** ranking, selection, or paid-vs-organic statement, and no
  data/feed requirements. Do not cite it for ranking.

### ACA-CGPT-013
- **Source:** Agentic commerce in production —
  https://developers.openai.com/commerce/guides/production
- **Tier:** 1 · **Fidelity:** byte · `notes/raw/oai-production.md`
- **Supports:** pre-launch certification checklist; TLS 1.2+; PCI scope boundaries; ToS/Privacy links
  "present and functional"; allowlist OpenAI's published IP ranges; merchant is merchant of record;
  `ORDER_UPDATE` webhook.
- **Negative finding:** no SLA, no feed cadence, and nothing on ranking.

---

## Shopify

### ACA-SHOP-001
- **Source:** Shopify Catalog — https://help.shopify.com/en/manual/shopify-catalog
- **Tier:** 1 (Shopify's own product) / 3 (where it describes AI channels) · **Fidelity:** byte
  (reader) · `notes/raw/sh-catalog.md`
- **Excerpt (verbatim):** "Shopify Catalog is a structured source of product information gathered
  from eligible products that are sold by stores on Shopify."
- **Excerpt (verbatim):** "You can't opt out of Shopify Catalog itself."
- **Excerpt `[paraphrase]`-free points (verbatim in capture):** inclusion "doesn't guarantee that a
  product will appear in a specific AI answer, be ranked in a specific position"; "each channel
  controls the final ranking, wording, and shopping experience"; consumers include Shop and "select
  AI platforms, shopping sites, and AI agents"; no need for "a separate product feed for different
  channels".
- **Supports:** the aggregation mechanism; the hard limits on what a merchant can promise.

### ACA-SHOP-002
- **Source:** Selling on ChatGPT —
  https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/chatgpt
- **Tier:** 3 · **Fidelity:** byte (reader) · `notes/raw/sh-agentic-chatgpt.md`
- **Published:** Wed, 21 Oct 2026 (header in capture) — the freshest ChatGPT-shopping source here.
- **Excerpt (verbatim):** "The ChatGPT channel acts as a discovery-focused referrer platform for
  customers to find your products. It's active by default for eligible stores"
- **Excerpt (verbatim):** "You don't need to do anything for your products to be discovered by
  ChatGPT through Shopify Catalog."
- **Excerpt (verbatim):** "ChatGPT is a product discovery channel. Customers using ChatGPT are
  redirected to buy products in your online store checkout, therefore there's no option to activate
  or deactivate a ChatGPT direct checkout setting in your Shopify admin."
- **Excerpt (verbatim):** "Ensure that your product descriptions include any relevant legal
  disclosures in the first 6,000 characters."
- **Excerpt (verbatim):** "There are no fees associated with selling in ChatGPT. You pay only your
  standard payment processing fees."
- **Excerpt (verbatim):** "your products might still be displayed or referenced by the AI channel
  through other external discovery and listing methods, such as web crawling and indexing"
- **Supports:** automatic enrolment; referrer-only model; opt-out steps; the 6,000-char rule.
- **Contradiction:** direct-checkout statement vs `ACA-CGPT-001`. See `05`.
- **Fidelity note:** a rendered fetch of this page also asserted a Settings→Policies *eligibility*
  requirement for ChatGPT. That sentence is **not in the raw capture**, so it is excluded. The
  policy recommendation in `02` rests on `ACA-SHOP-008` instead, which is byte-verified.

### ACA-SHOP-003
- **Source:** Shopify Catalog and product discovery for agentic storefronts —
  https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/products
- **Tier:** 1/3 · **Fidelity:** byte (reader) · `notes/raw/sh-agentic-products.md`
- **Published:** Wed, 21 Oct 2026
- **Excerpt (verbatim):** "the products are listed by default with their title, description,
  options, images, price, availability, and other key attributes, all structured in a way that AI
  agents can parse and understand. Shopify Catalog continuously updates your product data, so AI
  channels receive your latest inventory and prices."
- **Excerpt (verbatim):** "Every Shopify store automatically serves the following discovery URLs…
  `/agents.md` — this is your canonical agent discovery URL… `/llms.txt` and `/llms-full.txt`"
- **Excerpt (verbatim):** "You don't need a third-party app to generate these files. Shopify Catalog
  is the authoritative product data feed to your agentic channels. The agent discovery files are
  separate from Shopify Catalog, and they don't replace any Shopify Catalog capabilities."
- **Excerpt (verbatim):** "Bot management is handled directly for stores on Shopify, and you don't
  need to take any action. Shopify doesn't recommend a proxy configuration in front of Shopify, and
  can't provide support for this either."
- **Excerpt (verbatim):** "The rules that you set in your `/robots.txt` file are directional and
  advisory, and not all crawlers are guaranteed to follow them."
- **Excerpt (verbatim):** "Shopify's agentic storefronts support only direct-to-consumer (D2C)
  sales."
- **Excerpt (verbatim):** "AI agents might use the list price to advertise strikethrough pricing"
- **Also records:** eligibility surface in admin; Channel mapping for metafields/metaobjects/tag
  prefixes/title delimiters; variant grouping into a single listing; `agents.md.liquid` /
  `llms.txt.liquid` / `llms-full.txt.liquid` precedence; **Unlisted** as the only full removal; B2B
  detection methods and the custom-app gap.
- **Supports:** playbook actions 1, 7, 9, 10, 12 and most of §5 in `01`.

### ACA-SHOP-004
- **Source:** Editing robots.txt.liquid —
  https://help.shopify.com/en/manual/promoting-marketing/seo/editing-robots-txt
- **Tier:** 1 · **Fidelity:** byte (reader) · `notes/raw/sh-robots.md`
- **Excerpt (verbatim):** "Blocking AI crawlers at the `/robots.txt` or network layer affects only
  open-web discoverability. It doesn't stop your product data from being sent by Shopify Catalog to
  the agentic storefronts that you've activated."
- **Excerpt (verbatim):** "If you sell through agentic storefronts such as ChatGPT or Microsoft
  Copilot, then your product data is syndicated to those channels through Shopify Catalog,
  independently of `/robots.txt`."
- **Excerpt (verbatim):** "You can use Liquid to add or remove directives from the
  **robots.txt.liquid** template. This method preserves Shopify's ability to keep the file updated
  automatically in the future, and is recommended."
- **Also records:** default rule rationale (`Allow: /`, `Disallow: /admin`, `/cart/`, `/checkout`,
  `/account`, `/orders`, `/collections/*+*`, `/collections/*sort_by*`); unsupported-customization
  warning; "Incorrect use of the feature can result in loss of all traffic"; theme uploads don't
  import the template; "Changes are instant, but crawlers don't always react immediately"; remove
  prior Cloudflare-style workarounds first.
- **Supports:** playbook action 8, and the opening warning in `02`.

### ACA-SHOP-005
- **Source:** Data sharing and privacy for selling with agentic storefronts —
  https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/data-privacy
- **Tier:** 1/3 · **Fidelity:** byte (reader) · `notes/raw/sh-data-privacy.md`
- **Excerpt (verbatim):** AI channels "don't have access to your full order history, orders from
  other sales channels, or your general customer database"
- **Also records:** `Allow Shopify to manage for me` default and that "New agentic storefronts are
  added automatically as they join"; the three per-channel outcomes; ChatGPT offers Catalog access
  only; Copilot direct checkout requires Catalog access; Google/Gemini and Meta discovery run
  through their own sales channels.
- **Supports:** which channels support in-channel checkout; default-on enrolment.

### ACA-SHOP-006
- **Source:** Global Catalog MCP — https://shopify.dev/docs/agents/catalog/global-catalog
- **Tier:** 1 · **Fidelity:** byte (reader) · `notes/raw/sh-global-catalog.md`
- **Excerpt (verbatim):** "Use Global Catalog MCP when your agent needs to discover products across
  multiple Shopify merchants — for example, comparison shopping, cross-merchant discovery, or
  recommendations not tied to a specific store."
- **Excerpt (verbatim):** "Results are clustered by Universal Product ID (UPID) and include offers
  from multiple merchants."
- **Excerpt (verbatim):** "Multiple IDs that resolve to the same product are grouped into a single
  product in the response."
- **Excerpt (verbatim):** "Filter by Shopify taxonomy attributes. Supported names are `Color`,
  `Size`, and `Target gender`. Entries combine with AND logic. Values within one entry combine with
  OR logic. Unsupported attribute names are ignored and returned in `messages`."
- **Excerpt (verbatim):** "Treat them as discovery and merchandising signals, not as
  merchant-authored source text." (of `Inferred` fields)
- **Excerpt (verbatim):** "The `/api/ucp/mcp` endpoint requires an agent profile."
- **Excerpt (verbatim):** "Buyer signals for relevance and localization (`address_country`,
  `address_region`, `postal_code`, `language`, `currency`, and `intent`)."
- **Supports:** filterability as the deterministic lever (playbook action 4); UPID clustering as the
  cross-merchant comparison mechanism; inferred-field behaviour (action 5).
- **`[paraphrase]`:** the full global host `catalog.shopify.com/api/ucp/mcp` — rendered client-side,
  absent from the text capture.
- **Negative finding:** no ranking algorithm is documented, and UPID derivation is not described.

### ACA-SHOP-007
- **Source:** Requirements for being included in Shopify Catalog —
  https://help.shopify.com/en/manual/shopify-catalog/requirements
- **Tier:** 1 · **Fidelity:** byte (reader) · `notes/raw/sh-catalog-requirements.md`
- **Published:** Wed, 21 Oct 2026
- **Excerpt (verbatim):** "Your store must be on the Starter plan or higher, and your store can't be
  in private mode."
- **Excerpt (verbatim):** "Your products must have a title and at least 1 product image."
- **Excerpt (verbatim):** "Your products must have a price greater than 0. Free products aren't
  included in Shopify Catalog."
- **Excerpt (verbatim):** "Your products can't have Unlisted status or be hidden from search
  engines."
- **Excerpt (verbatim):** "The overall standing of your Shopify account is based on a number of
  factors, and is reviewed over time."
- **Also records:** verify email, two-step auth, passkey, identity/business verification;
  "Maintain a track record of genuine sales to real customers"; "Keep your chargeback rate low";
  pay invoices on time; Shopify Payments in good standing; resolve policy issues. Excluded
  categories include alcohol, tobacco/vaping, drug paraphernalia, prescription/medical, weapons and
  imitation weapons, explosives, lab/hazardous, adult, sexual health, bullion/coins/virtual
  currency, prop money, services and add-ons, event tickets, live animals, and "Uncategorized
  products".
- **Supports:** playbook action 1 in full, including the account-standing finding.

### ACA-SHOP-008
- **Source:** Optimizing your products for AI platforms —
  https://help.shopify.com/en/manual/shopify-catalog/optimizing-products
- **Tier:** 1 · **Fidelity:** byte (reader) · `notes/raw/sh-catalog-optimizing.md`
- **Published:** Wed, 21 Oct 2026
- **Excerpt (verbatim):** "You can improve the way your products rank in search results by following
  these best practices"
- **Excerpt (verbatim):** "Product details that are considered by the AI platforms or shopping sites
  include the following fields:" — Title; Description; Images; "Product organization details such as
  **Type**, **Vendor**, **Collections**, and **Tags**"; "**Barcode (ISBN, UPC, GTIN, etc.)**";
  "**Variants**, including **Option name**"; "**External product URL**, for stores on the Shopify
  Agentic plan".
- **Excerpt (verbatim):** "Make sure that your store policies are complete and up-to-date. This is
  important, for example, so that when a customer asks about your return policy in an AI
  interaction, the AI agent can reference the correct information that you've stored in Shopify."
- **Supports:** playbook actions 2, 3, 6. This is the closest thing to an official field-level
  ranking list for a Shopify merchant.

### ACA-SHOP-009
- **Source:** Commerce for agents (UCP on Shopify) — https://shopify.dev/docs/agents
- **Tier:** 1 · **Fidelity:** rendered
- **Excerpt `[paraphrase]`:** Global Catalog vs Storefront Catalog; Cart/Checkout/Order MCP; an
  agent profile "hosted at a well-known URL and referenced on every UCP request" with trust tiers;
  `@shopify/ucp-cli`.
- **Supports:** only the existence of `@shopify/ucp-cli` as a test tool in playbook action 4.
  Everything substantive is carried by `ACA-SHOP-006`, which is byte-captured.
- **Related observation:** `shopify.dev/docs/apps/build/storefront-mcp` is marked **Removed** —
  "The catalog and cart tools on `https://{shop}/api/mcp` were removed", replaced by
  `https://{shop}/api/ucp/mcp` (rendered). Any guide referencing `/api/mcp` is out of date.

### ACA-SHOP-010
- **Source:** Answering customer questions with your knowledge base —
  https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/knowledge-base
- **Tier:** 1 · **Fidelity:** byte (reader) · `notes/raw/sh-knowledge-base.md`
- **Excerpt (verbatim, grep-verified):** "source of truth for AI agents for all non-product
  information" about the store.
- **Also records:** queried "through the Storefront MCP"; auto-generated from public storefront and
  admin data; scanned facts stay unpublished until published; Shopify "never changes knowledge base
  content on your behalf"; 1,000-fact cap; rescan up to 48 hours; fact types Paragraph / Yes-No /
  Tags; the old Knowledge Base app deprecates 2027-01-15.
- **Supports:** playbook action 6.

### ACA-SHOP-011
- **Source:** `robots.txt.liquid` theme reference + Liquid `robots` / `group` / `rule` objects —
  https://shopify.dev/docs/storefronts/themes/architecture/templates/robots-txt-liquid,
  https://shopify.dev/docs/api/liquid/objects/robots, `.../group`, `.../rule`
- **Tier:** 1 · **Fidelity:** byte (reader) for the template page and the object pages
- **Excerpt (verbatim):** "Adding this template replaces Shopify's generated `robots.txt` output."
- **Excerpt (verbatim):** "Before you publish a customization, save a copy of your current
  `/robots.txt` output and compare it with the rendered template output."
- **Excerpt (verbatim):** "The default rule groups for the `robots.txt` file." (`robots.default_groups`)
- **Excerpt (verbatim):** "A rule consists of a directive, which can be either `Allow` or `Disallow`,
  and a value of the associated URL path."
- **Supports:** the Liquid snippet in playbook action 8.
- **Fidelity note:** the doc's own code sample is rendered client-side and is not in the capture. The
  snippet in `02` is constructed from the documented object properties, not copied from the sample.
  Flagged as such there.

### ACA-SHOP-012
- **Source:** Agentic readiness scanner — https://www.shopify.com/agentic-readiness
- **Tier:** 2 · **Fidelity:** byte (reader) · `notes/raw/sh-agentic-readiness.md`
- **Excerpt (verbatim, grep-verified):** "check your product page for the structured data that AI
  agents read" (to answer shoppers' questions)
- **Also records:** results are "informational signals for your product page that AI agents may use
  to discover, evaluate, and recommend your products", with no guarantee; "Agentic Storefronts is
  enabled automatically for eligible stores".
- **Supports:** playbook action 11 and the free self-test.

---

## Protocol bodies

### ACA-PROTO-001
- **Source:** Agentic Commerce Protocol — https://agenticcommerce.dev/ and `/docs`
- **Tier:** 1 · **Fidelity:** rendered
- **Excerpt `[paraphrase]`:** "An open standard for programmatic commerce flows between buyers, AI
  agents, and businesses"; created by Stripe and OpenAI; Apache 2.0; OpenAI "the first AI platform
  to implement ACP with ChatGPT"; "discovery mechanisms for identifying ACP-enabled merchants are
  still being built"; docs cover architecture, capability negotiation, lifecycle, security,
  checkout, payments, webhooks. Repo:
  https://github.com/agentic-commerce-protocol/agentic-commerce-protocol
- **Supports:** ACP provenance only. The ACP mechanics cited in `01` come from `ACA-CGPT-003`
  (byte).
- **Negative finding:** the ACP docs site has **no product-feed or discovery section**. Feed
  behaviour is OpenAI-specific, not part of the open standard.

### ACA-PROTO-002
- **Source:** Universal Commerce Protocol — https://ucp.dev/
- **Tier:** 1 · **Fidelity:** rendered
- **Excerpt `[paraphrase]`:** "The common language for platforms, agents, and businesses";
  co-developed for shopping by Google, Shopify, Etsy, Wayfair, Target, Walmart, Amazon, Microsoft,
  Meta, Salesforce, Stripe; businesses "remain the Merchant of Record"; Apache 2.0; MCP, A2A and
  AP2 support; capabilities Catalog Search/Lookup, Cart, Identity Linking, Checkout, Order.
- **Supports:** that two overlapping protocols exist — ACP (OpenAI/Stripe) and UCP (Google/Shopify
  et al.) — and that OpenAI is absent from the UCP backer list as published.
- **Note:** ucp.dev does not mention ACP, and agenticcommerce.dev does not mention UCP. Neither
  describes a merger. **UH** that they converge.

---

## My own observations

### ACA-OBS-001
- **What:** fetched OpenAI's published crawler IP files.
- **Method:** `curl` of `openai.com/{searchbot,gptbot,chatgpt-user,adsbot}.json`, 2026-10-30.
- **Result:** all 200. `creationTime` values: searchbot 2026-01-02, gptbot 2026-09-22, chatgpt-user
  2026-10-27, adsbot 2026-05-12. `adsbot.json` has only two prefixes (`130.131.229.128/25`,
  `20.168.90.128/25`). Prefixes observed across files fall in 13.x, 20.x, 104.208–104.210.x,
  128.85.x, 132.196.x, 135.234.x, 172.182.x.
- **Classification:** EO.
- **Inference:** those ranges are Microsoft Azure. Consistent with Azure-hosted crawling; **does not
  establish** Bing-based retrieval. Keep as **UH**.

### ACA-OBS-002
- **What:** a live Shopify store's agent-discovery surface.
- **Method:** `curl https://www.allbirds.com/agents.md`, `/llms.txt`, `/.well-known/ucp`,
  2026-10-30. Saved: `notes/raw/ab_agents.md`, `ab_llms.txt`.
- **Result (verbatim from `/agents.md`):** "This store implements the [Universal Commerce
  Protocol](https://ucp.dev) for product discovery, carts, and checkout." It instructs agents to
  `GET https://www.allbirds.com/.well-known/ucp` and connect to
  `https://www.allbirds.com/api/ucp/mcp`, and points to the Shop skill at
  `https://shop.com/SKILL.md`.
- **Result (`/.well-known/ucp`):** `"version":"2026-08-25"`, services `dev.ucp.shopping` and
  `dev.ucp.common` over MCP at `https://weareallbirds.myshopify.com/api/ucp/mcp`, capabilities
  `checkout`, `cart`, `fulfillment`, `discount`, `buyer_consent`, `order`; prior versions
  `2026-04-08`, `2026-01-23`.
- **Result:** `/agents.md` and `/llms.txt` are **not** byte-identical (5,750 vs 5,793 bytes),
  despite the docs saying all three "return the same content" by default <sup>`[ACA-SHOP-003]`</sup>. Minor,
  but it means "identical by default" should not be assumed in tests.
- **Classification:** EO. One store, one timestamp. Not generalised.

### ACA-OBS-003
- **What:** AI-crawler directives in a live Shopify store's robots.txt.
- **Method:** `curl https://www.allbirds.com/robots.txt`, 2026-10-30.
- **Result:** only two `User-agent` groups — `*` and `adsbot-google`. No OpenAI, Google-Extended or
  other AI-specific group. `Allow: /` present; `Disallow` on `/admin`, `/cart/`, `/checkout`,
  `/checkouts/`, `/orders`, `/account`, `/services`, `/cdn/wpm/*.js`, `/sf_*`. One sitemap line.
- **Classification:** EO.
- **Supports:** Shopify's default is permissive to OpenAI agents, so "add robots.txt rules to get
  into ChatGPT" is a no-op on a default store.

### ACA-OBS-004
- **What:** does a Shopify PDP serve a declared `OAI-SearchBot` user agent, and what structured data
  does it carry?
- **Method:** `curl -A "OAI-SearchBot/1.4; +https://openai.com/searchbot"` against
  `https://www.allbirds.com/products/mens-tree-runners`, 2026-10-30. Saved:
  `notes/raw/allbirds-pdp.html`. Parsed with an isolated Python process.
- **Result:** HTTP 200, 804,715 bytes. Two `application/ld+json` blocks. Block 1 `@type:
  ProductGroup` with `@context`, `@id`, `productGroupID`, `name` ("Men's Tree Runner"), `brand`
  (`{"@type":"Brand","name":"Allbirds"}`), `description`, `image`, `sku`, `offers`
  (`priceCurrency` USD, `price` 100, `itemCondition` NewCondition, `availability` InStock),
  `variesBy`, `hasVariant` (per-size variant URLs). Block 2 contains **only** `aggregateRating`
  (`ratingValue` "4.6", `reviewCount` "9951") with no `@type` on the wrapper object.
- **Classification:** EO.
- **Caveat:** tests user-agent handling, not IP reputation or signature verification. A 200 here
  does not prove OpenAI's crawlers are served from their real IPs.

### ACA-OBS-005
- **What:** `agents.md` on a headless Shopify store.
- **Method:** `curl https://www.vuori.com/agents.md`, 2026-10-30 (redirects to vuoriclothing.com).
- **Result:** returned a Next.js HTML document with
  `<meta name="robots" content="noindex,nofollow">` and a canonical pointing at a `gift_cards`
  path — i.e. the SPA shell/fallback route, not agent instructions. Its robots.txt does contain
  AI/SEO-crawler groups (`AhrefsBot`, `SiteAuditBot`, `Nutch`).
- **Classification:** EO. n=1.
- **Why it matters:** Vuori is one of the Shopify merchants OpenAI named in `ACA-CGPT-001`.
  "Every Shopify store automatically serves… `/agents.md`" <sup>`[ACA-SHOP-003]`</sup> did not hold for this
  storefront as fetched. Either custom-storefront behaviour differs or the route is unhandled by the
  headless front end. Recorded as a gap, not as a refutation of the Shopify doc.

### ACA-OBS-006
- **What:** search-engine access during this session.
- **Method:** attempted DuckDuckGo (html + lite), Bing, Brave, searx.be, Mojeek, Marginalia.
- **Result:** DuckDuckGo served a CAPTCHA; searx.be a browser check; Brave HTTP 429; Mojeek 403;
  Bing returned results unrelated to the queries. Only direct URL fetching, vendor sitemaps, and a
  text-extraction proxy worked.
- **Classification:** EO.
- **Why it is in the registry:** it explains a methodological limitation of this round. Source
  discovery was done by vendor sitemap enumeration and link-following, not by search. Third-party
  commentary is therefore under-sampled relative to primary docs — which biases this report toward
  vendor self-description. See `05`.
