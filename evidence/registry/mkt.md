# Registry — MKT (marketplaces and commerce platforms)

Schema: `evidence/README.md`. All entries accessed 2026-10-30. A robots.txt snapshot shows declared crawl policy on the access date only. It does not show what ChatGPT displays or whether data arrives by another path.

---

## Crawl policy toward OpenAI agents

### MKT-001 — Amazon.com and Amazon.in disallow OAI-SearchBot, GPTBot and ChatGPT-User site-wide
- **Claim:** Both robots.txt files contain separate groups with `Disallow: /` for GPTBot, ChatGPT-User and OAI-SearchBot.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1 (primary artifact)
- **Subject / topic:** Amazon / crawling
- **Source:** https://www.amazon.com/robots.txt ; https://www.amazon.in/robots.txt
- **Published:** live file · **Accessed:** 2026-10-30
- **Excerpt:** > "User-agent: GPTBot / Disallow: /" … "User-agent: ChatGPT-User / Disallow: /" … "User-agent: OAI-SearchBot / Disallow: /"
- **Establishes:** Per OpenAI's crawler rule (CGPT-006), Amazon pages are excluded from ChatGPT search answers except as navigational links. The files also block ~90 other AI agent tokens.
- **Limitations:** Does not show whether Amazon offers reach ChatGPT via third-party product data providers (CGPT-012). Not tested in ChatGPT.
- **Related:** CGPT-006, MKT-002, RES-022
- **Origin:** notes/d-…#D-01 · **Checked:** 2026-10-30 (amazon.in)

### MKT-002 — Amazon added the OAI-SearchBot and ChatGPT-User blocks on 2025-11-11/12; GPTBot was blocked by 2024-01-01
- **Claim:** Wayback captures show both groups appear between 2025-11-11 21:31 UTC and 2025-11-12 14:40 UTC. GPTBot is disallowed in every capture from 2024-01-01.
- **Classification:** VERIFIED FACT (archive captures). Link to the Perplexity complaint (filed 2025-11-04) is EVIDENCE-BASED INFERENCE from timing. · **Confidence:** High · **Tier:** 1 (archived primary file)
- **Subject / topic:** Amazon / crawling
- **Source:** https://web.archive.org/web/20251111213138id_/https://www.amazon.com/robots.txt ; https://web.archive.org/web/20251112144036id_/https://www.amazon.com/robots.txt
- **Published:** capture timestamps · **Accessed:** 2026-10-30
- **Excerpt:** > "User-agent: ChatGPT-User / Disallow: /" (added in the 2025-11-12 capture)
- **Establishes:** Amazon's full exclusion of ChatGPT search is about one year old.
- **Limitations:** amazon.in history not checked.
- **Related:** MKT-001, MKT-003
- **Origin:** notes/d-…#D-23 · **Checked:** pending

### MKT-003 — Amazon requires AI agents to self-identify; Amazon v. Perplexity injunction was vacated on appeal (2026-08-04)
- **Claim:** Amazon's Conditions of Use "Agent Terms" (added 2025-05-30) require agents to put "Agent/[agent name]" in the user-agent string. A district court enjoined Perplexity's agent on 2026-03-09. The Ninth Circuit vacated that injunction on 2026-08-04.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1 (court filings)
- **Subject / topic:** Amazon / agent policy
- **Source:** Complaint, Dkt. 1, No. 3:25-cv-09514 (N.D. Cal.) — https://storage.courtlistener.com/recap/gov.uscourts.cand.459191/gov.uscourts.cand.459191.1.0.pdf ; Ninth Circuit opinion No. 26-1444 — https://kfai-documents.s3.amazonaws.com/documents/28a88e7801/gov.uscourts.ca9.9bb73aa1-f12c-4519-875b-262201f0c5d5.61.1.pdf
- **Published:** 2025-11-04; 2026-08-04 · **Accessed:** 2026-10-30
- **Excerpt:** > "On May 30, 2025, Amazon updated the Amazon Store's Conditions of Use to add a dedicated section on AI Agents ("Agent Terms")." / > "The panel therefore vacated the preliminary injunction and remanded for further proceedings." (court-staff summary)
- **Establishes:** Amazon controls agent access by contract and robots.txt. The legal question is open.
- **Limitations:** The case concerns Perplexity, not OpenAI. The quoted appellate text is the staff summary.
- **Related:** MKT-001, MKT-004
- **Origin:** notes/d-…#D-17, #D-18 · **Checked:** pending

