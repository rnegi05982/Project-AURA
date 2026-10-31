# GB — Google merchant-side integrations for AI shopping: Merchant Center, Shopping Graph, UCP, AP2, ranking statements

- Scope: Agent GB. Merchant Center eligibility for AI Mode / Gemini / AI Overviews; product data specification; Shopping Graph; documented ranking statements; Universal Commerce Protocol (UCP); Agent Payments Protocol (AP2); agentic checkout onboarding; ads in AI surfaces.
- Date: 2026-10-30
- Method: Primary sources fetched in this session with a local Python fetcher (raw HTML saved, text extracted locally) and `git clone` for repos. Excerpts copied from the extracted text. support.google.com pages carry no visible date unless the page body states one; devsite pages carry "Last updated … UTC". Press (Tier 3) used only to locate primary sources and labelled.
- Status: COMPLETE for this pass. 45 findings. All excerpts were machine-checked against the saved page text / cloned repo files (198 quoted strings, 0 misses).

## Findings

### GB-01 UCP-powered checkout on Google: select merchants, interest form, Merchant Center `native_commerce` flag
- Claim: Google's Merchant Center Help states that UCP-powered checkout puts a checkout button on eligible listings in AI Mode and Gemini. It is available to select merchants via an early access program: meet requirements, submit an interest form, complete technical implementation. Only listings with `native_commerce(checkout_eligibility)` show the "Buy" button. The merchant stays seller of record.
- Classification: VERIFIED FACT
- Source: About the Universal Commerce Protocol (UCP) and UCP-powered checkout feature on Google — Google Merchant Center Help — https://support.google.com/merchants/answer/16837055?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "This article only applies to products with eligibility in the United States, Canada, and Australia, and for participating merchants and partners. You may see this checkout experience soon on specific surfaces such as AI Mode in Search and Gemini."
- Excerpt: > "Note: The checkout feature enabled by UCP is available for select merchants at this time."
- Excerpt: > "By integrating with UCP, you can implement a checkout button on eligible product listings in AI Mode in Google Search and on Gemini."
- Excerpt: > "The protocol will be available in phases. To participate in the early access program, make sure that you meet the following requirements. Then, submit this interest form, and complete the required technical implementation. Only product listings using the native_commerce(checkout_eligibility) product attribute will display the “Buy” button for this checkout experience."
- Excerpt: > "With the existing checkout button, the transaction occurs on your site. With the new checkout experience enabled, the checkout happens directly on Google’s surfaces while keeping you the merchant of record."
- Excerpt: > "Currently, the feature uses standard Funding Primary Account Numbers (FPANs) that users have stored on their Google Wallet."
- Establishes: Checkout in AI Mode/Gemini is gated (selection + implementation + feed flag). Payment is Google Pay with Wallet-stored FPANs.
- Limitations: "Requirements" link to https://developers.google.com/merchant/ucp (GB-04). The country sentence covers "eligibility", not live availability; GB-09 shows the consumer feature is US-only. Interest form URL: https://support.google.com/merchants/contact/ucp_integration_interest (not fetched; form).

### GB-02 Google distinguishes "agentic checkout" (buys on merchant site) from UCP checkout (on Google surfaces); UCP scope includes "product discovery"
- Claim: Google's agentic checkout feature buys on the merchant's own website. UCP is the protocol for programmatic exchange between the AI agent and merchant backend, covering "product discovery and checkout".
- Classification: VERIFIED FACT
- Source: About the Universal Commerce Protocol (UCP) and UCP-powered checkout feature on Google — Google Merchant Center Help — https://support.google.com/merchants/answer/16837055?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Google’s agentic checkout feature buys things on the customer’s behalf directly on a merchant’s website at the customer’s direction. UCP is the open protocol which standardizes the programmatic exchange of information (via API, MCP or A2A) between the AI Agent and the Merchant’s backend to enable a broad set of commerce journeys including product discovery and checkout on Google AI Mode and Gemini."
- Establishes: Two separate Google mechanisms exist: (a) agentic checkout on the merchant site (announced 2025-11-13, GB-17) and (b) UCP native checkout on Google surfaces.
- Limitations: "product discovery" via UCP is stated as a goal; no fetched Google doc shows Google calling a merchant UCP catalog endpoint for discovery in AI Mode (see GB-12, knowledge gaps).

### GB-03 `native_commerce` attribute: optional group attribute; `checkout_eligibility` boolean
- Claim: `native_commerce` is optional for all products. Sub-attribute `checkout_eligibility` = true shows the "Buy" button; false/empty keeps a standard listing. Google strongly recommends a supplemental feed.
- Classification: VERIFIED FACT
- Source: Native commerce [native_commerce] — Google Merchant Center Help — https://support.google.com/merchants/answer/17251586?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "The native commerce [native_commerce] attribute enables you to opt your eligible product listings into the "Buy Now" flow (also known as native checkout) on Google surfaces. When this attribute is correctly configured, customers can discover products and complete a purchase directly within interfaces such as Gemini and AI Mode in Google Search without being redirected to an external website."
- Excerpt: > "Optional for all products."
- Excerpt: > "true: This value enables the "Buy" button on supported Google surfaces."
- Excerpt: > "false (or leave empty): This value disables the “Buy” button, keeping the item as a standard product listing."
- Establishes: The checkout opt-in is a per-item feed flag. Default is off.
- Limitations: The main Product data specification page (GB-20) does not list `native_commerce`. This help page's XML example shows `consumer_notice_type`/`consumer_notice_message`; the developer guide (GB-05) names the sub-attributes `notice_type`/`notice_message` (contradiction, see section 4).

### GB-04 UCP on Google requires a Merchant Center account in good standing with products approved for free listings
- Claim: The UCP developer guide requires a Merchant Center account in good standing and products approved for free listings, plus return policy (cost, window, link) and at least one customer-support contact.
- Classification: VERIFIED FACT
- Source: Merchant Center setup (Prepare your Merchant Center account) — Google for Developers, UCP Guide — https://developers.google.com/merchant/ucp/guides/overview/merchant-center
- Published/updated: Last updated 2026-10-29 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "You must have a Merchant Center account in good standing and approved products for free listings in your account."
- Excerpt: > "You must define your return policies in Merchant Center, as it is a Merchant of Record requirement and will be referenced on the checkout screen."
- Excerpt: > "You must include return cost, return speed (window), and a link to the full policy."
- Excerpt: > "You must set your customer support information in Merchant Center. This information is used to generate the "Contact Merchant" link on the order confirmation page."
- Establishes: Free-listings approval is the base eligibility for UCP checkout and cart on Google.
- Limitations: Requirement is for UCP features, not for product visibility in AI Mode.

### GB-05 UCP feed attributes: `checkout_eligibility` (opt-in, default FALSE), `cart_eligibility` (opt-out, default eligible), `consumer_notice`, `merchant_item_id`, `variant_option`
- Claim: Checkout is opt-in per item; cart transfer is opt-out. Free-listings-approved products are automatically eligible for cart transfer once the merchant's UCP profile declares `dev.ucp.shopping.cart`. The `native_commerce` group is fully overwritten on each upload. `variant_option` is "strongly recommended"; incomplete variant data "can suppress the checkout button".
- Classification: VERIFIED FACT
- Source: Merchant Center setup — Google for Developers, UCP Guide — https://developers.google.com/merchant/ucp/guides/overview/merchant-center
- Published/updated: Last updated 2026-10-29 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "This is provided using a product attribute native_commerce(checkout_eligibility) containing a single boolean. If set to FALSE or missing, the product won't be eligible for checkout (defaults to FALSE)."
- Excerpt: > "Cart transfer operates on an opt-out model, meaning eligible products are included by default unless explicitly excluded."
- Excerpt: > "Default participation: products approved for free listings in Google Merchant Center are automatically eligible for cart transfer once dev.ucp.shopping.cart is declared in your UCP profile."
- Excerpt: > "Important: The native_commerce attribute group is fully overwritten with each upload and does not support incremental updates. You must include all applicable flags in every update, or missing flags will be erased and set to blank."
- Excerpt: > "When merchant_item_id is defined, it will take precedence over id in Agentic requests."
- Excerpt: > "Google uses variant_option to construct the on-page item selector in UCP and to allow merchants to customize variant selection for users. Providing complete variant data also prevents automated transactability discrepancies that can suppress the checkout button."
- Excerpt: > "notice_type: Must be one of legal_disclaimer, safety_warning, or prop_65."
- Establishes: Exact feed contract for UCP on Google. "Transactability" checks can suppress the Buy button.
- Limitations: Suppression of the checkout button is not a ranking statement.

### GB-06 Product categories ineligible for UCP checkout
- Claim: Google lists categories ineligible for UCP checkout: subscriptions, installments, personalized goods, refurbished/used/final-sale, pre-orders, bundled services, special shipping (freight), gifting, in-store activation, age-restricted, prohibited content, services, rentals, virtual items, software dependencies.
- Classification: VERIFIED FACT
- Source: Merchant Center setup — Google for Developers, UCP Guide — https://developers.google.com/merchant/ucp/guides/overview/merchant-center
- Published/updated: Last updated 2026-10-29 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "The following categories of products are ineligible for checkout. Ensure these items have native_commerce(checkout_eligibility) empty or set to FALSE."
- Excerpt: > "Non-new or final sale items: refurbished goods, used items, and items marked as "Final Sale" (no returns)."
- Excerpt: > "Pre-order items: products with future release dates and deferred fulfillment."
- Excerpt: > "Special shipping: items requiring non-standard delivery fees (e.g., freight, premium delivery)."
- Establishes: Merchant-side exclusion list for the Buy button.
- Limitations: None for scope.

### GB-07 Google's UCP FAQ: native integration "does not influence how we rank your offers"
- Claim: Google states that opting into UCP native integration does not affect ranking of offers in product listings. UCP offers only gain the direct-purchase option.
- Classification: VERIFIED FACT
- Source: Frequently asked questions — Google for Developers, UCP Guide — https://developers.google.com/merchant/ucp/faq
- Published/updated: Last updated 2026-10-16 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Will Native integration affect my product ranking?"
- Excerpt: > "No. Opting for our Native integration does not influence how we rank your offers in product listings. The user experience for listings remains consistent; however, offers integrated with UCP will feature the direct purchase option."
- Establishes: The only first-party statement found on UCP vs. ranking. It says UCP native checkout is ranking-neutral.
- Limitations: Scope is "Native integration" and "product listings". It does not address cart transfer, identity linking, Business Agent, or whether the presence of the Buy button changes user click behaviour (which could indirectly feed other signals — UNVERIFIED HYPOTHESIS).

