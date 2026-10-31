# Agent D: how marketplace products reach ChatGPT

- Scope: For 14 marketplaces: (a) official relationship with ChatGPT/OpenAI; (b) robots.txt treatment of OpenAI crawlers (OAI-SearchBot, GPTBot, ChatGPT-User). Also: India commerce initiatives, Amazon's stance on AI shopping agents, OpenAI docs on marketplace listings.
- Date: 2026-10-30. Status: complete for this pass (see Knowledge gaps).
- Method:
  - robots.txt: raw HTTP GET with `curl` on 2026-10-30 (~09:10–09:30 UTC). First pass sent a desktop Chrome User-Agent. Second pass sent curl's default User-Agent. Content was byte-identical between passes for every site that answered both, except Etsy (a random ASCII-art greeting comment differs). No crawler User-Agent was spoofed. Exact lines are quoted from the saved files.
  - Announcements: official newsrooms fetched raw with `curl` and converted to text; openai.com and etsy.com/news return 403 to direct fetches, so Wayback Machine `id_` snapshots were used (snapshot timestamps given per finding).
  - Court filings: CourtListener RECAP PDFs (N.D. Cal. docket 3:25-cv-09514) and the Ninth Circuit opinion PDF (No. 26-1444), via the Knight First Amendment Institute mirror; Calcutta High Court order (IndiaMART v. OpenAI) via a MediaNama-hosted PDF.
  - help.openai.com and chatgpt.com/merchants return 403 to curl/WebFetch; read with an in-app browser tab (rendered text).
  - robots.txt history: Wayback CDX index + `id_` captures for amazon.com and ebay.com.
- Limits of robots.txt evidence: a snapshot shows declared crawl policy on the access date only. It does not show whether OpenAI honors it, whether ChatGPT receives the marketplace's data through feeds, apps or third-party providers, or what ChatGPT actually displays.

## 1. Summary table

Legend: "No OpenAI group" = no user-agent group names OAI-SearchBot, GPTBot or ChatGPT-User; those bots then fall under the `*` group.

| Marketplace | Official ChatGPT/OpenAI relationship (finding) | OAI-SearchBot | GPTBot | ChatGPT-User | robots.txt fetch |
|---|---|---|---|---|---|
| Amazon.com | None for ChatGPT shopping found. Feb 27 2026 Amazon–OpenAI partnership = investment, AWS compute, custom models for Amazon apps (D-20). Blocks agents by robots.txt and Agent Terms; litigating Perplexity (D-17–D-19, D-23) | `Disallow: /` (since ≈2025-11-12) | `Disallow: /` (since ≤2024-01-01) | `Disallow: /` (since ≈2025-11-12) | 200 OK |
| Amazon.in | None found | `Disallow: /` | `Disallow: /` | `Disallow: /` | 200 OK |
| Walmart | Instant Checkout partnership announced Oct 14 2025 (D-07) → Walmart app in ChatGPT, Mar 24 2026 (D-08) → Agent Gateway/terms, Oct 21 2026 (D-09). US | No OpenAI group | No OpenAI group | No OpenAI group | 200 OK |
| Etsy | First live Instant Checkout partner, Sep 29 2025 (D-05) → Etsy app in ChatGPT, beta, May 5 2026 (D-10); catalog "already integrated" per OpenAI (D-22). US | No OpenAI group | No OpenAI group | No OpenAI group | 200 OK |
| eBay | Operator research-preview collaboration, Jan 23 2025 (D-12). No ChatGPT app/checkout found. robots.txt bans buy-for-me agents in checkout (D-02) | Dedicated group = `*` rules + `Allow: /sch/` (added Apr–Oct 2026) | `Disallow: /` except info pages (added Mar 2026) | Same group as OAI-SearchBot | 200 OK |
| Target | Target app in ChatGPT, beta from late Nov 2025; ads test Feb 2026; ACP discovery feed, Mar 2026 (D-11, D-08). US | No OpenAI group | No OpenAI group | No OpenAI group | 200 OK |
| Flipkart | None found (D-27). ChatGPT shopping results US-only (D-22) | No OpenAI group | No OpenAI group | No OpenAI group | 200 OK |
| Myntra | None found (D-27) | No OpenAI group | No OpenAI group | No OpenAI group | 200 OK (Chrome UA); curl UA: connection failed |
| Meesho | None found (D-27) | No OpenAI group | No OpenAI group | No OpenAI group | 403 (Chrome UA); 200 OK (curl UA) |
| JioMart | None found (D-27) | No OpenAI group | No OpenAI group | No OpenAI group | 200 OK |
| Mercado Libre (MX/BR/AR) | None found (D-29) | No OpenAI group (falls to `*`) | `Disallow: /` | `Disallow: /` | 200 OK (Chrome UA); 403 (curl UA). Item subdomains: 403 |
| Rakuten Ichiba (JP) | 2023 MoU (API, plugin-era business AI) (D-26); no ChatGPT shopping integration found | No OpenAI group | No OpenAI group | No OpenAI group | 200 OK (curl UA); Chrome UA got an Akamai stub |
| Shopee (SG, ID, TH, PH, VN, MY, TW, BR) | Sea × OpenAI partnership; Shopee app in ChatGPT in 8 markets, Jun 22 2026 (D-24) | No OpenAI group | No OpenAI group | No OpenAI group | 200 OK |
| Lazada (SG, MY, TH, PH, VN) | None found | `Allow: /` | `Allow: /` | `Allow: /` | 200 OK |
| Lazada (ID) | None found | No OpenAI group | No OpenAI group | No OpenAI group | 200 OK |
| Allegro (PL) | Allegro app in ChatGPT, May 12 2026; partnership ≈May 11 2026 (D-25) | No OpenAI group | No OpenAI group | No OpenAI group | 200 OK |

Cross-cutting: OpenAI states merchants are ranked partly on "whether they are the maker or primary seller" (D-21, D-05); its feed spec separates `seller_name` from `marketplace_seller` (D-06); shopping results are US-only (D-22); an Indian court order records OpenAI relying on the USTR Notorious Markets list for a marketplace (D-14).

## 2. Findings

Note: IDs are stable references; D-15 and D-16 appear before D-13 and D-14 because the file was written incrementally.

### D-01 Amazon.com and Amazon.in disallow all three OpenAI agents site-wide
- Claim: On 2026-10-30, amazon.com and amazon.in robots.txt each contain separate groups that disallow `/` for GPTBot, ChatGPT-User and OAI-SearchBot.
- Classification: VERIFIED FACT
- Source: robots.txt — Amazon — https://www.amazon.com/robots.txt ; https://www.amazon.in/robots.txt
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (identical in both files):
  > "User-agent: GPTBot
  > Disallow: /"
  >
  > "User-agent: ChatGPT-User
  > Disallow: /"
  >
  > "User-agent: OAI-SearchBot
  > Disallow: /"
- Establishes: Amazon's declared crawl policy excludes OpenAI's search crawler, training crawler and user-triggered fetcher from the whole site. The same files also disallow `/` for ClaudeBot, Claude-User, Claude-SearchBot, PerplexityBot, Perplexity-User, Google-Extended, GoogleAgent-Mariner, GoogleAgent-Shopping, meta-externalagent, Copilot and about 90 other AI/agent tokens.
- Limitations: OpenAI's crawler docs state robots.txt "may not apply" to ChatGPT-User (D-15). OpenAI docs state an OAI-SearchBot opt-out still allows "navigational links" (D-15). The file does not show whether Amazon product data reaches ChatGPT through other channels (feeds, third-party data providers, the Feb 2026 Amazon–OpenAI partnership). Not proof that ChatGPT never shows Amazon products.

