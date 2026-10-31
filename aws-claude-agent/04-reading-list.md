# Reading list

Every URL below was status-checked by me on **2026-10-30** and returned HTTP 200 unless noted.
Ordered by what it is actually useful for, not by prestige.

**Read this first.** Search engines blocked automated access throughout this session
(`[ACA-OBS-006]`): DuckDuckGo CAPTCHA, Brave 429, Mojeek 403, searx browser check, Bing returning
unrelated results. Sources were found by enumerating vendor sitemaps and following links from
primary docs. Consequence: **primary documentation is well covered; third-party SEO/industry
commentary is under-sampled.** That is a real limitation of this round, and it is why the "industry
commentary" section is short and honest rather than padded with plausible-looking links I could not
verify. If you want specific analyst or SEO-blog pieces covered, send URLs and I will fetch and
register them properly.

Also note the access asymmetry: `openai.com` and `help.openai.com` return **403** to non-browser
clients, so those pages were captured through the `r.jina.ai` text-extraction proxy. They open
normally in your browser.

---

## 1. If you read only four things

| # | Source | Why |
|---|---|---|
| 1 | **Shopify — Shopify Catalog and product discovery for agentic storefronts** · https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/products | The actual mechanism for a Shopify merchant. Explains why robots.txt is not the lever. |
| 2 | **Shopify — Optimizing your products for AI platforms** · https://help.shopify.com/en/manual/shopify-catalog/optimizing-products | The field-level list of what AI platforms read. Short. Act on it directly. |
| 3 | **OpenAI — Buy it in ChatGPT** · https://openai.com/index/buy-it-in-chatgpt/ | Contains the only published ChatGPT product-ranking factors. One paragraph; read it twice. |
| 4 | **OpenAI — Crawlers and user agents** · https://developers.openai.com/api/docs/bots | Settles which bot governs search visibility and which governs training. |

---

## 2. OpenAI / ChatGPT — primary (Tier 1–2)

**How products get in**
- Commerce docs index — https://developers.openai.com/commerce/
- Key concepts (the three ACP flows; the one ranking sentence) — https://developers.openai.com/commerce/guides/key-concepts
- Get started (approved-partners gate, SFTP, daily snapshot) — https://developers.openai.com/commerce/guides/get-started
- **Product feed schema** — https://developers.openai.com/commerce/specs/file-upload/products — the
  single densest document in this report. Required fields, GTIN check-digit rule, variant grouping,
  `is_eligible_search`, review fields. Note it never mentions schema.org.
- Products API schema (`categories.taxonomy` accepts `shopify`) — https://developers.openai.com/commerce/specs/api/products
- Best practices — https://developers.openai.com/commerce/guides/best-practices
- Production checklist — https://developers.openai.com/commerce/guides/production
- Whole corpus as one file, handy for diffing month to month — https://developers.openai.com/commerce/llms-full.txt
- Merchant application form — https://chatgpt.com/merchants

**Crawling, access, policy**
- Crawlers and user agents — https://developers.openai.com/api/docs/bots
- Published crawler IP ranges — https://openai.com/searchbot.json · https://openai.com/gptbot.json ·
  https://openai.com/chatgpt-user.json · https://openai.com/adsbot.json
- Signed-agent key directory — https://chatgpt.com/.well-known/http-message-signatures-directory
- Cloud browser / agent allowlisting (the target of the shopping-research "allowlisting" link) —
  https://help.openai.com/en/articles/11845367-chatgpt-agent-allowlisting
- Commerce policies — prohibited products — https://openai.com/policies/commerce-policies/
- Merchant Feed Terms of Service — https://openai.com/policies/merchant-feed-terms-of-service/ —
  read the crawler-blocking and no-guarantee clauses before any "block AI bots" decision.

**Announcements that state mechanism**
- Buy it in ChatGPT / Instant Checkout — https://openai.com/index/buy-it-in-chatgpt/
- Shopping research — https://openai.com/index/chatgpt-shopping-research/
- Introducing ChatGPT search (2024-10-31 — **stale**, cite only for history) — https://openai.com/index/introducing-chatgpt-search/
- Ads in ChatGPT — https://openai.com/index/expanding-access-to-ai-with-chatgpt-ads/

---

## 3. Shopify — primary (Tier 1, and Tier 3 where it describes ChatGPT)

All the `help.shopify.com` agentic pages carry a published date of **2026-10-21**, making them the
freshest sources in this report.

- Agentic storefronts overview — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts
- **Selling on ChatGPT** — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/chatgpt
- **Product discovery for agentic storefronts** — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/products
- Data sharing and privacy — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/data-privacy
- Knowledge base — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/knowledge-base
- Shopify Catalog — https://help.shopify.com/en/manual/shopify-catalog
- Catalog requirements (incl. account standing) — https://help.shopify.com/en/manual/shopify-catalog/requirements
- **Optimizing products for AI platforms** — https://help.shopify.com/en/manual/shopify-catalog/optimizing-products
- Customizing product data / channel mapping — https://help.shopify.com/en/manual/shopify-catalog/mapping
- Editing robots.txt.liquid — https://help.shopify.com/en/manual/promoting-marketing/seo/editing-robots-txt
- Optimizing your store for AI — https://help.shopify.com/en/manual/promoting-marketing/seo/optimizing-store-for-ai
- Crawling your store / Web Bot Auth for your own crawlers — https://help.shopify.com/en/manual/promoting-marketing/seo/crawling-your-store
- Free structured-data scanner — https://www.shopify.com/agentic-readiness
- Agentic storefronts product page — https://www.shopify.com/agentic-storefronts
- Supplemental terms — https://www.shopify.com/legal/terms-agentic-storefronts