### GB-08 Google's UCP FAQ: surfaces at launch, traffic identification headers, AP2 relation, "powered by our Shopping Graph"
- Claim: UCP integrations power AI Mode in Google Search, Gemini web app and Gemini mobile app. Google identifies UCP requests with a `UCP-Agent` header and a User-Agent starting `Google/UCP`; health checks use `Google-UCP-Prober/1.0`. Google calls AP2 a "specialized payment layer within UCP". Google says UCP supports discovery and consideration "powered by our Shopping Graph".
- Classification: VERIFIED FACT
- Source: Frequently asked questions — Google for Developers, UCP Guide — https://developers.google.com/merchant/ucp/faq
- Published/updated: Last updated 2026-10-16 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "At launch, your UCP integration will power experiences on AI Mode in Google Search, as well as both the Gemini web application and the Gemini mobile app. We are planning support for other surfaces in the future."
- Excerpt: > "Merchant Center remains central to our ecosystem. You must ensure your product feeds, brand assets, return policies, and business contact information are complete and up-to-date there."
- Excerpt: > "Unlike protocols focused solely on payments, we support the broader shopping journey (including discovery and consideration) powered by our Shopping Graph."
- Excerpt: > "HTTP Headers: You can identify incoming UCP requests at the network level by verifying that the request meets two conditions: a header with the label UCP-Agent:Profile is present, and the User-Agent value begins with Google/UCP."
- Excerpt: > "These health check requests will include a specific User-Agent header: User-Agent: Google-UCP-Prober/1.0."
- Excerpt: > "AP2 is our standard for secure, agent-led payment transactions. We use UCP to orchestrate the broader purchase lifecycle, while AP2 can be used as a specialized payment layer within UCP. This is particularly useful for future scenarios involving autonomous AI agent transactions."
- Excerpt: > "UCP on Google's AI surfaces only supports PAN_ONLY for the allowed_auth_methods field."
- Establishes: Discovery on Google's side is attributed to the Shopping Graph (fed by Merchant Center), not to merchant UCP endpoints. AP2 is positioned as future/optional within UCP on Google.
- Limitations: Contradiction on Gemini app: developer landing page says "Gemini web (app coming soon)" (GB-10).

### GB-09 Consumer side: AI Mode "Buy" is US-only, signed-in 18+, English
- Claim: Google Search Help states AI Mode checkout works only for signed-in 18+ users in the US, in English, with eligible merchants and product restrictions. The merchant handles payment, shipping, returns and support. Account linking (loyalty) is "only available for select merchants in the US".
- Classification: VERIFIED FACT
- Source: Make purchases and manage orders directly from AI Mode in Google Search — Google Search Help — https://support.google.com/websearch/answer/16833721?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "You can now check out with eligible U.S. retailers right from certain product listings on Google in AI Mode in Search."
- Excerpt: > "This feature is only available for signed in 18+ users in the US, in English."
- Excerpt: > "When you select the desired option (such as color, size, format), eligible products will show the "Buy" button."
- Excerpt: > "Important: For all purchases, the merchant handles your payment, shipping, returns, and customer support."
- Establishes: Live consumer availability is US-only as of the access date.
- Limitations: Contradicts the Merchant Center page wording "eligibility in the United States, Canada, and Australia" (GB-01) only in appearance: MC page describes product eligibility scope; consumer page describes live rollout. Recorded in section 4.