### MKT-004 — Amazon runs its own agentic shopping; its 2026 OpenAI deal concerns models for Amazon, not Amazon products in ChatGPT
- **Claim:** Amazon's Shop Direct and Buy for Me buy from other merchants' sites. The 2026-02-27 Amazon–OpenAI announcement covers investment, compute and custom models for Amazon apps. It has no term about Amazon products in ChatGPT.
- **Classification:** VERIFIED FACT (announcement contents). "No Amazon catalog deal with ChatGPT exists" is UNVERIFIED. · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** Amazon / partnerships
- **Source:** "OpenAI and Amazon announce strategic partnership" — Amazon — https://www.aboutamazon.com/news/aws/amazon-open-ai-strategic-partnership-investment ; "Amazon introduces feeds…Shop Direct" — https://www.aboutamazon.com/news/retail/amazon-shop-direct-external-stores
- **Published:** 2026-02-27; 2026-03-11 · **Accessed:** 2026-10-30
- **Excerpt:** > "OpenAI and Amazon will collaborate to develop customized models available to Amazon developers to power Amazon’s customer-facing applications."
- **Establishes:** Amazon is a competing AI shopping surface, not a ChatGPT data partner on record.
- **Limitations:** Absence in one document.
- **Related:** MKT-001
- **Origin:** notes/d-…#D-19, #D-20 · **Checked:** pending

### MKT-005 — eBay opens search pages to OAI-SearchBot and ChatGPT-User, blocks GPTBot, and bans buy-for-me agents in checkout
- **Claim:** eBay's robots.txt (v30.2, August 2026) puts OAI-SearchBot and ChatGPT-User in a group that adds `Allow: /sch/`. GPTBot is disallowed. The header bans buy-for-me agents from checkout. These OpenAI groups were added between 2026-04-27 and 2026-10-30.
- **Classification:** VERIFIED FACT (file contents, archive history) · **Confidence:** High · **Tier:** 1 (primary artifact)
- **Subject / topic:** eBay / crawling
- **Source:** https://www.ebay.com/robots.txt
- **Published:** file comment "v30.2_COM_August_2026" · **Accessed:** 2026-10-30
- **Excerpt:** > "# Checkouts are strictly for human users." … "User-agent: OAI-SearchBot / User-agent: ChatGPT-User / User-agent: Claude-SearchBot / User-agent: Claude-User" … "Allow: /sch/"
- **Establishes:** A marketplace can separate search visibility (allowed) from training (blocked) and agent checkout (banned).
- **Limitations:** No eBay–OpenAI feed or app found.
- **Related:** CGPT-006, CGPT-007
- **Origin:** notes/d-…#D-02 · **Checked:** pending

### MKT-006 — Lazada (SG, MY, TH, PH, VN) explicitly allows all three OpenAI agents
- **Claim:** Five Lazada country sites end their robots.txt with `Allow: /` groups for OAI-SearchBot, GPTBot and ChatGPT-User. Lazada Indonesia names none.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1 (primary artifact)
- **Subject / topic:** Lazada / crawling
- **Source:** https://www.lazada.sg/robots.txt (and .com.my, .co.th, .com.ph, .vn, .co.id)
- **Published:** live file · **Accessed:** 2026-10-30
- **Excerpt:** > "User-agent: OAI-SearchBot / Allow: / / User-agent: GPTBot / Allow: / / User-agent: ChatGPT-User / Allow: /"
- **Establishes:** The only in-scope marketplace that names OpenAI agents to allow them.
- **Limitations:** No partnership found. The `*` group already allows most paths.
- **Related:** MKT-008
- **Origin:** notes/d-…#D-03 · **Checked:** pending

### MKT-007 — Mercado Libre blocks GPTBot and ChatGPT-User but not OAI-SearchBot
- **Claim:** MX, BR and AR root robots.txt files disallow `/` for GPTBot and ChatGPT-User (plus Amazonbot, PerplexityBot, ClaudeBot). OAI-SearchBot falls under `*`.
- **Classification:** VERIFIED FACT (file). "OAI-SearchBot may crawl listings" is EVIDENCE-BASED INFERENCE. · **Confidence:** Medium · **Tier:** 1 (primary artifact)
- **Subject / topic:** Mercado Libre / crawling
- **Source:** https://www.mercadolibre.com.mx/robots.txt
- **Published:** live file · **Accessed:** 2026-10-30
- **Excerpt:** > "User-agent: GPTBot / User-agent: ChatGPT-User / Disallow: /"
- **Establishes:** Search visibility kept, training and user-fetch blocked.
- **Limitations:** Item subdomains (articulo., produto.) returned 403; their rules are unknown.
- **Related:** MKT-005
- **Origin:** notes/d-…#D-04 · **Checked:** pending