**Developer surface**
- Commerce for agents (UCP on Shopify) — https://shopify.dev/docs/agents
- Quickstart — https://shopify.dev/docs/agents/get-started/quickstart
- **Global Catalog MCP** (UPID clustering, the filter list) — https://shopify.dev/docs/agents/catalog/global-catalog
- Storefront Catalog MCP — https://shopify.dev/docs/agents/catalog/storefront-catalog
- `robots.txt.liquid` template — https://shopify.dev/docs/storefronts/themes/architecture/templates/robots-txt-liquid
- Liquid `robots` object — https://shopify.dev/docs/api/liquid/objects/robots
- Storefront MCP (**marked Removed** — `/api/mcp` retired for `/api/ucp/mcp`; useful for spotting
  out-of-date tutorials) — https://shopify.dev/docs/apps/build/storefront-mcp

---

## 4. The two protocols

**ACP — Agentic Commerce Protocol (OpenAI + Stripe)**
- https://agenticcommerce.dev/ · https://agenticcommerce.dev/docs
- https://github.com/agentic-commerce-protocol/agentic-commerce-protocol
- Stripe implementation — https://docs.stripe.com/agentic-commerce
- Shared Payment Tokens — https://docs.stripe.com/agentic-commerce/concepts/shared-payment-tokens

**UCP — Universal Commerce Protocol (Google, Shopify, Etsy, Walmart, Amazon, Microsoft, Meta,
Salesforce, Stripe, Target, Wayfair)**
- https://ucp.dev/
- https://github.com/Universal-Commerce-Protocol/ucp
- Google's merchant-side integration — https://developers.google.com/merchant/ucp/
- Observed live on a Shopify store — https://www.allbirds.com/.well-known/ucp ·
  https://www.allbirds.com/agents.md · https://shop.com/SKILL.md

Worth knowing: neither protocol's site mentions the other. Treat convergence talk as speculation.

**Underlying standard**
- RFC 9421, HTTP Message Signatures (what Web Bot Auth is built on) — https://www.rfc-editor.org/rfc/rfc9421.html

---

## 5. Structured data

- schema.org `Product` — https://schema.org/Product
- Google product structured data (the de-facto reference most themes follow) —
  https://developers.google.com/search/docs/appearance/structured-data/product
- Google Merchant Center product data spec — https://support.google.com/merchants/answer/7052112 —
  still the cleanest field-by-field reference for retail attributes, and the vocabulary
  (`gtin`, `mpn`, `condition`, `availability`, `age_group`, `size_system`) that OpenAI's feed spec
  closely parallels without citing.

---

## 6. Industry commentary (short, by necessity)

Only pieces I could actually verify. Each is a genuinely independent account of AI-agent traffic —
useful precisely because they are not vendor self-description, which everything above is.

- **Cloudflare — Signed Agents** — https://blog.cloudflare.com/signed-agents/ — how the
  infrastructure layer now distinguishes a legitimate shopping agent from a scraper. Directly
  relevant to playbook action 9.
- **Cloudflare — Web Bot Auth** — https://blog.cloudflare.com/web-bot-auth/ — the mechanism behind
  the `Signature-Agent` header OpenAI asks you to allowlist.
- **Cloudflare — "Perplexity is using stealth, undeclared crawlers…"** —
  https://blog.cloudflare.com/perplexity-is-using-stealth-undeclared-crawlers-to-evade-website-no-crawl-directives/
  — the evidential counterweight to every vendor crawler policy: declared user agents and published
  IP ranges are claims, not guarantees. Read before trusting any robots.txt-based control.
- **Cloudflare — verified bots directory** — https://developers.cloudflare.com/bots/concepts/bot/verified-bots/

Known-blocked to automated fetch but fine in a browser: Search Engine Land (`403`). I did not cite
anything from it, and no claim in `01`/`02` rests on a Tier 4 source.

---

## 7. For round 2 (Gemini)

Already located, not yet read:
- Shopify — Selling on Google AI Mode and Gemini — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google
- Shopify — Selling on Microsoft Copilot — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/microsoft
- Google — merchant UCP integration — https://developers.google.com/merchant/ucp/
- Google Merchant Center product data spec — https://support.google.com/merchants/answer/7052112

The structural difference to test first: Shopify says Google AI Mode and Gemini discovery "is
powered by individual sales channels rather than a Shopify Catalog access setting"
`[ACA-SHOP-005]`, and that those channels **do** support in-channel checkout — unlike ChatGPT. So
for Gemini the Google & YouTube sales channel and Merchant Center feed are the levers, not Shopify
Catalog.
