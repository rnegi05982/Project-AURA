# Registry — GOOG (Google merchant and search infrastructure)

Schema: `evidence/README.md`. Covers Merchant Center, Shopping Graph, Google's UCP implementation, Shopping ranking statements, Search Central, crawlers and structured data. Consumer AI surfaces are in `gem.md`. Accessed 2026-10-30 unless stated.

---

## UCP on Google (merchant side)

### GOOG-001 — UCP checkout on Google is gated: early access, interest form, and a per-item `native_commerce` flag (default off)
- **Claim:** UCP-powered checkout puts a "Buy" button on eligible listings in AI Mode and Gemini for select merchants. Merchants submit an interest form and implement the integration. Only items with `native_commerce(checkout_eligibility)` = true show Buy. Cart transfer is opt-out once the UCP profile declares cart support.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / checkout
- **Source:** "About the Universal Commerce Protocol (UCP) and UCP-powered checkout feature on Google" — Merchant Center Help — https://support.google.com/merchants/answer/16837055?hl=en ; "Merchant Center setup" — Google for Developers — https://developers.google.com/merchant/ucp/guides/overview/merchant-center
- **Published:** dev guide last updated 2026-10-29 · **Accessed:** 2026-10-30
- **Excerpt:** > "This is provided using a product attribute native_commerce(checkout_eligibility) containing a single boolean. If set to FALSE or missing, the product won't be eligible for checkout (defaults to FALSE)."
- **Establishes:** Checkout is opt-in per product; it is not required for discovery.
- **Limitations:** Help page says eligibility covers US, Canada and Australia; consumer checkout is US-only (GEM-014).
- **Related:** GOOG-002, GOOG-003, GEM-014
- **Origin:** notes/gb-…#GB-01, #GB-03, #GB-05 · **Checked:** pending

### GOOG-002 — UCP on Google requires Merchant Center in good standing, free-listings approval, return policy and support contact
- **Claim:** The UCP guide requires an account in good standing with products approved for free listings, return policy (cost, window, link) and customer-support info. Used, refurbished, final-sale, pre-order, subscription and freight items are ineligible for checkout.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / merchant eligibility
- **Source:** "Merchant Center setup" — Google for Developers — https://developers.google.com/merchant/ucp/guides/overview/merchant-center
- **Published:** last updated 2026-10-29 · **Accessed:** 2026-10-30
- **Excerpt:** > "You must have a Merchant Center account in good standing and approved products for free listings in your account."
- **Establishes:** Free-listings approval is the base layer for every Google AI commerce feature.
- **Limitations:** Requirements are for checkout, not visibility.
- **Related:** GOOG-010
- **Origin:** notes/gb-…#GB-04, #GB-06 · **Checked:** pending

### GOOG-003 — Google: UCP native integration "does not influence how we rank your offers"
- **Claim:** Google's UCP FAQ says opting into native integration does not change offer ranking; integrated offers only gain the direct-purchase option.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / ranking
- **Source:** "Frequently asked questions" — Google for Developers (UCP) — https://developers.google.com/merchant/ucp/faq
- **Published:** last updated 2026-10-16 · **Accessed:** 2026-10-30
- **Excerpt:** > "No. Opting for our Native integration does not influence how we rank your offers in product listings."
- **Establishes:** Adopting UCP checkout is not a ranking lever, per Google. Contrast: OpenAI once listed Instant Checkout as a merchant-ranking factor (CGPT-016).
- **Limitations:** Covers native checkout only. Indirect effects through user behaviour are not addressed.
- **Related:** GOOG-004, CGPT-016
- **Origin:** notes/gb-…#GB-07 · **Checked:** 2026-10-31

### GOOG-004 — Google's UCP FAQ: discovery is "powered by our Shopping Graph"; UCP traffic is identifiable
- **Claim:** Google says UCP integrations power AI Mode and the Gemini apps, and that it supports the broader journey, including discovery, "powered by our Shopping Graph". UCP requests carry a `UCP-Agent` header and a User-Agent beginning `Google/UCP`.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / discovery
- **Source:** "Frequently asked questions" — Google for Developers (UCP) — https://developers.google.com/merchant/ucp/faq
- **Published:** last updated 2026-10-16 · **Accessed:** 2026-10-30
- **Excerpt:** > "Unlike protocols focused solely on payments, we support the broader shopping journey (including discovery and consideration) powered by our Shopping Graph."
- **Establishes:** Discovery input on Google AI surfaces = Shopping Graph, fed by Merchant Center.
- **Limitations:** The landing page still says "Gemini web (app coming soon)"; the FAQ says both web and mobile.
- **Related:** GOOG-019, UCP-004
- **Origin:** notes/gb-…#GB-08, #GB-10 · **Checked:** 2026-10-31