### MKT-008 — Flipkart, Myntra, Meesho, JioMart, Walmart, Target, Etsy, Rakuten, Shopee and Allegro name no OpenAI agent
- **Claim:** These robots.txt files have no OpenAI-specific group. OpenAI agents follow the `*` rules, which leave product paths open.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1 (primary artifact)
- **Subject / topic:** Marketplaces / crawling
- **Source:** robots.txt of each site (e.g. https://www.flipkart.com/robots.txt, https://www.walmart.com/robots.txt)
- **Published:** live files · **Accessed:** 2026-10-30
- **Excerpt:** > Flipkart `*` group includes "Disallow: /search?" and "Disallow: */sellers/*" (no product-path disallow)
- **Establishes:** Indian marketplaces' product pages are crawlable by OAI-SearchBot as declared.
- **Limitations:** Meesho and Rakuten blocked one User-Agent at the CDN; network-level bot blocking can differ from robots.txt.
- **Related:** MKT-001, CGPT-022
- **Origin:** notes/d-…#D-16 · **Checked:** 2026-10-30 (Flipkart)

## Official relationships with ChatGPT

### MKT-009 — Walmart: Instant Checkout plan (2025-10-14) → in-ChatGPT app (2026-03-24) → Agent Gateway and agent terms (2026-10-21)
- **Claim:** Walmart announced Instant Checkout in ChatGPT, then launched an app instead. On 2026-10-21 it announced agent terms and an MCP-based Agent Gateway, and listed ChatGPT among its integrations.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Walmart / integrations
- **Source:** https://corporate.walmart.com/news/2025/10/14/walmart-partners-with-openai-to-create-ai-first-shopping-experiences ; https://corporate.walmart.com/news/2026/10/Making-It-Possible-for-Agents-to-Shop-on-Behalf-of-Customers
- **Published:** 2025-10-14; 2026-10-21 · **Accessed:** 2026-10-30
- **Excerpt:** > "Agents that do not follow these terms will be blocked from Walmart’s site." / > "We price products, not people, so the prices that an AI agent sees are the same prices that a human would see on Walmart.com"
- **Establishes:** Large marketplaces admit agents on their own terms and interfaces.
- **Limitations:** Gateway not yet launched on publication date.
- **Related:** CGPT-041
- **Origin:** notes/d-…#D-07, #D-08, #D-09 · **Checked:** pending

### MKT-010 — Etsy: first Instant Checkout partner (2025-09); app in ChatGPT in beta (2026-05-05); catalog integrated
- **Claim:** Etsy says ChatGPT "works well as a discovery channel". Its ChatGPT app hands purchases to Etsy. OpenAI names Etsy's catalog as already integrated.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1 (Etsy post via Wayback 2026-05-14)
- **Subject / topic:** Etsy / integrations
- **Source:** "From Keywords to Conversation…" — Etsy — https://www.etsy.com/news/from-keywords-to-conversation-etsyas-next-steps-into-conversational-search-with-app-in-chatgpt
- **Published:** 2026-05-05 · **Accessed:** 2026-10-30
- **Excerpt:** > "That experience made something clear: ChatGPT works well as a discovery channel. Shoppers often chose to come to Etsy from their chats to learn more before making a purchase."
- **Establishes:** A marketplace's own account of why in-chat checkout gave way to discovery.
- **Limitations:** App region not stated.
- **Related:** CGPT-017, CGPT-021
- **Origin:** notes/d-…#D-10 · **Checked:** pending

### MKT-011 — Target reaches ChatGPT three ways: an app, ACP discovery feeds, and an ads test
- **Claim:** Target launched a ChatGPT app in beta (late Nov 2025), is named as an ACP discovery integrator (2026-03-24), and tested labeled ads in ChatGPT (Feb 2026).
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Target / integrations
- **Source:** https://corporate.target.com/press/release/2025/11/target-to-launch-first-of-its-kind-conversational,-curated-shopping-experience-in-chatgpt ; https://corporate.target.com/press/fact-sheet/2026/02/conversational-ai-advertising
- **Published:** 2025-11-19; 2026-02-09 · **Accessed:** 2026-10-30
- **Excerpt:** > "This ad would appear separately and distinctly, and not influence the answer provided by ChatGPT."
- **Establishes:** Organic feed, app and paid ad are separate surfaces for one retailer.
- **Limitations:** US context.
- **Related:** CGPT-018, CGPT-042
- **Origin:** notes/d-…#D-11 · **Checked:** pending

### MKT-012 — Shopee app in ChatGPT in 8 markets (2026-06-22); Allegro app (2026-05-12)
- **Claim:** Sea says the Shopee app is in ChatGPT for users in Indonesia, Malaysia, the Philippines, Singapore, Thailand, Taiwan, Vietnam and Brazil. Allegro says its app is available to every ChatGPT user. Both hand purchases to their own checkout.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Shopee, Allegro / integrations
- **Source:** https://www.sea.com/news/406 ; https://media.allegro.pl/457629-allegro-uruchamia-apke-na-chatgpt-i-tworzy-nowy-standard-w-konwersacyjnym-e-commerceie
- **Published:** 2026-06-22; 2026-05-12 · **Accessed:** 2026-10-30
- **Excerpt:** > "The Shopee App is now available in ChatGPT for users from Indonesia, Malaysia, the Philippines, Singapore, Thailand, Taiwan, Vietnam, and Brazil."
- **Establishes:** Apps reach users outside the US, unlike ChatGPT's own shopping results (CGPT-022).
- **Limitations:** Whether Shopee or Allegro send ACP feeds for general results is not stated.
- **Related:** CGPT-022, CGPT-038
- **Origin:** notes/d-…#D-24, #D-25 · **Checked:** pending

### MKT-013 — OpenAI's feed spec separates the supplying seller from the marketplace
- **Claim:** `seller_name` is required on every row. `marketplace_seller` ("Marketplace where checkout occurs") is conditionally required for third-party marketplace offers.
- **Classification:** VERIFIED FACT (spec). Display rule for marketplace offers: UNVERIFIED. · **Confidence:** High · **Tier:** 1
- **Subject / topic:** OpenAI feed / marketplaces
- **Source:** https://developers.openai.com/commerce/specs/file-upload/products.md
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "For a third-party seller, `seller_name` identifies that seller and `marketplace_seller` identifies the marketplace where checkout occurs."
- **Establishes:** Marketplaces can submit third-party offers through feeds.
- **Limitations:** "Primary seller" (CGPT-015) is undefined.
- **Related:** CGPT-015, CGPT-028
- **Origin:** notes/d-…#D-06 · **Checked:** pending

## India

### MKT-014 — Razorpay, NPCI and OpenAI announced a UPI agentic-payments private beta in ChatGPT (2025-10-09)
- **Claim:** Razorpay announced a private beta using UPI Circle and UPI Reserve Pay, with bigbasket demos. No 2026 primary status update was found.
- **Classification:** VERIFIED FACT (announcement). Current status: UNVERIFIED. · **Confidence:** Medium · **Tier:** 1 (participant)
- **Subject / topic:** India / payments
- **Source:** https://razorpay.com/blog/razorpay-unveils-agentic-payments-on-chatgpt-with-npci-indias-first-ai-powered-conversational-payment-experience/
- **Published:** 2025-10-09 · **Accessed:** 2026-10-30
- **Excerpt:** > "This private beta is just the first step. Over the coming months, Razorpay, NPCI, and OpenAI will work together to move this innovation from a proof-of-concept into full production."
- **Establishes:** The only OpenAI-linked commerce initiative in India found at a primary source.
- **Limitations:** Predates OpenAI's 2026-03-24 checkout pivot.
- **Related:** CGPT-046
- **Origin:** notes/d-…#D-13 · **Checked:** pending

### MKT-015 — Calcutta High Court order records OpenAI "relying on the USTR" list and ChatGPT linking sellers' own sites instead of IndiaMART
- **Claim:** The 2026-05-20 order dismissed IndiaMART's interim plea. It records IndiaMART's allegation that ChatGPT links sellers' own websites instead of IndiaMART listings, and OpenAI's reliance on the USTR Notorious Markets list.
- **Classification:** VERIFIED FACT (order contents). How the rule works inside ChatGPT is not described. · **Confidence:** Medium · **Tier:** 1 (court order; third-party-hosted copy)
- **Subject / topic:** India / marketplace display
- **Source:** IndiaMart Inter Mesh Ltd vs Open AI Inc. and Ors. — High Court at Calcutta — https://www.medianama.com/wp-content/uploads/2026/05/indiamart-open-ai-675345.pdf
- **Published:** 2026-05-20 · **Accessed:** 2026-10-30
- **Excerpt:** > "The petitioner cannot also impugn the policy adopted by the respondents in relying on the USTR." / > "Significantly, at an earlier point of time, the petitioner itself has blocked ChatGPT from accessing its website."
- **Establishes:** Non-relevance policies can change which marketplace links appear. A seller's own site can replace a marketplace link.
- **Limitations:** Parties' submissions, not findings of fact. Surface (search vs shopping) not stated.
- **Related:** CGPT-010, CGPT-026
- **Origin:** notes/d-…#D-14 · **Checked:** pending

### MKT-016 — No OpenAI partnership found for Flipkart, Myntra, Meesho or JioMart; Nykaa app reported (Tier 3)
- **Claim:** Searches found no OpenAI relationship for the four Indian marketplaces. MediaNama reports Nykaa listing storefronts as apps in ChatGPT for users in India.
- **Classification:** UNVERIFIED (negative search; Nykaa at Tier 3 only) · **Confidence:** Low · **Tier:** 3
- **Subject / topic:** India / integrations
- **Source:** "Nykaa taps OpenAI for conversational shopping…" — MediaNama — https://www.medianama.com/2026/06/223-nykaa-openai-conversational-shopping-beauty-fashion/
- **Published:** 2026-06-17 · **Accessed:** 2026-10-30
- **Excerpt:** > "to list its beauty and fashion storefronts as connected apps in ChatGPT, allowing users in India to get product recommendations through conversations in ChatGPT, before being routed to Nykaa’s app or website to complete a purchase."
- **Establishes:** India's documented ChatGPT commerce paths are apps and payment pilots, not product results.
- **Limitations:** Needs Nykaa or exchange-filing confirmation.
- **Related:** CGPT-046, MKT-008
- **Origin:** notes/d-…#D-27 · **Checked:** pending

## Other commerce platforms (non-Shopify paths into ChatGPT)

### MKT-017 — Stripe's Agentic Commerce Suite is the shared rail for Wix, BigCommerce, WooCommerce and others
- **Claim:** Stripe ACS (2025-12-11) lets businesses sell across AI agents with one integration. Stripe extended it to platforms in April 2026. OpenAI names Stripe as an ACP feed delivery path (CGPT-018).
- **Classification:** VERIFIED FACT (Stripe statements). "Main non-Shopify path into ChatGPT" is EVIDENCE-BASED INFERENCE. · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** Platforms / integrations
- **Source:** https://stripe.com/newsroom/news/agentic-commerce-suite ; https://stripe.com/newsroom/news/sessions-2026
- **Published:** 2025-12-11; 2026-04-29 · **Accessed:** 2026-10-30
- **Excerpt:** > "Stripe is also bringing the Agentic Commerce Suite to platforms, so businesses on Wix, BigCommerce, WooCommerce and more can easily sell to customers inside AI apps."
- **Establishes:** Non-Shopify stores need an opt-in integration; Shopify stores are default-on (SHOP-001).
- **Limitations:** Per-platform go-live for ChatGPT not published.
- **Related:** CGPT-018, ACP-007
- **Origin:** notes/c-…#C-37 · **Checked:** pending

### MKT-018 — commercetools: "OpenAI ChatGPT supports product discovery" (AI Hub GA, 2026-07-30)
- **Claim:** commercetools' AI Hub release says ChatGPT supports product discovery, while Gemini supports discovery through checkout via UCP.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Platforms / integrations
- **Source:** "AI Hub is now generally available" — commercetools docs — https://docs.commercetools.com/api/releases/2026-07-30-ai-hub-is-now-generally-available
- **Published:** 2026-07-30 · **Accessed:** 2026-10-30
- **Excerpt:** > "OpenAI ChatGPT supports product discovery."
- **Establishes:** Independent platform confirmation that ChatGPT is discovery-only in 2026.
- **Limitations:** Add-on product.
- **Related:** CGPT-021
- **Origin:** notes/c-…#C-33 · **Checked:** pending

### MKT-019 — Salesforce lists its ChatGPT catalog integration "GA July 2026", synced from Business Manager
- **Claim:** Salesforce's June 2026 release lists ChatGPT integration GA July 2026, with catalogs synced from Business Manager.
- **Classification:** VERIFIED FACT (announcement). Actual GA: UNVERIFIED. · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** Platforms / integrations
- **Source:** https://www.salesforce.com/news/stories/agentforce-commerce-announcement/
- **Published:** 2026-06-24 · **Accessed:** 2026-10-30
- **Excerpt:** > "Through our OpenAI integration, your product catalog connects directly to ChatGPT, synced straight from Business Manager — no extra software, no third-party tools."
- **Establishes:** Salesforce Commerce Cloud reaches ChatGPT via ACP feed.
- **Limitations:** No post-July source fetched.
- **Related:** CGPT-018
- **Origin:** notes/c-…#C-32 · **Checked:** pending

### MKT-020 — BigCommerce merchants syndicate to OpenAI via Feedonomics Agentic Catalog Exports (April 2026)
- **Claim:** Commerce (BigCommerce) says merchants began syndicating catalogs to OpenAI and Gemini via Feedonomics ACE in April 2026.
- **Classification:** VERIFIED FACT · **Confidence:** Medium (enterprise service) · **Tier:** 1
- **Subject / topic:** Platforms / integrations
- **Source:** "Commerce Announces First Quarter 2026 Financial Results" — https://investors.bigcommerce.com/news-releases/news-release-details/commerce-announces-first-quarter-2026-financial-results
- **Published:** 2026-05-07 · **Accessed:** 2026-10-30
- **Excerpt:** > "In April 2026, the Company announced that merchants are now syndicating catalog data to key agentic discovery channels including OpenAI and Google Gemini, using Feedonomics Agentic Catalog Exports (ACE)…"
- **Establishes:** Feed services are a delivery path for non-Shopify stores.
- **Limitations:** Availability to all BigCommerce merchants not stated.
- **Related:** MKT-017
- **Origin:** notes/c-…#C-31 · **Checked:** pending

### MKT-021 — WooCommerce, Wix and Adobe Commerce paths to ChatGPT are opt-in or in progress
- **Claim:** WooCommerce says its Stripe ACP integration is "built" and that ChatGPT is a discovery channel; its own setting exposes UCP. Wix says its Stripe ACS integration is "rolling out gradually". Adobe committed to ACP and UCP and ships a crawler-facing layer.
- **Classification:** VERIFIED FACT (vendor statements). Live ChatGPT availability per platform: UNVERIFIED. · **Confidence:** Medium · **Tier:** 1 (vendor)
- **Subject / topic:** Platforms / integrations
- **Source:** https://woocommerce.com/posts/ai-product-discovery/ (excerpt) ; https://woocommerce.com/posts/ai-commerce-trends-stripe-sessions/ ; https://www.wix.com/blog/agentic-commerce-on-wix ; https://business.adobe.com/blog/product-discovery-on-llm-surfaces-is-available-in-adobe-commerce
- **Published:** 2026-03-17; 2026-05-14; 2026-07-27; 2026-08-07 · **Accessed:** 2026-10-30
- **Excerpt:** > "For stores, this means ChatGPT is already a discovery channel today. Products can be found, compared, and recommended inside a chat session. The transaction completes in the store’s environment and checkout." (WooCommerce, 2026-03-17 post)
- **Establishes:** Only Shopify (and Etsy) are default-on for ChatGPT. Others rely on opt-in feeds or crawl.
- **Limitations:** Vendor marketing.
- **Related:** MKT-017, SHOP-001
- **Origin:** notes/c-…#C-30, #C-34, #C-35 · **Checked:** pending

## Google: crawl policy and relationships

Origin files for this section: `research/ai-platforms/gemini/notes/gd-…` (GD-xx) and `gc-…` (GC-xx).

### MKT-022 — Amazon blocks Google-Extended and GoogleAgent-* tokens but leaves Googlebot and Storebot-Google under `*`
- **Claim:** amazon.com and amazon.in disallow `/` for Google-Extended, GoogleAgent-Mariner, GoogleAgent-Shopping, GoogleOther, Google-CloudVertexBot and others. Googlebot and Storebot-Google have no group and follow `*`, which does not disallow `/dp/` product pages.
- **Classification:** VERIFIED FACT (file contents). "Googlebot may crawl Amazon product pages" is an EVIDENCE-BASED INFERENCE. · **Confidence:** High · **Tier:** 1 (primary artifact)
- **Subject / topic:** Amazon / crawling (Google)
- **Source:** https://www.amazon.com/robots.txt ; https://www.amazon.in/robots.txt
- **Published:** live file · **Accessed:** 2026-10-30
- **Excerpt:** > "User-agent: Google-Extended / Disallow: /" … "User-agent: GoogleAgent-Shopping / Disallow: /"
- **Establishes:** Amazon stays eligible for Google Search and AI Mode (GOOG-026) while opting out of Gemini app grounding (GOOG-027). Contrast: Amazon blocks OAI-SearchBot, OpenAI's search crawler (MKT-001).
- **Limitations:** Google's documented agent token is `Google-Agent`, which Amazon does not name (GOOG-032). A vendor study lists no Amazon among Gemini's cited retailers (Tier 3).
- **Related:** MKT-001, GOOG-027, GOOG-032
- **Origin:** notes/gd-…#GD-17; notes/ge-…#GE-38 · **Checked:** pending

### MKT-023 — Amazon sits on the UCP Shopping Tech Council; no Amazon catalog integration with Gemini or AI Mode found
- **Claim:** UCP's maintainer file lists an Amazon representative on the Shopping Tech Council. No source shows Amazon integrating UCP checkout or a catalog with Gemini/AI Mode.
- **Classification:** VERIFIED FACT (membership); integration absence UNVERIFIED · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** Amazon / protocols
- **Source:** MAINTAINERS.md — Universal-Commerce-Protocol/.github — https://github.com/Universal-Commerce-Protocol/.github/blob/main/MAINTAINERS.md
- **Published:** last commit touching file 2026-10-12 · **Accessed:** 2026-10-30
- **Excerpt:** > "| Jordan Williams | Amazon     |"
- **Establishes:** Protocol governance and crawl policy are different layers for Amazon.
- **Limitations:** TechCrunch (Tier 3) reports Amazon listings appeared in Gemini without a Buy button in India.
- **Related:** UCP-003, MKT-022
- **Origin:** notes/gd-…#GD-26 · **Checked:** pending

### MKT-024 — Walmart and Etsy: UCP co-developers with live Google surfaces (Walmart-built Gemini experience; Etsy checkout from 2026-02-11)
- **Claim:** Walmart announced a Walmart-built experience inside Gemini via UCP (2026-01-11, US first) and is a named Universal Cart checkout merchant (2026-10-15). Google said UCP checkout was rolling out for Etsy and Wayfair items in AI Mode and Gemini on 2026-02-11.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Walmart, Etsy / Google integrations
- **Source:** https://corporate.walmart.com/news/2026/01/11/walmart-and-google-turn-ai-discovery-into-effortless-shopping-experiences ; "What to expect in digital advertising and commerce in 2026" — Google — https://blog.google/products/ads-commerce/digital-advertising-commerce-2026/
- **Published:** 2026-01-11; 2026-02-11 · **Accessed:** 2026-10-30
- **Excerpt:** > "In fact, UCP-powered checkout is rolling out now, letting US shoppers buy items from Etsy and Wayfair, right in AI Mode in Search and the Gemini app (with Shopify, Target, and Walmart coming soon)."
- **Establishes:** Marketplaces that co-develop UCP get in-surface checkout on Google.
- **Limitations:** US only.
- **Related:** UCP-001, MKT-009, MKT-010
- **Origin:** notes/gd-…#GD-25, #GD-27, #GD-28 · **Checked:** pending

### MKT-025 — Flipkart names Storebot-Google to allow it into `/viewcart`; Flipkart is Google's only named Indian UCP partner
- **Claim:** Flipkart's robots.txt has a Storebot-Google group with `Allow: /viewcart`, the only marketplace in scope naming Google's Shopping crawler. Flipkart is a UCP endorser, and Google says Flipkart is partnering on UCP agentic shopping for Indian shoppers (GEM-016).
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1 (primary artifact)
- **Subject / topic:** Flipkart / Google
- **Source:** https://www.flipkart.com/robots.txt
- **Published:** live file · **Accessed:** 2026-10-30
- **Excerpt:** > "# Allow Store bot / User-agent: Storebot-Google / Allow: /viewcart"
- **Establishes:** Flipkart actively accommodates Google Shopping; it has no OpenAI arrangement on record (MKT-016).
- **Limitations:** Rule intent beyond the comment is not stated.
- **Related:** GEM-016, UCP-001, MKT-016
- **Origin:** notes/gd-…#GD-19, #GD-29 · **Checked:** pending

### MKT-026 — Other marketplaces name no Google AI token; eBay and Mercado Libre block other AI agents but not Google-Extended
- **Claim:** Walmart, Etsy, Target, Meesho, JioMart, Myntra, Lazada, Allegro and Mercado Libre name no Google AI token. eBay's Googlebot group equals its `*` group and its AI block list omits Google-Extended. Mercado Libre blocks Amazon, Perplexity, Anthropic and OpenAI agents but no Google token.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1 (primary artifacts)
- **Subject / topic:** Marketplaces / crawling (Google)
- **Source:** robots.txt of each site (e.g. https://www.ebay.com/robots.txt, https://www.mercadolibre.com.mx/robots.txt)
- **Published:** live files · **Accessed:** 2026-10-30
- **Excerpt:** > (Mercado Libre) "User-agent: Amazonbot / User-agent: PerplexityBot / User-agent: Perplexity-User / User-agent: ClaudeBot / User-agent: Claude-User / User-agent: GPTBot / User-agent: ChatGPT-User / Disallow: /"
- **Establishes:** Marketplaces treat Google AI access more permissively than OpenAI's. Only Amazon opts out of Gemini grounding.
- **Limitations:** Mercado Libre and Myntra files were read as rendered browser text.
- **Related:** MKT-005, MKT-007, MKT-022
- **Origin:** notes/gd-…#GD-18, #GD-22, #GD-35 · **Checked:** pending

### MKT-027 — Shopee and Google announced an "agentic shopping prototype" (2026-02-19)
- **Claim:** Sea said Shopee and Google will jointly explore an AI agentic shopping prototype across both platforms.
- **Classification:** VERIFIED FACT (announcement); live integration UNVERIFIED · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** Shopee / Google
- **Source:** "Sea and Google Deepen Partnership…" — Sea Limited — https://www.sea.com/news/384
- **Published:** 2026-02-19 · **Accessed:** 2026-10-30
- **Excerpt:** > "Advancing Agentic Commerce: Shopee and Google will jointly explore the building of an AI agentic shopping prototype that can seamlessly integrate across Shopee and Google platforms to enhance the e-commerce discovery, engagement, and transaction experience."
- **Establishes:** Shopee works with both OpenAI (app, MKT-012) and Google.
- **Limitations:** "Explore" language.
- **Related:** MKT-012
- **Origin:** notes/gd-…#GD-32 · **Checked:** pending

### MKT-028 — Platforms → Google: only Shopify is default-on for Google checkout; all rely on Merchant Center for discovery
- **Claim:** Salesforce says merchants "can now turn on" UCP checkout on Google (2026-10-26). BigCommerce offers Google UCP checkout in early access. WooCommerce marks Google UCP "Coming soon". Stripe says US entities can already sell via Gemini. Wix and Squarespace send products to Merchant Center. Every platform that states a Google discovery path names Merchant Center.
- **Classification:** VERIFIED FACT (vendor statements); the cross-platform comparison is an EVIDENCE-BASED INFERENCE · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** Platforms / Google
- **Source:** "Peak-Ready Precision: The October 2026 B2C Commerce Release" — Salesforce — https://www.salesforce.com/blog/b2c-commerce-october-26-release/ ; "Agentic Commerce" — WooCommerce — https://woocommerce.com/agentic-commerce/ ; "Google Agentic Checkout…" — BigCommerce — https://www.bigcommerce.com/articles/ecommerce/google-agentic-checkout/
- **Published:** 2026-10-26; 2026-10-25; 2026-10-13 · **Accessed:** 2026-10-30
- **Excerpt:** > "Merchants can now turn on UCP-powered checkout on Google to enable shoppers to seamlessly discover and buy products directly on surfaces like the Gemini app and Google Search, including AI Mode — while staying the merchant of record." (Salesforce)
- **Establishes:** On Google, Merchant Center is the common discovery input for every platform; checkout enrollment differs.
- **Limitations:** Vendor statements; live status per merchant varies.
- **Related:** SHOP-025, SHOP-026, MKT-017
- **Origin:** notes/gc-…#GC-27 to #GC-35 · **Checked:** pending

### MKT-029 — No Google AI-shopping relationship found for eBay, Mercado Libre, Rakuten, Lazada, Allegro, Myntra, Meesho or JioMart
- **Claim:** English searches and Google/UCP documents show no UCP participation, Gemini/AI Mode integration or AI-shopping partnership with Google for these eight marketplaces.
- **Classification:** UNVERIFIED HYPOTHESIS that none exists (negative search); absence from named Google/UCP documents is VERIFIED FACT · **Confidence:** Low · **Tier:** n/a
- **Subject / topic:** Marketplaces / Google
- **Source:** documents in UCP-001, MKT-023, MKT-024
- **Published:** n/a · **Accessed:** 2026-10-30
- **Excerpt:** [no text: negative search result]
- **Establishes:** Their documented path into Gemini/AI Mode is the general one: Search index and Shopping Graph.
- **Limitations:** Non-English searches not run.
- **Related:** MKT-026
- **Origin:** notes/gd-…#GD-37 · **Checked:** pending