### D-02 eBay gives OAI-SearchBot and ChatGPT-User a dedicated group that allows search pages, and blocks GPTBot
- Claim: eBay's robots.txt (version string "v30.2_COM_August_2026") puts GPTBot in an "LLM / AI bot" group with `Disallow: /`, and puts OAI-SearchBot, ChatGPT-User, Claude-SearchBot and Claude-User in a separate group. That group copies the `*` rules except it replaces the `/sch/` rule set with `Allow: /sch/` and omits two GraphQL disallows. It also has an OAI-AdsBot group limited to ad-tagged item and browse URLs. The file header prohibits buy-for-me agents in checkout.
- Classification: VERIFIED FACT (contents of the file). The reading "eBay intends ChatGPT search to see search-result pages that ordinary crawlers may not" is EVIDENCE-BASED INFERENCE.
- Source: robots.txt — eBay — https://www.ebay.com/robots.txt
- Published/updated: file comment "v30.2_COM_August_2026"
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "# Checkouts are strictly for human users. 
  > # * Automated scraping, buy-for-me agents, LLM-driven bots, or any 
  > #   end-to-end flow that attempts to place orders without human review 
  > #   is strictly prohibited."

  > "User-agent: Bytespider
  > User-agent: CCBot
  > User-agent: ChatGLM-Spider
  > User-agent: ClaudeBot
  > User-agent: PerplexityBot
  > User-agent: anthropic-ai
  > User-agent: AmazonBot
  > User-agent: meta-externalagent
  > User-agent: GPTBot
  > User-agent: Applebot-Extended
  > Disallow: /"
  > (followed by `Allow:` lines for /adchoice, /authenticity-guarantee, /motors/blog, /motors/diy, /help, /sellercenter, /ebaylive/seller, /sl/sell, /sh/landing, /giftcards, /shp/calc/rates)

  > "User-agent: OAI-SearchBot
  > User-agent: ChatGPT-User
  > User-agent: Claude-SearchBot
  > User-agent: Claude-User
  > Disallow: /*_kw"
  > … "Allow: /sch/
  > Disallow: /sch/ajax
  > Disallow: /sch/ebayadvsearch?_"

  > "User-agent: OAI-AdsBot
  > Allow: /b/*?*mkcid=32*
  > Allow: /itm/*?*mkcid=32* 
  > Disallow: /"
- Diff method: lines 30–264 (`*` group) vs lines 787–1009 (OpenAI/Claude search group) with `diff`. Differences: `*` has `Disallow: /d/graphql`, `Disallow: /looking-glass-proxy/graphql`, and a 10-line `/sch/` block ending `Disallow: /sch/`; the OpenAI group has only `Allow: /sch/`. Item pages (`/itm/`) get the same rules in both groups.
- Establishes: eBay treats OpenAI's search and user-fetch agents differently from OpenAI's training crawler, and more permissively than generic crawlers for `/sch/` search pages.
- History (Wayback captures of https://www.ebay.com/robots.txt, VERIFIED FACT): version "v24.2_COM_September_2025" (capture 2025-11-08) has no "buy-for-me" text; "v24.3_COM_November_2025" (capture 2025-11-20) adds the buy-for-me prohibition. GPTBot first appears in "v25_COM_March_2026" (capture 2026-03-26). No OAI-SearchBot, ChatGPT-User or OAI-AdsBot group in any capture through "v26.2_COM_April_2026" (2026-04-27). So the OpenAI search/user group and the OAI-AdsBot group were added between 2026-04-27 and 2026-10-30 (live file "v30.2_COM_August_2026").
- Limitations: Declared policy only. Does not show any eBay–OpenAI data feed. No Wayback captures after 2026-04-27 were listed in the CDX index, so the exact addition date is unknown.

### D-03 Lazada (SG, MY, TH, PH, VN) explicitly allows all three OpenAI agents; Lazada Indonesia does not name them
- Claim: lazada.sg, lazada.com.my, lazada.co.th, lazada.com.ph and lazada.vn robots.txt end with explicit `Allow: /` groups for OAI-SearchBot, GPTBot and ChatGPT-User. lazada.co.id has no OpenAI group.
- Classification: VERIFIED FACT
- Source: robots.txt — Lazada — https://www.lazada.sg/robots.txt (and .com.my, .co.th, .com.ph, .vn, .co.id)
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (lazada.sg, full file tail):
  > "User-agent: OAI-SearchBot
  > Allow: /
  > User-agent: GPTBot
  > Allow: /
  > User-agent: ChatGPT-User
  > Allow: /"
- lazada.co.id full file:
  > "User-agent: *
  > Disallow: /wow/gcp/id/member/login-signup
  > Disallow: /undefined/
  > Disallow: */undefined/$
  > Disallow: */undefined$
  > User-agent: Googlebot-Image"
- Establishes: Lazada is the only marketplace in scope that names OpenAI agents in order to allow them.
- Limitations: An explicit Allow does not establish a partnership. No Lazada × OpenAI announcement has been checked yet. The `*` group in these files already allows nearly everything, so the explicit groups change little in practice.

### D-04 Mercado Libre blocks GPTBot and ChatGPT-User but does not name OAI-SearchBot
- Claim: mercadolibre.com.mx, mercadolivre.com.br and mercadolibre.com.ar robots.txt open with one group that disallows `/` for Amazonbot, PerplexityBot, Perplexity-User, ClaudeBot, Claude-User, GPTBot and ChatGPT-User. OAI-SearchBot is not named, so it falls under `*`, which allows product paths.
- Classification: VERIFIED FACT (file contents). "OAI-SearchBot may crawl Mercado Libre listing pages" is EVIDENCE-BASED INFERENCE from robots.txt grouping rules.
- Source: robots.txt — Mercado Libre — https://www.mercadolibre.com.mx/robots.txt (BR and AR files have the same first group)
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "User-agent: Amazonbot
  > User-agent: PerplexityBot
  > User-agent: Perplexity-User
  > User-agent: ClaudeBot
  > User-agent: Claude-User
  > User-agent: GPTBot
  > User-agent: ChatGPT-User
  > Disallow: /"
- Establishes: Mercado Libre separates OpenAI's search crawler (not blocked) from OpenAI's training crawler and user-fetcher (blocked).
- Limitations: Product detail pages live on subdomains (articulo.mercadolibre.com.mx, produto.mercadolivre.com.br). Their robots.txt returned HTTP 403 to curl; not captured. The root-domain file may not govern those hosts.

### D-05 OpenAI launched Instant Checkout with US Etsy sellers on 2025-09-29 and stated a ranking rule that mentions "primary seller"
- Claim: OpenAI's launch post says US ChatGPT Plus, Pro and Free users can buy from US Etsy sellers in chat, with Shopify merchants "coming soon". It says product results are "organic and unsponsored". It lists "whether a merchant is the primary seller" as a factor when ranking multiple merchants that sell the same product.
- Classification: VERIFIED FACT (what the post says, as of the snapshot). Superseded in part by D-08.
- Source: Buy it in ChatGPT: Instant Checkout and the Agentic Commerce Protocol — OpenAI — https://openai.com/index/buy-it-in-chatgpt/ (direct fetch: 403; read via Wayback snapshot https://web.archive.org/web/20261022061422id_/https://openai.com/index/buy-it-in-chatgpt/ , captured 2026-10-22)
- Published/updated: September 29, 2025; no update note in the 2026-10-22 snapshot
- Accessed: 2026-10-30
- Tier: 1 (via archive)
- Excerpt:
  > "U.S. ChatGPT Plus, Pro, and Free users can now buy directly from U.S. Etsy sellers right in chat, with over a million Shopify merchants, like Glossier, SKIMS, Spanx and Vuori, coming soon. Today, Instant Checkout supports single-item purchases."

  > "Product results are organic and unsponsored, ranked purely on relevance to the user."

  > "Instant Checkout items are not preferred in product results. When ranking multiple merchants that sell the same product, ChatGPT considers factors like availability, price, quality, whether a merchant is the primary seller, and whether Instant Checkout is enabled, to optimize the user experience."
- Establishes: OpenAI's own stated ranking factors for same-product, multi-merchant results as of Sep 2025. "Primary seller" is the only factor that touches the marketplace-vs-brand question.
- Limitations: "Primary seller" is not defined in the post. The post predates the March 2026 shift (D-08) and the Feb 2026 ads test (D-11). The post was not edited to reflect the Instant Checkout change, so the page is outdated on checkout.