### GOOG-005 — UCP go-live needs Google approval; hub rolls out in the US first; platform merchants go through their platform
- **Claim:** Google must approve each integration before it goes live. The Merchant Center UCP hub is rolling out in the US, with Australia and Canada "next year". Merchants on third-party platforms are told to contact their platform.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / onboarding
- **Source:** "Integration overview" — https://developers.google.com/merchant/ucp/guides/overview ; "How to onboard to the UCP integration hub in Merchant Center" — https://support.google.com/merchants/answer/16992327?hl=en
- **Published:** dev page last updated 2026-10-19 · **Accessed:** 2026-10-30
- **Excerpt:** > "If you work with a third-party service provider or platform, please connect directly with them to learn more about their plans for Universal Commerce Protocol integration."
- **Establishes:** Shopify merchants reach Google UCP through Shopify, not directly (see SHOP entries).
- **Limitations:** India not named.
- **Related:** GOOG-001
- **Origin:** notes/gb-…#GB-11, #GB-12 · **Checked:** pending

### GOOG-006 — Native checkout runs in a Google UI; cart transfer hands a cart to the merchant site
- **Claim:** In native checkout the user enters payment and fulfillment in a Google UI; the agent is excluded from that step. The Cart API only creates and transfers a cart to the merchant site. Google implements UCP versions 2026-01-23 and 2026-04-08.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / checkout
- **Source:** "Native checkout overview" — https://developers.google.com/merchant/ucp/guides/overview/native-checkout ; "Cart overview" — https://developers.google.com/merchant/ucp/guides/overview/cart-overview
- **Published:** last updated 2026-10-16 · **Accessed:** 2026-10-30
- **Excerpt:** > "Manual checkout: The user now interacts only with the Google UI to fill in sensitive fulfillment and payment details and submit the order. The Agent is not involved in this part, ensuring determinism."
- **Establishes:** Google's checkout is human-confirmed, not autonomous.
- **Limitations:** None.
- **Related:** UCP-002
- **Origin:** notes/gb-…#GB-13, #GB-14 · **Checked:** pending