### GB-10 Google UCP developer landing page: "Use your existing Merchant Center account shopping feeds"; Native vs Embedded checkout; Lodging and Food waitlists
- Claim: Google's UCP landing page says UCP reach comes from existing Merchant Center feeds, on AI Mode and "Gemini web (app coming soon)". Two integration paths: Native checkout (default) and Embedded checkout (iframe, approved merchants only). UCP is expanding to Lodging and Food.
- Classification: VERIFIED FACT
- Source: Getting started with Universal Commerce Protocol on Google — Google for Developers — https://developers.google.com/merchant/ucp
- Published/updated: not stated on page
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Use your existing Merchant Center account shopping feeds to capture high-intent customers during discovery. UCP unlocks access to users on surfaces like AI Mode in Google Search and Gemini web (app coming soon)."
- Excerpt: > "An additional optional path for specific, approved merchants. Best for those with highly bespoke branding or complex checkout flows that require an iframe-based solution."
- Excerpt: > "UCP is expanding to new industries, starting with Lodging and Food"
- Excerpt: > "UCP is fully compatible with protocols such as AP2, A2A, and MCP. It supports transport REST API and MCP binding."
- Establishes: Discovery input for UCP on Google = Merchant Center feeds.
- Limitations: "Gemini web (app coming soon)" conflicts with the FAQ (GB-08) and Gemini Help (GB-15). The landing page may be stale. Embedded checkout guide now resolves to an `/archive/` URL (https://developers.google.com/merchant/ucp/archive/checkout/embedded, Last updated 2026-08-19 UTC), suggesting Embedded checkout docs were archived — not confirmed.

### GB-11 Implementation steps; Google approval required before going live
- Claim: Google's Direct API path: prepare Merchant Center (shipping, returns, feed), join the waitlist, get Google approval, publish a UCP profile, secure endpoints, then implement Native checkout (with Google Pay handler and order lifecycle) or the Cart path. Identity Linking (OAuth 2.0) and promo codes are optional.
- Classification: VERIFIED FACT
- Source: Integration overview — Google for Developers, UCP Guide — https://developers.google.com/merchant/ucp/guides/overview
- Published/updated: Last updated 2026-10-19 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Because UCP is an evolving standard, not all features defined in the spec are available on Google's surfaces."
- Excerpt: > "Once you're ready, join the waitlist to get in contact with Google for UCP implementation. Your integration must be approved by Google before you can go live on AI Mode in Google Search and Gemini."
- Excerpt: > "You can choose to integrate a checkout path (to support purchases directly on Google) or a cart path (to receive shopping carts and hand off to your website)."
- Establishes: Go-live is gated by Google approval. Google implements a subset of the UCP spec.
- Limitations: None for scope.

### GB-12 UCP integration hub in Merchant Center: US rollout, AU/CA next year; sandbox; capability selection
- Claim: The Merchant Center UCP integration hub is rolling out gradually in the US, with Australia and Canada "next year" / "early next year". Selected merchants get a sandbox validating UCP profile, cart transfer and native checkout APIs. Merchants select capabilities: cart transfer, native checkout, identity linking. Third-party platform merchants are told to contact their platform.
- Classification: VERIFIED FACT
- Source: How to onboard to the UCP integration hub in Merchant Center — Google Merchant Center Help — https://support.google.com/merchants/answer/16992327?hl=en ; About Universal Commerce Protocol (UCP) integration hub in Merchant Center — Google for Developers — https://developers.google.com/merchant/ucp/guides/merchant-center/overview
- Published/updated: Help page not stated; developer page Last updated 2026-10-19 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (Help): > "The Merchant Center integration is gradually rolling out in the U.S., with Australia and Canada to follow next year."
- Excerpt (Help): > "As soon as you’re selected to participate, we’ll notify you, and then you’ll have access to the onboarding experience in Merchant Center. There, you’ll also be able to access a sandbox environment to validate your integration, including your UCP profile, cart transfer to a merchant site, and native checkout APIs."
- Excerpt (Help): > "With the UCP integration hub, merchants can select UCP capabilities such as cart transfer to merchant site, native checkout on Google, and identity linking."
- Excerpt (Help): > "If you work with a third-party service provider or platform, please connect directly with them to learn more about their plans for Universal Commerce Protocol integration."
- Excerpt (Dev): > "Important: the UCP integration hub is gradually rolling out in the United States, with Australia and Canada to follow early next year."
- Establishes: Onboarding sequence: technical implementation → interest form → selection → hub access.
- Limitations: Shopify merchants: Google defers to the platform. Shopify's mechanism is covered in C-16/C-17 (ChatGPT notes), not re-fetched here.

### GB-13 Native checkout: Google renders the UI; agent excluded from payment step; SLOs
- Claim: In native checkout the agent hands control to a Google UI; the user enters payment and fulfillment there "to ensure determinism". Google expects ≥95% availability and p95 latency ≤4 s (create), ≤5 s (update), ≤10 s (complete). Multi-item checkout is supported.
- Classification: VERIFIED FACT
- Source: Native checkout overview — Google for Developers, UCP Guide — https://developers.google.com/merchant/ucp/guides/overview/native-checkout
- Published/updated: Last updated 2026-10-16 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Manual checkout: The user now interacts only with the Google UI to fill in sensitive fulfillment and payment details and submit the order. The Agent is not involved in this part, ensuring determinism."
- Excerpt: > "Google now supports multiple distinct line items in a single checkout session."
- Excerpt: > "Businesses integrating with Google are expected to meet these targets for API performance and availability."
- Establishes: Google's checkout is human-confirmed in a Google UI, not autonomous.
- Limitations: API versions referenced: 2026-04-08 and 2026-01-23.

### GB-14 UCP Cart API on Google (`dev.ucp.shopping.cart`): one-way cart transfer to merchant site, UCP 2026-04-08+
- Claim: Google's Cart API transfers a user's Universal Cart to the merchant website through `CreateCart` only. It requires UCP version 2026-04-08 and a profile at `/.well-known/ucp`. Native checkout is not required for cart transfer.
- Classification: VERIFIED FACT
- Source: Cart overview — Google for Developers, UCP Guide — https://developers.google.com/merchant/ucp/guides/overview/cart-overview
- Published/updated: Last updated 2026-10-16 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "The UCP Cart API (Capability Name: dev.ucp.shopping.cart ) enables the transfer of a user's shopping cart from Google surfaces, such as AI Mode in Google Search and Gemini, directly to your website."
- Excerpt: > "This initial release is limited to cart creation and transfer using the CreateCart method. Features like updating, deleting, or synchronizing cart contents between Google and your system are not supported."
- Excerpt: > "Publish your UCP profile at /.well-known/ucp and include the dev.ucp.shopping.cart capability"
- Establishes: Lowest-effort UCP path for merchants: cart handoff, no payments integration.
- Limitations: None for scope.

### GB-15 Gemini shopping uses the Shopping Graph; available in 21 countries; checkout only with eligible merchants
- Claim: Gemini Apps Help says Gemini uses Shopping Graph information to find and compare products. Shopping in Gemini is available in 21 listed countries/regions. Buying is from "select merchants" via a "Buy" button in the Gemini web app, paid with Google Pay.
- Classification: VERIFIED FACT
- Source: Get help with your shopping in Gemini Apps — Gemini Apps Help — https://support.google.com/gemini/answer/16730149?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "You can use Gemini Apps as your personal AI-powered shopping assistant. Gemini uses information from Google’s Shopping Graph to help you find products, compare options, and make purchase decisions."
- Excerpt: > "Shopping with Gemini Apps is currently available in the following countries & regions:"
- Excerpt: > "There’s a “Buy” button on product listings that are eligible for purchase within the Gemini web app."
- Excerpt: > "Personalized shopping experiences: Gemini Apps can provide relevant and personalized product recommendations using Personal Intelligence."
- Establishes: Countries listed: Argentina, Australia, Brazil, Canada, Chile, Colombia, Hong Kong, India, Japan, Indonesia, Malaysia, Mexico, New Zealand, Philippines, Saudi Arabia, Singapore, Taiwan, Thailand, UAE, US, Vietnam. Gemini product data source = Shopping Graph.
- Limitations: Purchase section is titled for the Gemini web app; no country restriction is stated for the Buy button on this page (other pages say US).

### GB-16 Universal Cart: US-only; checkout on Google for participating merchants, else cart populated on merchant site
- Claim: Universal cart is US-only. Products can be added from Search & Shopping, AI Mode and Gemini Apps. Checkout is via Google Pay for participating merchants or by populating the merchant-site cart.
- Classification: VERIFIED FACT
- Source: Manage your universal cart — Gemini Apps Help — https://support.google.com/gemini/answer/17085590?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Important: This feature is currently available only in the United States."
- Excerpt: > "Check out on the merchant site: For other merchants, Google helps you populate your cart on the merchant's website so you can complete the purchase there."
- Excerpt: > "By adding items to your universal cart, you may receive relevant contextual emails and push notifications, such as price drops or availability updates."
- Establishes: Cart handoff is the non-native-checkout path.
- Limitations: Does not say whether non-UCP merchants receive populated carts (mechanism unstated on this page; GB-14 implies UCP Cart API).

### GB-17 Agentic checkout (Nov 2025) and Shopping Graph scale claim: 50B+ listings, 2B updated hourly
- Claim: On 2025-11-13 Google launched agentic checkout (Google buys on the merchant's site after price tracking, with user confirmation), and said AI Mode is powered by the Shopping Graph with "more than 50 billion product listings, 2 billion of which are updated every hour". Gemini app shopping launched for US users that day.
- Classification: VERIFIED FACT (Google's claim)
- Source: Google Shopping launches agentic checkout and more AI shopping tools — The Keyword (Google blog) — https://blog.google/products-and-platforms/products/shopping/agentic-checkout-holiday-ai-shopping/
- Published/updated: 2025-11-13
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "And because AI Mode is powered by the Shopping Graph (which includes more than 50 billion product listings, 2 billion of which are updated every hour) you can trust you’re seeing fresh information and unmatched selection."
- Excerpt: > "If the merchant is eligible, we'll now give you the option to have Google buy it for you on the merchant's site using Google Pay. We’ll always ask for your permission first, and only buy after you’ve confirmed the purchase and shipping details."
- Excerpt: > "Agentic checkout is starting to roll out now on Search, including in AI Mode, from eligible merchants in the U.S. like Wayfair, Chewy, Quince and select Shopify merchants, with many more coming soon."
- Establishes: Shopping Graph refresh claim (as of Nov 2025). Agentic checkout predates UCP.
- Limitations: Scale numbers are marketing claims; not independently verifiable. Merchant eligibility criteria for agentic checkout are not stated here.

### GB-18 UCP launch (2026-01-11): co-developers, endorsers, Business Agent, new Merchant Center attributes, Direct Offers pilot
- Claim: On 2026-01-11 Google launched UCP, co-developed with Shopify, Etsy, Wayfair, Target and Walmart and endorsed by 20+ others. The same post announced Business Agent, "dozens of new data attributes" for conversational commerce, and the Direct Offers Google Ads pilot in AI Mode labelled "Sponsored deal".
- Classification: VERIFIED FACT
- Source: New tech and tools for retailers to succeed in an agentic shopping era — The Keyword (Google blog) — https://blog.google/products/ads-commerce/agentic-commerce-ai-tools-protocol-retailers-platforms/
- Published/updated: 2026-01-11 (datePublished in page metadata)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "UCP was co-developed with industry leaders including Shopify, Etsy, Wayfair, Target and Walmart, and endorsed by more than 20 others across the ecosystem like Adyen, American Express, Best Buy, Flipkart, Macy’s Inc., Mastercard, Stripe, The Home Depot, Visa and Zalando."
- Excerpt: > "To start, UCP will soon power a new checkout feature on eligible Google product listings in AI Mode in Search and the Gemini app, allowing shoppers to check out from eligible U.S. retailers right as they’re researching on Google."
- Excerpt: > "That’s why we’re announcing dozens of new data attributes in Merchant Center designed for easy discovery in the conversational commerce era, on surfaces like AI Mode, Gemini and Business Agent."
- Excerpt: > "These new attributes complement retailers’ existing data feeds and go beyond traditional keywords to include things like answers to common product questions, compatible accessories or substitutes."
- Excerpt: > "This new Google Ads pilot allows advertisers to present exclusive offers for shoppers who are ready to buy — like a special 20% off discount — directly in AI Mode."
- Excerpt: > "With Direct Offers, retailers set up relevant offers they want to feature in their campaign settings and Google will use AI to determine when an offer is relevant to display."
- Establishes: Confirms the lead "UCP announced 2026-01-11 with Shopify, Etsy, Wayfair, Target, Walmart". Confirms Business Agent and Direct Offers exist.
- Limitations: "dozens of new data attributes" (Jan) vs six conversational attributes listed in Help (GB-21): the Jan announcement scope is larger than what Help lists today (see section 4). Image caption text "User flow of Direct Offers pilot in AI Mode, labeled “Sponsored deal.”" is a caption, not body text.

### GB-19 Google Marketing Live (2026-05-20): Universal Cart, UCP to ads (Direct Offers, YouTube Shopping ads), CA/AU/UK rollout plan, AI performance insights, conversational attributes global
- Claim: Google announced Universal Cart, UCP-powered checkout in Direct Offers and Shopping ads on YouTube (Demand Gen), BNPL via Affirm/Klarna in Google Pay, UCP checkout rollout to Canada and Australia "in the coming months" and later the UK, hotels and food delivery, AI performance insights, and conversational attributes available to retailers globally.
- Classification: VERIFIED FACT
- Source: How we’re helping retailers thrive with new Universal Commerce Protocol features and AI tools on Google — The Keyword (Google blog) — https://blog.google/products-and-platforms/products/shopping/shopping-updates-google-marketing-live/
- Published/updated: 2026-05-20
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Soon, when brands who have integrated UCP show exclusive promotions with Direct Offers or run Shopping ads on YouTube with product feeds on Demand Gen campaigns, people can easily buy on the spot."
- Excerpt: > "UCP-powered checkout will roll out across Canada and Australia in the coming months, and later to the U.K."
- Excerpt: > "Now, retailers globally can use conversational attributes to update their product descriptions to reflect the more conversational way people search."
- Excerpt: > "Regardless of how a shopper chooses to buy, the retailer always remains the merchant of record."
- Establishes: 2026 timeline of UCP expansion on Google.
- Limitations: As of 2026-10-30, Help pages still say AU/CA hub "next year" (GB-12) and consumer checkout US-only (GB-09): the May "coming months" CA/AU rollout had not reached the consumer Help page.

### GB-20 Product data specification: Google states the data is used for query matching and as input to AI-powered formats; no page date
- Claim: The Product data specification says Google uses the data "to match your products to the right queries" and as "a foundational input" for AI-powered ad formats. Missing or incorrect data can cause disapprovals, "limited eligibility" or display issues. "Optional" attributes are defined as helping "boost your product's performance".
- Classification: VERIFIED FACT
- Source: Product data specification — Google Merchant Center Help — https://support.google.com/merchants/answer/7052112?hl=en
- Published/updated: not stated on page. Latest dated spec change: "Merchant Center product data specification update 2026", April 14, 2026 (GB-25); warranty attribute announcement October 2026 (changelog).
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Use this guide to format your product information for Merchant Center. Google uses this data to match your products to the right queries, and as a foundational input to help optimize and enhance the content of the ads being served in our AI powered formats and experiences."
- Excerpt: > "Incorrect, inaccurate, or missing product information can cause disapprovals, limited eligibility, incorrect displays for your products, or other Issues in Merchant Center."
- Excerpt: > "Required: Submit this attribute. If you don't, your product won't be able to serve in ads and free listings."
- Excerpt: > "Optional: You can submit this attribute if you want to help boost your product's performance."
- Establishes: Google's own statement of how data quality matters: query matching, eligibility, display. Requirement-level definitions (Required / It depends / Optional; the page uses no "Recommended" level in its definitions, though some entries say "strongly recommended").
- Limitations: "boost your product's performance" is not a ranking-factor statement. The page names no AI surface (AI Mode, Gemini) and does not list `native_commerce`, `consumer_notice`, `merchant_item_id` or `video_link` (see section 4). The spec page has no last-updated date.

### GB-21 Conversational attributes: six optional attributes "designed to complement" the spec, for AI Mode "and more"
- Claim: Merchant Center Help lists six conversational attributes: `question_and_answer`, `document_link`, `related_product`, `item_group_title`, `variant_option`, `popularity_rank`. They are optional, do not affect approval, and Google recommends a supplemental data source.
- Classification: VERIFIED FACT
- Source: How to use conversational attributes — Google Merchant Center Help — https://support.google.com/merchants/answer/17085370?hl=en
- Published/updated: not stated. Related: Accelerate with Google "Conversational Attributes" page datePublished 2026-05-13, dateModified 2026-09-16 (https://business.google.com/us/accelerate/announcements/conversational-attributes/).
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Conversational attributes help AI systems and conversational agents better understand your products’ specific nuances. They are completely optional, and designed to complement your primary Merchant Center product data specification. By submitting these attributes, you can help customers discover information about your products across AI-driven surfaces, like AI Mode in Search and more while also enhancing traditional search experiences."
- Excerpt: > "Including them won't impact the approval status of your existing products."
- Excerpt: > "Note: If you already submit specific details in the description [description], product highlight [product_highlight], or product detail [product_detail] attributes - you don't need to duplicate that data again in the conversational attributes."
- Establishes: Confirms the lead "Merchant Center conversational attributes". Announced Jan 2026 as "dozens of new data attributes" (GB-18); GML 2026-05-20 said retailers "globally" can use them (GB-19).
- Limitations: "help customers discover information" is not a ranking statement. Google does not state whether AI Mode ranking uses any of these fields.

### GB-22 `question_and_answer`: "primarily intended for use in conversational experiences such as AI mode"; Google extracts FAQs from `document_link` PDFs
- Claim: Q&A is optional, all countries, up to 30 pairs, 1,000 chars per question/answer, 10,000 total. No prices/dates; no keyword lists. If `document_link` PDFs contain the same info, Google extracts FAQ information from those documents instead.
- Classification: VERIFIED FACT
- Source: Question and answer [question_and_answer] — Google Merchant Center Help — https://support.google.com/merchants/answer/17085211?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Note: This attribute is primarily intended for use in conversational experiences such as AI mode in Google Search."
- Excerpt: > "The question and answer [question_and_answer] attribute can be used in all countries."
- Excerpt: > "Only add information about the product. Don’t add time-related information such as prices and dates."
- Excerpt: > "Don't submit if you're also submitting the document link [document_link] attribute and the same information can be found in these documents. We'll extract FAQ information from those documents instead."
- Establishes: Google reads merchant-supplied PDFs (`document_link`) for FAQ extraction.
- Limitations: Use in AI Mode answers is stated as intent ("primarily intended"), not as a ranking input.

### GB-23 `popularity_rank`: merchant-assessed 0–100 sales popularity; "primarily intended" for AI Mode
- Claim: `popularity_rank` is optional, 0–100, merchant-assessed, based on recent sales. The help page says it is "primarily intended" for conversational experiences such as AI Mode. The spec says it does not reflect user ratings.
- Classification: VERIFIED FACT
- Source: Popularity rank [popularity_rank] — Google Merchant Center Help — https://support.google.com/merchants/answer/17085297?hl=en ; Product data specification — https://support.google.com/merchants/answer/7052112?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (attribute page): > "Note: This attribute is primarily intended for use in conversational experiences such as AI Mode in Google Search."
- Excerpt (attribute page): > "Use this attribute to communicate how well your products are selling, like your latest best sellers, and help consumers make a more informed buying decision."
- Excerpt (attribute page): > "Categorize your products. Determine the value of the popularity_rank [popularity_rank] attribute based on recent sales of the product compared to products in the same general category."
- Excerpt (spec): > "Use to rank the popularity of this product in your entire inventory as a percentage. The higher the number the more popular your product is."
- Excerpt (spec): > "Note that this reflects the popularity of this product on your platform as assessed by you. It does not reflect user ratings of the product."
- Establishes: A merchant-declared popularity field exists for AI Mode.
- Limitations: The field existing does not prove Google ranks on it. Scope conflict: "entire inventory" (spec) vs "same general category" (attribute page); decimals "supported" (spec) vs "at most 1 decimal point" (attribute page). See section 4.

### GB-24 `related_product` and `variant_option`: relationship types and variant dimensions
- Claim: `related_product` (max 30) supports relationship types `part_of_set`, `required_part`, `often_bought_with`, `substitute`, `different_brand`, `accessory`, with identifier type `gtin` or `id`. `variant_option` (max 30, 5,000 chars) gives name:value variant dimensions with `item_group_id` and `item_group_title`.
- Classification: VERIFIED FACT
- Source: Product data specification — Google Merchant Center Help — https://support.google.com/merchants/answer/7052112?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Required part [required_part] Part that is necessary for the product to function, for example a battery for a battery-operated lamp."
- Excerpt: > "substitute [substitute] Product that this product can be substituted for, for example a cheaper alternative."
- Excerpt: > "Specify variant option [variant_option] in combination with item group ID [item_group_id] and Item group title [item_group_title]to define all variant-identifying properties of the product."
- Establishes: Compatibility/accessory/substitute data now has a structured field (matches the Jan 2026 blog's "compatible accessories or substitutes", GB-18). `variant_option` is shared with UCP (GB-05): Google uses it for the UCP item selector.
- Limitations: No statement that related products drive recommendations in AI Mode.

### GB-25 2026 spec changes: `video_link`, product-level shipping attributes, loyalty shipping labels, 500×500 image minimum from 2027-01-31; videos appear in AI Mode
- Claim: The 2026 annual spec update (April 14, 2026) added `handling_cutoff_time`, `minimum_order_value`, loyalty sub-attributes on `shipping`, and an optional `video_link` (serving from June 30, 2026). Image minimum rises to 500×500 with enforcement January 31, 2027. Merchant Center Help says product videos appear in AI Mode, free Search listings and Google Ads.
- Classification: VERIFIED FACT
- Source: Merchant Center product data specification update 2026 — Google Merchant Center Help — https://support.google.com/merchants/answer/16989427?hl=en ; About using product videos across Google Shopping — Google Merchant Center Help — https://support.google.com/merchants/answer/18545837?hl=en
- Published/updated: 2026-04-14 (announcement); video page not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "We’re announcing a new, optional video link [video_link] attribute which will allow merchants to submit links to product videos."
- Excerpt: > "Starting June 30, 2026 videos submitted via the video link [video_link] attribute will become eligible to serve."
- Excerpt: > "we’re increasing the minimum resolution for images submitted in the image link [image_link] and additional image link [additional_image_link] attributes to 500x500 pixels across all product categories and marketing methods."
- Excerpt (video page): > "These videos appear across various Google surfaces, including AI Mode, free Search listings, and Google Ads campaigns."
- Excerpt (video page): > "By combining visual proof (supplied by your product videos) with text context (supplied by conversational attributes like question_and_answer or document_link), you allow AI Mode in Search to deliver accurate, multi-layered responses to complex customer inquiries."
- Establishes: Video is a documented AI Mode display input. Image-size enforcement date.
- Limitations: `video_link` is absent from the Product data specification page as fetched (present in Merchant API `videoLinks[]`, Last updated 2026-10-27). No ranking statement.

### GB-26 AI performance insights: Merchant Center report for AI Mode / AI Overviews visibility; organic only; Google's advice is product-data completeness
- Claim: Merchant Center has an "AI performance" report (Analytics > Products) for English-language queries in AU, CA, IN, NZ, US. It reports share of voice vs. Merchant-Center-defined competitors, shopping stages, top terms and "popular attributes" missing from feeds. Data covers organic AI traffic (free listings) only.
- Classification: VERIFIED FACT
- Source: About AI performance insights — Google Merchant Center Help — https://support.google.com/merchants/answer/17200695?hl=en ; Insights for AI-powered shopping experiences coming soon — Google Merchant Center Help — https://support.google.com/merchants/answer/17117204?hl=en
- Published/updated: announcement May 27, 2026; report page not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "The AI performance insights report provides a transparent view of how your brand is discovered across Google’s generative AI ecosystem, specifically revealing your performance for conversational queries with shopping intent on AI Mode and AI Overviews."
- Excerpt: > "AI performance insights are currently available for English-language queries for Merchant Center accounts in Australia, Canada, India, New Zealand, and the United States."
- Excerpt: > "“Traffic”: Current data is strictly limited to organic AI traffic (for example, free listings). Paid Ads traffic isn't included in this report."
- Excerpt: > "Provide high quality data and keep your Merchant Center account updated: We recommend to follow the same free listings product requirements, recommendations and provide high quality product data attributes."
- Excerpt: > "Implement recommendations from AI insights report: Add the relevant search terms into your product titles and descriptions, and populate any missing attributes."
- Excerpt (announcement): > "These insights are designed to help you understand how your products are being discovered on AI Mode, AI Overviews in Search, or the Gemini app."
- Establishes: Free listings are the organic path measured on AI Mode/AI Overviews. Google ties AI-surface visibility advice to attribute completeness and title/description terms.
- Limitations: The report page names AI Mode and AI Overviews; the May announcement also named the Gemini app. Google's recommendation to add terms is advice, not a disclosed ranking mechanism. Recorded as Google's statement, not as AURA advice.

### GB-27 Free listings: on by default; may appear on Gemini; crawled products can show without Merchant Center
- Claim: Free listings are on by default for new accounts and may show on Search, Maps, Gemini, YouTube, the Shopping tab, Images and Lens. Products crawled from a store "can show up on Google" even without schema.org markup or Merchant Center. Free-listings status grants permission but does not guarantee display.
- Classification: VERIFIED FACT
- Source: Free listings for products — Google Merchant Center Help — https://support.google.com/merchants/answer/13889434?hl=en (requested as answer/9199328, redirected)
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "With a free listing, the products you sell can appear at no cost on Google Search, Google Maps, Gemini, YouTube, the Shopping tab, Google Images, and Google Lens."
- Excerpt: > "When you create a new Merchant Center account, you're opted in to free listings by default."
- Excerpt: > "Content from your online store: Products and their details that have been crawled on your online store can show up on Google. This can occur even if the information hasn’t been marked up using schema.org or added in Merchant Center."
- Excerpt: > "Note: The status on the Free listings page controls permission to show products for free across Google, but doesn't guarantee that your products will be shown to customers. We rely on the data that you provide to us to match your products with what customers might be searching for."
- Establishes: Answer to Q1 (partial): Merchant Center is the documented path for free listings on Gemini; crawled products may appear on Google without Merchant Center.
- Limitations: This page lists Gemini but not AI Mode or AI Overviews by name. No page states whether crawl-only products can appear as AI Mode product cards (knowledge gap).

### GB-28 Search Central: Merchant Center "isn't mandatory" for Search results, mandatory for the Shopping tab; AI features need no extra technical requirements
- Claim: Google Search Central says uploading to Merchant Center is not mandatory to appear in Search results but is mandatory for the Shopping tab. For AI Overviews/AI Mode supporting links there are no additional technical requirements; keeping Merchant Center up to date is listed among SEO best practices.
- Classification: VERIFIED FACT
- Source: Share your product data with Google — Google Search Central — https://developers.google.com/search/docs/specialty/ecommerce/share-your-product-data-with-google ; AI features and your website — Google Search Central — https://developers.google.com/search/docs/appearance/ai-features
- Published/updated: Last updated 2025-12-10 UTC (both)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "While uploading product data to Google Merchant Center isn't mandatory to appear in Google search results, it can enhance Google's understanding of your products. Participation in Google Merchant Center is mandatory for some Google surfaces, such as listings in the Google Shopping tab."
- Excerpt: > "Web crawling is not guaranteed to find all products on your site."
- Excerpt: > "To be eligible to be shown as a supporting link in AI Overviews or AI Mode, a page must be indexed and eligible to be shown in Google Search with a snippet, fulfilling the Search technical requirements. There are no additional technical requirements."
- Excerpt: > "Checking that your Merchant Center and Business Profile information is up-to-date"
- Establishes: Supporting-link eligibility (web pages) and product-listing eligibility (Merchant Center/free listings) are documented separately.
- Limitations: Neither page addresses AI Mode product cards or Gemini product listings. The "share product data" page still recommends the Content API, which Google's UCP guide labels "deprecated" (section 4).

### GB-29 No AI-surface-specific opt-out for listings or ads
- Claim: The `excluded_destination`/`included_destination` values contain no AI Mode, AI Overviews or Gemini value. Google Ads says advertisers cannot target or opt out of AI Overviews/AI Mode separately from Search.
- Classification: VERIFIED FACT (spec value list; Ads FAQ). "No AI-only opt-out exists for free listings" = EVIDENCE-BASED INFERENCE (absence in fetched pages).
- Source: Product data specification — https://support.google.com/merchants/answer/7052112?hl=en ; About ads in AI-powered experiences in Google Search — Google Ads Help — https://support.google.com/google-ads/answer/18826097?hl=en (requested as answer/16297775, redirected)
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (spec, supported values): > "Shopping_ads" … "Display_ads" … "Local_inventory_ads" … "Free_listings" … "Free_local_listings" … "Cloud_retail" … "Local_cloud_retail" … "Youtube_affiliate" … "Youtube_merchandise"
- Excerpt (Ads): > "No. AI Overviews and AI Mode are core experiences within Google Search. Just like other features on the Google Search results page, you can't target ads exclusively to AI Overviews or AI Mode, or opt out of showing ads in them separately from Search."
- Establishes: Merchant controls are surface-generic (free listings on/off, destination exclusion). Opt-in/opt-out exists only for checkout (`native_commerce`) and cart transfer (`cart_eligibility`).
- Limitations: Search Central lists `nosnippet`/`noindex` and robots.txt as controls for web content in AI features (GB-28 source); these act on pages, not Merchant Center listings.

### GB-30 Shopping Graph: definition and sources (Merchant Center, Manufacturer Center, web crawl, reviews, YouTube)
- Claim: Google describes the Shopping Graph as an ML-powered, real-time data set of products and sellers. Listings update via Merchant Center or "what retailers and brands post across the web". It pulls images, descriptions, reviews and YouTube videos. Brands and retailers also send data via Manufacturer Center. Shopping Graph info powers Search, Ads, YouTube and generative AI features.
- Classification: VERIFIED FACT
- Source: 4 ways Google’s Shopping Graph helps you find what you want — The Keyword — https://blog.google/products-and-platforms/products/shopping/shopping-graph-explained/ ; Sources of shopping info — Google Shopping Help — https://support.google.com/googleshopping/answer/14336735?hl=en
- Published/updated: blog 2023-02-07; help page not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (blog): > "The Shopping Graph is our ML-powered, real-time data set of the world’s products and sellers."
- Excerpt (blog): > "Listings show products and their sellers, and they’re updated constantly — either through information retailers share directly via Google Merchant Center or from what retailers and brands post across the web."
- Excerpt (blog): > "To narrow down your options, the Shopping Graph scans billions of listings while also pulling relevant data from the web — like images, descriptions, reviews and YouTube videos."
- Excerpt (help): > "Brands, retailers, and other content providers send their product info directly to Google through tools like Merchant Center and Manufacturer Center."
- Excerpt (help): > "Power AI-driven experiences like review summaries, buying guidance, or product recommendations."
- Excerpt (help): > "Ranked lists and info you find in AI Overviews and more aren’t sponsored, and you only find results related to what you search."
- Establishes: Shopping Graph has two documented ingestion paths (feeds, web) plus review and video sources. Gemini (GB-15) and AI Mode (GB-17) are documented consumers.
- Limitations: The explainer is from 2023 (35B listings figure superseded, GB-31). No document gives precedence rules between feed and crawled data.

### GB-31 Shopping Graph scale and refresh claims over time
- Claim: Google's figures: 35B+ listings (Feb 2023); 50B+ listings with 2B+ refreshed hourly (May 2025, Nov 2025, Jan 2026). Sundar Pichai (2026-01-11) said the Shopping Graph has provided real-time product info "since 2021" and was brought to the Gemini app "last year".
- Classification: VERIFIED FACT (Google's claims)
- Source: Read Sundar Pichai’s remarks at the 2026 National Retail Federation — The Keyword — https://blog.google/company-news/inside-google/message-ceo/nrf-2026-remarks/ ; Shop with AI Mode, use AI to buy and try clothes on yourself virtually — The Keyword — https://blog.google/products-and-platforms/products/shopping/google-shopping-ai-mode-virtual-try-on-update/
- Published/updated: 2026-01-11; 2025-05-20
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (NRF): > "Since 2021, our Shopping Graph provides information on products in real time. It has over 50 billion product listings, including inventory, prices and reviews. More than 2 billion of those listings are refreshed every single hour."
- Excerpt (NRF): > "And last year, we brought the Shopping Graph to the Gemini app, so it’s a lot more helpful for people asking shopping-related questions, too."
- Excerpt (I/O 2025): > "Our new AI Mode shopping experience brings together Gemini capabilities with our Shopping Graph to help you browse for inspiration, think through considerations and narrow down products."
- Excerpt (I/O 2025): > "AI Mode will start a query fan-out, which means it runs several simultaneous searches to figure out what makes a bag good for rainy weather and long journeys, and then use those criteria to suggest waterproof options with easy access to pockets."
- Establishes: AI Mode shopping = Gemini + Shopping Graph + query fan-out (Google's description).
- Limitations: Refresh rate is aggregate; no per-merchant refresh SLA is documented. "Refreshed" is undefined (crawl vs feed).

### GB-32 Documented ranking statements: Shopping tab, Shopping ads, "Top recommendations"
- Claim: Google's consumer pages state: Shopping tab listings rank by relevance to search terms, plus personalization from recent activity; parameter weights are set by algorithms. Shopping ads rank by bids plus relevance. "Top recommendations" are selected on relevance, ratings, price and product features. Sponsored/Ad labels mark paid influence.
- Classification: VERIFIED FACT
- Source: How Google Shopping works — Google Shopping Help — https://support.google.com/googleshopping/answer/9128904?hl=en ; Recommendations & personalization — Google Shopping Help — https://support.google.com/googleshopping/answer/9116422?hl=en ; Understand how shopping results are generated — Google Shopping Help — https://support.google.com/googleshopping/answer/15456476?hl=en ; How shopping recommendations work on Google Search — https://support.google.com/googleshopping/answer/10269376?hl=en
- Published/updated: not stated (all)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "By default, ranking of product listings on the Shopping tab is based on relevance to a user's current search terms. Personalized listings on Google are shown to users based on recent activity, such as searches."
- Excerpt: > "The relative importance of these parameters is determined by algorithms to maximize listings' relevance to users."
- Excerpt: > "By default, ranking of Shopping ads is based on a combination of advertiser bids and relevance, such as a user’s current search terms and activity."
- Excerpt: > "Products are ranked based on relevance, as well as your search terms and other Google activity. Unless they’re labeled “Sponsored” or “Ad,” Google is not compensated for clicks into results on Google Shopping."
- Excerpt: > "Results labeled as “Top recommendations” are selected based on relevance to your search, ratings, price, and product features. Google isn’t compensated for clicks into these results."
- Excerpt: > "Shopping recommendations on Google Search are based on what's popular or trending across the web."
- Establishes: The only documented named factors for organic product selection: relevance, personalization, ratings, price, product features, popularity/trending (for recommendations).
- Limitations: Scope is Google Shopping / Search shopping features. No fetched page states ranking factors for AI Mode product results or Gemini product cards specifically. "Price" is named without saying "price competitiveness". Shipping, returns, availability and merchant quality are not named as ranking factors on these pages (but see GB-33).

### GB-33 Store Quality: shipping, returns, browsing, purchase signals; "may boost" Shopping-tab visibility
- Claim: Merchants with approved products are auto-enrolled in the Store Quality program. Metrics: delivery time/cost, return window/cost, image resolution/count, site speed, purchase experience. Google says improving a missing shipping-speed rating "may boost their visibility and performance on the 'Shopping' tab". Top Quality Store badge requires an "Exceptional" overall score (AU, CA, GB, IN, JP, NZ, US).
- Classification: VERIFIED FACT
- Source: About the Store Quality program — Google Merchant Center Help — https://support.google.com/merchants/answer/14261098?hl=en ; About the Top Quality Store badge — Google Shopping Help — https://support.google.com/googleshopping/answer/11115998?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "After a quick check, they realize that they’re providing shipping costs without providing shipping speed. So, they create a shipping service for their products that includes both shipping costs and shipping speed. After the lookback window passes, their rating updates with a new value to reflect their shipping speed, which may boost their visibility and performance on the "Shopping" tab."
- Excerpt: > "You won't be penalized if you don’t offer a certain level of customer experience or if you don’t provide some or all of the requested information. You just won't receive the benefits listed above."
- Excerpt: > "All merchants on the platform are eligible to receive benefits from the program, and your performance is evaluated against all other merchants."
- Excerpt (badge): > "To make a store Top Quality, Google asks businesses for data on certain experience categories when you shop, like shipping and returns policies, among others. Google also checks user ratings and the business’s website to measure its quality and accessibility."
- Establishes: The closest Google statement linking merchant quality (shipping/returns) to visibility. Scope: Shopping tab.
- Limitations: "may boost" is hedged and appears inside an example. The listed benefits are the badge and early feature access, not ranking. No statement extends this to AI Mode or Gemini. Internal tension: "won't be penalized" vs "may boost visibility" (section 4).

### GB-34 Store ratings: shown on free listings; "can help merchants improve the performance of ads and free listings"
- Claim: Store ratings come from Google Customer Reviews, supported review partners and Google-led research. They generally need ~100 reviews in a rolling 24-month window, are per-country, and show on ads only at ≥3.5 stars. Google says they can improve ads and free-listings performance.
- Classification: VERIFIED FACT
- Source: Google store ratings: An overview for Merchants — Google Merchant Center Help — https://support.google.com/merchants/answer/190657?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "As a result, store ratings can help merchants improve the performance of ads and free listings and drive more qualified shoppers to their landing pages."
- Excerpt: > "Minimum number of reviews: A merchant generally needs to collect at least 100 eligible, unique reviews to enable Google to calculate a reliable store rating."
- Excerpt: > "Store ratings display a rating next to a merchant’s name when shoppers interact with a free product listing within Search or Shopping, helping shoppers build trust with businesses from which to purchase a product."
- Establishes: Store rating is a displayed trust signal on free listings. "Performance" is framed via shopper trust/CTR.
- Limitations: Not a ranking statement. No AI Mode/Gemini mention.

### GB-35 Ads in AI Overviews and AI Mode: same campaigns and feed, "Sponsored" label, contextual matching, AI explainers, English markets
- Claim: Existing Search, Shopping and Performance Max campaigns are automatically eligible for ads within AI Overviews and AI Mode. Ads are labelled "Sponsored". Google matches ads to the query or contextually to query plus AI response. Gemini-generated "AI explainers" may accompany ads and cannot be edited or opted out of. Within-answer ads serve in English in US, AU, CA, IN, ID (AIO only), KE, MY, NZ, NG, PK (text only), PH, SG. Google states ads do not influence organic AI answers.
- Classification: VERIFIED FACT
- Source: About ads in AI-powered experiences in Google Search — Google Ads Help — https://support.google.com/google-ads/answer/18826097?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "All ads in AI Overviews and AI Mode are clearly labeled as "Sponsored" and visually distinguished from organic content. Paid advertising does not influence the organic responses generated by Google AI."
- Excerpt: > "Eligible campaign types: Existing Search, Shopping, and Performance Max campaigns are automatically eligible to serve ads within AI Overviews and AI Mode."
- Excerpt: > "AI explainers aren't part of ad headlines or descriptions. Unlike creative assets, advertisers can't manually write, edit, approve, or opt out of them"
- Excerpt: > "Keep Merchant Center product feeds complete and fresh for Shopping ads: Ensure your Merchant Center product data matches your landing pages and includes descriptive titles and descriptions, multiple high-resolution product and lifestyle images, accurate pricing and sale prices, product ratings and highlights, and clear shipping and return policies."
- Excerpt: > "No. Organic AI Overviews and AI Mode responses are generated independently using Google's Search quality and ranking systems. Buying ads doesn't influence organic AI answers, and whether your site is cited organically doesn't affect your ad auction eligibility."
- Establishes: Shopping ads in AI surfaces use the same Merchant Center feed. Label = "Sponsored".
- Limitations: The page covers Google Search only; it does not mention ads in the Gemini app. No fetched first-party page documents ads in the Gemini app (knowledge gap).

### GB-36 Direct Offers (pilot, Jan 2026) and May 2026 ad formats: "Sponsored deal", UCP native checkout in Direct Offers, Highlighted Answers, AI-powered Shopping ads
- Claim: Direct Offers launched as a Google Ads pilot in January 2026 for exclusive offers in AI Mode. On 2026-05-20 Google added promotion bundling, native checkout for UCP merchants, and travel offers, and said Direct Offers will surface in the AI Mode response. Google also announced Conversational Discovery ads, Highlighted Answers (ads inside AI Mode recommendation lists), AI-powered Shopping ads with Gemini explainers, and Business Agent for Leads.
- Classification: VERIFIED FACT
- Source: A new generation of ads for the AI era of Search — The Keyword — https://blog.google/products/ads-commerce/google-marketing-live-search-ads/ ; New tech and tools for retailers… — https://blog.google/products/ads-commerce/agentic-commerce-ai-tools-protocol-retailers-platforms/
- Published/updated: 2026-05-20; 2026-01-11
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Since launching the Direct Offers pilot in January 2026, brands like Chewy, Gap and L’Oreal have surfaced highly relevant deals as shoppers explore their options."
- Excerpt: > "Native checkout: We’ve added native checkout integration for Universal Commerce Protocol (UCP) merchants."
- Excerpt: > "With these updates, Direct Offers will now naturally surface in the AI Mode response as shoppers explore options, making deals more instantly discoverable."
- Excerpt: > "Highlighted Answers: When people are researching, they want helpful suggestions. Now, when AI Mode provides a list of recommendations — like the best language apps for an upcoming trip — highly relevant, high-quality ads are eligible to appear on that list as a Highlighted Answer."
- Excerpt: > "These formats will also continue to be clearly labeled as “Sponsored.”"
- Establishes: Paid placements can appear inside AI Mode recommendation lists (Highlighted Answers) and in the AI Mode response (Direct Offers), labelled. Connects UCP to ads.
- Limitations: No Google Ads Help page for Direct Offers was found (search returned none). Eligibility (campaign types, countries) for Direct Offers is not documented in fetched first-party pages. Formats are described as tests/"coming soon".

### GB-37 Business Agent: brand chat agent on Search; US eligibility; uses Merchant Center + website; Shopify activation path
- Claim: Business Agent is a Gemini-powered brand chat on Google Search. Customization requires a US e-commerce store, verified Merchant Center, at least 50 approved free listings and a claimed brand profile. It answers from Merchant Center data and the merchant's website. Shopify merchants can activate via the Google & YouTube app. Agentic checkout in Business Agent is "coming soon".
- Classification: VERIFIED FACT
- Source: Get started with Business Agent — Google Merchant Center Help — https://support.google.com/merchants/answer/16410382?hl=en
- Published/updated: not stated. Launch announced 2026-01-11 (GB-18).
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Business Agent is a conversational experience on Google Search that allows shoppers to chat with your brand."
- Excerpt: > "Have at least 50 free listings approved."
- Excerpt: > "Business Agent uses Gemini models to analyze information from your Merchant Center account and additional business data you provide, including your website."
- Excerpt: > "Coming soon: Business Agent will enable you to train your agent further using your business data, like brand guidelines, services, and size guides, which can improve the answers and helpfulness of this virtual associate more. Performance insights and agentic checkout are also coming soon."
- Excerpt: > "A standard Google-branded version of Business Agent is shown to customers until you complete customization."
- Establishes: Confirms the lead "Business Agent". A default Google-branded agent appears before customization.
- Limitations: Business Agent appears when users search for the brand (brand profile); it is not a discovery/ranking surface for non-brand queries.

### GB-38 Merchant-site agentic checkout ("Buy for me with GPay"): select merchants accepting Google Pay; criteria unpublished
- Claim: Google Pay Help says agentic checkout works with "select merchants that accept Google Pay" and that "eligibility requirements apply". The page says US and Australia at the top and "only in the US" in troubleshooting. BNPL via agentic checkout is limited to select purchases in Gemini and AI Mode (US, USD).
- Classification: VERIFIED FACT (statements); merchant eligibility criteria: not documented
- Source: About Agentic checkout with Google Pay — Google Pay Help — https://support.google.com/googlepay/answer/16421147?hl=en ; About price tracking on Google — Google Shopping Help — https://support.google.com/googleshopping/answer/13971184?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "This feature is currently only available in the US and Australia, in English and for select merchants that accept Google Pay as a payment method."
- Excerpt: > "This feature is available at select merchants in supported countries. We’re working to expand the number of merchants where Agentic checkout can be used. Eligibility requirements apply and merchant availability can change."
- Excerpt: > "Important: Buy now, pay later is currently only available for users in the US. This feature is also limited to select purchases within Gemini and AI Mode in Search, and for transactions made in US dollars."
- Excerpt (price tracking): > "Behind the scenes, our agentic checkout feature will then make the purchase from the merchant's website on your behalf with Google Pay."
- Establishes: Merchant-site agentic checkout requires accepting Google Pay; no merchant opt-in/opt-out mechanism is documented in fetched pages.
- Limitations: No Merchant Center page documents eligibility or opt-out for merchant-site agentic checkout (knowledge gap).

### GB-39 UCP on Google: identity linking, loyalty only at checkout, "Personalized search results are planned", mandatory order webhooks
- Claim: Identity Linking uses OAuth 2.0 with scopes `dev.ucp.shopping.order:read` and `dev.ucp.shopping.checkout:manage`. Google supports loyalty only at checkout for verified, account-linked users; personalized search results from loyalty are "planned for a future release". Merchants must push order created/shipped/delivered events to a Google webhook.
- Classification: VERIFIED FACT
- Source: Loyalty — Google for Developers UCP Guide — https://developers.google.com/merchant/ucp/guides/overview/loyalty ; Identity Linking — https://developers.google.com/merchant/ucp/guides/overview/identity-linking ; Order lifecycle — https://developers.google.com/merchant/ucp/guides/overview/order-lifecycle
- Published/updated: Loyalty Last updated 2026-10-22 UTC; Identity Linking 2026-10-02 UTC; Order lifecycle 2026-10-13 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Note: Google surfaces support loyalty integration only at checkout for verified, account-linked users. Personalized search results are planned for a future release."
- Excerpt: > "If you do not implement identity linking, you must support guest experiences."
- Excerpt: > "After checkout is completed and an order is placed, you must push status updates to Google using the order webhook."
- Establishes: As of the access date, loyalty/identity data does not affect Google search results (Google's statement of a future plan).
- Limitations: "planned" is forward-looking.

### GB-40 UCP spec repo: Apache-2.0, date-versioned releases v2026-01-11 → v2026-08-25; capabilities and transports
- Claim: UCP lives at github.com/Universal-Commerce-Protocol/ucp under Apache License 2.0 ("Copyright 2026 UCP Authors"). Release tags: v2026-01-11, v2026-01-23, v2026-04-08, v2026-08-25 (ucp.dev/latest = 2026-08-25). Transports: REST (core), MCP, A2A, Embedded Protocol. Standard capabilities in the v2026-08-25 overview table: Cart, Checkout, Identity Linking, Order; Catalog (search, lookup) is specified in separate pages from v2026-04-08. Unreleased drafts on `main`: Ask capability, return-policy extension, Lodging booking.
- Classification: VERIFIED FACT
- Source: Universal-Commerce-Protocol/ucp — GitHub — https://github.com/Universal-Commerce-Protocol/ucp (git clone, HEAD bbfe5e1, 2026-10-29; `git ls-remote --tags`; release branches fetched) ; https://ucp.dev/latest/specification/overview/
- Published/updated: last commit 2026-10-29; latest release v2026-08-25
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (README): > "The Universal Commerce Protocol (UCP) addresses a fragmented commerce landscape by providing a standardized common language and functional primitives. It enables platforms (like AI agents and apps), businesses, Payment Service Providers (PSPs), and Credential Providers (CPs) to communicate effectively, ensuring secure and consistent commerce experiences across the web."
- Excerpt (README): > "**Declare** supported capabilities to enable autonomous discovery by platforms."
- Excerpt (README): > "**Transport Agnostic:** The protocol is designed to work across various transports. Businesses can offer Capabilities via REST APIs, MCP (Model Context Protocol), or A2A, depending on their infrastructure."
- Excerpt (overview spec): > "UCP supports multiple transport protocols. Platforms and businesses effectively negotiate the transport via `services` on their profiles."
- Excerpt (versioning.md): > "UCP uses date-based version identifiers in `YYYY-MM-DD` format"
- Excerpt (announcements.md): > "This release introduces major protocol enhancements, key structural refactorings to support multi-vertical expansion, payments security improvements (3DS2), structured request constraints, independent capability versioning, grocery shopping readiness and many more."
- Establishes: Version history: v2026-01-11 spec files = checkout (REST/MCP/A2A), identity-linking, order, AP2 mandates, discount, fulfillment, buyer-consent, embedded checkout; v2026-04-08 adds cart, catalog, loyalty, embedded cart, signatures; v2026-08-25 restructures into shopping/common/payment, adds location. Google's surfaces implement versions 2026-01-23 and 2026-04-08 (GB-13, GB-14).
- Limitations: "autonomous discovery" in the README means capability discovery via profiles (`/.well-known/ucp`), not product ranking. The v2026-08-25 overview capability table omits Catalog although catalog pages ship in that release (internal inconsistency).

### GB-41 UCP governance: Google and Shopify permanent; Google holds proxy votes for open Governing Council seats until Dec 2028
- Claim: UCP's Governing Council has 5 seats: 1 permanent each for Google and Shopify, 3 elected. Current members: Amit Handa (Google), Ilya Grigorik (Shopify), Twum Djin (Stripe), 2 open. Google holds proxy vote for open seats until Dec 2028 and is custodian of the ucp.dev domain. Four domain Tech Councils exist: Shopping, Food, Lodging, Payments (16 seats each).
- Classification: VERIFIED FACT
- Source: GOVERNANCE.md and MAINTAINERS.md — Universal-Commerce-Protocol/.github — https://github.com/Universal-Commerce-Protocol/.github (git clone, HEAD 2026-10-29) ; docs/documentation/announcements.md — https://github.com/Universal-Commerce-Protocol/ucp
- Published/updated: last commit 2026-10-29
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (GOVERNANCE): > "GC serves as the ultimate owner of all UCP assets. Google acts as the custodian of the UCP.dev domain, holding and managing it to foster adoption of UCP."
- Excerpt (GOVERNANCE): > "Open elected seats may be filled at any time via GC election and approval. Google holds proxy vote for all open seats until Dec 2028 to facilitate rapid early stage growth & adoption of the protocol."
- Excerpt (GOVERNANCE): > "Includes 16 members, 4 permanent members from each founding organization (Google & Shopify), each with 1 vote (total 8 votes)."
- Excerpt (announcements): > "We are excited to welcome inaugural members Adyen NV, Ant International, Coinbase, Global Payments, Google, PayPal, Shopify, and Stripe to the Payments TC."
- Excerpt (announcements): > "Developed by the Lodging Technical Council (Amadeus, Booking.com, Expedia, Google, Hilton, Marriott, and Trip.com) and open-source contributors"
- Establishes: Shopping TC rows (MAINTAINERS): Google ×5 (incl. GC member Amit Handa), Shopify ×4, Etsy, Meta, Amazon, Target, Microsoft, Stripe, Salesforce, Wayfair. With 2 of 3 elected GC seats open, Google holds 3 of 5 GC votes by proxy until Dec 2028 (EVIDENCE-BASED INFERENCE from the proxy rule and current membership). OpenAI is absent (consistent with B-34/C-16).
- Limitations: Contradiction: the 2026-04-24 announcement lists "Greg Smith (Amazon)"; MAINTAINERS.md lists "Greg Smith | Google" and "Jordan Williams | Amazon" (section 4).

### GB-42 UCP Catalog capability exists, but Google documents product discovery on its surfaces as Shopping Graph-based; ranking in UCP catalog search is the business's own
- Claim: UCP defines `dev.ucp.shopping.catalog.search` and `.lookup` for platforms to search a business's catalog. The spec treats context signals as hints a business may "down-rank". Google's UCP docs for AI Mode/Gemini require Merchant Center feeds and attribute discovery to the Shopping Graph. The only fetched Google page where a Google agent calls a merchant's `search_catalog` is the "UCP in connected apps" grocery sample.
- Classification: VERIFIED FACT (spec text; Google doc text). "UCP does not feed AI Mode/Gemini product discovery or ranking today" = EVIDENCE-BASED INFERENCE (from GB-07, GB-08, GB-10 and absence of a catalog path in Google's shopping guides).
- Source: Catalog Capability — UCP spec (repo `docs/specification/shopping/catalog/index.md`, `search.md`) — https://github.com/Universal-Commerce-Protocol/ucp ; Grocery ordering — Google for Developers UCP Guide — https://developers.google.com/merchant/ucp/guides/connected-apps/grocery
- Published/updated: repo HEAD 2026-10-29; grocery page Last updated 2026-10-26 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (spec): > "The Catalog capability allows platforms to search and browse business product catalogs. This enables product discovery before checkout"
- Excerpt (spec): > "Catalog responses (pricing, availability, etc.) reflect the Business's current terms for the given request but are not transactional commitments — checkout is authoritative."
- Excerpt (spec): > "When `query` is omitted, the request represents a browse operation — the business returns products matching the provided filters without text-relevance ranking."
- Excerpt (spec): > "Context signals are provisional—not authoritative data. Businesses SHOULD use these values when verified inputs (e.g., shipping address) are absent, and MAY ignore or down-rank them if inconsistent with higher-confidence signals"
- Excerpt (Google grocery): > "This guide describes a sample integration for a grocery ordering experience using the Universal Commerce Protocol (UCP)."
- Excerpt (Google grocery): > "The agent searches the merchant's catalog for the ingredients. The agent makes one search_catalog call per ingredient."
- Establishes: In UCP, the merchant ranks results returned by its own catalog endpoint. On Google's shopping surfaces, discovery is documented as Shopping Graph + Merchant Center.
- Limitations: The grocery guide does not name the Google surface that runs the agent. Shopify's UCP catalog endpoints (C-17) are not documented by Google as consumed by AI Mode/Gemini.

### GB-43 UCP ↔ AP2 relationship (UCP docs and AP2 FAQ)
- Claim: UCP's docs call AP2 the trust layer for agent-led transactions, implemented as an AP2 mandates extension on Checkout. The AP2 FAQ says UCP orchestrates the purchase lifecycle and AP2 is "the specialized payment layer"; merchants on Google's AI surfaces should use UCP and can add AP2 for autonomous purchases.
- Classification: VERIFIED FACT
- Source: UCP and AP2 — UCP repo `docs/documentation/ucp-and-ap2.md` — https://github.com/Universal-Commerce-Protocol/ucp ; AP2 FAQ — `docs/faq.md` — https://github.com/google-agentic-commerce/AP2
- Published/updated: UCP repo HEAD 2026-10-29; AP2 repo HEAD 2026-04-29
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (UCP): > "AP2 serves as the trust layer for agent-led transactions completed on behalf of a user, mandating a secure, verifiable exchange of intents and authorizations between Platforms and businesses."
- Excerpt (AP2 FAQ): > "While the Universal Commerce Protocol orchestrates the broader purchase lifecycle, AP2 is the specialized payment layer responsible for authorizing and signing transactions."
- Excerpt (AP2 FAQ): > "If you are a merchant who would like to showcase products and allow users to complete inline checkout on Google’s AI surfaces like AI Mode and Gemini, then you should use Universal Commerce Protocol. You can enhance the protocol with the AP2 extension if you plan to build autonomous purchase scenarios where AI Agents can make purchases in the user’s absence."
- Excerpt (AP2 FAQ): > "The Universal Commerce Protocol is different in that it enables native buying on AI Mode and Gemini."
- Establishes: AP2 is optional for Google's current human-confirmed checkout (GB-13: Google UI, PAN_ONLY, FPANs). AP2 targets "human not present" purchases.
- Limitations: No fetched Google page says AP2 is used in production on AI Mode/Gemini today.

### GB-44 AP2: announced 2025-09-16; v0.2 (2026-04-28) adds "Human Not Present"; donated to the FIDO Alliance; mandate model changed
- Claim: Google announced AP2 on 2025-09-16 with 60+ organizations. AP2 v0.1.0 (2025-09-16) defined Intent, Cart and Payment Mandates. On 2026-04-28 Google released v0.2 and announced donation of AP2 to the FIDO Alliance. The v0.2 spec defines Checkout Mandate and Payment Mandate. Repo license: Apache 2.0.
- Classification: VERIFIED FACT
- Source: Announcing Agent Payments Protocol (AP2) — Google Cloud Blog — https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol ; We’re donating Agent Payments Protocol to the FIDO Alliance… — The Keyword — https://blog.google/products-and-platforms/platforms/google-pay/agent-payments-protocol-fido-alliance/ ; google-agentic-commerce/AP2 — GitHub — https://github.com/google-agentic-commerce/AP2 (CHANGELOG.md; tags v0.1.0, v0.2.0; `docs/ap2/specification.md`)
- Published/updated: 2025-09-16; 2026-04-28; repo HEAD 2026-04-29
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (Cloud blog): > "Today, Google announced the Agent Payments Protocol (AP2), an open protocol developed with leading payments and technology companies to securely initiate and transact agent-led payments across platforms."
- Excerpt (Keyword): > "Now, to help further scale this technology and promote industry-wide innovation, we’re donating the Agent Payments Protocol (AP2) to the FIDO Alliance, a renowned industry association focused on creating open standards."
- Excerpt (Keyword): > "Today on GitHub, we’re also releasing AP2 v.0.2, which introduces critical updates for autonomous transactions, including “Human Not Present” payments"
- Excerpt (CHANGELOG): > "## 0.2.0 (2026-04-28)"
- Excerpt (v0.2 spec): > "Mandate types: Checkout Mandate and Payment Mandate."
- Excerpt (AP2 FAQ): > "The core specification work will continue in [FIDO](https://blog.google/products-and-platforms/platforms/google-pay/agent-payments-protocol-fido-alliance/), ensuring it continues as an open, interoperable protocol for all agentic payments."
- Establishes: Confirms the lead "AP2 announced Sept 2025". AP2 governance is moving from Google to FIDO.
- Limitations: The Cloud blog's Intent/Cart Mandate description is superseded by v0.2 terminology (section 4). Repo shows no commits after 2026-04-29.

### GB-45 Agent-addressed instruction files in the UCP repo (recorded, not followed)
- Claim: The UCP repo root contains `AGENTS.md`, `CLAUDE.md` (imports `@AGENTS.md`), `AGENT_IMPLEMENTER.md` and `AGENT_CONTRIBUTOR.md`, written to AI coding agents. Content is contribution/implementation guidance (schema source of truth, commit conventions, when to fetch `llms.txt`).
- Classification: VERIFIED FACT
- Source: Universal-Commerce-Protocol/ucp — GitHub — https://github.com/Universal-Commerce-Protocol/ucp (files at repo root)
- Published/updated: repo HEAD 2026-10-29
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "You are an AI agent tasked with implementing the Universal Commerce Protocol (UCP) in a client, server, or UCP node."
- Establishes: Protocol maintainers target AI coding agents as implementers. No instruction targets shopping agents or ranking.
- Limitations: Data only. AURA did not act on these files.

## Merchant Center attributes relevant to AI surfaces

Requirement levels copied from the Product data specification (https://support.google.com/merchants/answer/7052112?hl=en) unless another source is named. "Spec page" = that page as fetched 2026-10-30.

| Attribute | Requirement (verbatim or near-verbatim from source) | Note |
|---|---|---|
| `id` | Required | UCP: must match Checkout API item ID, or map via `merchant_item_id` (GB-05) |
| `title` / `structured_title` | Required | `structured_title` flags GenAI-written titles (`trained_algorithmic_media`) |
| `description` / `structured_description` | Required | Same GenAI flag |
| `link` | Required | |
| `image_link` | Required | 500×500 minimum enforced from 2027-01-31 (GB-25) |
| `additional_image_link` | Optional | Free listings page: "Recommended" |
| `availability` | Required | |
| `price` | Required | |
| `sale_price` | Optional | |
| `brand` | "Required (For all new products, except movies, books, and musical recording brands)" | |
| `gtin` | "It Depends (strongly recommended if available)" | Free listings: needed for Shopping Knowledge Panel matching |
| `mpn` | "Required (Only if your product does not have a manufacturer assigned GTIN)" | |
| `condition` | "Required if your product is used or refurbished" / "Optional for new products" | Used/refurbished excluded from UCP checkout (GB-06) |
| `google_product_category` | Optional | |
| `product_type` | Optional | |
| `item_group_id` | Required (BR, FR, DE, JP, UK, US if variant) / "Required for free listings for all product variants" | |
| `item_group_title` | "Optional, use if the product is a variant" | Conversational attribute (GB-21) |
| `variant_option` | "Optional. Use if the product is a variant" | Conversational attribute; UCP guide: "strongly recommended" for checkout (GB-05) |
| `color`, `size`, `age_group`, `gender` | Required for apparel in listed countries | |
| `material`, `pattern` | Required if variant-distinguishing; otherwise Optional | |
| `product_highlight` | Optional (2–100, max 150 chars) | Do not repeat Q&A/detail/description |
| `product_detail` | Optional (up to 100) | |
| `question_and_answer` | Optional (max 30 pairs, 10,000 chars) | "primarily intended for … AI mode" (GB-22) |
| `document_link` | Optional | Google extracts FAQ from PDFs (GB-22) |
| `related_product` | Optional (max 30) | `required_part`, `accessory`, `substitute`, etc. (GB-24) |
| `popularity_rank` | Optional (0–100) | "primarily intended for … AI Mode" (GB-23) |
| `product_length` / `width` / `height` / `weight` | Optional | |
| `certification` | Required where certification info must be shown; otherwise Optional | |
| `warranty` | Required where warranty info must be shown (e.g. Québec Bill 29); otherwise Optional | Added Oct 2026 |
| `shipping` | "It depends" (cost required for Shopping ads and free listings in listed countries incl. US) | Store Quality uses cost + transit time (GB-33) |
| `handling_cutoff_time`, `minimum_order_value`, `free_shipping_threshold` | Optional | 2026 additions (GB-25) |
| `return` | "Optional (Strongly recommended for each product)" | UCP checkout requires return cost, window, link (GB-04) |
| `return_policy_label` | Optional | |
| `loyalty_program` | Optional (AU, JP, UK, DE, FR, CA, MX, BR, US only) | |
| `excluded_destination` / `included_destination` | Optional | No AI-surface value (GB-29) |
| `canonical_link` | "Recommended for all products" — Free listings page (https://support.google.com/merchants/answer/13889434) | |
| `video_link` | Optional — 2026 spec update announcement; not on spec page | AI Mode display (GB-25) |
| `native_commerce` (`checkout_eligibility`, `cart_eligibility`) | "Optional for all products" — native_commerce Help page | Checkout opt-in default FALSE; cart opt-out default eligible (GB-03, GB-05) |
| `consumer_notice` | "mandatory for items with regulatory warning requirements" — UCP guide | UCP checkout only |
| `merchant_item_id` | Custom attribute — UCP guide | Overrides `id` in agentic requests |

## Contradictions and superseded information

1. UCP checkout country scope. Merchant Center UCP page: "eligibility in the United States, Canada, and Australia" (GB-01). Search Help: Buy in AI Mode "only available for signed in 18+ users in the US" (GB-09). GML blog (2026-05-20): CA/AU "in the coming months", UK later (GB-19). Onboarding Help: AU/CA "next year"; developer page: "early next year" (GB-12). As of 2026-10-30, consumer checkout is US-only; CA/AU slipped from "coming months" (May 2026) to "next year".
2. Gemini app availability for UCP checkout. FAQ (Last updated 2026-10-16): "both the Gemini web application and the Gemini mobile app" (GB-08). Developer landing page: "Gemini web (app coming soon)" (GB-10). Gemini Help purchase section covers the web app only (GB-15). Landing page is likely stale.
3. `consumer_notice` sub-attribute names. Help page example uses `consumer_notice_type` / `consumer_notice_message` (GB-03). UCP developer guide uses `notice_type` / `notice_message` (GB-05).
4. Boolean case. Help page uses `true`/`false`; UCP guide uses `TRUE`/`FALSE` and composite `TRUE:FALSE`. Not necessarily a conflict (case-insensitivity not stated).
5. Product data specification page is incomplete vs. other first-party pages: it omits `video_link` (announced 2026-04-14, present in Merchant API `videoLinks[]`), `native_commerce`, `consumer_notice`, `merchant_item_id`.
6. `popularity_rank` scope and precision. Spec: rank "in your entire inventory", "Decimal values are supported". Attribute page: compare "to products in the same general category", "Use at most 1 decimal point" (GB-23).
7. Return attribute name. Spec names `return` ("Return[return]"); UCP guide refers to "the returns attribute".
8. Jan 2026 "dozens of new data attributes" (GB-18) vs six conversational attributes listed in Help (GB-21). Either the remainder shipped as other attributes (e.g. `video_link`, shipping attributes) or did not ship; not resolved.
9. Agentic checkout country. Google Pay Help says "US and Australia" at the top and "only in the US" in troubleshooting on the same page (GB-38).
10. UCP Tech Council membership. Announcement 2026-04-24: "Greg Smith (Amazon)". MAINTAINERS.md (2026-10-29): "Greg Smith | Google" and "Jordan Williams | Amazon" (GB-41).
11. Store Quality: "You won't be penalized…" vs example "may boost their visibility and performance on the 'Shopping' tab" (GB-33). Not strictly contradictory (benefit vs penalty) but ambiguous about ranking.
12. Content API status. Search Central "Share your product data" (Last updated 2025-12-10) recommends the Content API for immediate updates; UCP Merchant Center guide (Last updated 2026-10-29) labels "Content API (deprecated)" and recommends Merchant API (GB-28).
13. AP2 mandate model superseded. Cloud blog 2025-09-16 and AP2 v0.1.0: Intent, Cart, Payment Mandates. AP2 v0.2 (2026-04-28): Checkout Mandate and Payment Mandate (GB-44).
14. Shopping Graph size superseded: 35B (2023-02-07) → 50B+ (2025-05-20 onward) (GB-30, GB-31).
15. UCP spec internal: v2026-08-25 overview "Standard Capabilities" table omits Catalog, while catalog search/lookup pages ship in that release (GB-40).
16. Embedded checkout guide now resolves under `/merchant/ucp/archive/checkout/embedded` while the landing page still promotes Embedded checkout (GB-10). Status unconfirmed.

## Knowledge gaps

- No first-party page states the ranking factors for products in AI Mode, AI Overviews product results or Gemini product cards. Documented factors exist only for Google Shopping / "Top recommendations" (GB-32).
- No first-party page states whether Google ranks on `popularity_rank`, `question_and_answer`, `related_product`, `product_highlight`, `product_detail` or video. Google states intended use only.
- No first-party statement links shipping speed/cost, return policy, store rating or Store Quality to AI Mode/Gemini visibility. The only visibility link is "may boost … on the 'Shopping' tab" (GB-33).
- Price competitiveness: "price" is named for "Top recommendations"; no statement on relative price vs. other merchants.
- Whether crawl-only products (no Merchant Center) appear as AI Mode or Gemini product listings is not documented (GB-27 says crawled products "can show up on Google" generically).
- Feed vs crawl precedence inside the Shopping Graph is undocumented.
- Merchant eligibility criteria and any opt-out for merchant-site agentic checkout ("Buy for me with GPay") are undocumented (GB-38).
- The full requirement list behind "make sure you meet the following requirements" on the Merchant Center UCP page links to developers.google.com/merchant/ucp; the waitlist/interest forms were not fetched (forms).
- Ads in the Gemini app: no first-party page found. Press reports exist but were not used.
- Direct Offers: no Google Ads Help page found; eligibility and countries undocumented in fetched sources.
- Whether UCP cart-transfer or native-checkout participation changes click-through or downstream signals that feed ranking: no source. GB-07 covers only "Native integration" and states no ranking effect.
- Which Google surface runs the "UCP in connected apps" grocery agent (GB-42).
- No fees for UCP checkout are stated in fetched pages; the "Checkout Addendum" to Merchant Center ToS was not fetched (linked only).

## Unfetched sources

- https://support.google.com/merchants/contact/ucp_integration_interest — interest form; not fetched (form, not documentation).
- Checkout Addendum to the Google Merchant Center Terms of Service (linked from https://support.google.com/merchants/answer/17515932) — not fetched.
- Google Ads Help page for Direct Offers — not found by search; may not exist publicly.
- Press used only to locate sources (not cited as evidence): searchengineland.com, ppc.land, seroundtable.com, techwyse.com (search result listings only; pages not fetched).

## Source list

Tier 1 — Google Merchant Center Help
- About the Universal Commerce Protocol (UCP) and UCP-powered checkout feature on Google — https://support.google.com/merchants/answer/16837055?hl=en
- How to onboard to the UCP integration hub in Merchant Center — https://support.google.com/merchants/answer/16992327?hl=en
- Universal Commerce Protocol Checkout Terms of Service (US only) — https://support.google.com/merchants/answer/17515932?hl=en
- Native commerce [native_commerce] — https://support.google.com/merchants/answer/17251586?hl=en
- Product data specification — https://support.google.com/merchants/answer/7052112?hl=en
- How to use conversational attributes — https://support.google.com/merchants/answer/17085370?hl=en
- Question and answer [question_and_answer] — https://support.google.com/merchants/answer/17085211?hl=en
- Popularity rank [popularity_rank] — https://support.google.com/merchants/answer/17085297?hl=en
- About using product videos across Google Shopping — https://support.google.com/merchants/answer/18545837?hl=en
- Merchant Center product data specification update 2026 — https://support.google.com/merchants/answer/16989427?hl=en
- Merchant Center announcements change log — https://support.google.com/merchants/announcements/6192467?hl=en
- Insights for AI-powered shopping experiences coming soon — https://support.google.com/merchants/answer/17117204?hl=en
- About AI performance insights — https://support.google.com/merchants/answer/17200695?hl=en
- Free listings for products — https://support.google.com/merchants/answer/13889434?hl=en
- Get started with Business Agent — https://support.google.com/merchants/answer/16410382?hl=en
- About the Store Quality program — https://support.google.com/merchants/answer/14261098?hl=en
- Google store ratings: An overview for Merchants — https://support.google.com/merchants/answer/190657?hl=en
- Add a checkout link for your products — https://support.google.com/merchants/answer/13945960?hl=en (context only)

Tier 1 — Google for Developers (UCP guide, Merchant API, Search Central)
- Getting started with Universal Commerce Protocol on Google — https://developers.google.com/merchant/ucp
- Frequently asked questions — https://developers.google.com/merchant/ucp/faq
- Integration overview — https://developers.google.com/merchant/ucp/guides/overview
- Merchant Center setup — https://developers.google.com/merchant/ucp/guides/overview/merchant-center
- Native checkout overview — https://developers.google.com/merchant/ucp/guides/overview/native-checkout
- Cart overview — https://developers.google.com/merchant/ucp/guides/overview/cart-overview
- Identity Linking — https://developers.google.com/merchant/ucp/guides/overview/identity-linking
- Loyalty — https://developers.google.com/merchant/ucp/guides/overview/loyalty
- Order lifecycle — https://developers.google.com/merchant/ucp/guides/overview/order-lifecycle
- About UCP integration hub in Merchant Center — https://developers.google.com/merchant/ucp/guides/merchant-center/overview
- UCP Analytics (Merchant Center) — https://developers.google.com/merchant/ucp/guides/merchant-center/analytics
- Grocery ordering (UCP in connected apps) — https://developers.google.com/merchant/ucp/guides/connected-apps/grocery
- Embedded checkout (archive path) — https://developers.google.com/merchant/ucp/archive/checkout/embedded
- ProductAttributes — Merchant API — https://developers.google.com/merchant/api/reference/rest/products_v1/ProductAttributes
- Share your product data with Google — https://developers.google.com/search/docs/specialty/ecommerce/share-your-product-data-with-google
- AI features and your website — https://developers.google.com/search/docs/appearance/ai-features

Tier 1 — Google consumer help
- Make purchases and manage orders directly from AI Mode in Google Search — https://support.google.com/websearch/answer/16833721?hl=en
- Get help with your shopping in Gemini Apps — https://support.google.com/gemini/answer/16730149?hl=en
- Manage your universal cart — https://support.google.com/gemini/answer/17085590?hl=en
- How Google Shopping works — https://support.google.com/googleshopping/answer/9128904?hl=en
- Recommendations & personalization — https://support.google.com/googleshopping/answer/9116422?hl=en
- How shopping recommendations work on Google Search — https://support.google.com/googleshopping/answer/10269376?hl=en
- Understand how shopping results are generated — https://support.google.com/googleshopping/answer/15456476?hl=en
- Sources of shopping info — https://support.google.com/googleshopping/answer/14336735?hl=en
- About the Top Quality Store badge — https://support.google.com/googleshopping/answer/11115998?hl=en
- About price tracking on Google — https://support.google.com/googleshopping/answer/13971184?hl=en
- About Agentic checkout with Google Pay — https://support.google.com/googlepay/answer/16421147?hl=en
- About ads in AI-powered experiences in Google Search — https://support.google.com/google-ads/answer/18826097?hl=en

Tier 1 — Google blogs
- New tech and tools for retailers to succeed in an agentic shopping era (2026-01-11) — https://blog.google/products/ads-commerce/agentic-commerce-ai-tools-protocol-retailers-platforms/
- Read Sundar Pichai’s remarks at the 2026 National Retail Federation (2026-01-11) — https://blog.google/company-news/inside-google/message-ceo/nrf-2026-remarks/
- How we’re helping retailers thrive with new UCP features and AI tools on Google (2026-05-20) — https://blog.google/products-and-platforms/products/shopping/shopping-updates-google-marketing-live/
- A new generation of ads for the AI era of Search (2026-05-20) — https://blog.google/products/ads-commerce/google-marketing-live-search-ads/
- Google Shopping launches agentic checkout and more AI shopping tools (2025-11-13) — https://blog.google/products-and-platforms/products/shopping/agentic-checkout-holiday-ai-shopping/
- Shop with AI Mode, use AI to buy and try clothes on yourself virtually (2025-05-20) — https://blog.google/products-and-platforms/products/shopping/google-shopping-ai-mode-virtual-try-on-update/
- 4 ways Google’s Shopping Graph helps you find what you want (2023-02-07) — https://blog.google/products-and-platforms/products/shopping/shopping-graph-explained/
- We’re donating Agent Payments Protocol to the FIDO Alliance (2026-04-28) — https://blog.google/products-and-platforms/platforms/google-pay/agent-payments-protocol-fido-alliance/
- Announcing Agent Payments Protocol (AP2) (2025-09-16) — https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol
- Accelerate with Google: Conversational Attributes (2026-05-13, modified 2026-09-16) — https://business.google.com/us/accelerate/announcements/conversational-attributes/
- Accelerate with Google: Ads in AI Mode (2026-05-13) — https://business.google.com/us/accelerate/announcements/ads-in-ai-mode/ (context only)

Tier 1 — Protocol repos and sites
- Universal-Commerce-Protocol/ucp (clone; README, LICENSE, docs/versioning.md, docs/documentation/announcements.md, roadmap.md, ucp-and-ap2.md, docs/specification/**, AGENTS.md etc.) — https://github.com/Universal-Commerce-Protocol/ucp
- Universal-Commerce-Protocol/.github (GOVERNANCE.md, MAINTAINERS.md) — https://github.com/Universal-Commerce-Protocol/.github
- UCP site — https://ucp.dev/ ; https://ucp.dev/latest/specification/overview/
- google-agentic-commerce/AP2 (README, LICENSE, CHANGELOG.md, docs/faq.md, docs/ap2/specification.md, tag v0.1.0) — https://github.com/google-agentic-commerce/AP2
- AP2 site — https://ap2-protocol.org/ (fetched; content matches repo docs/index.md)