### D-06 OpenAI's product feed spec has a `marketplace_seller` field separate from `seller_name`
- Claim: OpenAI's Agentic Commerce product feed spec requires `seller_name` on every row. For third-party marketplace offers it defines `marketplace_seller` ("Marketplace where checkout occurs") as "Conditionally required" and dependent on feed setup. Standard uploads target the US only.
- Classification: VERIFIED FACT (spec text). How ChatGPT labels marketplace offers in the UI is not stated in the spec: UNVERIFIED.
- Source: Agentic Commerce — full documentation (Products, file upload spec) — OpenAI Developers — https://developers.openai.com/commerce/llms-full.txt (page twin: https://developers.openai.com/commerce/specs/file-upload/products.md)
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "| `seller_name`  | String         | Required    | Name of the seller supplying this offer. For marketplace offers, see [merchant information](#merchant-info)."

  > "For a third-party seller, `seller_name` identifies that seller and
  > `marketplace_seller` identifies the marketplace where checkout occurs. The
  > latter requires [feed setup](#additional-supported-data)."

  > "| `marketplace_seller` | String           | Conditionally required for third-party marketplace offers; requires setup | Marketplace where checkout occurs. Keep distinct from the supplying `seller_name`."

  > "The standard OpenAI-format upload currently targets the US."

  > "Onboarding product feeds in ChatGPT is currently available to approved
  >   partners."
- Also in the spec: `seller_url` "For a marketplace offer, use the specific seller's page."; `store_review_count` / `store_star_rating` (store-level reviews, "requires setup"); `target_countries` "the shared format currently represents `US`, `CA`, and `MX`"; Key concepts page: "recommended attributes—like rich media, reviews, and performance signals—improve ranking, relevance, and user trust."
- Establishes: OpenAI's data model distinguishes the supplying seller from the marketplace where checkout happens. A marketplace can submit third-party offers through ACP feeds.
- Limitations: The spec describes inputs, not display or ranking. It does not say which marketplaces have feeds. Access is limited to "approved partners".

### D-07 Walmart × OpenAI: Instant Checkout partnership announced 2025-10-14
- Claim: Walmart announced a partnership with OpenAI that "will start with" letting Walmart and Sam's Club customers "soon" shop through ChatGPT using Instant Checkout.
- Classification: VERIFIED FACT (announcement content). Superseded in part by D-08 (Walmart moved to an app).
- Source: Walmart Partners with OpenAI to Create AI-First Shopping Experiences — Walmart Inc. — https://corporate.walmart.com/news/2025/10/14/walmart-partners-with-openai-to-create-ai-first-shopping-experiences
- Published/updated: Oct. 14, 2025
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Today, the company announced a new partnership with OpenAI that will start with allowing customers and members to soon shop Walmart through ChatGPT using Instant Checkout."
  > "Partnership will allow customers and members to complete purchases from Walmart directly within ChatGPT."
- Establishes: Official start of the Walmart–OpenAI commerce relationship; US.
- Limitations: Announcement of intent ("soon"). No launch date for Instant Checkout is in the post.

### D-08 OpenAI (2026-03-24): merchants may use their own checkout; ACP extended to discovery; Walmart app in ChatGPT; named retailers integrated for discovery
- Claim: OpenAI said the initial Instant Checkout "did not offer the level of flexibility" it wanted, so merchants can use their own checkout while OpenAI focuses on product discovery. ACP now carries product feeds and promotions for discovery. Target, Sephora, Nordstrom, Lowe's, Best Buy, The Home Depot and Wayfair "have integrated into ACP for discovery". Shopify merchant data reaches ChatGPT through Shopify Catalog. Walmart launched an in-ChatGPT app with account linking, loyalty and Walmart payments.
- Classification: VERIFIED FACT (post content)
- Source: Powering Product Discovery in ChatGPT — OpenAI — https://openai.com/index/powering-product-discovery-in-chatgpt/ (direct fetch: 403; read via Wayback https://web.archive.org/web/20261012013103id_/https://openai.com/index/powering-product-discovery-in-chatgpt/ , captured 2026-10-12)
- Published/updated: March 24, 2026
- Accessed: 2026-10-30
- Tier: 1 (via archive)
- Excerpt:
  > "We’ve found that the initial version of Instant Checkout did not offer the level of flexibility that we aspire to provide, so we’re allowing merchants to use their own checkout experiences while we focus our efforts on product discovery."

  > "Through ACP, merchants share product feeds and promotions so their catalogs are fully represented in ChatGPT. We support multiple delivery paths, including through third-party providers like Salesforce and Stripe, so merchants can participate with the systems they already use."

  > "Already, leading retailers including Target, Sephora, Nordstrom, Lowe’s, Best Buy, The Home Depot, and Wayfair have integrated into ACP for discovery."

  > "For merchants on Shopify, product data is already integrated into ChatGPT through Shopify Catalog, helping products appear more accurately and completely in relevant user conversations."

  > "Today, we are excited to share that Walmart is introducing an in-ChatGPT app experience that takes users from discovery in ChatGPT into a tailored Walmart environment that supports account linking, loyalty and Walmart payments."

  > "These updates are rolling out to all ChatGPT free, Go, Plus, and Pro users this week"
- Establishes: Since 2026-03-24 the primary official path for retailer catalogs into ChatGPT is ACP product feeds (discovery), plus optional merchant apps. No marketplace from this agent's list except Walmart and Target is named. Amazon, eBay, Etsy are not named in the discovery list.
- Limitations: The post does not say whether Instant Checkout was fully removed. Trade press differs on dates (Mar 4, 5, 17, 20) for the earlier pullback (see Contradictions).

### D-09 Walmart (2026-10-21): Agent Profiles, Walmart Agent Gateway (MCP), terms for AI agents; lists ChatGPT among its integrations
- Claim: Walmart lists "conversational commerce integrations with Muse, ChatGPT, Gemini and others". It announced Agent Profiles (launching "in the next month"), a Walmart Agent Gateway using MCP (beta for companies/developers) and terms that agents must follow or be blocked.
- Classification: VERIFIED FACT
- Source: Walmart Makes It Possible for Agents to Shop on Behalf of Customers, While Keeping Customers in Control — Walmart Inc. — https://corporate.walmart.com/news/2026/10/Making-It-Possible-for-Agents-to-Shop-on-Behalf-of-Customers
- Published/updated: Oct. 21, 2026
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Today, we serve customers through stores and clubs, online shopping, pickup and delivery, Sparky and conversational commerce integrations with Muse, ChatGPT, Gemini and others."

  > "we are building the Walmart Agent Gateway which will give agents a faster, more reliable way to shop by using an MCP (model text protocol)."

  > "Agents that do not follow these terms will be blocked from Walmart’s site."

  > "We price products, not people, so the prices that an AI agent sees are the same prices that a human would see on Walmart.com"
- Establishes: As of Oct 2026 Walmart's official position is to admit third-party agents under its own terms and a dedicated MCP gateway. Note: "model text protocol" is Walmart's wording (MCP usually expands to Model Context Protocol).
- Limitations: Agent Profiles and Gateway were not yet launched on the publication date.

### D-10 Etsy: first live Instant Checkout partner (Sep 2025); Etsy app in ChatGPT live in beta (2026-05-05), purchase completes on Etsy
- Claim: Etsy says it was the "first live integration partner" for ChatGPT Instant Checkout and that ChatGPT "works well as a discovery channel". The Etsy app in ChatGPT returns listings that users can compare or click through to Etsy.
- Classification: VERIFIED FACT
- Source: From Keywords to Conversation: Etsy’s next steps into conversational search with an app in ChatGPT — Etsy, Inc. — https://www.etsy.com/news/from-keywords-to-conversation-etsyas-next-steps-into-conversational-search-with-app-in-chatgpt (direct fetch: 403; read via Wayback https://web.archive.org/web/20260514223505id_/… , captured 2026-05-14)
- Published/updated: 5 May 2026
- Accessed: 2026-10-30
- Tier: 1 (via archive)
- Excerpt:
  > "The Etsy app in ChatGPT is now live in beta, allowing users to search and compare Etsy items directly in conversation."

  > "In September, we became the first live integration partner for ChatGPT Instant Checkout. That experience made something clear: ChatGPT works well as a discovery channel. Shoppers often chose to come to Etsy from their chats to learn more before making a purchase."
- Supporting (Tier 3): TechCrunch, "Etsy launches its app within ChatGPT as it continues its AI push", 2026-05-05, https://techcrunch.com/2026/05/05/etsy-launches-its-app-within-chatgpt-as-it-continues-its-ai-push/ — "However, the initiative ended in March" (refers to Instant Checkout).
- Also: Etsy llms.txt (https://www.etsy.com/llms.txt, "Last updated: 2026-09-25") states its robots.txt "applies one ruleset to all user agents with no AI-specific carve-outs." This matches the robots.txt fetch.
- Establishes: Etsy moved from in-chat checkout to an app that hands off purchase to Etsy.
- Limitations: Etsy's post does not state the app's country availability. "Ended in March" is a Tier 3 claim; Etsy's post does not say Instant Checkout ended.

### D-11 Target: app in ChatGPT (beta from late Nov 2025), ACP discovery, and an ads test in ChatGPT (Feb 2026)
- Claim: Target announced a ChatGPT app with multi-item baskets, fresh food and Drive Up/Order Pickup/shipping, launching in beta the week after 2025-11-19. A Feb 2026 fact sheet describes Target and Roundel testing "Sponsored, contextual and clearly labeled ads" in ChatGPT. A June 2026 fact sheet says Target has shopping experiences in Google, Microsoft Copilot and ChatGPT.
- Classification: VERIFIED FACT
- Sources:
  - Target to Launch First-of-its-Kind Conversational, Curated Shopping Experience in ChatGPT — Target Corp. — https://corporate.target.com/press/release/2025/11/target-to-launch-first-of-its-kind-conversational,-curated-shopping-experience-in-chatgpt — Nov 19, 2025
  - About Target's conversational AI advertising test — Target Corp. — https://corporate.target.com/press/fact-sheet/2026/02/conversational-ai-advertising — Updated Feb 9, 2026
  - Target Shopping Experiences in Conversational AI — Target Corp. — https://corporate.target.com/press/fact-sheet/2026/06/conversational-ai — Updated Jun 18, 2026
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Launching next week in beta, Target will offer a complete shopping experience through its app in ChatGPT, with the ability to purchase multiple items in a single transaction, shop fresh food products, and select drive up, pick up or shipping fulfillment options."

  > "Ads are served based on keywords in a guest’s ChatGPT prompt, ensuring they’re relevant to the conversation. … This ad would appear separately and distinctly, and not influence the answer provided by ChatGPT."

  > "Target is the first mass retailer with shopping experiences available to consumers across three leading AI platforms: Google Search, including AI Mode, and the Gemini app; Microsoft Copilot; and OpenAI’s ChatGPT."
- Establishes: Target reaches ChatGPT through three channels: its own app, ACP discovery feeds (D-08), and paid ads (test).
- Limitations: Region not stated explicitly in the ChatGPT sections; checkout uses a Target account (US context).

### D-12 eBay × OpenAI: Operator research-preview collaboration (2025-01-23); no ChatGPT checkout or app found
- Claim: eBay announced it was one of the first companies collaborating with OpenAI on the Operator research preview.
- Classification: VERIFIED FACT (announcement). "No eBay app/checkout in ChatGPT exists" is UNVERIFIED (searches found none).
- Source: Announcing a New Collaboration Between eBay and OpenAI — eBay Inc. — https://innovation.ebayinc.com/stories/ebay-openai-operator-assistant/
- Published/updated: Jan 23, 2025
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Operator acts as a virtual assistant, autonomously performing tasks across the internet, including online shopping, and directs users to eBay for unique inventory finds."
- Establishes: eBay's only OpenAI consumer-shopping tie found is Operator (2025). eBay's Aug 2026 robots.txt now prohibits "buy-for-me agents" in checkout (D-02).
- Limitations: Operator has since been folded into ChatGPT agent (not verified here). Seller-side ChatGPT Enterprise offers exist in press (Tier 3), not checked at source.

### D-15 OpenAI crawler docs: OAI-SearchBot opt-out removes a site from ChatGPT search answers except navigational links; robots.txt "may not apply" to ChatGPT-User; OAI-AdsBot exists
- Claim: See excerpt.
- Classification: VERIFIED FACT
- Source: Overview of OpenAI Crawlers — OpenAI Developers — https://developers.openai.com/api/docs/bots (Markdown twin https://developers.openai.com/api/docs/bots.md)
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Sites that are opted out of OAI-SearchBot will not be shown in ChatGPT search answers, though can still appear as navigational links."

  > "Because these actions are initiated by a user, robots.txt rules may not apply. ChatGPT-User is not used to determine whether content may appear in Search."

  > "OAI-AdsBot is used to validate the safety of web pages submitted as ads on ChatGPT."

  > "For search results, please note it can take ~24 hours from a site’s robots.txt update for our systems to adjust."
- Establishes: Interpretation key for the table. Amazon (OAI-SearchBot disallowed) is, per OpenAI's own rule, excluded from ChatGPT search answers built from crawling, except navigational links. Sites with no OpenAI group (Walmart, Target, Etsy, Flipkart, etc.) are crawlable by OAI-SearchBot subject to `*` rules.
- Limitations: The doc covers crawled web content. It does not address products that enter ChatGPT through ACP feeds, Shopify Catalog, merchant apps or licensed third-party data.

### D-16 Remaining robots.txt observations (no OpenAI-specific group)
- Classification: VERIFIED FACT
- Accessed: 2026-10-30 · Tier: 1 · Published/updated: not stated (all)
- Walmart (https://www.walmart.com/robots.txt): groups only for `*`, Adsbot-Google, Mediapartners-Google, Slurp. `*` includes "Disallow: /search" and does not disallow `/ip/` product paths.
- Target (https://www.target.com/robots.txt): single `*` group. Includes "Disallow: /s?" and "Disallow: /cart"; no `/p/` disallow.
- Etsy (https://www.etsy.com/robots.txt): groups Spinn3r (`Disallow: /`), AdsBot-Google-Mobile, `*`. `*` includes "Disallow: /search?*q=" and "Disallow: /listing/*/stubs/*". Comment line: "# llms.txt: https://www.etsy.com/llms.txt".
- Flipkart (https://www.flipkart.com/robots.txt): groups for Mediapartners-Google, Adsbot-Google, Googlebot-Image, Storebot-Google, `*`. `*` includes "Disallow: /search?" and "Disallow: */sellers/*".
- Myntra (https://www.myntra.com/robots.txt): single `*` group beginning "Allow: /".
- Meesho (https://www.meesho.com/robots.txt): single `*` group; includes "Disallow: */search". First request (Chrome User-Agent) returned an Akamai "Access Denied" 403 page; second request (curl default User-Agent) returned 200.
- JioMart (https://www.jiomart.com/robots.txt): first group "User-agent: * / Allow: /"; then a long list of legacy bots (Baiduspider, Wget, etc.). No OpenAI, Anthropic or Perplexity tokens.
- Rakuten Ichiba (https://www.rakuten.co.jp/robots.txt): groups `*`, AdsBot-Google, Googlebot. `*` includes "Disallow: /shops/". Item host https://item.rakuten.co.jp/robots.txt has only `*` with query-parameter disallows. https://search.rakuten.co.jp/robots.txt has only `*`. First request (Chrome User-Agent) returned a 51-byte Akamai stub "Reference  #<esi:vars name="AKAMAI_DEBUG_STRING"/>"; plain curl returned the file.
- Shopee (sg, co.id, co.th, ph, vn, com.my, tw, com.br): each file has a group for Googlebot/Googlebot-Mobile/Bingbot and a `*` group. shopee.sg `*` sets "Crawl-delay:1".
- Allegro (https://allegro.pl/robots.txt): groups `*`, Mediapartners-Google, CCBot. `*` includes "disallow: /offer/" and "disallow: /produkt/warianty/".
- Limitations: "No OpenAI group" means OpenAI bots follow `*`. Whether a given product URL is crawlable depends on the path; only key product/search rules were checked.

### D-13 India: Razorpay × NPCI × OpenAI "Agentic Payments" on ChatGPT announced as a private beta (2025-10-09)
- Claim: Razorpay announced a private beta of Agentic Payments with NPCI and OpenAI's ChatGPT, using UPI Circle and UPI Reserve Pay. Demos showed checkout from bigbasket inside a ChatGPT conversation. Razorpay said the three would move it "from a proof-of-concept into full production" over the coming months.
- Classification: VERIFIED FACT (announcement). Current (Oct 2026) live status: UNVERIFIED — no 2026 primary update found.
- Source: Razorpay Unveils Agentic Payments on ChatGPT with NPCI: An AI-Powered Conversational Payment Experience — Razorpay — https://razorpay.com/blog/razorpay-unveils-agentic-payments-on-chatgpt-with-npci-indias-first-ai-powered-conversational-payment-experience/
- Published/updated: October 9, 2025
- Accessed: 2026-10-30
- Tier: 1 (participant's own announcement)
- Excerpt:
  > "Razorpay—India’s leading payments and banking platform—has just announced the private beta launch of Agentic Payments, developed in a landmark collaboration with NPCI (the force behind UPI) and OpenAI’s ChatGPT."

  > "By leveraging new capabilities from NPCI—specifically UPI Circle and UPI Reserve Pay—the system allows users to securely pre-authorize their trusted AI agent to make purchases within pre-set, user-defined spending limits."

  > "This private beta is just the first step. Over the coming months, Razorpay, NPCI, and OpenAI will work together to move this innovation from a proof-of-concept into full production."
- Establishes: The only official OpenAI-linked payment initiative in India found at a participant's primary source. Named merchants: bigbasket (Tata) and Vodafone Idea (Vi). No marketplace from this agent's list is named.
- Limitations: Not an OpenAI or NPCI page. Announced 2025-10-09, before OpenAI's Mar 2026 checkout change (D-08); its relationship to that change is not stated anywhere found.

### D-14 India: Calcutta High Court (2026-05-20) dismissed IndiaMART's interim plea to force ChatGPT to show IndiaMART links; order records OpenAI's reliance on the USTR Notorious Markets list
- Claim: Justice Ravi Krishan Kapur dismissed IndiaMART InterMesh's interim application (GA-COM/1/2025 in IP-COM/57/2025). The order records IndiaMART's allegation that ChatGPT bypasses IndiaMART listing links and links sellers' own sites, and that ChatGPT refused to display IndiaMART because IndiaMART is on the USTR Notorious Markets List 2024. It records OpenAI's submission that IndiaMART "cannot also impugn the policy adopted by the respondents in relying on the USTR." It notes IndiaMART had earlier blocked ChatGPT from its own site.
- Classification: VERIFIED FACT (contents of the order). "OpenAI uses the USTR Notorious Markets list to suppress marketplace links" is EVIDENCE-BASED INFERENCE from OpenAI's recorded submission; the order does not describe the mechanism.
- Source: IndiaMart Inter Mesh Limited vs Open AI Inc. and Ors., order of the High Court at Calcutta (IPR Division) — copy hosted by MediaNama — https://www.medianama.com/wp-content/uploads/2026/05/indiamart-open-ai-675345.pdf (located via MediaNama, "Calcutta HC refuses to order OpenAI to show IndiaMart links on ChatGPT: what this means", 2026-05-22, https://www.medianama.com/2026/05/223-calcutta-hc-rejects-indiamart-plea-against-chatgpt-link-exclusion/ , Tier 3)
- Published/updated: Heard 06.05.2026; Judgment 20.05.2026
- Accessed: 2026-10-30
- Tier: 1 (court order; third-party-hosted copy)
- Excerpt:
  > "For example, on a specific enquiry using results only on or from IndiaMart, the response of ChatGPT is to bypass sending the links of the sellers posts through the IndiaMart website and providing the sellers' website/link directly."

  > "transpires that the respondents have refused to display the content of IndiaMart in view of its name featuring on the United States Trade Representative Review of Notorious Markets List 2024 (USTR)."

  > "The petitioner also alleges discrimination inasmuch as other active links DHGate, Pinduoduo, Shopee, Taobao which are on the USTR List are readily accessible in the responses generated by ChatGPT."

  > "The petitioner cannot also impugn the policy adopted by the respondents in relying on the USTR."

  > "Is IndiaMart reflected and displayed on ChatGPT? Yes. Is IndiaMart reflected and displayed in a manner in which it would like to be reflected and displayed on ChatGPT? No."

  > "Significantly, at an earlier point of time, the petitioner itself has blocked ChatGPT from accessing its website."
- Establishes: The only primary document found that describes (through litigants' submissions) a marketplace-specific display rule in ChatGPT: links to a marketplace can be replaced by links to the underlying sellers' own sites, and OpenAI acknowledged a policy that relies on the USTR list. MediaNama reports the same judge had found a "strong prima facie case" in a December 2025 order (Tier 3; that order not fetched).
- Limitations: IndiaMART is a B2B marketplace outside this agent's list. Statements are parties' submissions, not court findings of fact. The order does not say which ChatGPT surface (search answers vs shopping results) is affected. Shopee being "readily accessible" is IndiaMART's allegation, not verified.

### D-17 Amazon v. Perplexity: complaint (2025-11-04) cites Amazon's Agent Terms (added 2025-05-30) requiring agents to self-identify in the User-Agent string
- Claim: Amazon's complaint alleges Perplexity's Comet agent impersonated Google Chrome. It quotes Amazon's Conditions of Use "Agent Terms", which require agents to include "Agent/[agent name]" in the user-agent string and not to conceal agentic activity.
- Classification: VERIFIED FACT (contents of the complaint)
- Source: Complaint, Amazon.com Services LLC v. Perplexity AI, Inc., No. 3:25-cv-09514 (N.D. Cal.), Dkt. 1 — CourtListener RECAP — https://storage.courtlistener.com/recap/gov.uscourts.cand.459191/gov.uscourts.cand.459191.1.0.pdf
- Published/updated: Filed 11/04/25
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "On May 30, 2025, Amazon updated the Amazon Store's Conditions of Use to add a dedicated section on AI Agents ("Agent Terms")."

  > "3. Technical Requirements. Agents must:
  > i. In all HTTP/HTTPS requests, identify that the request is from an Agent and disclose the name of the Agent by including the following in the request's user agent string: "Agent/[agent name]" (e.g., Agent/AmazonAgent)"

  > "Perplexity falsely identifies its Comet AI agent activity as coming from Google Chrome"
- Also fetched: Amazon's cease-and-desist letter to Perplexity dated October 31, 2025 (https://assets.aboutamazon.com/2d/47/6801224e4607900ef4e61a80a319/2025-10-31-amazon-cease-desist-ltr-to-perplexity.pdf): "Perplexity must stop disguising Comet as a Google Chrome browser, transparently identify Comet AI agents".
- Establishes: Amazon's stated rule for third-party shopping agents is contractual (Conditions of Use) plus technical (User-Agent self-identification), separate from robots.txt.
- Limitations: Allegations, not findings. The case concerns Perplexity, not OpenAI.

### D-18 Amazon v. Perplexity: district court granted a preliminary injunction (2026-03-09); Ninth Circuit vacated it (2026-08-04)
- Claim: Judge Maxine M. Chesney granted Amazon's motion for preliminary injunctive relief on 2026-03-09. A Ninth Circuit panel (No. 26-1444, opinion by Judge Milan D. Smith, Jr.) vacated it on 2026-08-04, holding Amazon unlikely to succeed on CFAA and CDAFA claims because the user, not Perplexity, "accessed" Amazon.
- Classification: VERIFIED FACT
- Sources:
  - Order Granting Plaintiff's Motion for Preliminary Injunctive Relief, Dkt. 81 — https://storage.courtlistener.com/recap/gov.uscourts.cand.459191/gov.uscourts.cand.459191.81.0.pdf — Filed 03/09/26
  - Opinion, Amazon.com Services, LLC v. Perplexity AI, Inc., No. 26-1444 (9th Cir.), DktEntry 61.1 — copy hosted by Knight First Amendment Institute — https://kfai-documents.s3.amazonaws.com/documents/28a88e7801/gov.uscourts.ca9.9bb73aa1-f12c-4519-875b-262201f0c5d5.61.1.pdf (landing page https://knightcolumbia.org/documents/bx1xspxwhb) — August 4, 2026
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (opinion, staff summary — "This summary constitutes no part of the opinion of the court"):
  > "Rather, it was the user who "accessed" Amazon's computers, with the help of Perplexity's AI agent, the "Assistant," to carry out specific acts on Amazon.com."

  > "The panel therefore vacated the preliminary injunction and remanded for further proceedings."
- Supporting (Tier 3): Engadget, 2026-08-04, Amazon statement: "We respectfully disagree with today's decision on the preliminary injunction … We remain confident in our case and are evaluating our next steps." https://www.engadget.com/2230471/perplexity-has-successfully-overturned-amazon-injunction-on-its-ai-shopping-bot
- Establishes: As of 2026-10-30 no injunction bars a user-directed AI agent (Perplexity's) from Amazon; the merits case continues in N.D. Cal.
- Limitations: Quote is from the court-staff summary, not the opinion body. Rehearing status: MediaPost (Tier 3, 403 on fetch) reportedly says rehearing was denied — UNVERIFIED. Ruling concerns CFAA/CDAFA only, not contract claims.

### D-19 Amazon's own statements: third-party agents "should operate openly"; Amazon runs its own agentic shopping (Buy for Me, Shop Direct feeds, Alexa for Shopping)
- Claim: Amazon's public statement says third-party purchase agents should operate openly and respect service-provider decisions. Separately, Amazon accepts third-party merchant feeds into Shop Direct and completes purchases on other merchants' sites with "Buy for Me". Rufus was merged into "Alexa for Shopping" on 2026-05-13.
- Classification: VERIFIED FACT
- Sources:
  - Statement about Perplexity — Amazon — https://www.aboutamazon.com/news/company-news/amazon-perplexity-comet-statement — datePublished 2025-11-04
  - Amazon introduces feeds to make it easier for merchants to reach more customers through AI-powered Shop Direct — Amazon — https://www.aboutamazon.com/news/retail/amazon-shop-direct-external-stores — datePublished 2026-03-11
  - Meet Alexa for Shopping, your personalized, agentic AI assistant on Amazon — Amazon — https://www.aboutamazon.com/news/retail/alexa-for-shopping-ai-assistant — datePublished 2026-05-13
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "We think it’s fairly straightforward that third-party applications that offer to make purchases on behalf of customers from other businesses should operate openly and respect service provider decisions whether or not to participate."

  > "Shop Direct now includes over 100 million products from more than 400,000 merchants, with tens of millions of products available to purchase through the AI-powered Buy for Me feature."

  > "Amazon brings together Rufus and Alexa+ to create ‘Alexa for Shopping’ on the Amazon Shopping app and website."
- Establishes: Amazon blocks outside AI agents by robots.txt (D-01) and terms (D-17) while running its own cross-merchant agent that buys on other sites.
- Limitations: Shop Direct is US-only per the post ("available for all U.S. customers"). No Amazon statement found about OpenAI specifically.

### D-20 Amazon × OpenAI strategic partnership (2026-02-27) covers investment, AWS compute and custom models for Amazon apps; no ChatGPT shopping term found
- Claim: Amazon announced a $50 billion investment in OpenAI and a collaboration on customized models "to power Amazon’s customer-facing applications". The announcement text fetched contains no term about Amazon products in ChatGPT.
- Classification: VERIFIED FACT (announcement content). "No Amazon catalog deal with ChatGPT exists" is UNVERIFIED (absence in one document).
- Source: OpenAI and Amazon announce strategic partnership — Amazon — https://www.aboutamazon.com/news/aws/amazon-open-ai-strategic-partnership-investment
- Published/updated: datePublished 2026-02-27
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "OpenAI and Amazon will collaborate to develop customized models available to Amazon developers to power Amazon’s customer-facing applications. Amazon teams will be able to tailor OpenAI models for use across AI products and agents that serve customers directly."
- Establishes: The direction of the disclosed relationship is OpenAI models into Amazon products, not Amazon products into ChatGPT.
- Limitations: Press (Bloomberg, Forrester; Tier 3, not fetched) reports e-commerce discussions; terms not public.

### D-21 OpenAI Help Center: merchants for the same product are ranked partly on "whether they are the maker or primary seller"; product results are "not influenced by any OpenAI partnerships"
- Claim: OpenAI's help article on shopping states how products and merchants are selected. Merchant lists come from "third-party providers or directly from the merchants themselves". Merchant ranking factors include "whether they are the maker or primary seller of that item". Shopify merchant data arrives through Shopify Catalog.
- Classification: VERIFIED FACT (article content)
- Source: Shopping with ChatGPT Search — OpenAI Help Center — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search (requested as …/11128490-improved-shopping-results-from-chatgpt-search; redirected). WebFetch and curl returned 403; text read in the in-app browser.
- Published/updated: "Updated: 2 days ago" as displayed on 2026-10-30 (≈ 2026-10-28; exact date not stated)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Product results are selected independently by ChatGPT and are not ads, nor influenced by any OpenAI partnerships."

  > "Structured metadata from first-party and third-party providers (e.g., price, product description) and other third-party content."

  > "When you select a product, ChatGPT may show a list of merchants offering it. This list is generated by ChatGPT based on merchant and product metadata from third-party providers or directly from the merchants themselves. Merchants are ranked based on factors like availability, price, quality, and whether they are the maker or primary seller of that item."

  > "Prices shown in ChatGPT’s initial response typically reflect the price from the first merchant listed, which may not be the lowest available price."

  > "When more than one merchant offers the product, that option may have a “Best price” label."
- Establishes: The only OpenAI document found that states a rule touching marketplace vs. brand selection: "maker or primary seller" is a ranking factor. OpenAI does not define "primary seller" or say how a marketplace offer is labeled. The article names no marketplace.
- Limitations: Factor list is non-exhaustive ("factors like"). Weighting is not given. The article does not say whether a marketplace (e.g., Walmart Marketplace, Amazon third-party sellers) counts as "primary seller". Updated recently; earlier wording not compared.

### D-22 OpenAI merchants page: shopping is live in the U.S. only; Shopify and Etsy catalogs are already integrated; standalone Instant Checkout is being phased out
- Claim: chatgpt.com/merchants says shopping is live for U.S. ChatGPT users, Shopify and Etsy sellers need no setup, purchases complete on merchant sites or apps, there are no fees on purchases that start in ChatGPT, and a product feed is optional if ChatGPT already crawls the site.
- Classification: VERIFIED FACT
- Source: Power product discovery in ChatGPT — OpenAI — https://chatgpt.com/merchants/ (curl: 403; read in the in-app browser)
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "If you sell through Shopify or Etsy, your catalog is already integrated, and no additional setup or application is required."

  > "Shopping is currently live for ChatGPT users in the U.S. We’re building a merchant platform for self-serve data integration later this year, and plan to expand to more merchants and regions over time."

  > "We’re moving away from a standalone Instant Checkout experience in ChatGPT and prioritizing better shopping discovery and merchant-owned checkout experiences. Users can discover and evaluate products in ChatGPT, but purchases are completed on merchant-owned websites or apps."

  > "Do I need a product feed if ChatGPT already crawls my site?
  > No, but feeds give you greater control over how your products appear, helping ensure more accurate and up-to-date information."

  > "Apps are optional and are best suited for larger merchants who want more control over the shopping and purchase experience."
- Establishes: Four official paths for marketplace products into ChatGPT: (1) crawl (OAI-SearchBot), (2) ACP product feed, (3) platform catalog integration (Shopify, Etsy named), (4) merchant app. Etsy is the only marketplace in scope OpenAI names as catalog-integrated. Shopping results are US-only; this is why Indian marketplaces (Flipkart, Myntra, Meesho, JioMart) have no shopping-results relationship on record.
- Limitations: "Shopping" here means product-results surfaces. Apps (Shopee, Allegro, Nykaa) operate outside the US (D-24, D-25, D-27), so "U.S. only" does not cover apps.

### D-23 Amazon added ChatGPT-User and OAI-SearchBot disallows between 2025-11-11 and 2025-11-12; GPTBot was disallowed by 2024-01-01
- Claim: Wayback captures of www.amazon.com/robots.txt show `User-agent: GPTBot / Disallow: /` in every capture checked from 2024-01-01. The captures of 2025-11-11 21:31 UTC lack ChatGPT-User and OAI-SearchBot; the capture of 2025-11-12 14:40 UTC adds both. The file grew from 9 groups (2025-07-16) to 101 groups (2026-05-15 onward).
- Classification: VERIFIED FACT (archive captures). Exact change time within that window: not determinable. Link to the Perplexity complaint filed 2025-11-04 (D-17): EVIDENCE-BASED INFERENCE (timing only).
- Source: Wayback Machine CDX index and captures of https://www.amazon.com/robots.txt — Internet Archive — e.g. https://web.archive.org/web/20251111213138id_/https://www.amazon.com/robots.txt and https://web.archive.org/web/20251112144036id_/https://www.amazon.com/robots.txt
- Published/updated: capture timestamps as stated
- Accessed: 2026-10-30
- Tier: 1 (archived primary file)
- Excerpt (`diff` of the two captures):
  > "> Disallow: /
  > > 
  > > User-agent: ChatGPT-User
  > > Disallow: /
  > > 
  > > User-agent: OAI-SearchBot"
- Group counts by capture: 2025-06-18: 6; 2025-08-07: 20; 2025-10-28: 35; 2025-11-12: 47; 2026-01-13: 49; 2026-05-15: 101; 2026-10-14: 101 (7,947 bytes, same size as the live file fetched 2026-10-30).
- Establishes: Amazon's full block of OpenAI's search crawler and user-fetcher is about one year old as of 2026-10-30; the training-crawler block is older.
- Limitations: Archive capture frequency limits precision. amazon.in history not checked.

### D-24 Shopee (Sea) × OpenAI (2026-06-22): Shopee app in ChatGPT in 8 markets; purchase continues on Shopee
- Claim: Sea and OpenAI announced a strategic partnership. The Shopee app is available in ChatGPT for users in Indonesia, Malaysia, the Philippines, Singapore, Thailand, Taiwan, Vietnam and Brazil. Users get recommendations in ChatGPT and continue the purchase on Shopee. ChatGPT for Business trials go to Shopee sellers.
- Classification: VERIFIED FACT
- Source: Sea and OpenAI Deepen Strategic Partnership to Drive AI Adoption and Innovation Across Southeast Asia and Brazil — Sea Limited — https://www.sea.com/news/406
- Published/updated: 22 June, 2026
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "The Shopee App is now available in ChatGPT for users from Indonesia, Malaysia, the Philippines, Singapore, Thailand, Taiwan, Vietnam, and Brazil. This makes Shopee the first e-commerce platform of its kind to be available across Southeast Asia and Latin America in ChatGPT."

  > "The Shopee App in ChatGPT enables users to discover products sold on Shopee through natural conversational prompts. … before seamlessly continuing their shopping journey on the Shopee platform."

  > "Since 2025, Sea and OpenAI have collaborated to make ChatGPT more accessible to users through marketing promotions and the ShopeeVIP membership program."
- Establishes: Shopee reaches ChatGPT through an app (user-invoked), not through OpenAI-specific robots.txt rules (Shopee files have no OpenAI group, D-16).
- Limitations: Does not say whether Shopee supplies ACP product feeds for ChatGPT's general shopping results.

### D-25 Allegro app in ChatGPT launched 2026-05-12, open to all ChatGPT users; "Kup na Allegro" hands off to Allegro checkout
- Claim: Allegro's press office says its ChatGPT app is available to every ChatGPT user. A "Kup na Allegro" (Buy on Allegro) button takes the user to Allegro's payment and delivery form with the chosen products.
- Classification: VERIFIED FACT
- Source: Allegro uruchamia apkę na ChatGPT i tworzy nowy standard w konwersacyjnym e-commerce’ie — Biuro Prasowe Allegro (Allegro press office) — https://media.allegro.pl/457629-allegro-uruchamia-apke-na-chatgpt-i-tworzy-nowy-standard-w-konwersacyjnym-e-commerceie
- Published/updated: 12.05.2026
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (Polish original; English gloss is this agent's translation, not verbatim):
  > "Przycisk „Kup na Allegro” przenosi użytkownika prosto do formularza opcji płatności i dostaw, z wybranymi wcześniej produktami, gotowymi do kupienia."
  > [gloss: The "Buy on Allegro" button takes the user straight to the payment and delivery options form, with the previously chosen products ready to buy.]

  > "Aplikacja jest już dostępna dla każdego użytkownika i użytkowniczki ChatGPT."
  > [gloss: The app is already available to every ChatGPT user.]
- Supporting (Tier 3): Spider's Web, 2026-05, https://spidersweb.pl/2026/05/allegro-chatgpt-aplikacja-zakupy-sztuczna-inteligencja.html — says Allegro announced cooperation with OpenAI the day before the app launch.
- Establishes: Allegro reaches ChatGPT through an app with checkout on Allegro.
- Limitations: Partnership announcement (≈2026-05-11) not fetched at source. "Every ChatGPT user" may still be limited by app availability rules per region (not verified).

### D-26 Rakuten × OpenAI: MoU of 2023-08-02 (plugin-era); no Rakuten Ichiba ChatGPT app or shopping integration found
- Claim: Rakuten signed an MoU with OpenAI in 2023 and planned to bring "Rakuten AI experiences into ChatGPT products by leveraging the OpenAI plugin architecture", aimed at business users.
- Classification: VERIFIED FACT (2023 announcement). Current status: UNVERIFIED; no 2026 Rakuten Ichiba × ChatGPT shopping announcement found in English or Japanese searches.
- Source: Rakuten to Collaborate with OpenAI to Develop State-of-the-Art AI Experiences for Consumers and Businesses — Rakuten Group, Inc. — https://global.rakuten.com/corp/news/press/2023/0802_01.html
- Published/updated: August 2, 2023
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Additionally, the Rakuten Group will bring Rakuten AI experiences into ChatGPT products by leveraging the OpenAI plugin architecture, enabling businesses to use natural language for interacting with AI agents that conduct research, analyze data, optimize inventory, pricing, automate business processes and more."
- Establishes: The documented Rakuten–OpenAI relationship is an API/business-AI collaboration, not consumer shopping in ChatGPT.
- Limitations: OUTDATED: the ChatGPT plugin architecture referenced has been superseded by apps (not verified here at source). Rakuten robots.txt has no OpenAI group (D-16).

### D-27 India 2026: Nykaa apps in ChatGPT (June 2026, Tier 3); no Flipkart, Myntra, Meesho or JioMart × OpenAI partnership found
- Claim: MediaNama reports Nykaa signed a multi-year agreement with OpenAI to list Nykaa beauty and fashion storefronts as connected apps in ChatGPT for users in India, with purchase completed on Nykaa. Searches found no OpenAI partnership for Flipkart, Myntra, Meesho or JioMart.
- Classification: Nykaa: UNVERIFIED at primary source (Tier 3 report only). Absence for the four marketplaces: UNVERIFIED (negative search result, not proof).
- Source: Nykaa taps OpenAI for conversational shopping across beauty and fashion — MediaNama — https://www.medianama.com/2026/06/223-nykaa-openai-conversational-shopping-beauty-fashion/
- Published/updated: June 17, 2026
- Accessed: 2026-10-30
- Tier: 3
- Excerpt:
  > "to list its beauty and fashion storefronts as connected apps in ChatGPT, allowing users in India to get product recommendations through conversations in ChatGPT, before being routed to Nykaa’s app or website to complete a purchase."
- Other India items seen in search results only (Tier 3, not fetched; listed for follow-up): Pine Labs × OpenAI (Feb 2026, India AI Impact Summit); Swiggy MCP integrations with ChatGPT (Jan 2026); Eternal (Zomato/Blinkit) × OpenAI; GoKwik/PayU D2C experience in ChatGPT (Jul 2026). Pine Labs' own Q4 FY26 earnings-call transcript (search snippet only) describes it as one of "the first few design partners with OpenAI".
- Establishes: As of 2026-10-30, the India marketplaces in scope have no OpenAI relationship on record; India's documented paths are apps (Nykaa) and payments pilots (D-13). ChatGPT shopping results are US-only (D-22).
- Limitations: Nykaa claim needs Nykaa/BSE filing confirmation.

### D-28 Instacart app in ChatGPT with Instant Checkout (2025-12-08)
- Claim: Instacart announced it was the first grocery partner to launch an app in ChatGPT and the first app to offer checkout inside ChatGPT, built on ACP.
- Classification: VERIFIED FACT (announcement; excerpt fragments via WebFetch). Current checkout status after D-08/D-22: UNVERIFIED.
- Source: Instacart App Launches in OpenAI ChatGPT — Instacart — https://company.instacart.com/pressreleases/instacart-app-launches-in-openai-chatgpt
- Published/updated: Dec 8, 2025
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (verbatim fragments; WebFetch limited quote length):
  > "Instacart is the first app within ChatGPT’s app ecosystem to offer checkout directly within ChatGPT,"
  > "powered by the Agentic Commerce Protocol."
- Establishes: The app-plus-checkout model OpenAI later pointed merchants toward (D-08).
- Limitations: Not a marketplace in this agent's list; included because the brief named it. Region: release cites North America retailers; does not name the US explicitly.

### D-29 Mercado Libre: no official OpenAI/ChatGPT relationship found
- Claim: No Mercado Libre × OpenAI announcement found in English or Spanish searches. Its robots.txt blocks GPTBot and ChatGPT-User but not OAI-SearchBot (D-04).
- Classification: UNVERIFIED HYPOTHESIS that none exists (negative search).
- Source: none (searches only). A Tier 3 search summary attributes to CEO Ariel Szarfsztejn a Q4 2025 earnings-call remark that it was early to judge OpenAI's partnerships; not fetched.
- Accessed: 2026-10-30
- Limitations: Mercado Libre investor materials were not checked directly.

## 3. Contradictions and superseded information
- SUPERSEDED: OpenAI's Sep 29 2025 post (D-05) still describes Instant Checkout as live, with no update note in the 2026-10-22 snapshot. OpenAI's Mar 24 2026 post (D-08) and the merchants page (D-22: "moving away from a standalone Instant Checkout experience") replace it. The ranking sentence in D-05 ("primary seller") survives in updated form in the Help Center (D-21: "maker or primary seller").
- SUPERSEDED: Walmart's Oct 2025 release (D-07) promised Instant Checkout; by Mar 24 2026 Walmart had an in-ChatGPT app (D-08).
- SUPERSEDED/OUTDATED: Rakuten's 2023 MoU (D-26) refers to the ChatGPT "plugin architecture"; ChatGPT now uses apps.
- Date conflict (Tier 3): trade press dates the Instant Checkout pullback to Mar 4, 5, 17 or 20 2026. The only primary source found is OpenAI's Mar 24 2026 post (D-08). TechCrunch says Instant Checkout "ended in March"; Etsy's own post (D-10) does not say it ended.
- Factual error in press (Tier 3): Engadget (2026-08-04) says Amazon "filed a lawsuit against Perplexity in March 2026". The complaint's own header shows "Filed 11/04/25" (D-17). March 2026 is the injunction date (D-18).
- Scope conflict: OpenAI says shopping is "currently live for ChatGPT users in the U.S." (D-22), yet Shopee (8 non-US markets, D-24), Allegro (Poland, D-25) and Nykaa (India, D-27, Tier 3) run apps in ChatGPT outside the US. Resolution (EVIDENCE-BASED INFERENCE): "shopping" on the merchants page means ChatGPT's own product-results surface; merchant apps are a separate surface with wider availability.
- Tension: OpenAI says product results are "not influenced by any OpenAI partnerships" (D-21), while the IndiaMART order records OpenAI defending a policy of "relying on the USTR" list (D-14). These are compatible (a policy list is not a partnership) but show that non-relevance rules do affect which marketplace links appear.
- Etsy robots.txt vs Etsy llms.txt: consistent. llms.txt (updated 2026-09-25) says robots.txt "applies one ruleset to all user agents with no AI-specific carve-outs"; the 2026-10-30 fetch confirms no OpenAI group.

## 4. Knowledge gaps
- No primary OpenAI statement on how a marketplace offer is labeled in the UI (e.g., "Sold by X on Y"). The feed spec has `marketplace_seller` (D-06) but no display rule.
- "Primary seller" (D-05, D-21) is undefined. Unknown whether Walmart Marketplace or Amazon third-party offers count as primary seller.
- Whether ChatGPT shows Amazon product listings at all after the Nov 2025 OAI-SearchBot block: not tested (no live ChatGPT queries were run). OpenAI's rule (D-15) says opted-out sites appear only as navigational links in search answers; licensed third-party product data (D-21: "third-party providers") could still carry Amazon offers — UNVERIFIED.
- Which "third-party providers" supply product metadata to ChatGPT: not named in any OpenAI page fetched.
- Whether Walmart, Target, eBay, Mercado Libre, Shopee or Allegro submit ACP product feeds for the general shopping results (as opposed to apps): only Target is named as an ACP discovery integrator (D-08); Etsy and Shopify are named as catalog-integrated (D-22).
- Razorpay/NPCI UPI pilot (D-13): no 2026 status update found at a primary source.
- Nykaa × OpenAI (D-27), Pine Labs × OpenAI, Swiggy, Eternal, GoKwik/PayU: not verified at primary sources.
- Lazada: explicit OpenAI `Allow: /` groups (D-03) with no partnership found; the date they were added was not checked (no Wayback history pulled).
- Mercado Libre item subdomains' robots.txt (articulo., produto.) not captured (403).
- Amazon v. Perplexity: rehearing-denial reports (Tier 3) not verified; merits case status after remand not checked.
- IndiaMART: the December 2025 Calcutta HC order (reportedly favourable to IndiaMART) not fetched.
- OAI-AdsBot and ChatGPT ads: only Target's test (D-11) and OpenAI's bot doc (D-15) fetched; ad placement rules for marketplaces not researched (out of scope).

## 5. Unfetched sources
- https://openai.com/index/buy-it-in-chatgpt/ — HTTP 403 (WebFetch and curl). Used Wayback snapshot 20261022061422.
- https://openai.com/index/powering-product-discovery-in-chatgpt/ — not fetched directly (openai.com returns 403). Used Wayback snapshot 20261012013103.
- https://help.openai.com/en/articles/11128490-improved-shopping-results-from-chatgpt-search — HTTP 403 (WebFetch and curl). Read successfully in the in-app browser (D-21).
- https://chatgpt.com/merchants — HTTP 403 (curl). Read successfully in the in-app browser (D-22).
- https://www.etsy.com/news/from-keywords-to-conversation-etsyas-next-steps-into-conversational-search-with-app-in-chatgpt — HTTP 403 (WebFetch and curl). Used Wayback snapshot 20260514223505.
- https://articulo.mercadolibre.com.mx/robots.txt, https://produto.mercadolivre.com.br/robots.txt, https://listado.mercadolibre.com.mx/robots.txt — HTTP 403 (curl default User-Agent). Not retried.
- https://www.meesho.com/robots.txt — HTTP 403 Akamai "Access Denied" with Chrome User-Agent; succeeded with curl default User-Agent.
- https://www.rakuten.co.jp/robots.txt — first request (Chrome User-Agent) returned a 51-byte Akamai stub with `Content-Type: text/html`; succeeded with curl default User-Agent.
- https://www.myntra.com/robots.txt — second request (curl default User-Agent) failed to connect (curl code 000); first request succeeded.
- https://www.mediapost.com/publications/article/417007/appeals-court-sides-against-amazon-lifts-perplexi.html — HTTP 403. Not used.
- https://investors.instacart.com/news-releases/news-release-details/instacart-app-launches-openai-chatgpt-first-company-offer-new — HTTP 403 (curl). Used https://company.instacart.com/pressreleases/instacart-app-launches-in-openai-chatgpt via WebFetch instead.
- https://archive.org/wayback/available API — HTTP 429 (rate limit) once; web.archive.org `id_` and CDX endpoints worked afterwards.
- WebFetch cannot fetch web.archive.org; all archive reads used curl.
- about.allegro.eu/news and /pl/news — HTTP 404. Used media.allegro.pl instead.
- Not attempted: Nykaa/BSE filing, Pine Labs press release, NPCI site, Mercado Libre investor site, Bloomberg Law opinion coverage (paywall).

## 6. Source list
Tier 1 — robots.txt (all accessed 2026-10-30)
- https://www.amazon.com/robots.txt
- https://www.amazon.in/robots.txt
- https://www.walmart.com/robots.txt
- https://www.etsy.com/robots.txt
- https://www.ebay.com/robots.txt
- https://www.target.com/robots.txt
- https://www.flipkart.com/robots.txt
- https://www.myntra.com/robots.txt
- https://www.meesho.com/robots.txt
- https://www.jiomart.com/robots.txt
- https://www.mercadolibre.com.mx/robots.txt ; https://www.mercadolivre.com.br/robots.txt ; https://www.mercadolibre.com.ar/robots.txt
- https://www.rakuten.co.jp/robots.txt ; https://item.rakuten.co.jp/robots.txt ; https://search.rakuten.co.jp/robots.txt
- https://shopee.sg/robots.txt ; https://shopee.co.id/robots.txt ; https://shopee.co.th/robots.txt ; https://shopee.ph/robots.txt ; https://shopee.vn/robots.txt ; https://shopee.com.my/robots.txt ; https://shopee.tw/robots.txt ; https://shopee.com.br/robots.txt
- https://www.lazada.sg/robots.txt ; https://www.lazada.com.my/robots.txt ; https://www.lazada.co.th/robots.txt ; https://www.lazada.com.ph/robots.txt ; https://www.lazada.vn/robots.txt ; https://www.lazada.co.id/robots.txt
- https://allegro.pl/robots.txt
- Wayback captures/CDX for https://www.amazon.com/robots.txt and https://www.ebay.com/robots.txt (2024-01-01 to 2026-10-14)

Tier 1 — OpenAI
- Buy it in ChatGPT: Instant Checkout and the Agentic Commerce Protocol (Sep 29 2025) — https://openai.com/index/buy-it-in-chatgpt/ (via Wayback 20261022061422)
- Powering Product Discovery in ChatGPT (Mar 24 2026) — https://openai.com/index/powering-product-discovery-in-chatgpt/ (via Wayback 20261012013103)
- Shopping with ChatGPT Search (Help Center, updated ≈2026-10-28) — https://help.openai.com/en/articles/11128490-shopping-with-chatgpt-search
- Power product discovery in ChatGPT (merchants page) — https://chatgpt.com/merchants/
- Overview of OpenAI Crawlers — https://developers.openai.com/api/docs/bots.md
- Agentic Commerce full documentation — https://developers.openai.com/commerce/llms-full.txt ; index https://developers.openai.com/commerce/llms.txt

Tier 1 — marketplaces and partners
- Walmart, Oct 14 2025 — https://corporate.walmart.com/news/2025/10/14/walmart-partners-with-openai-to-create-ai-first-shopping-experiences
- Walmart, Oct 21 2026 — https://corporate.walmart.com/news/2026/10/Making-It-Possible-for-Agents-to-Shop-on-Behalf-of-Customers
- Etsy, May 5 2026 — https://www.etsy.com/news/from-keywords-to-conversation-etsyas-next-steps-into-conversational-search-with-app-in-chatgpt (via Wayback 20260514223505)
- Etsy llms.txt (updated 2026-09-25) — https://www.etsy.com/llms.txt
- Target, Nov 19 2025 — https://corporate.target.com/press/release/2025/11/target-to-launch-first-of-its-kind-conversational,-curated-shopping-experience-in-chatgpt
- Target, Feb 9 2026 — https://corporate.target.com/press/fact-sheet/2026/02/conversational-ai-advertising
- Target, Jun 18 2026 — https://corporate.target.com/press/fact-sheet/2026/06/conversational-ai
- eBay, Jan 23 2025 — https://innovation.ebayinc.com/stories/ebay-openai-operator-assistant/
- Sea/Shopee, Jun 22 2026 — https://www.sea.com/news/406
- Allegro, 12.05.2026 — https://media.allegro.pl/457629-allegro-uruchamia-apke-na-chatgpt-i-tworzy-nowy-standard-w-konwersacyjnym-e-commerceie
- Rakuten, Aug 2 2023 — https://global.rakuten.com/corp/news/press/2023/0802_01.html
- Instacart, Dec 8 2025 — https://company.instacart.com/pressreleases/instacart-app-launches-in-openai-chatgpt
- Razorpay, Oct 9 2025 — https://razorpay.com/blog/razorpay-unveils-agentic-payments-on-chatgpt-with-npci-indias-first-ai-powered-conversational-payment-experience/
- Amazon, Statement about Perplexity (2025-11-04) — https://www.aboutamazon.com/news/company-news/amazon-perplexity-comet-statement
- Amazon, cease-and-desist letter (Oct 31 2025) — https://assets.aboutamazon.com/2d/47/6801224e4607900ef4e61a80a319/2025-10-31-amazon-cease-desist-ltr-to-perplexity.pdf
- Amazon, Shop Direct feeds (2026-03-11) — https://www.aboutamazon.com/news/retail/amazon-shop-direct-external-stores
- Amazon, Alexa for Shopping (2026-05-13) — https://www.aboutamazon.com/news/retail/alexa-for-shopping-ai-assistant
- Amazon, OpenAI strategic partnership (2026-02-27) — https://www.aboutamazon.com/news/aws/amazon-open-ai-strategic-partnership-investment

Tier 1 — court documents
- Complaint, Amazon.com Services LLC v. Perplexity AI, Inc., 3:25-cv-09514 (N.D. Cal.), filed 11/04/25 — https://storage.courtlistener.com/recap/gov.uscourts.cand.459191/gov.uscourts.cand.459191.1.0.pdf
- Order granting preliminary injunction, Dkt. 81, filed 03/09/26 — https://storage.courtlistener.com/recap/gov.uscourts.cand.459191/gov.uscourts.cand.459191.81.0.pdf
- Ninth Circuit opinion, No. 26-1444, Aug 4 2026 — https://kfai-documents.s3.amazonaws.com/documents/28a88e7801/gov.uscourts.ca9.9bb73aa1-f12c-4519-875b-262201f0c5d5.61.1.pdf
- Calcutta High Court, IndiaMart Inter Mesh Ltd v. Open AI Inc. & Ors., GA-COM/1/2025 in IP-COM/57/2025, judgment 20.05.2026 — https://www.medianama.com/wp-content/uploads/2026/05/indiamart-open-ai-675345.pdf

Tier 3 — press (used only to locate primary sources or where noted)
- TechCrunch, "Etsy launches its app within ChatGPT as it continues its AI push", 2026-05-05 — https://techcrunch.com/2026/05/05/etsy-launches-its-app-within-chatgpt-as-it-continues-its-ai-push/
- Engadget, "Perplexity has successfully overturned Amazon's injunction on its AI shopping bot", 2026-08-04 — https://www.engadget.com/2230471/perplexity-has-successfully-overturned-amazon-injunction-on-its-ai-shopping-bot
- MediaNama, "Calcutta HC refuses to order OpenAI to show IndiaMart links on ChatGPT: what this means", 2026-05-22 — https://www.medianama.com/2026/05/223-calcutta-hc-rejects-indiamart-plea-against-chatgpt-link-exclusion/
- MediaNama, "Nykaa taps OpenAI for conversational shopping across beauty and fashion", 2026-06-17 — https://www.medianama.com/2026/06/223-nykaa-openai-conversational-shopping-beauty-fashion/
- Spider's Web, "Allegro wchodzi do ChatGPT…", 2026-05 — https://spidersweb.pl/2026/05/allegro-chatgpt-aplikacja-zakupy-sztuczna-inteligencja.html