### GOOG-007 — Loyalty data does not personalize search results yet ("planned")
- **Claim:** Google supports loyalty only at checkout for account-linked users. Personalized search results from loyalty data are planned for a future release.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / personalization
- **Source:** "Loyalty" — Google for Developers (UCP) — https://developers.google.com/merchant/ucp/guides/overview/loyalty
- **Published:** last updated 2026-10-22 · **Accessed:** 2026-10-30
- **Excerpt:** > "Note: Google surfaces support loyalty integration only at checkout for verified, account-linked users. Personalized search results are planned for a future release."
- **Establishes:** Identity linking is not a discovery lever today.
- **Limitations:** Conflicts in tone with a Sept 2026 blog example of member pricing in results (notes/ga-…#GA-09).
- **Related:** GEM-011
- **Origin:** notes/gb-…#GB-39 · **Checked:** pending

### GOOG-008 — Business Agent: a brand chat agent on Search for US stores with ≥50 approved free listings
- **Claim:** Business Agent is a Gemini-powered brand chat on Search. Customization needs a US e-commerce store, verified Merchant Center, at least 50 approved free listings and a claimed brand profile. It answers from Merchant Center data and the website. Shopify merchants activate it via the Google & YouTube app.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / merchant agents
- **Source:** "Get started with Business Agent" — Merchant Center Help — https://support.google.com/merchants/answer/16410382?hl=en
- **Published:** not stated (launched 2026-01-11) · **Accessed:** 2026-10-30
- **Excerpt:** > "Business Agent uses Gemini models to analyze information from your Merchant Center account and additional business data you provide, including your website."
- **Establishes:** A brand-query surface, not a non-brand discovery surface.
- **Limitations:** US only.
- **Related:** GOOG-012
- **Origin:** notes/gb-…#GB-37 · **Checked:** pending

## Merchant Center and product data

### GOOG-009 — Google uses Merchant Center data "to match your products to the right queries"; missing data limits eligibility
- **Claim:** The Product data specification says Google uses the data for query matching and as input to AI-powered formats. Missing or incorrect data can cause disapprovals or "limited eligibility". Optional attributes "help boost your product's performance".
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / product data
- **Source:** "Product data specification" — Merchant Center Help — https://support.google.com/merchants/answer/7052112?hl=en
- **Published:** not stated (latest dated update 2026-04-14) · **Accessed:** 2026-10-30
- **Excerpt:** > "Google uses this data to match your products to the right queries, and as a foundational input to help optimize and enhance the content of the ads being served in our AI powered formats and experiences."
- **Establishes:** Feed data drives query matching and eligibility, per Google.
- **Limitations:** "Boost performance" is not a ranking-factor statement. AI surfaces are not named.
- **Related:** GOOG-012, GOOG-017
- **Origin:** notes/gb-…#GB-20 · **Checked:** pending

### GOOG-010 — Free listings are on by default and can appear on Gemini; crawled products can show without Merchant Center
- **Claim:** Free listings may show on Search, Maps, Gemini, YouTube, Shopping, Images and Lens. New accounts are opted in. Products crawled from a store "can show up on Google" even without schema.org markup or Merchant Center. Free-listings status does not guarantee display.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / discovery paths
- **Source:** "Free listings for products" — Merchant Center Help — https://support.google.com/merchants/answer/13889434?hl=en
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Content from your online store: Products and their details that have been crawled on your online store can show up on Google. This can occur even if the information hasn’t been marked up using schema.org or added in Merchant Center."
- **Establishes:** Two paths into the Shopping Graph: Merchant Center feeds and crawl.
- **Limitations:** Whether crawl-only products appear as AI Mode or Gemini product cards is undocumented.
- **Related:** GOOG-011, GOOG-019
- **Origin:** notes/gb-…#GB-27 · **Checked:** pending

### GOOG-011 — Search Central: Merchant Center is optional for Search but mandatory for the Shopping tab; AI features need no extra technical requirements
- **Claim:** Merchant Center is not mandatory to appear in Search results but is mandatory for the Shopping tab. A page is eligible as an AI Overviews/AI Mode supporting link if it is indexed and snippet-eligible; there are no extra technical requirements.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / eligibility
- **Source:** "Share your product data with Google" — https://developers.google.com/search/docs/specialty/ecommerce/share-your-product-data-with-google ; "AI features and your website" — https://developers.google.com/search/docs/appearance/ai-features
- **Published:** last updated 2025-12-10 (both) · **Accessed:** 2026-10-30
- **Excerpt:** > "To be eligible to be shown as a supporting link in AI Overviews or AI Mode, a page must be indexed and eligible to be shown in Google Search with a snippet, fulfilling the Search technical requirements. There are no additional technical requirements."
- **Establishes:** Web-page citations and product listings have separate eligibility rules.
- **Limitations:** Neither page addresses AI Mode product cards.
- **Related:** GOOG-010
- **Origin:** notes/gb-…#GB-28 · **Checked:** pending

### GOOG-012 — Six optional "conversational attributes" target AI Mode
- **Claim:** Merchant Center lists `question_and_answer`, `document_link`, `related_product`, `item_group_title`, `variant_option` and `popularity_rank`. They are optional, do not affect approval, and help AI systems "better understand" products on surfaces like AI Mode.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / product data
- **Source:** "How to use conversational attributes" — Merchant Center Help — https://support.google.com/merchants/answer/17085370?hl=en
- **Published:** not stated (announced 2026-01-11; global 2026-05-20) · **Accessed:** 2026-10-30
- **Excerpt:** > "Conversational attributes help AI systems and conversational agents better understand your products’ specific nuances. They are completely optional, and designed to complement your primary Merchant Center product data specification."
- **Establishes:** Google built feed fields specifically for AI Mode. One test shows they enter answer text (GEM-013).
- **Limitations:** No statement that they affect ranking.
- **Related:** GOOG-013, GOOG-014, GEM-013
- **Origin:** notes/gb-…#GB-21 · **Checked:** pending

### GOOG-013 — `question_and_answer` is "primarily intended" for AI Mode; Google extracts FAQs from `document_link` PDFs
- **Claim:** Q&A allows up to 30 pairs, no prices or dates. If linked PDFs hold the same information, Google extracts FAQ content from those documents instead.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / product data
- **Source:** "Question and answer [question_and_answer]" — Merchant Center Help — https://support.google.com/merchants/answer/17085211?hl=en
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Note: This attribute is primarily intended for use in conversational experiences such as AI mode in Google Search."
- **Establishes:** Google reads merchant PDFs (manuals, spec sheets) for AI Mode answers.
- **Limitations:** Intent, not a ranking statement.
- **Related:** GOOG-012
- **Origin:** notes/gb-…#GB-22 · **Checked:** pending

### GOOG-014 — `popularity_rank`: merchant-declared 0–100 sales popularity for AI Mode
- **Claim:** `popularity_rank` is optional and merchant-assessed from recent sales. Google says it is "primarily intended" for AI Mode and does not reflect user ratings.
- **Classification:** VERIFIED FACT (field exists). Use in ranking: UNVERIFIED HYPOTHESIS. · **Confidence:** Medium (spec and attribute page disagree on scope) · **Tier:** 1
- **Subject / topic:** Google / product data
- **Source:** "Popularity rank [popularity_rank]" — Merchant Center Help — https://support.google.com/merchants/answer/17085297?hl=en
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Use this attribute to communicate how well your products are selling, like your latest best sellers, and help consumers make a more informed buying decision."
- **Establishes:** A popularity signal channel exists on Google (OpenAI dropped its equivalent, CGPT-030).
- **Limitations:** "Entire inventory" (spec) vs "same general category" (attribute page).
- **Related:** CGPT-030, ACP-007
- **Origin:** notes/gb-…#GB-23 · **Checked:** pending

### GOOG-015 — `related_product` and `variant_option` encode accessories, substitutes and variants
- **Claim:** `related_product` supports types such as `accessory`, `substitute`, `required_part`, `often_bought_with`. `variant_option` defines variant dimensions and drives the UCP item selector; incomplete variant data can suppress the Buy button.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / product data
- **Source:** "Product data specification" — https://support.google.com/merchants/answer/7052112?hl=en ; UCP "Merchant Center setup" — https://developers.google.com/merchant/ucp/guides/overview/merchant-center
- **Published:** not stated; 2026-10-29 · **Accessed:** 2026-10-30
- **Excerpt:** > "Providing complete variant data also prevents automated transactability discrepancies that can suppress the checkout button."
- **Establishes:** Variant completeness affects checkout display.
- **Limitations:** No statement that related products drive recommendations.
- **Related:** GOOG-001
- **Origin:** notes/gb-…#GB-24, #GB-05 · **Checked:** pending

### GOOG-016 — 2026 spec changes: `video_link` (shown in AI Mode), new shipping fields, 500×500 image minimum from 2027-01-31
- **Claim:** The 2026 spec update added `video_link` (eligible from 2026-06-30), product-level shipping fields, and raises the image minimum to 500×500 pixels, enforced 2027-01-31. Merchant Center says product videos appear in AI Mode.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / product data
- **Source:** "Merchant Center product data specification update 2026" — https://support.google.com/merchants/answer/16989427?hl=en ; "About using product videos across Google Shopping" — https://support.google.com/merchants/answer/18545837?hl=en
- **Published:** 2026-04-14 · **Accessed:** 2026-10-30
- **Excerpt:** > "These videos appear across various Google surfaces, including AI Mode, free Search listings, and Google Ads campaigns."
- **Establishes:** A dated compliance deadline for images.
- **Limitations:** No ranking statement.
- **Related:** GOOG-009
- **Origin:** notes/gb-…#GB-25 · **Checked:** pending

### GOOG-017 — Merchant Center "AI performance" report covers AI Mode and AI Overviews, including India (English queries)
- **Claim:** The AI performance insights report shows share of voice for shopping-intent queries on AI Mode and AI Overviews, for English queries in AU, CA, IN, NZ and US. Data covers organic (free listings) only. Google's advice: complete attributes and add relevant terms to titles and descriptions.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / measurement
- **Source:** "About AI performance insights" — Merchant Center Help — https://support.google.com/merchants/answer/17200695?hl=en
- **Published:** announced 2026-05-27 · **Accessed:** 2026-10-30
- **Excerpt:** > "AI performance insights are currently available for English-language queries for Merchant Center accounts in Australia, Canada, India, New Zealand, and the United States."
- **Establishes:** Indian merchants have a first-party measurement tool for Google AI surfaces. ChatGPT offers none for India.
- **Limitations:** Google's advice is not a disclosed mechanism.
- **Related:** GEM-002, SHOP-013
- **Origin:** notes/gb-…#GB-26; notes/ga-…#GA-10 · **Checked:** pending

### GOOG-018 — No AI-surface-specific opt-out for listings or ads
- **Claim:** Merchant Center destinations have no AI Mode, AI Overviews or Gemini value. Advertisers cannot target or exclude AI Overviews/AI Mode separately from Search.
- **Classification:** VERIFIED FACT (value list; Ads FAQ). "No AI-only opt-out for free listings" is an EVIDENCE-BASED INFERENCE. · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** Google / controls
- **Source:** "Product data specification" — https://support.google.com/merchants/answer/7052112?hl=en ; "About ads in AI-powered experiences in Google Search" — https://support.google.com/google-ads/answer/18826097?hl=en
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "you can't target ads exclusively to AI Overviews or AI Mode, or opt out of showing ads in them separately from Search."
- **Establishes:** Participating in free listings or Shopping ads means participating in AI surfaces.
- **Limitations:** Page-level controls (nosnippet, robots) act on web pages, not listings.
- **Related:** GOOG-010
- **Origin:** notes/gb-…#GB-29 · **Checked:** pending

## Shopping Graph and ranking statements

### GOOG-019 — Shopping Graph scale: "over 60 billion product listings" (May 2026); earlier "2 billion … refreshed every hour"
- **Claim:** Google states the Shopping Graph has 60+ billion listings (2026-05-19, 2026-10-15). Earlier statements (2025-05 to 2026-04) said 50B+ listings with 2B+ refreshed hourly; the hourly figure has not been restated since.
- **Classification:** VERIFIED FACT (Google's claims) · **Confidence:** Medium (marketing figures) · **Tier:** 1
- **Subject / topic:** Google / data sources
- **Source:** "Introducing the Universal Cart and more ways to help you shop" — https://blog.google/products-and-platforms/products/shopping/google-shopping-cart/ ; NRF 2026 remarks — https://blog.google/company-news/inside-google/message-ceo/nrf-2026-remarks/
- **Published:** 2026-05-19; 2026-01-11 · **Accessed:** 2026-10-30
- **Excerpt:** > "People shop across Google more than a billion times a day, powered by advanced AI and the Shopping Graph — the world’s most comprehensive catalog of over 60 billion product listings."
- **Establishes:** Scale and freshness claims for Google's product index.
- **Limitations:** Listings ≠ unique products. "Refreshed" undefined.
- **Related:** GOOG-020, CGPT-027 (OpenAI daily feed cadence)
- **Origin:** notes/ga-…#GA-03, #GA-05; notes/gb-…#GB-31 · **Checked:** pending

### GOOG-020 — Shopping Graph sources: Merchant Center, Manufacturer Center, and what retailers post across the web
- **Claim:** Google describes the Shopping Graph as updated through Merchant Center or "from what retailers and brands post across the web", plus reviews and YouTube videos. The help page names Merchant Center and Manufacturer Center and says Shopping Graph info powers generative AI features such as recommendations.
- **Classification:** VERIFIED FACT · **Confidence:** Medium (the web-crawl statement is from a 2023 post) · **Tier:** 1
- **Subject / topic:** Google / data sources
- **Source:** "4 ways Google's Shopping Graph helps you find what you want" — https://blog.google/products-and-platforms/products/shopping/shopping-graph-explained/ ; "Sources of shopping info" — https://support.google.com/googleshopping/answer/14336735?hl=en
- **Published:** 2023-02-07; help not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Listings show products and their sellers, and they’re updated constantly — either through information retailers share directly via Google Merchant Center or from what retailers and brands post across the web."
- **Establishes:** Feed and crawl both feed the index that powers Gemini and AI Mode (GEM-001, GEM-003).
- **Limitations:** Precedence between feed and crawled data is undocumented.
- **Related:** GOOG-010, GOOG-019
- **Origin:** notes/gb-…#GB-30; notes/ga-…#GA-19 · **Checked:** pending

### GOOG-021 — Store Quality "may boost" Shopping-tab visibility; Top Quality Store badge scores shipping, returns, ratings, site
- **Claim:** Merchants are auto-enrolled in Store Quality (delivery, returns, images, site speed). Google's example says better shipping data "may boost" visibility on the Shopping tab. The Top Quality Store badge uses shipping/returns data, user ratings and website checks.
- **Classification:** VERIFIED FACT · **Confidence:** Medium (hedged, Shopping tab only) · **Tier:** 1
- **Subject / topic:** Google / ranking signals
- **Source:** "About the Store Quality program" — https://support.google.com/merchants/answer/14261098?hl=en ; "About the Top Quality Store badge" — https://support.google.com/googleshopping/answer/11115998?hl=en
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "…which may boost their visibility and performance on the "Shopping" tab."
- **Establishes:** Google's closest statement linking shipping/returns to visibility.
- **Limitations:** Not extended to AI Mode or Gemini.
- **Related:** GOOG-022
- **Origin:** notes/gb-…#GB-33; notes/ga-…#GA-48 · **Checked:** pending

### GOOG-022 — Documented ranking factors exist only for Google Shopping: relevance, activity; "Top recommendations" = relevance, ratings, price, features
- **Claim:** Shopping tab listings rank by relevance to search terms plus personalization from recent activity. "Top recommendations" are selected on relevance, ratings, price and product features. Search shopping recommendations use popularity/trending. Shopping ads rank on bids plus relevance.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / ranking
- **Source:** "How Google Shopping works" — https://support.google.com/googleshopping/answer/9128904?hl=en ; "Understand how shopping results are generated" — https://support.google.com/googleshopping/answer/15456476?hl=en ; "How shopping recommendations work on Google Search" — https://support.google.com/googleshopping/answer/10269376?hl=en
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Results labeled as “Top recommendations” are selected based on relevance to your search, ratings, price, and product features. Google isn’t compensated for clicks into these results."
- **Establishes:** The only named factor list for AI-generated product recommendations at Google.
- **Limitations:** Not stated to apply to AI Mode, AI Overviews or the Gemini app (GEM-007).
- **Related:** GEM-007, CGPT-015
- **Origin:** notes/gb-…#GB-32; notes/ga-…#GA-20, #GA-21, #GA-22 · **Checked:** pending

### GOOG-023 — Store ratings need ~100 reviews in 24 months and "can help" free-listing performance
- **Claim:** Store ratings come from Google Customer Reviews, review partners and Google research. They generally need ~100 reviews in a rolling 24-month window, per country. Google says they can improve ads and free-listings performance.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / ranking signals
- **Source:** "Google store ratings: An overview for Merchants" — https://support.google.com/merchants/answer/190657?hl=en
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "As a result, store ratings can help merchants improve the performance of ads and free listings and drive more qualified shoppers to their landing pages."
- **Establishes:** A displayed trust signal on free listings.
- **Limitations:** "Performance" is framed via shopper trust, not ranking. No AI-surface mention.
- **Related:** GOOG-021
- **Origin:** notes/gb-…#GB-34 · **Checked:** pending

### GOOG-024 — Shopping ads in AI Overviews and AI Mode use the same Merchant Center feed; existing campaigns are auto-eligible
- **Claim:** Existing Search, Shopping and Performance Max campaigns automatically serve in AIO and AI Mode. Gemini writes "AI explainers" for some ads; advertisers cannot edit or opt out of them.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / ads
- **Source:** "About ads in AI-powered experiences in Google Search" — Google Ads Help — https://support.google.com/google-ads/answer/18826097?hl=en
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Eligible campaign types: Existing Search, Shopping, and Performance Max campaigns are automatically eligible to serve ads within AI Overviews and AI Mode."
- **Establishes:** One feed serves organic free listings and Shopping ads in AI surfaces.
- **Limitations:** No Gemini-app ads documented (GEM-010).
- **Related:** GEM-007, GEM-008
- **Origin:** notes/gb-…#GB-35 · **Checked:** pending

### GOOG-025 — Merchant-site agentic checkout works with select merchants that accept Google Pay; criteria unpublished
- **Claim:** Google Pay Help says agentic checkout works with "select merchants that accept Google Pay" and that "eligibility requirements apply". No merchant opt-in or opt-out is documented.
- **Classification:** VERIFIED FACT (statements); criteria not documented · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** Google / checkout
- **Source:** "About Agentic checkout with Google Pay" — Google Pay Help — https://support.google.com/googlepay/answer/16421147?hl=en
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "This feature is available at select merchants in supported countries. We’re working to expand the number of merchants where Agentic checkout can be used. Eligibility requirements apply and merchant availability can change."
- **Establishes:** Accepting Google Pay is a precondition.
- **Limitations:** Country scope conflicts within the page (US vs US+AU).
- **Related:** GEM-015
- **Origin:** notes/gb-…#GB-38; notes/ga-…#GA-33 · **Checked:** pending

## Crawlers, controls and structured data

### GOOG-026 — Googlebot is the crawl control for AI Overviews and AI Mode; there is no separate AI crawler
- **Claim:** Googlebot preferences affect all Google Search features. Google says robots.txt directives for Googlebot are the control for how sites are crawled for Search, because AI is integral to Search. Common crawlers always obey robots.txt when crawling automatically.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / crawling
- **Source:** "List of Google's common crawlers" — https://developers.google.com/crawling/docs/crawlers-fetchers/google-common-crawlers ; "AI features and your website" — https://developers.google.com/search/docs/appearance/ai-features
- **Published:** last updated 2026-10-30; 2025-12-10 · **Accessed:** 2026-10-30
- **Excerpt:** > "AI is built into Search and integral to how Search functions, which is why robots.txt directives for Googlebot is the control for site owners to manage access to how their sites are crawled for Search."
- **Establishes:** Blocking Googlebot removes a site from AIO/AI Mode citations and from Search. There is no AI-only robots.txt token for Search.
- **Limitations:** Since 2026-08-31 a Search Console control also exists (GOOG-028).
- **Related:** GOOG-027, GOOG-028
- **Origin:** notes/gd-…#GD-02 · **Checked:** pending

### GOOG-027 — Google-Extended controls Gemini Apps and Vertex AI training and grounding; it does not affect Search
- **Claim:** Google-Extended is a robots.txt control token. It governs use of crawled content for training Gemini models and for grounding in Gemini Apps and Vertex AI. It does not affect Search inclusion or ranking. Google plans to support the AIPREF training signal in early 2027.
- **Classification:** VERIFIED FACT · **Confidence:** High (wording conflict with Search Console help; see Limitations) · **Tier:** 1
- **Subject / topic:** Google / crawling
- **Source:** "List of Google's common crawlers" — Google Crawling docs — https://developers.google.com/crawling/docs/crawlers-fetchers/google-common-crawlers
- **Published:** last updated 2026-10-30 · **Accessed:** 2026-10-30
- **Excerpt:** > "Google-Extended does not impact a site's inclusion in Google Search nor is it used as a ranking signal in Google Search."
- **Establishes:** Blocking Google-Extended can remove a site from Gemini app grounding while leaving AIO and AI Mode untouched. One study found Gemini never cited sites that block it (RES-039).
- **Limitations:** Search Console help says Google-Extended limits training of models used in Search generative AI features; the two pages are not fully consistent. Whether Shopping Graph product data reaches the Gemini app regardless of Google-Extended is not stated.
- **Related:** GOOG-026, RES-039, MKT-022
- **Origin:** notes/gd-…#GD-01 · **Checked:** 2026-10-31

### GOOG-028 — Search Console "Search generative AI control" (worldwide since 2026-08-31) includes or excludes a site from AI Overviews, AI Mode and Discover AI
- **Claim:** A per-property setting can exclude a site's links and content from Search generative AI features, including grounding. Default is include. It is not a ranking signal for other Search features, does not affect AI training, and does not override Merchant Center or Google Ads participation. Google's AI optimization guide makes inclusion an eligibility requirement.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / controls
- **Source:** "Search generative AI control" — Search Console Help — https://support.google.com/webmasters/answer/16908024 ; "Optimizing your website for generative AI features on Google Search" — https://developers.google.com/search/docs/fundamentals/ai-optimization-guide
- **Published:** rollout note 2026-08-31; guide last updated 2026-07-10 · **Accessed:** 2026-10-30
- **Excerpt:** > "Note: As of August 31, 2026, we’ve rolled out this control to all websites worldwide."
- **Establishes:** Merchants must check this setting is on "include". It makes the 2025-12-10 "AI features" page outdated on controls.
- **Limitations:** Whether excluding a site also removes its Merchant Center listings from AI Mode is not stated beyond "doesn't override".
- **Related:** GOOG-011, GOOG-026
- **Origin:** notes/gd-…#GD-04 · **Checked:** 2026-10-31

### GOOG-029 — Google's AI optimization guide: structured data "isn't required"; Merchant Center feeds help products appear in AI responses; llms.txt not used
- **Claim:** Google says AI Overviews and AI Mode ground on the Search index via core ranking systems. AI responses can include product listings, and Merchant Center feeds can help visibility. Structured data is not required for generative AI search. Google Search does not use llms.txt or other "special" AI files.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / structured data, product data
- **Source:** "Optimizing your website for generative AI features on Google Search" — Google Search Central — https://developers.google.com/search/docs/fundamentals/ai-optimization-guide
- **Published:** last updated 2026-07-10 · **Accessed:** 2026-10-30
- **Excerpt:** > "Where appropriate, generative AI responses can include product listings, product information, and information about local businesses. Using products like Merchant Center (such as Merchant Center feeds) and Google Business Profiles can help your products and services to be visible in both AI responses and other Google Search results." / > "Structured data isn't required for generative AI search, and there's no special schema.org markup you need to add."
- **Establishes:** For Google AI shopping, the documented product-data path is Merchant Center, not page markup.
- **Limitations:** "Can help" is not a ranking statement.
- **Related:** GOOG-010, GOOG-033, RES-033, RES-044
- **Origin:** notes/gd-…#GD-05 · **Checked:** pending

### GOOG-030 — nosnippet and max-snippet limit AI Overviews/AI Mode inputs; in-page structured data is exempt from max-snippet
- **Claim:** `nosnippet` prevents content from being a direct input to AIO and AI Mode. `max-snippet` limits how much content may be used, except where the publisher supplies in-page structured data or has a license.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / controls, structured data
- **Source:** "Robots meta tag, data-nosnippet, and X-Robots-Tag specifications" — https://developers.google.com/search/docs/crawling-indexing/robots-meta-tag
- **Published:** last updated 2026-03-24 · **Accessed:** 2026-10-30
- **Excerpt:** > "For instance, if the publisher supplies content in the form of in-page structured data or has a license agreement with Google, this setting does not interrupt those more specific permitted uses."
- **Establishes:** The only Google sentence tying structured data to AI-surface input handling.
- **Limitations:** Not a ranking statement.
- **Related:** GOOG-029
- **Origin:** notes/gd-…#GD-06 · **Checked:** pending

### GOOG-031 — Storebot-Google is Google Shopping's crawler; JavaScript-generated Product markup makes Shopping crawls "less frequent and less reliable"
- **Claim:** Storebot-Google preferences affect all Google Shopping surfaces. Google warns that dynamically generated Product markup makes Shopping crawls less frequent and less reliable for price and availability.
- **Classification:** VERIFIED FACT. "Storebot-Google feeds AI Mode product units" is an UNVERIFIED HYPOTHESIS. · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / crawling
- **Source:** "List of Google's common crawlers" — https://developers.google.com/crawling/docs/crawlers-fetchers/google-common-crawlers ; "Merchant listing structured data" — https://developers.google.com/search/docs/appearance/structured-data/merchant-listing
- **Published:** 2026-10-30; 2026-09-08 · **Accessed:** 2026-10-30
- **Excerpt:** > "Be aware that dynamically-generated markup can make Shopping crawls less frequent and less reliable, which can be an issue for fast-changing content like product availability and price."
- **Establishes:** Server-rendered product data is the reliable form for Google's Shopping crawl.
- **Limitations:** AI Mode is not named.
- **Related:** GOOG-034
- **Origin:** notes/gd-…#GD-07 · **Checked:** 2026-10-31 (Storebot sentence)

### GOOG-032 — Google's documented agent fetcher is Google-Agent; user-triggered fetchers "generally ignore robots.txt"
- **Claim:** Google lists `Google-Agent` (from 2026-03-20) for agents acting on user request, identified by IP ranges and experimental Web Bot Auth. User-triggered fetchers generally ignore robots.txt. Google's list has no `GoogleAgent-Mariner` or `GoogleAgent-Shopping`.
- **Classification:** VERIFIED FACT (page contents) · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / crawling, agents
- **Source:** "List of Google user-triggered fetchers" — https://developers.google.com/crawling/docs/crawlers-fetchers/google-user-triggered-fetchers
- **Published:** last updated 2026-08-19 · **Accessed:** 2026-10-30
- **Excerpt:** > "Because the fetch was requested by a user, these fetchers generally ignore robots.txt rules."
- **Establishes:** robots.txt groups for undocumented GoogleAgent-* tokens (e.g. Amazon, MKT-022) may not bind Google's agent.
- **Limitations:** Which Google products use Google-Agent is not stated.
- **Related:** CGPT-008, MKT-022
- **Origin:** notes/gd-…#GD-09 · **Checked:** pending

### GOOG-033 — Merchant listing markup requires the page to be the point of sale; Google recommends markup plus a Merchant Center feed
- **Claim:** Merchant listings need an `Offer` because the merchant must be the seller; pages linking to other sellers are not eligible. Required: name, image, offers with price > 0 and currency. GTIN, shipping, returns and ratings are recommended. Google recommends both markup and a feed.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / structured data
- **Source:** "Merchant listing (Product, Offer) structured data" — https://developers.google.com/search/docs/appearance/structured-data/merchant-listing ; "Introduction to Product structured data" — https://developers.google.com/search/docs/appearance/structured-data/product
- **Published:** 2026-09-08; 2025-12-10 · **Accessed:** 2026-10-30
- **Excerpt:** > "Providing both structured data on web pages and a Merchant Center feed maximizes your eligibility to experiences and helps Google correctly understand and verify your data."
- **Establishes:** Markup governs rich-result eligibility and data verification; Google does not describe it as an AI-surface ranking input.
- **Limitations:** None of the Product markup pages mentions AI Mode, AI Overviews or Gemini.
- **Related:** GOOG-029, SHOP-022
- **Origin:** notes/gd-…#GD-11, #GD-12 · **Checked:** pending

### GOOG-034 — Google applies one robots.txt group per crawler; Storebot-Google falls back to `*`, not to a Googlebot group
- **Claim:** Google uses only the most specific matching group; specific and `*` groups are not combined. Storebot-Google follows `*` when it has no group of its own, even if a Googlebot group exists. `crawl-delay` is unsupported.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Google / crawling
- **Source:** "How Google interprets the robots.txt specification" — https://developers.google.com/crawling/docs/robots-txt/robots-txt-spec
- **Published:** last updated 2026-10-23 · **Accessed:** 2026-10-30
- **Excerpt:** > "Storebot-Google follows group 2, because there is no specific Storebot-Google group."
- **Establishes:** A custom robots.txt can give Search and Shopping crawlers different access without intending to.
- **Limitations:** Does not cover user-triggered fetchers.
- **Related:** GOOG-031, SHOP-017
- **Origin:** notes/gd-…#GD-34 · **Checked:** pending

### GOOG-035 — Google publishes no marketplace-versus-brand ranking rule
- **Claim:** No fetched Google document states how Search, Shopping, AI Mode or Gemini choose between a marketplace offer and a brand-site offer. The closest rules: merchant listings require the page owner to be the seller, and UCP keeps the retailer as merchant of record.
- **Classification:** VERIFIED FACT (absence across fetched documents) · **Confidence:** Medium (absence of evidence) · **Tier:** 1
- **Subject / topic:** Google / ranking
- **Source:** documents in GOOG-033, GOOG-003, GOOG-022
- **Published:** various · **Accessed:** 2026-10-30
- **Excerpt:** > "Product snippets accept an Offer or AggregateOffer but merchant listings require an Offer as the merchant has to be the seller of the product in order to be eligible for merchant listing experiences."
- **Establishes:** Google has no published equivalent of OpenAI's "maker or primary seller" factor (CGPT-015).
- **Limitations:** Merchant Center help on multi-seller accounts was not fetched.
- **Related:** CGPT-015, GOOG-022
- **Origin:** notes/gd-…#GD-15 · **Checked:** pending
