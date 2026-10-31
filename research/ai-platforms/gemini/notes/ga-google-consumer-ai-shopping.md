# GA — Google consumer-facing AI shopping (Gemini app, AI Mode, AI Overviews, Shopping)

- Scope: Google's consumer-facing documentation on AI shopping in the Gemini app, AI Mode (Google Search), AI Overviews and the Google Shopping tab. Each surface is reported separately. A shared pipeline is stated only where Google states it.
- Research date: 2026-10-30 (access date for every source below).
- Method: blog.google category RSS feeds (Shopping, Search, Gemini, Ads & Commerce, India) to enumerate 2026 posts. Raw HTML fetched with curl; text extracted locally with a stdlib HTML parser; excerpts copied character-for-character from the extracted text. WebSearch used only to locate sources. Help-center pages fetched the same way where possible.
- Tier 1 = blog.google (incl. regional editions), support.google.com, other Google-owned official pages. Tier 3 = press, used to locate primary sources and, labeled, for two facts no primary source covered (GA-43, GA-44).
- Status: COMPLETE for this pass (48 findings). Closing sections finalized 2026-10-31; no source was fetched on 2026-10-31. All 156 quoted excerpts were machine-checked against the fetched page text (0 mismatches). Help-center page dates not captured; re-check before registry promotion.

## Findings

### GA-01 Universal Cart launched in the U.S. on 2026-10-15 across Search and the Gemini app
- Claim: Universal Cart is live in the U.S. across Google Search (incl. AI Mode) and the Gemini app since 2026-10-15. It saves products from multiple retailers, tracks price drops and restocks, shows promo codes and suggests payment methods.
- Classification: VERIFIED FACT
- Surface: multiple (AI Mode / Search, Gemini app)
- Source: An intelligent new shopping cart — Google (The Keyword) — https://blog.google/products-and-platforms/products/shopping/universal-cart-launch/
- Published/updated: 2026-10-15 (datePublished 2026-10-15T13:00:00Z)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Today, Universal Cart is rolling out in the U.S. across Google Search and in the Gemini app."
- Excerpt: > "Let’s say you save a handbag from Steve Madden to your cart in AI Mode in Search, and later a sweater from Quince and lipgloss from Ulta Beauty in the Gemini app. Those products will be there in your cart when you come back later so you can pick up right where you left off."
- Excerpt: > "The cart is built on the 60+ billion continually refreshed product listings in Google’s Shopping Graph. This allows it to proactively work for you in the background, sending notifications about price drops or when an item comes back in stock."
- Establishes: One cart object is shared between AI Mode and the Gemini app. The cart reads Shopping Graph listings for price and stock monitoring.
- Limitations: Does not say whether AI Mode and the Gemini app use the same product-selection/ranking pipeline. Shared cart ≠ shared ranking. YouTube and Gmail entry points (announced at I/O 2026, GA-04) are not stated as live.

### GA-02 Universal Cart checkout: Google Pay on Google or transfer to merchant site; merchant stays seller of record
- Claim: From the cart, a user either pays with Google Pay on Google (UCP-powered) or transfers items to the merchant's own cart. Named merchants: Nike, Sephora, Target, Ulta Beauty, Walmart, Wayfair, "many Shopify merchants".
- Classification: VERIFIED FACT
- Surface: multiple (Search incl. AI Mode, Gemini app)
- Source: An intelligent new shopping cart — Google (The Keyword) — https://blog.google/products-and-platforms/products/shopping/universal-cart-launch/
- Published/updated: 2026-10-15
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "You can securely check out with Google Pay in just a few taps with many of your favorite stores right in the cart, or you can transfer your items directly to the merchant’s cart to finish buying on their site. Try these simplified checkout experiences with merchants like Nike, Sephora, Target, Ulta Beauty, Walmart, Wayfair, and many Shopify merchants. Either way, you will receive direct confirmations and customer support from the merchant, and they will remain the seller of record."
- Excerpt: > "The Universal Cart is built on Google Wallet so it understands your card perks and can intelligently help you choose between payment methods. It’ll also show you relevant promo codes right from the cart."
- Establishes: Two checkout paths exist. Payment uses Google Pay / Google Wallet. Merchant is seller of record.
- Limitations: "many Shopify merchants" is not enumerated. Eligibility criteria for in-cart checkout are not stated in this post.

### GA-03 Shopping Graph size: "over 60 billion product listings" (May 2026) and "60+ billion continually refreshed" (Oct 2026)
- Claim: Google's current stated Shopping Graph size is 60+ billion product listings. The 2026-05 and 2026-10 posts give no hourly refresh figure.
- Classification: VERIFIED FACT (statement); refresh mechanism undocumented
- Surface: multiple
- Source: Introducing the Universal Cart and more ways to help you shop — Google (The Keyword) — https://blog.google/products-and-platforms/products/shopping/google-shopping-cart/
- Published/updated: 2026-05-19
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "People shop across Google more than a billion times a day, powered by advanced AI and the Shopping Graph — the world’s most comprehensive catalog of over 60 billion product listings."
- Establishes: The 50-billion figure (GA-05) is superseded as of 2026-05-19 by "over 60 billion". Second source for 60+: GA-01 (2026-10-15).
- Limitations: "Listings" ≠ unique products. No statement of sources mix (feeds vs. crawl) in this post. No refresh-rate number after Jan 2026.

### GA-04 I/O 2026 (2026-05-19/20): Universal Cart announced for Search, Gemini, YouTube, Gmail; UCP checkout to expand to Canada, Australia, then U.K.
- Claim: At I/O 2026 Google announced Universal Cart (Search + Gemini app U.S. "this summer"; YouTube and Gmail later), UCP-powered checkout expansion to Canada and Australia "in the coming months" and later the U.K., UCP for YouTube (U.S.), hotel booking and local food delivery, and AP2 starting with Gemini Spark.
- Classification: VERIFIED FACT (announcement); actual Canada/Australia/U.K. launch not verified (see GA-12)
- Surface: multiple
- Source: Introducing the Universal Cart and more ways to help you shop — Google (The Keyword) — https://blog.google/products-and-platforms/products/shopping/google-shopping-cart/
- Published/updated: 2026-05-19
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Universal Cart is rolling out across Search and the Gemini app in the U.S. this summer, with YouTube and Gmail to follow."
- Excerpt: > "Building on that momentum, we’re expanding our UCP-powered checkout experience on Google to Canada and Australia in the coming months and later to the U.K. UCP is also coming to YouTube in the U.S., and to even more verticals, starting soon with hotel booking and local food delivery."
- Excerpt: > "Since the cart was built on Google Wallet, it understands your payment method perks, loyalty information and merchant offers so it can help you choose."
- Excerpt: > "We’ll begin bringing AP2 to Google products in the coming months, starting with Gemini Spark."
- Establishes: The "summer" U.S. date slipped to 2026-10-15 (GA-01). Non-U.S. UCP checkout was future-tense as of May 2026.
- Limitations: Announcement language ("coming months"). No India mention for UCP checkout or Universal Cart.

### GA-05 Shopping Graph (Jan 2026): "over 50 billion product listings", "more than 2 billion … refreshed every single hour"; Shopping Graph brought to the Gemini app in 2025
- Claim: In January 2026 Google CEO stated 50B+ listings with 2B+ refreshed hourly, including inventory, prices and reviews. He stated the Shopping Graph was brought to the Gemini app "last year" (2025).
- Classification: VERIFIED FACT (statement); superseded on size by GA-03
- Surface: multiple (Search, AI Mode, Gemini app)
- Source: The AI platform shift and the opportunity ahead for retail (NRF 2026 remarks, Sundar Pichai) — Google (The Keyword) — https://blog.google/company-news/inside-google/message-ceo/nrf-2026-remarks/
- Published/updated: 2026-01-11 (modified 2026-01-12)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Since 2021, our Shopping Graph provides information on products in real time. It has over 50 billion product listings, including inventory, prices and reviews. More than 2 billion of those listings are refreshed every single hour. It’s information at the speed of retail."
- Excerpt: > "And last year, we brought the Shopping Graph to the Gemini app, so it’s a lot more helpful for people asking shopping-related questions, too."
- Establishes: The "50 billion / 2 billion per hour" lead is verified as a Jan-2026 statement. The Gemini app uses the Shopping Graph for shopping questions.
- Limitations: Size figure superseded (GA-03). Hourly-refresh figure is not repeated in 2026-05/10 posts; whether it still holds is unknown.

### GA-06 UCP launched 2026-01-11 at NRF; first use case is native checkout ("buy button") in AI Mode and Gemini
- Claim: Google introduced the Universal Commerce Protocol on 2026-01-11, co-built with Shopify, Etsy, Wayfair, Target and Walmart. Native checkout via Google Pay inside AI Mode and Gemini is the first use case. The retailer remains merchant of record.
- Classification: VERIFIED FACT
- Surface: AI Mode, Gemini app
- Source: The AI platform shift and the opportunity ahead for retail — Google (The Keyword) — https://blog.google/company-news/inside-google/message-ceo/nrf-2026-remarks/
- Published/updated: 2026-01-11
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "It’s open, agnostic, built together with industry leaders Shopify, Etsy, Wayfair, Target and Walmart, and endorsed by 20+ more."
- Excerpt: > "There’s a lot that UCP will enable, and we are starting with native checkout. Soon you’ll see a buy button directly on Google surfaces including AI Mode in Search and Gemini."
- Excerpt: > "So if you’re searching for a suitcase from Monos, the protocol will allow the merchant to personalize a "new member" price or offer loyalty enrollment instantly. For returning customers, retailers can provide special offers based on past purchases or suggest helpful additions like packing cubes at checkout. And with a few taps via Google Pay, the purchase is complete without ever leaving the conversation."
- Excerpt: > "Throughout this process, the retailer remains the merchant of record, allowing them to own and shape the customer relationship."
- Establishes: UCP checkout is a Google-surface feature in AI Mode and Gemini. Merchants can personalize price/offers at checkout.
- Limitations: "Soon" — Jan 2026 post does not state the live date or countries.

### GA-07 UCP capabilities added 2026-03-19: Cart, Catalog (real-time variants/inventory/pricing), Identity Linking; Merchant Center onboarding
- Claim: UCP gained optional Cart, Catalog and Identity Linking capabilities. Google will bring "relevant" UCP capabilities to AI Mode and the Gemini app and simplify UCP onboarding in Merchant Center.
- Classification: VERIFIED FACT
- Surface: AI Mode, Gemini app
- Source: AI shopping gets simpler with Universal Commerce Protocol updates — Google (The Keyword) — https://blog.google/products-and-platforms/products/shopping/ucp-updates/
- Published/updated: 2026-03-19 (modified 2026-04-07)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "UCP adopters will be able to access a new Catalog capability that lets agents retrieve select real-time product details from a retailer’s catalog where necessary — like variants, inventory and pricing."
- Excerpt: > "Building on existing standards, UCP will also support Identity Linking. That allows shoppers on UCP-integrated platforms to receive the same loyalty or member benefits they would on a retailer’s site when they’re logged in — like pricing or free shipping — making shopping more connected across the web."
- Excerpt: > "At Google, we’ll continue to bring relevant UCP capabilities to shopping experiences in AI Mode in Search, the Gemini app and beyond. Additionally, we are actively working to onboard more retailers of all sizes to agentic experiences on Google with a simplified UCP onboarding process in Google’s Merchant Center, rolling out over the coming months."
- Establishes: A protocol path exists for real-time product data direct from merchant catalogs, beside the Shopping Graph.
- Limitations: Does not say which UCP capabilities Google's own surfaces use today. Capability exists ≠ used for ranking.

### GA-08 Sep 2026: UCP "already enables direct checkout for hundreds of thousands of brands and retailers across Google"; Merchant Center UCP hub adds cart transfer (U.S.; AU/CA early 2027)
- Claim: As of 2026-09-16, UCP-powered direct checkout covers hundreds of thousands of brands and retailers. New hub capabilities roll out in the U.S., with Australia and Canada "early next year". Tapestry (Coach, Kate Spade) sells via UCP checkout in Search incl. AI Mode and in the Gemini app.
- Classification: VERIFIED FACT (statement)
- Surface: multiple (Search incl. AI Mode, Gemini app)
- Source: Boost your holiday sales with these agentic commerce updates — Google (The Keyword) — https://blog.google/products-and-platforms/products/shopping/google-shopping-updates-holiday-shopping/
- Published/updated: 2026-09-16
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "UCP already enables direct checkout for hundreds of thousands of brands and retailers across Google. Now, merchants who use the hub for UCP-powered checkout can also enable capabilities like cart transfer to a merchant site and enhanced checkout flow testing, with analytics and more coming soon. The new capabilities are gradually rolling out in the U.S., with Australia and Canada to follow early next year."
- Excerpt: > "Retailers like Tapestry, which owns beloved brands like Coach and Kate Spade, were able to efficiently integrate UCP-powered checkout on Google and start selling their products in Search — including AI Mode — and the Gemini app to get ready for the gifting season."
- Establishes: UCP checkout is live at scale in the U.S. as of Sep 2026. Australia/Canada hub capabilities are dated "early next year" (2027).
- Limitations: Does not state whether UCP checkout itself (vs. hub capabilities) is live in Canada/Australia. "Hundreds of thousands" is unquantified. Merchant-facing post.

### GA-09 Conversational attributes from merchant feeds were used in 50% of relevant AI Mode product recommendations (lululemon test)
- Claim: Google states that merchant-submitted "conversational attributes" were incorporated in 50% of relevant AI Mode product recommendations during a test with lululemon. Google also recommends the video link attribute and loyalty data.
- Classification: VERIFIED FACT (statement about a single test); general ranking effect = EVIDENCE-BASED INFERENCE only
- Surface: AI Mode
- Source: Boost your holiday sales with these agentic commerce updates — Google (The Keyword) — https://blog.google/products-and-platforms/products/shopping/google-shopping-updates-holiday-shopping/
- Published/updated: 2026-09-16
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "In addition to those best practices, you can optimize your feed by using the video link attribute to automatically power highly visual, shoppable ad formats and submitting conversational attributes to add richer context to your product listings. During testing with lululemon, conversational attributes submitted from the brand were incorporated 50% of the time in relevant product recommendations in AI Mode, providing shoppers with more precise and helpful answers."
- Excerpt: > "Connecting your loyalty data in Merchant Center highlights member perks and pricing across Google. For instance, when a member of Minted’s loyalty program, Minted More, searches for holiday cards, they’ll see tailored results with member pricing."
- Establishes: Merchant Center feed text (conversational attributes) flows into AI Mode recommendation text. Loyalty data changes results shown to signed-in members.
- Limitations: "Incorporated" means used in answer text; it does not say the attribute changes which products are selected or their order. One brand, no method disclosed.

### GA-10 Conversational attributes available to retailers globally (May 2026); AI performance insights in Merchant Center for AU, CA, IN, NZ, US
- Claim: Retailers globally can submit conversational attributes. AI performance insights (share of voice on AI Mode and AI Overviews) was announced for Australia, Canada, India, New Zealand and the U.S. (May 2026) and declared available in those countries (Sep 2026).
- Classification: VERIFIED FACT
- Surface: AI Mode, AI Overviews (merchant-facing measurement)
- Source: How we’re helping retailers thrive with new Universal Commerce Protocol features and AI tools on Google — Google (The Keyword) — https://blog.google/products-and-platforms/products/shopping/shopping-updates-google-marketing-live/
- Published/updated: 2026-05-20
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "People are coming to AI Mode and Gemini to shop every day, and to help brands connect with those shoppers, we’re introducing new insights and tools that will help them get discovered. The new AI performance insights tool in Merchant Center gives you a clear view into how your brand is performing on AI surfaces by comparing your share of voice against similar brands. It's rolling out in Australia, Canada, India, New Zealand and the U.S. in the coming months."
- Excerpt: > "Strong product descriptions are critical for brands to get discovered in the AI era. Now, retailers globally can use conversational attributes to update their product descriptions to reflect the more conversational way people search."
- Second source: https://blog.google/products-and-platforms/products/shopping/google-shopping-updates-holiday-shopping/ (2026-09-16): > "AI performance insights in Merchant Center is now available to businesses across Australia, Canada, India, New Zealand, and the U.S. This feature gives retailers a clear view of how their brand and products are being discovered by comparing their share of voice with other brands across surfaces like AI Mode and AI Overviews, while enabling them take action to help boost discoverability even more."
- Establishes: India is a named market for AI-surface shopping measurement. Implies AI Mode / AI Overviews product visibility exists for India merchants.
- Limitations: Measurement tool availability ≠ consumer feature availability. Does not cover the Gemini app explicitly in the Sep text.

### GA-11 Direct Offers and Shopping ads on YouTube get UCP checkout (announced May 2026)
- Claim: Brands with UCP integration that run Direct Offers ("exclusive promotions") or YouTube Shopping ads via Demand Gen will let users buy on the spot. Affirm and Klarna BNPL to be embedded in Google Pay.
- Classification: VERIFIED FACT (announcement, "Soon")
- Surface: multiple (ads)
- Source: How we’re helping retailers thrive with new Universal Commerce Protocol features and AI tools on Google — Google (The Keyword) — https://blog.google/products-and-platforms/products/shopping/shopping-updates-google-marketing-live/
- Published/updated: 2026-05-20
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Soon, when brands who have integrated UCP show exclusive promotions with Direct Offers or run Shopping ads on YouTube with product feeds on Demand Gen campaigns, people can easily buy on the spot. And shoppers looking for more flexibility will even have the option to buy now and pay later, with new Affirm and Klarna options embedded directly into Google Pay."
- Establishes: Direct Offers is an ad format that carries promotions and can connect to UCP checkout.
- Limitations: This post does not define Direct Offers' surfaces (AI Mode vs. Gemini) or labeling. See Direct Offers primary source (later finding) for definition.

### GA-12 Ads in AI Mode expanded to India and 9 other countries (2026-10-28); "Sponsored" label; multiturn ads in U.S.; sponsored vs. organic product list items
- Claim: On 2026-10-28 Google scaled ads in AI Mode to Australia, Canada, India, Kenya, Malaysia, New Zealand, Nigeria, Pakistan, the Philippines and Singapore. Multiturn (follow-up) ads launch in the U.S. Ads are labeled "Sponsored". AI Mode contains both sponsored and organic "product list items".
- Classification: VERIFIED FACT
- Surface: AI Mode
- Source: Ads in AI Mode expand to new markets. — Google (The Keyword, Ads & Commerce) — https://blog.google/products/ads-commerce/ads-in-ai-mode-global/
- Published/updated: 2026-10-28
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Our research shows that people are comfortable with ads in AI Mode and find them highly relevant. In fact, click-through rates are already similar between sponsored and organic product list items within AI Mode."
- Excerpt: > "Now we're scaling ads in AI Mode in Australia, Canada, India, Kenya, Malaysia, New Zealand, Nigeria, Pakistan, the Philippines, and Singapore. In Q4 2026, we plan to expand to additional locales, including Brazil, Mexico, and the United Kingdom."
- Excerpt: > "To allow ads in follow-up queries in AI Mode, we are launching multiturn ads in the U.S."
- Excerpt: > "Ads will be clearly labeled as “Sponsored.” We’ll continue testing new formats to ensure ads remain helpful and relevant."
- Establishes: AI Mode product lists mix organic and sponsored items; the sponsored ones carry a "Sponsored" label. India has ads in AI Mode as of 2026-10-28.
- Limitations: Does not say how sponsored items are positioned relative to organic, or whether ad presence affects organic selection. Linked help page (support.google.com/google-ads/answer/18826097) fetched separately (see later finding).

### GA-13 I/O 2026: AI Overviews and AI Mode merged into one AI Search experience worldwide; AI Mode >1B monthly users; Gemini 3.5 Flash default
- Claim: On 2026-05-20 Google merged AI Overviews and AI Mode into "one, seamless AI Search experience", live worldwide on desktop and mobile. AI Mode passed 1 billion monthly users and moved to Gemini 3.5 Flash as default model globally.
- Classification: VERIFIED FACT
- Surface: AI Mode, AI Overviews
- Source: 100 things we announced at Google I/O 2026 — Google (The Keyword) — https://blog.google/innovation-and-ai/technology/ai/google-io-2026-all-our-announcements/
- Published/updated: 2026-05-20 (modified 2026-06-01)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "AI Mode is our most powerful AI Search, and it has surpassed more than 1 billion monthly users. And today we’re upgrading the experience with Gemini 3.5 Flash as the new default model, globally."
- Excerpt: > "We’re also making it even easier to continue the conversation with Search, bringing AI Overviews and AI Mode into one, seamless AI Search experience. You can flow effortlessly from your question, to a search results page with an AI Overview, to a follow-up in AI Mode, all with links to learn more. The new seamless AI Search experience is live today across desktop and mobile, worldwide."
- Establishes: AI Overviews and AI Mode are now one conversational flow in the UI. Pre-May-2026 sources that treat them as separate entry points are partly outdated.
- Limitations: "One experience" describes UI flow. It does not state that AI Overviews and AI Mode use the same product retrieval or ranking. Keep reporting the surfaces separately.

### GA-14 Personal Intelligence in AI Mode: Gmail and Google Photos connections (Calendar soon), ~200 countries, 98 languages, no subscription
- Claim: AI Mode users can connect Gmail and Google Photos (Calendar soon) as "Personal Intelligence". Expanded to nearly 200 countries and territories in 98 languages at I/O 2026.
- Classification: VERIFIED FACT
- Surface: AI Mode
- Source: 100 things we announced at Google I/O 2026 — Google (The Keyword) — https://blog.google/innovation-and-ai/technology/ai/google-io-2026-all-our-announcements/
- Published/updated: 2026-05-20
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "We’re expanding Personal Intelligence in AI Mode to more people in nearly 200 countries and territories across 98 languages — no subscription required."
- Excerpt: > "With AI Mode in Search, you can securely connect apps like Gmail and Google Photos, and soon Google Calendar. Personal Intelligence was designed with transparency, choice and control at its core. You’re always in control — you choose if and when you want to connect apps like Gmail and Google Photos."
- Establishes: Opt-in Gmail/Photos context exists in AI Mode in most countries.
- Limitations: Does not state that Personal Intelligence changes shopping product selection. Shopping-specific use is not documented in this source.

### GA-15 India (2026-04-07): Gemini app shopping (English, Hindi) and upgraded AI Mode shopping (English; Hindi "soon"); Virtual Try-On launched in India in 2025
- Claim: Google India states the Gemini app shows shoppable product listings, comparison tables, prices and places to buy, powered by the Shopping Graph, in English and Hindi. AI Mode shopping in India shows price, reviews and inventory info, shoppable images and comparison tables; English now, Hindi soon. Virtual Try-On launched in India "last year".
- Classification: VERIFIED FACT
- Surface: Gemini app, AI Mode
- Source: New ways Google is using AI to make shopping easier — Google India (The Keyword, en-in) — https://blog.google/intl/en-in/products/explore-communicate/new-ways-google-is-using-ai-to-make-shopping-easier/
- Published/updated: 2026-04-07
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "We're making it easier than ever to find exactly what you need, with tools that bring together our Gemini models and Google’s Shopping Graph, our dataset of more than 50 billion of the world’s products, 2 billion of which are updated every hour. Last year, we launched our Virtual Try-On tool in India, and we’ve been excited to see how it’s made shopping easier for users by helping them virtually try apparel listings on themselves."
- Excerpt: > "You can move beyond simple text suggestions and get shoppable product listings, comparison tables, prices from across the web and places to buy right in the Gemini app. Shopping in Gemini is powered by the Shopping Graph so you can trust you’re seeing fresh information and unmatched selection. This experience is currently available in English and Hindi."
- Excerpt: > "When you ask a shopping question, AI Mode provides an intelligently organized response that brings together rich visuals and and all the details you need (like price, reviews and inventory info), helping you quickly and confidently decide what to buy. For example, if you’re looking for visual inspiration, you’ll see shoppable images. Or, if you’re deciding between a few options, you’ll see a comparison table with a side-by-side view of considerations specific to that product, including insights from reviews to help you quickly understand the differences. This experience is currently available in English and we'll be rolling out in Hindi soon."
- Establishes: India has Gemini-app shopping (EN, HI) and AI Mode shopping (EN) since at least 2026-04-07. Both are stated to draw on the Shopping Graph (Gemini explicitly; AI Mode implicitly via the intro sentence).
- Limitations: No mention of INR, agentic checkout, UCP, Universal Cart or other Indian languages. Hindi AI Mode shopping rollout not confirmed in a later source (gap). Uses the older "50 billion / 2 billion hourly" figures one month before the global "60 billion" figure — see Contradictions.


### GA-16 Gemini app shopping (help center): Shopping Graph source; product cards, grouping, comparisons, links, Personal Intelligence recommendations; 21 countries incl. India
- Claim: The Gemini Apps help center states Gemini uses Shopping Graph information for shopping. Responses can include image-led product cards, theme groups, aspect-based comparisons, direct product links and Personal-Intelligence-based recommendations. Requirements: 18+, personal account, Keep Activity on. Supported countries include India.
- Classification: VERIFIED FACT
- Surface: Gemini app (mobile, gemini.google.com, Gemini in Chrome)
- Source: Get help with your shopping in Gemini Apps — Google (Gemini Apps Help) — https://support.google.com/gemini/answer/16730149?hl=en
- Published/updated: not stated (page date rendered by JS; not captured)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "You can use Gemini Apps as your personal AI-powered shopping assistant. Gemini uses information from Google’s Shopping Graph to help you find products, compare options, and make purchase decisions."
- Excerpt: > "Visually-rich results: Gemini Apps can show you products with clear images and key information."
- Excerpt: > "Grouping by theme: Gemini Apps can organize products into groups to make it easier to explore related items."
- Excerpt: > "Product comparisons: Gemini Apps can compare multiple products based on the aspects you select to help you make an informed decision."
- Excerpt: > "Personalized shopping experiences: Gemini Apps can provide relevant and personalized product recommendations using Personal Intelligence."
- Excerpt: > "Works with eligible merchants with some product restrictions, including those that require ID verification like alcohol or tobacco, and digital goods products that require customization or special delivery requirements."
- Excerpt (country list, verbatim items): "Argentina", "Australia", "Brazil", "Canada", "Chile", "Colombia", "Hong Kong", "India", "Japan", "Indonesia", "Malaysia", "Mexico", "New Zealand", "Philippines", "Saudi Arabia", "Singapore", "Taiwan", "Thailand", "UAE", "US", "Vietnam" — under > "Shopping with Gemini Apps is currently available in the following countries & regions:"
- Establishes: Gemini-app shopping is a Shopping Graph-backed feature in 21 countries/regions including India. Personal Intelligence can personalize product recommendations.
- Limitations: No ranking factors are documented. No language list on this page (India languages come from GA-15). No statement that the Gemini app uses the same ranking as AI Mode. "Eligible merchants" criteria are not defined.

### GA-17 Gemini app "Buy" button: in-chat purchase via Google Pay on gemini.google.com; account linking for loyalty/member pricing
- Claim: Eligible product listings show a "Buy" button in the Gemini web app. Checkout prefills Google Pay payment and address; "Gemini makes the purchase for you". Users can link retailer loyalty accounts for member pricing and points. Order follow-ups come from the merchant.
- Classification: VERIFIED FACT
- Surface: Gemini app (web)
- Source: Get help with your shopping in Gemini Apps — Google (Gemini Apps Help) — https://support.google.com/gemini/answer/16730149?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "There’s a “Buy” button on product listings that are eligible for purchase within the Gemini web app."
- Excerpt: > "Your payment information is encrypted and kept private as Gemini makes the purchase for you."
- Excerpt: > "Any post-purchase follow ups, such as order confirmation emails, will come directly from the merchant."
- Excerpt: > "For participating merchants, you can link your existing memberships and shopping programs to your Google Account. Linking your accounts offers several benefits during the checkout process:"
- Excerpt: > "Access to member-only pricing and retailer deals"
- Establishes: In-chat checkout exists in the Gemini web app. The account-linking flow matches UCP Identity Linking (GA-07) in function.
- Limitations: Page does not state which countries have the Buy button (the 21-country list covers "shopping", not checkout). Link to UCP is EVIDENCE-BASED INFERENCE (page does not name UCP). Mobile app Buy availability not stated.

### GA-18 Universal Cart help: U.S. only; add from Google Search & Shopping, AI Mode, Gemini Apps; Gemini/AI Mode have limited cart access
- Claim: Universal Cart is U.S.-only. Items can be added from Google Search & Shopping, AI Mode and Gemini Apps. Checkout is Google Pay for participating merchants or cart population on the merchant site for others. Gemini Apps and AI Mode cannot list cart items, add items "directly", or report order status in chat.
- Classification: VERIFIED FACT
- Surface: multiple (Search & Shopping, AI Mode, Gemini app)
- Source: Manage your universal cart — Google (Gemini Apps Help) — https://support.google.com/gemini/answer/17085590?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Important: This feature is currently available only in the United States."
- Excerpt: > "Check out with Google Pay: For participating merchants, you can complete your transaction on Google using your saved payment methods."
- Excerpt: > "Check out on the merchant site: For other merchants, Google helps you populate your cart on the merchant's website so you can complete the purchase there."
- Excerpt: > "You can save items to your cart through Gemini Apps and AI Mode. These surfaces have limited access to your data and may be unable to complete the following."
- Excerpt: > "Based on your Wallet settings, cart can provide AI-identified insights on available offers and rewards from credit cards saved in your Wallet. You always have the final say on which card you choose for your purchases. Offers and rewards displayed are determined by your payment provider, not Google."
- Establishes: Universal Cart has no India availability. The cart is a Wallet-backed object separate from the chat surfaces.
- Limitations: "may be unable" is hedged. Does not describe which merchants qualify for Google Pay checkout.

### GA-19 Shopping Graph inputs (Google Shopping Help): Merchant Center and Manufacturer Center feeds; used in Search, Ads, YouTube and Generative AI features; AI Overviews ranked lists "aren't sponsored"
- Claim: Brands, retailers and other content providers send product info through Merchant Center and Manufacturer Center into the Shopping Graph. Shopping Graph info powers Search results, Ads, YouTube and generative AI features (review summaries, buying guidance, recommendations). Google states AI Overviews ranked lists are not sponsored.
- Classification: VERIFIED FACT
- Surface: multiple (incl. AI Overviews)
- Source: Sources of shopping info — Google (Google Shopping Help) — https://support.google.com/googleshopping/answer/14336735?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "The Shopping Graph is a dynamic repository of product info that provides an up-to-date view of the products available."
- Excerpt: > "Brands, retailers, and other content providers send their product info directly to Google through tools like Merchant Center and Manufacturer Center. This info, including details like product names, descriptions, prices, images, and reviews, is used across Google experiences."
- Excerpt: > "For example, info from the Shopping Graph may be used in Search Results, Ads, YouTube, or Generative AI features to:"
- Excerpt: > "Power AI-driven experiences like review summaries, buying guidance, or product recommendations."
- Excerpt: > "Ranked lists and info you find in AI Overviews and more aren’t sponsored, and you only find results related to what you search."
- Establishes: Merchant Center / Manufacturer Center feeds are a documented Shopping Graph input. The same Shopping Graph feeds generative AI shopping features.
- Limitations: Page names only direct-submission inputs. It does not mention web crawling, YouTube content or third-party review sites as Shopping Graph inputs. The help page's language list is EU-heavy; it may be written for EU transparency obligations (unverified). "AI Overviews … aren't sponsored" conflicts in scope with GA-12/GA-24 (ads appear within AI Overviews in labeled sections) — see Contradictions.

### GA-20 Shopping tab ranking (Google Shopping Help): relevance to current search terms by default; personalization from recent activity; "Sponsored" offers ranked partly by advertiser payment
- Claim: On the Shopping tab, default ranking is relevance to current search terms. Personalized listings use recent activity (Search Services History; Personalized Recommendations setting). Items labeled "Sponsored" may be ranked and grouped partly by advertiser payment. Product data comes from seller feeds with possible update delay.
- Classification: VERIFIED FACT
- Surface: Shopping (Shopping tab)
- Source: How Google Shopping works — Google (Google Shopping Help) — https://support.google.com/googleshopping/answer/9128904?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "By default, ranking of product listings on the Shopping tab is based on relevance to a user's current search terms. Personalized listings on Google are shown to users based on recent activity, such as searches."
- Excerpt: > "The relative importance of these parameters is determined by algorithms to maximize listings' relevance to users."
- Excerpt: > "Offers that have the "Sponsored" label means that advertiser payment to Google may also influence how items are ranked and grouped. Google is compensated for clicks on these ads."
- Excerpt: > "Online retailers submit feeds containing product information to Google Shopping. Since this product information comes directly from the seller, this means we’re able to show the current prices, latest offers and current product availability."
- Excerpt: > "Ratings are compiled from reviews across sources and aggregated into an overall rating for display on Google. As a result, Shopping ratings may not match the ratings available on a given merchant's website."
- Establishes: Documented Shopping tab ranking inputs: query relevance + personal activity; ads ranking adds payment. Reviews come from Google Customer Reviews, merchants and third-party review providers.
- Limitations: Shopping tab only. Not stated to apply to AI Mode, AI Overviews or Gemini app. Page carries a banner that settings are being updated.

### GA-21 Shopping results "Top recommendations": selected by relevance, ratings, price, product features; AI-researched content supported by Shopping data
- Claim: Google Shopping results are "ranked based on relevance, as well as your search terms and other Google activity". AI-generated "Top recommendations" are selected on relevance, ratings, price and product features, without compensation. Product recommendations and insights are generated with AI using Google's Shopping data.
- Classification: VERIFIED FACT
- Surface: Shopping (Google Shopping results; AI-generated recommendations module)
- Source: Understand how shopping results are generated — Google (Google Shopping Help) — https://support.google.com/googleshopping/answer/15456476?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Products are ranked based on relevance, as well as your search terms and other Google activity. Unless they’re labeled “Sponsored” or “Ad,” Google is not compensated for clicks into results on Google Shopping."
- Excerpt: > "Product recommendations and insights are generated with the help of AI, which is used to research product information. It’s supported by Google’s Shopping data, aggregated from brands, stores, and other content providers."
- Excerpt: > "Results labeled as “Top recommendations” are selected based on relevance to your search, ratings, price, and product features. Google isn’t compensated for clicks into these results."
- Excerpt: > "Important: The price may vary based on your location. The merchant confirms the final price."
- Establishes: The only Google-documented factor list for AI-generated product recommendations: relevance, ratings, price, product features. Organic vs. paid separation by label.
- Limitations: Applies to Google Shopping results. The page does not say AI Mode or Gemini use the same "Top recommendations" logic. Weights are undocumented.

### GA-22 Shopping recommendations on Search: based on popularity/trends; personalization from search, browsing and YouTube history; Shopping ads ranked by bids + relevance
- Claim: Shopping recommendations on Google Search are based on popularity/trending across the web, plus (if Personal results on) past searches, browsing history and YouTube watch history. Shopping ads rank on advertiser bids and relevance.
- Classification: VERIFIED FACT
- Surface: Shopping (Search shopping recommendations, Shopping ads)
- Source: How shopping recommendations work on Google Search — Google (Google Shopping Help) — https://support.google.com/googleshopping/answer/10269376?hl=en ; Recommendations & personalization — https://support.google.com/googleshopping/answer/9116422?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (10269376): > "Shopping recommendations on Google Search are based on what's popular or trending across the web."
- Excerpt (10269376): > "If you’re signed in to your Google Account and have Personal results turned on, recommendations may also be based on your activity in Google products like:"
- Excerpt (9116422): > "By default, ranking of Shopping ads is based on a combination of advertiser bids and relevance, such as a user’s current search terms and activity."
- Excerpt (9116422): > "To help you get better results on Google Shopping, your past Google activity is used to:"
- Establishes: Popularity/trending and personal history are documented recommendation inputs on Search. Ads rank on bid × relevance.
- Limitations: These pages predate or do not mention AI Mode/Gemini. Applicability to AI surfaces is EVIDENCE-BASED INFERENCE at most.

### GA-23 Saved shopping preferences (brands, department, styles) boost results across Search, Shopping, Discover — U.S., Canada, Australia, India
- Claim: Users in the U.S., Canada, Australia and India can save favorite brands, department and style preferences. Saved brands "show up more often" in results. Preferences may apply on Search, Shopping, Discover and other surfaces.
- Classification: VERIFIED FACT
- Surface: Shopping / Search (AI Mode and Gemini not named)
- Source: Manage shopping preferences on Google — Google (Google Shopping Help) — https://support.google.com/googleshopping/answer/13005558?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Important: This feature is only available in the US, Canada, Australia, and India."
- Excerpt: > "Your shopping preferences may be reflected on Search, Shopping, Discover and other Google surfaces."
- Excerpt: > "You can save brands in some product categories, like “jeans” or “shoes.” Products from your favorite brands will show up more often in your search results."
- Establishes: An explicit user-preference ranking boost exists in India.
- Limitations: Does not name AI Mode or the Gemini app.

### GA-24 Ads in AI Overviews and AI Mode (Google Ads Help): "Sponsored" label; ads don't influence organic AI answers; India eligible (English); Gemini-written "AI explainers"
- Claim: Ads appear within or beside AI Overviews and AI Mode responses in "Sponsored" sections. Existing Search, Shopping and PMax campaigns are eligible; text and Shopping ads serve. Ads match to the query or contextually to query + AI response. Google states paid ads do not influence organic AI responses. Ads within AI Overviews/AI Mode serve in the U.S., Australia, Canada, India, Indonesia (AIO only), Kenya, Malaysia, New Zealand, Nigeria, Pakistan (text only), Philippines, Singapore — English only.
- Classification: VERIFIED FACT (statement); "no influence" mechanism undocumented
- Surface: AI Overviews, AI Mode
- Source: About ads in AI-powered experiences in Google Search — Google (Google Ads Help) — https://support.google.com/google-ads/answer/18826097?hl=en
- Published/updated: not stated (linked from 2026-10-28 post, GA-12)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "All ads in AI Overviews and AI Mode are clearly labeled as "Sponsored" and visually distinguished from organic content. Paid advertising does not influence the organic responses generated by Google AI."
- Excerpt: > "In AI Overviews and AI Mode, Google matches ads either directly to the user's query (when the search already expresses clear commercial intent) or contextually to both the user's query and the AI response (when someone asks a longer, exploratory, or conversational question and commercial intent emerges from the helpful next steps in the response)."
- Excerpt: > "In some placements across AI surfaces, ads may also appear with AI explainers, which are concise, independent text generated by Google's Gemini models to help people understand how an ad or group of ads relates to what they're looking for."
- Excerpt: > "No. Organic AI Overviews and AI Mode responses are generated independently using Google's Search quality and ranking systems. Buying ads doesn't influence organic AI answers, and whether your site is cited organically doesn't affect your ad auction eligibility."
- Excerpt: > "Countries: United States, Australia, Canada, India, Indonesia (AI Overviews only), Kenya, Malaysia, New Zealand, Nigeria, Pakistan (text ads only), Philippines, and Singapore"
- Excerpt: > "Languages: English"
- Establishes: Organic AI answers are generated by "Search quality and ranking systems". Ads are a separate auction rendered in labeled sections. India: English-language ads inside AI Overviews and AI Mode.
- Limitations: Google's statement of separation is not independently verifiable. Ads matched to the AI response text create a dependency of ad selection on organic output (not the reverse).

### GA-25 Direct Offers (Jan 2026 pilot): advertiser discounts shown in AI Mode, labeled "Sponsored deal"; Google AI decides relevance
- Claim: Direct Offers is a Google Ads pilot (launched 2026-01-11) that shows advertiser-set exclusive offers (e.g., 20% off) in AI Mode. Google AI decides when an offer is relevant. Image caption labels it "Sponsored deal". Organic selection is described as separate: "Google already elevates the most relevant products".
- Classification: VERIFIED FACT
- Surface: AI Mode
- Source: New tech and tools for retailers to succeed in an agentic shopping era — Google (The Keyword, Ads & Commerce) — https://blog.google/products/ads-commerce/agentic-commerce-ai-tools-protocol-retailers-platforms/
- Published/updated: 2026-01-11
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "That’s why we’re continuing to test ads in AI Mode and we’re now introducing Direct Offers. This new Google Ads pilot allows advertisers to present exclusive offers for shoppers who are ready to buy — like a special 20% off discount — directly in AI Mode."
- Excerpt: > "Google already elevates the most relevant products to meet your search criteria. But often, you are only ready to buy if you’re getting a great deal. Now relevant retailers have an opportunity to also feature a special discount."
- Excerpt: > "User flow of Direct Offers pilot in AI Mode, labeled “Sponsored deal.”"
- Excerpt: > "With Direct Offers, retailers set up relevant offers they want to feature in their campaign settings and Google will use AI to determine when an offer is relevant to display."
- Establishes: Direct Offers is a paid format inside AI Mode. Organic product selection is described as relevance-based.
- Limitations: The "Sponsored deal" label text comes from an image caption. Pilot scope (U.S.? advertisers) not stated in this excerpt. No Gemini-app mention.

### GA-26 Direct Offers expansion (May 2026): promotion bundling built by Gemini, UCP native checkout, travel; offers "naturally surface in the AI Mode response"
- Claim: At GML 2026 (2026-05-20) Google expanded the Direct Offers pilot: Gemini constructs deals/bundles; UCP merchants get native checkout; travel partners join. Direct Offers will "naturally surface in the AI Mode response". New AI Mode ad tests: Conversational Discovery ads and Highlighted Answers (ads eligible to appear on AI Mode recommendation lists), with Gemini-written "independent AI explainer", labeled "Sponsored". AI-powered Shopping ads (Gemini-written explainer) come to Search.
- Classification: VERIFIED FACT (announcement; "coming soon" items unverified as live)
- Surface: AI Mode, Search
- Source: A new generation of ads for the AI era of Search — Google (The Keyword, Ads & Commerce) — https://blog.google/products/ads-commerce/google-marketing-live-search-ads/
- Published/updated: 2026-05-20
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Highlighted Answers: When people are researching, they want helpful suggestions. Now, when AI Mode provides a list of recommendations — like the best language apps for an upcoming trip — highly relevant, high-quality ads are eligible to appear on that list as a Highlighted Answer."
- Excerpt: > "To help people evaluate their choices, both of these new formats will feature an independent AI explainer as part of the ad. Our Gemini model evaluates and synthesizes information about a product or service, and displays that context alongside the advertiser’s creative. This coherent, independent response ensures transparency and builds trust. These formats will also continue to be clearly labeled as “Sponsored.”"
- Excerpt: > "Since launching the Direct Offers pilot in January 2026, brands like Chewy, Gap and L’Oreal have surfaced highly relevant deals as shoppers explore their options."
- Excerpt: > "Native checkout: We’ve added native checkout integration for Universal Commerce Protocol (UCP) merchants. This gives shoppers a faster way to secure promotions, helping merchants seamlessly turn high-intent research into completed sales."
- Excerpt: > "With these updates, Direct Offers will now naturally surface in the AI Mode response as shoppers explore options, making deals more instantly discoverable."
- Excerpt: > "Now, if someone searches for an espresso machine, Gemini will pull up your most relevant products and instantly write a custom explainer highlighting why your product may be the right choice for them."
- Establishes: Ads can be placed inside AI Mode recommendation lists (Highlighted Answers, test). This narrows the visual gap between organic and paid items; separation rests on the "Sponsored" label.
- Limitations: Test formats; live status as of 2026-10-30 not confirmed by a later source. No Gemini-app ad format announced here.

### GA-27 Gemini app ads: Google states Gemini Apps chats "are not being used to show you ads"; cart and Google Pay data can be used for ads per settings
- Claim: The Gemini Apps Privacy Hub (updated 2026-10-26) says Gemini chats are not used to show ads and promises notice if this changes. Cart/order data added from Gemini is stored in Google Wallet and can be used "for personalization and ads (depending on your settings)". No primary source found that announces an ad format in the Gemini app.
- Classification: VERIFIED FACT (statement); absence of Gemini-app ads = EVIDENCE-BASED INFERENCE (no announcement found; not an exhaustive check)
- Surface: Gemini app
- Source: Gemini Apps Privacy Hub — Google (Gemini Apps Help) — https://support.google.com/gemini/answer/13594961?hl=en
- Published/updated: "Last updated: October 26, 2026"
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Your Gemini Apps chats are not being used to show you ads. If this changes, we will clearly communicate it to you."
- Excerpt: > "When you add products to your Google shopping cart from Gemini, cart and order data is saved to your Google Wallet. This data is used in accordance with the Google Terms and Privacy Policy, and your Wallet settings, including for personalization and ads (depending on your settings)."
- Establishes: As of 2026-10-26 Google states Gemini chat content does not drive ads. Shopping actions taken from Gemini (cart, Google Pay) can feed ads elsewhere.
- Limitations: "Chats not used to show ads" is narrower than "no ads in Gemini". Press reports (Tier 3, not fetched) describe Google executives as "open" to Gemini ads in 2026 — unverified here.

### GA-28 Gemini app grounding: "some Gemini responses are grounded on Search results"; Gemini always may use public Google Search info
- Claim: Google states some Gemini responses are grounded on Search results. Gemini automatically uses public information from Google Search (always, even signed out or Keep Activity off), Flights, Hotels, Maps and YouTube. Shopping answers use the Shopping Graph (GA-16).
- Classification: VERIFIED FACT (statement); product-query grounding pipeline undocumented
- Surface: Gemini app
- Source: Gemini Apps Privacy Hub — https://support.google.com/gemini/answer/13594961?hl=en (updated 2026-10-26); Use & manage Connected Apps in Gemini — https://support.google.com/gemini/answer/13695044?hl=en (not stated)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (13594961): > "We rely on other Google services and infrastructure to provide Gemini Apps. For example, some Gemini responses are grounded on Search results."
- Excerpt (13695044): > "Gemini automatically uses public information from certain Google services, including:"
- Excerpt (13695044): > "To use public information from Google Flights, Google Hotels, Google Maps, and YouTube, Keep Activity must be on. Gemini can always use public information from Google Search, even if Keep Activity is off or you’re signed out."
- Establishes: Search grounding exists in the Gemini app. Shopping help names the Shopping Graph, not Search results, as the shopping data source.
- Limitations: No Google document states whether product queries in the Gemini app are grounded on Search web results, on the Shopping Graph only, or both. "Google Shopping" is not in the list of services Gemini uses public info from. Gap.

### GA-29 Gemini Personal Intelligence: Search services data (incl. Shopping), Gmail, Wallet (U.S.), YouTube, Photos; not in EEA, Switzerland, UK, Nigeria
- Claim: Personal Intelligence in the Gemini app can connect Contacts, Google Photos, Google Wallet (U.S. only), Google Workspace (Gmail, Calendar, Drive), Search services (Search incl. AI Mode, Maps, Shopping, etc.) and YouTube. It can make recommendations from preferences. Not available in the EEA, Nigeria, Switzerland or the UK.
- Classification: VERIFIED FACT
- Surface: Gemini app
- Source: Connect your Google apps to personalize your Gemini experience — Google (Gemini Apps Help) — https://support.google.com/gemini/answer/16598406?hl=en ; About personalization with Connected Apps — https://support.google.com/gemini/answer/16836988?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (16598406): > "Do things for you, like make recommendations based on your preferences, or create a tailored itinerary."
- Excerpt (16598406): > "Search services, which includes your saved data in services like Search, Maps, and Shopping."
- Excerpt (16598406): > "Google Wallet (in the US only), which includes your payment methods, receipts, data from Google services saved in Wallet, and financial account info linked with services such as Plaid."
- Excerpt (16598406): > "Not available in the European Economic Area, Nigeria, Switzerland, or the United Kingdom."
- Excerpt (16836988): > "Google Search services, which include Search (including AI Mode and Discover), Maps (excluding Timeline), Shopping, Flights, Hotels, Translate, and News"
- Establishes: Gemini can personalize shopping recommendations from Shopping/Search history and Gmail (with opt-in). India is not in the exclusion list.
- Limitations: India availability of Personal Intelligence is not stated positively. No document describes how personal context changes product ranking.

### GA-30 AI Mode Personal Intelligence: uses Search Services History; Gmail, Calendar, Photos connections; Jan 2026 launch stated "recommendations for things like shopping"
- Claim: AI Mode personalization uses Search Services History (18+, history and personalized recommendations on). Users can connect Gmail, Google Calendar and Google Photos. The Jan 2026 launch named shopping recommendations as a use.
- Classification: VERIFIED FACT
- Surface: AI Mode
- Source: Get AI-powered responses with AI Mode in Google Search — Google (Google Search Help) — https://support.google.com/websearch/answer/16011537?hl=en ; The latest AI news we announced in January — Google (The Keyword) — https://blog.google/innovation-and-ai/products/google-ai-updates-january-2026/
- Published/updated: help page not stated; recap 2026-02-04
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (16011537): > "Personal Intelligence in AI Mode references previous searches and activity saved in your Search Services History to provide suggestions tailored to your tastes and preferences."
- Excerpt (16011537): > "Note: Consenting to this experience means that all Search services will be permitted to access Workspace and Google Photos. Search services include Google Search (incl. AI Mode, Discover), Maps, Shopping, News, Flights, Hotels, and Translate."
- Excerpt (recap): > "Starting with Google AI Pro and Ultra subscribers, you can securely opt-in and connect AI Mode to apps like Gmail and Google Photos for responses that are tailored just for you, including recommendations for things like shopping and travel."
- Establishes: AI Mode shopping responses can be personalized from search history and connected Gmail/Photos. Connecting grants the Shopping service access too.
- Limitations: Mechanism (re-ranking vs. query rewriting) undocumented. Subscriber-only in Jan 2026; expanded to ~200 countries free in May 2026 (GA-14).

### GA-31 AI Mode mechanism: "query fan-out" across multiple data sources; available in India and in Hindi and 10+ other Indian languages
- Claim: AI Mode splits a question into subtopics and searches each "across multiple data sources", then synthesizes. AI Mode is available in India; supported languages include Hindi, Bengali, Gujarati, Kannada, Malayalam, Marathi, Odia, Punjabi, Tamil, Telugu, Urdu (and others).
- Classification: VERIFIED FACT
- Surface: AI Mode
- Source: Get AI-powered responses with AI Mode in Google Search — Google (Google Search Help) — https://support.google.com/websearch/answer/16011537?hl=en
- Published/updated: not stated (mentions Gemini 4 Argon, so updated on/after 2026-10-13)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "AI mode uses a “query fan-out” technique, dividing your question into subtopics and searching for each one simultaneously across multiple data sources. It then brings those results together to provide an easy-to-understand response."
- Excerpt: > "AI Mode relies on Google Search's deep understanding of web information, meaning that responses are supported by high quality web content to improve factuality."
- Excerpt (language list items, verbatim): "Bengali", "Gujarati", "Hindi", "Kannada", "Malayalam", "Marathi", "Odia", "Punjabi", "Tamil", "Telugu", "Urdu"; country list includes "India".
- Establishes: AI Mode (general) works in Hindi and other Indian languages in India.
- Limitations: General AI Mode language support ≠ shopping-experience language support. GA-15 says AI Mode shopping in India is English with Hindi "soon". The "multiple data sources" are not enumerated (Shopping Graph not named on this page).

### GA-32 AI Overviews availability includes India and Indian languages; AI Overviews → AI Mode follow-up flow
- Claim: AI Overviews are available in India and in Bengali, Hindi, Marathi, Tamil, Telugu (among others). Users can continue from an AI Overview into AI Mode.
- Classification: VERIFIED FACT
- Surface: AI Overviews
- Source: Find information in faster & easier ways with AI Overviews in Google Search — Google (Google Search Help) — https://support.google.com/websearch/answer/14901683?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "You'll find AI Overviews in your Google Search results when our systems determine that generative AI can be especially helpful – for example, when you want to quickly understand information from a range of sources."
- Excerpt: > "You can now seamlessly transition from an AI Overview to a deeper conversation in AI Mode. This feature is available on mobile devices in all regions and languages where AI Overviews and AI Mode are supported."
- Excerpt (list items, verbatim): "India"; "Bengali", "Hindi", "Marathi", "Tamil", "Telugu".
- Establishes: AI Overviews exist for Indian users in several Indian languages.
- Limitations: The help page says nothing about product cards or shopping data in AI Overviews. Shopping-specific AI Overviews behavior is documented only indirectly (GA-19, GA-24).

### GA-33 Agentic checkout ("Buy for me with GPay"): price-tracking-triggered purchase on merchant site; U.S. and Australia (conflicting); BNPL in Gemini and AI Mode (U.S.)
- Claim: Agentic checkout buys a tracked item on the merchant's website via Google Pay after user confirmation when the target price is reached. The Google Pay help page says U.S. and Australia (English, select merchants) at the top, and "only in the US" in its troubleshooting section. BNPL with agentic checkout is U.S.-only and limited to select purchases in Gemini and AI Mode.
- Classification: VERIFIED FACT (statements); country scope contradictory within the source
- Surface: Search incl. AI Mode, Gemini app
- Source: About Agentic checkout with Google Pay — Google (Google Pay Help) — https://support.google.com/googlepay/answer/16421147?hl=en ; About price tracking on Google — Google (Google Shopping Help) — https://support.google.com/googleshopping/answer/13971184?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (16421147): > "This feature is currently only available in the US and Australia, in English and for select merchants that accept Google Pay as a payment method."
- Excerpt (16421147): > "This feature is currently available only in the US, in English, and with select merchants that accept Google Pay as a payment method."
- Excerpt (16421147): > "Important: Buy now, pay later is currently only available for users in the US. This feature is also limited to select purchases within Gemini and AI Mode in Search, and for transactions made in US dollars."
- Excerpt (16421147): > "If the price goes up, the purchase won't go through, and you won't be charged. Agentic checkout is designed to buy the product if the final price is the same as, or lower than the total price you confirmed."
- Excerpt (13971184): > "In certain situations, you may find a "Buy for me with GPay" button for products you track like this: ."
- Excerpt (13971184): > "Behind the scenes, our agentic checkout feature will then make the purchase from the merchant's website on your behalf with Google Pay."
- Establishes: Agentic checkout (2025 design) operates on the merchant's website, distinct from UCP native checkout on Google. No India availability.
- Limitations: Internal contradiction on Australia. Whether agentic checkout has been folded into UCP / Universal Cart is not stated.

### GA-34 Price tracking available in U.S., Canada, Australia, Japan and India
- Claim: Google's Track Price feature is available in the U.S., Canada, Australia, Japan and India.
- Classification: VERIFIED FACT
- Surface: Search / Shopping (Google app and web)
- Source: About price tracking on Google — Google (Google Shopping Help) — https://support.google.com/googleshopping/answer/13971184?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Price tracking is available in the United States, Canada, Australia, Japan, and India. We’re rolling out updates to price tracking. All features may not be available on all devices or Google surfaces."
- Establishes: India has price tracking but not agentic checkout (GA-33).
- Limitations: Not stated for the Gemini app specifically.

### GA-35 Virtual Try-On: 18 countries incl. India; uses images found via Google Image Search; not available on Shopping ads
- Claim: Google Try-On works in 18 countries including India, on Google Shopping, Search and Images, for signed-in 18+ users with Search Services History and Personalized Recommendations on. It uses images found via Google Image Search; "Sponsored" products lack the button. U.S. users can create a Nano Banana avatar.
- Classification: VERIFIED FACT
- Surface: Shopping / Search (AI Mode not named)
- Source: How the Google Try-On tool works — Google (Google Shopping Help) — https://support.google.com/googleshopping/answer/16253678?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Be in Argentina, Australia, Brazil, Canada, Chile, Colombia, Hong Kong, India, Indonesia, Japan, Malaysia, Mexico, New Zealand, Philippines, Singapore, South Korea, UK, or the US."
- Excerpt: > "This feature is not available for Shopping Ads so products under “Sponsored” will not have the “Try it on” button."
- Excerpt: > "Google Try-On uses images found on websites through Google Image Search. To request the removal of your domain's images from Try-On, complete the opt-out form."
- Establishes: Try-On draws on the web image index, not only feeds. India is supported.
- Limitations: Does not say whether Try-On is offered inside AI Mode or the Gemini app. (Gemini outfit visualization by photo upload is a separate image-generation use, see stylist post 2026-10-19 — not a shopping feature.)

### GA-36 "Let Google Call": Duplex + Gemini call nearby stores for stock/price/deals; U.S. English, excluding 5 states
- Claim: For "near me" product searches, Google calls stores (Duplex + Gemini), then emails/texts a summary plus Shopping Graph local inventory. U.S. English only; not in Indiana, Louisiana, Minnesota, Montana, Nebraska. Most apparel and grocery not supported.
- Classification: VERIFIED FACT
- Surface: Search (AI Mode not named in help page)
- Source: Ask Google to call nearby stores for you — Google (Google Shopping Help) — https://support.google.com/googleshopping/answer/16742225?hl=en ; Let AI do the hard parts of your holiday shopping — https://blog.google/products-and-platforms/products/shopping/agentic-checkout-holiday-ai-shopping/ (2025-11-13)
- Published/updated: help page not stated; blog 2025-11-13
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (help): > "This feature supports English queries from signed-in customers on Search in the US, except in these states:"
- Excerpt (help): > "You get an email or text with a summary of the calls made on your behalf. It shows whether nearby stores have the items you need, the price, any available offers, and additional inventory from stores listed in Google Shopping Graph."
- Excerpt (blog): > "This feature is powered by our Duplex technology, with a big Gemini model upgrade that helps us identify the best stores to call, suggest helpful questions to ask based on the product you want and summarize the conversations into key takeaways."
- Establishes: Store phone calls are a live data source for local availability in U.S. Search.
- Limitations: No India availability. Not documented in the Gemini app.

### GA-37 Nov 2025 baseline: AI Mode shopping upgrade, Gemini app shopping (U.S.), agentic checkout (U.S., incl. AI Mode)
- Claim: On 2025-11-13 Google launched (U.S.) upgraded AI Mode shopping (price, reviews, inventory, shoppable images, comparison tables with review insights), Gemini app shopping powered by the Shopping Graph, Let Google Call and agentic checkout on Search incl. AI Mode with Wayfair, Chewy, Quince and select Shopify merchants.
- Classification: VERIFIED FACT
- Surface: AI Mode, Gemini app, Search
- Source: Let AI do the hard parts of your holiday shopping — Google (The Keyword) — https://blog.google/products-and-platforms/products/shopping/agentic-checkout-holiday-ai-shopping/
- Published/updated: 2025-11-13
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "When you ask AI Mode a shopping question, you’ll get an intelligently organized response that brings together rich visuals and all the details you need (like price, reviews and inventory info), helping you quickly and confidently decide what to buy. AI Mode responses are tailored to your specific question and formatted for your needs."
- Excerpt: > "And because AI Mode is powered by the Shopping Graph (which includes more than 50 billion product listings, 2 billion of which are updated every hour) you can trust you’re seeing fresh information and unmatched selection."
- Excerpt: > "You can find shoppable product listings, comparison tables, prices from across the web and places to buy right in the Gemini app. This is available to all Gemini users in the U.S. starting today — simply ask a shopping-related question to get started."
- Excerpt: > "If the merchant is eligible, we'll now give you the option to have Google buy it for you on the merchant's site using Google Pay. We’ll always ask for your permission first, and only buy after you’ve confirmed the purchase and shipping details."
- Excerpt: > "Agentic checkout is starting to roll out now on Search, including in AI Mode, from eligible merchants in the U.S. like Wayfair, Chewy, Quince and select Shopify merchants, with many more coming soon."
- Establishes: AI Mode is explicitly "powered by the Shopping Graph". Gemini app shopping started U.S.-only on 2025-11-13; by Oct 2026 it covers 21 countries (GA-16).
- Limitations: Superseded in parts (Shopping Graph size, Gemini country scope). "Prices from across the web" wording suggests web-sourced offers; mechanism undocumented.

### GA-38 Business Agent: brand-voiced chat agent on Search (U.S., Jan 2026); Merchant Center conversational attributes for AI Mode, Gemini, Business Agent
- Claim: Business Agent lets shoppers chat with a retailer's branded agent on Search (live 2026-01-12 with Lowe's, Michael's, Poshmark, Reebok; eligible U.S. retailers). Google announced "dozens of new data attributes" in Merchant Center for discovery "on surfaces like AI Mode, Gemini and Business Agent", including product Q&A, compatible accessories and substitutes.
- Classification: VERIFIED FACT
- Surface: Search, AI Mode, Gemini app
- Source: New tech and tools for retailers to succeed in an agentic shopping era — Google (The Keyword) — https://blog.google/products/ads-commerce/agentic-commerce-ai-tools-protocol-retailers-platforms/
- Published/updated: 2026-01-11
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "We’re also launching Business Agent, a new way for shoppers to chat with brands, right on Search. It’s like a virtual sales associate that can answer product questions in a brand’s voice, enabling retailers to connect with consumers during critical shopping moments and help drive sales."
- Excerpt: > "That’s why we’re announcing dozens of new data attributes in Merchant Center designed for easy discovery in the conversational commerce era, on surfaces like AI Mode, Gemini and Business Agent. These new attributes complement retailers’ existing data feeds and go beyond traditional keywords to include things like answers to common product questions, compatible accessories or substitutes."
- Excerpt: > "To start, UCP will soon power a new checkout feature on eligible Google product listings in AI Mode in Search and the Gemini app, allowing shoppers to check out from eligible U.S. retailers right as they’re researching on Google. The feature is built with security at its core: shoppers can buy confidently with Google Pay using payment methods and shipping info already saved in Google Wallet and soon, will be able to make a purchase with PayPal."
- Establishes: Merchant Center feed attributes are a stated discovery input for both AI Mode and the Gemini app. UCP checkout started with "eligible U.S. retailers".
- Limitations: "Designed for easy discovery" is a goal statement, not a ranking disclosure. PayPal "soon" not confirmed later.


### GA-39 I/O 2025 origin: AI Mode shopping = Gemini + Shopping Graph; "50 billion" listings, "2 billion" refreshed hourly; query fan-out for product criteria; panel "personalized to your tastes"
- Claim: On 2025-05-20 Google described AI Mode shopping as Gemini plus the Shopping Graph (50B+ listings, 2B+ refreshed each hour). AI Mode runs a query fan-out to derive product criteria, then suggests products; a right-hand panel of images and listings is "personalized to your tastes". Agentic checkout ("buy for me") adds the item to the merchant-site cart and checks out with Google Pay.
- Classification: VERIFIED FACT (statement); fan-out-to-ranking mechanism undocumented
- Surface: AI Mode
- Source: Shop with AI Mode, use AI to buy and try clothes on yourself virtually — Google (The Keyword) — https://blog.google/products-and-platforms/products/shopping/google-shopping-ai-mode-virtual-try-on-update/
- Published/updated: 2025-05-20
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Our new AI Mode shopping experience brings together Gemini capabilities with our Shopping Graph to help you browse for inspiration, think through considerations and narrow down products. The Shopping Graph now has more than 50 billion product listings, from global retailers to local mom and pop shops, each with details like reviews, prices, color options and availability. And you know you’re getting fresh and accurate information you can trust, because every hour more than 2 billion of those product listings are refreshed on Google."
- Excerpt: > "It understands that you’re looking for visual inspiration and so it will show you a beautiful, browsable panel of images and product listings personalized to your tastes."
- Excerpt: > "If you want to narrow your options down to bags suitable for a trip to Portland, Oregon in May, AI Mode will start a query fan-out, which means it runs several simultaneous searches to figure out what makes a bag good for rainy weather and long journeys, and then use those criteria to suggest waterproof options with easy access to pockets."
- Excerpt: > "Behind the scenes, we’ll add the item to your cart on the merchant's site and securely complete the checkout on your behalf with Google Pay."
- Establishes: The "50 billion / 2 billion every hour" lead is verified; first stated 2025-05-20. AI Mode derives attribute criteria from fan-out searches before selecting products.
- Limitations: Superseded on size (GA-03). The panel UI may have changed since 2025.

### GA-40 Search Central: AI Overviews and AI Mode "may use different models and techniques"; both may fan out "across subtopics and data sources"; Merchant Center info listed as best practice
- Claim: Google's developer documentation states AI Overviews and AI Mode can use different models and techniques, so their responses and links vary. Both may use query fan-out across subtopics and data sources. Keeping Merchant Center and Business Profile info up to date is listed among SEO fundamentals.
- Classification: VERIFIED FACT
- Surface: AI Overviews, AI Mode
- Source: AI features and your website — Google Search Central — https://developers.google.com/search/docs/appearance/ai-features
- Published/updated: "Last updated 2025-12-10 UTC."
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "Both AI Overviews and AI Mode may use a "query fan-out" technique — issuing multiple related searches across subtopics and data sources — to develop a response."
- Excerpt: > "AI Mode and AI Overviews may use different models and techniques, so the set of responses and links they show will vary."
- Excerpt: > "Checking that your Merchant Center and Business Profile information is up-to-date"
- Establishes: Google itself says AI Overviews and AI Mode are not one identical pipeline. Supports reporting them separately even after the May 2026 UI merge (GA-13).
- Limitations: Page predates the May 2026 merge. Product-result selection is not described.

### GA-41 India AI Mode languages (Oct 2025): English and Hindi first; Bengali, Kannada, Malayalam, Marathi, Tamil, Telugu, Urdu added; "comparing products" named as a use
- Claim: Google India stated AI Mode launched in English and Hindi in India and expanded to seven more Indian languages from 2025-10-08. Search Live in AI Mode came to India in English and Hindi.
- Classification: VERIFIED FACT
- Surface: AI Mode
- Source: Supercharging Search for India: New Languages in AI Mode & Search Live debuts — Google India (The Keyword, en-in) — https://blog.google/intl/en-in/products/supercharging-search-for-india-new-languages-in-ai-mode-search-live-debuts/
- Published/updated: 2025-10-08
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "The response since launching in English and Hindi across India has been incredible, with people already using it for a wide range of needs, from help with education and writing to comparing products and planning trips."
- Excerpt: > "To help millions more people in India ask complex questions in their preferred language, we’re rolling out AI Mode in Bengali, Kannada, Malayalam, Marathi, Tamil, Telugu, and Urdu."
- Establishes: AI Mode (general) supports nine Indian languages in India.
- Limitations: General AI Mode language support, not shopping-module language support (see GA-15: AI Mode shopping English, Hindi "soon" as of 2026-04-07).

### GA-42 India (Sep 2026, Think with Google): ads inside AI Mode and Direct Offers marketed to Indian advertisers; Flipkart "already partnering" on UCP agentic checkout
- Claim: Google's India GML 2026 recap tells Indian marketers to "Reach shoppers with ads directly inside AI Mode" and use Direct Offers. It states Flipkart is "already partnering with Google" to offer the UCP agentic experience to Indian shoppers. It cites AI Overviews at 2.5B+ monthly users.
- Classification: VERIFIED FACT (statement); India live status of Direct Offers and UCP checkout not stated
- Surface: AI Mode, AI Overviews, Gemini app
- Source: Google Marketing Live: What’s next for marketers in India (page title "Win AI search-powered shoppers in India") — Think with Google APAC (Google) — https://business.google.com/en-all/think/future-of-marketing/google-marketing-live-india-ai-search/
- Published/updated: "September 2026"
- Accessed: 2026-10-30
- Tier: 1 (Google-owned marketing page)
- Excerpt: > "Convert AI Search users efficiently. Reach shoppers with ads directly inside AI Mode. And to win their purchase, use Direct Offers, which dynamically trigger custom discounts when purchase intent peaks."
- Excerpt: > "Agentic commerce: To enable Gemini users’ agents to securely complete checkout and buy your eligible products in Google, we’ve introduced the Universal Commerce Protocol (UCP), an open standard for agentic commerce. The UCP acts as a universal translator between merchants’ inventories and AI agents. Merchants like Flipkart are already partnering with Google to offer this agentic experience to Indian shoppers, and help brands grow sales."
- Excerpt: > "There are billions of enticing reasons to do so: AI Overviews has over 2.5 billion monthly users, while AI Mode has surpassed 1 billion monthly users."
- Establishes: Google positions UCP agentic checkout and AI Mode ads for India. Flipkart is the only named Indian UCP partner (also a UCP endorser in GA-38's source list: "Flipkart").
- Limitations: Marketing page. Does not state that Direct Offers or UCP checkout is generally available in India, nor payment method (no UPI/INR mention). Universal Cart help says U.S. only (GA-18).

### GA-43 India Flipkart "Buy" test in Gemini and AI Mode (press, Sep 2026)
- Claim: TechCrunch reports a limited test (from ~2026-09-26) where some Indian users see a Buy button on select Flipkart listings in Gemini and AI Mode, opening a Flipkart-branded checkout. Amazon listings appeared without Buy. Broader rollout reportedly planned "later in October". Google spokesperson gave a generic testing statement.
- Classification: VERIFIED FACT (press statement only; Tier 3; Google has not confirmed details) — Confidence Low
- Surface: Gemini app, AI Mode
- Source: Google tests buying from Walmart-owned Flipkart through Gemini and AI Mode in India — TechCrunch — https://techcrunch.com/2026/09/26/google-tests-buying-from-walmart-owned-flipkart-through-gemini-and-ai-mode-in-india/
- Published/updated: 2026-09-26
- Accessed: 2026-10-30
- Tier: 3
- Excerpt: > "Users in the test see a Buy button on select Flipkart product listings appearing in Gemini and Google’s AI Mode, which takes them directly to a Flipkart checkout flow without leaving the AI interface, according to people familiar with the matter and as seen by TechCrunch."
- Excerpt: > "Asked about the Flipkart test, a Google spokesperson told TechCrunch the company is “always testing new features and experiences to help people discover and connect with businesses more easily.”"
- Establishes: An India in-chat purchase test was reported. It appears to differ from Google-hosted UCP checkout (merchant-branded flow).
- Limitations: Anonymous sourcing. Wider October rollout not verified. No Google primary source fetched for the test. Google has a disclosed investment in Flipkart (per TechCrunch).

### GA-44 Australia UCP checkout launch (press, June 2026)
- Claim: Australian trade press reports Google launched UCP in Australia (~2026-06-17) with Kogan, Bunnings, Adore Beauty, Petbarn and THE ICONIC, enabling single-item purchases within Search incl. AI Mode and the Gemini app.
- Classification: VERIFIED FACT (press statement only; Tier 3; no Google primary found) — Confidence Low
- Surface: AI Mode, Gemini app
- Source: Google taps top Aussie retailers in AI shopping rollout — Inside Retail Australia — https://insideretail.com.au/digital/ecommerce/google-taps-top-aussie-retailers-in-ai-shopping-rollout-202606
- Published/updated: 2026-06-17 (page metadata)
- Accessed: 2026-10-30
- Tier: 3
- Excerpt: > "With the likes of Kogan, Bunnings, Adore Beauty, Petbarn, and The Iconic involved, shoppers will be able to make single-item purchases directly within Google search, including AI Mode, and the Gemini app."
- Establishes: Non-U.S. UCP checkout likely began in Australia mid-2026.
- Limitations: Conflicts with Google's 2026-09-16 wording that hub capabilities reach Australia "early next year" (GA-08) — the two may refer to different things (checkout vs. hub features). Google en-au blog primary not found.

### GA-45 Merchant Center UCP help: product eligibility U.S., Canada, Australia; "Buy" only for listings with native_commerce attribute; UCP checkout on Google vs. agentic checkout on merchant site
- Claim: Google's Merchant Center help says UCP checkout applies to products with eligibility in the U.S., Canada and Australia. Only listings using the `native_commerce` (checkout_eligibility) attribute show the "Buy" button. Agentic checkout buys on the merchant's website; UCP checkout happens on Google's surfaces with the merchant as merchant of record. Payments use FPANs stored in Google Wallet.
- Classification: VERIFIED FACT
- Surface: AI Mode, Gemini app
- Source: About the Universal Commerce Protocol (UCP) and UCP-powered checkout feature on Google — Google (Merchant Center Help) — https://support.google.com/merchants/answer/16837055?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "This article only applies to products with eligibility in the United States, Canada, and Australia, and for participating merchants and partners. You may see this checkout experience soon on specific surfaces such as AI Mode in Search and Gemini."
- Excerpt: > "Only product listings using the native_commerce(checkout_eligibility) product attribute will display the “Buy” button for this checkout experience."
- Excerpt: > "Google’s agentic checkout feature buys things on the customer’s behalf directly on a merchant’s website at the customer’s direction. UCP is the open protocol which standardizes the programmatic exchange of information (via API, MCP or A2A) between the AI Agent and the Merchant’s backend to enable a broad set of commerce journeys including product discovery and checkout on Google AI Mode and Gemini."
- Excerpt: > "Currently, the feature uses standard Funding Primary Account Numbers (FPANs) that users have stored on their Google Wallet. More forms of payments may become available in the future."
- Establishes: Two distinct buy mechanisms exist: agentic checkout (merchant site, 2025) and UCP native checkout (on Google, 2026). The Buy button is gated by a Merchant Center product attribute. India is not an eligible country on this page.
- Limitations: "soon" wording looks stale against GA-08 (live at scale Sep 2026). Merchant-facing page.

### GA-46 Gemini in Chrome auto browse launched in India (Oct 2026): agentic tasks incl. "order groceries"; AI Pro/Ultra; English-set devices
- Claim: Gemini in Chrome reached all Android users in India, and auto browse (agentic) is available on desktop and Android to AI Pro and AI Ultra subscribers in India. Google gives "order groceries for the week" as an example task. Auto browse asks confirmation before some sensitive tasks; limited to English-set devices.
- Classification: VERIFIED FACT
- Surface: Gemini (in Chrome) — listed as a Gemini shopping surface in GA-16
- Source: Bringing Gemini in Chrome with auto browse to India — Google India (The Keyword, en-in) — https://blog.google/intl/en-in/products/bringing-gemini-in-chrome-with-auto-browse-to-india/
- Published/updated: 2026-10-07
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "At the same time, we’ve also made Gemini in Chrome’s auto browse feature available on desktop and Android for AI Pro and AI Ultra subscribers in India"
- Excerpt: > "Auto browse can handle tedious everyday tasks for you, helping you do things like book parking for an event, fill out a long form, or order groceries for the week."
- Excerpt: > "Gemini in Chrome’s agentic feature, autobrowse, is currently limited to devices set to English, with upcoming plans to release more languages in the near future."
- Establishes: The only Google-documented agentic purchase-capable feature live in India (browser automation on merchant sites, paid tiers).
- Limitations: Not a Shopping Graph or UCP feature. Does not document product selection.

### GA-47 Gemini Spark (agent): announced 2026-05-20; payment authorization with budget/merchant limits "down the line"; AP2 to start with Spark; July 2026 web errands with saved passwords
- Claim: Gemini Spark is a background personal agent (trusted testers, then U.S. AI Ultra beta). Google said Spark would later "authorize payments while specifying the budget and merchants" and that AP2 would come to Google products starting with Spark. In July 2026 Spark gained web errands using logged-in accounts and saved passwords.
- Classification: VERIFIED FACT (announcements); live purchase capability not verified
- Surface: Gemini app
- Source: 100 things we announced at Google I/O 2026 — https://blog.google/innovation-and-ai/technology/ai/google-io-2026-all-our-announcements/ (2026-05-20); The latest AI news we announced in July 2026 — https://blog.google/innovation-and-ai/technology/ai/google-ai-updates-july-2026/ (2026-08-04)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (I/O): > "Down the line, we’ve got a packed roadmap of features for Google Spark that we’ll be shipping throughout the summer. For example: You’ll be able to text or email Spark directly, create custom sub-agents and even authorize payments while specifying the budget and merchants."
- Excerpt (July recap): > "Now, with your permission, Spark can use your logged-in accounts and saved passwords to handle tedious web errands, like scheduling viewings for apartments or researching flight options and starting the booking process."
- Establishes: Gemini's agent roadmap includes budget/merchant-constrained purchasing via AP2.
- Limitations: No fetched source confirms Spark payments or AP2 are live as of 2026-10-30. No India statement for Spark.

### GA-48 Top Quality Store badge: Google scores merchant shipping/returns policies, user ratings and website quality
- Claim: Google awards a Top Quality Store badge using merchant-submitted experience data (shipping, returns), user ratings and checks of the merchant's website quality and accessibility.
- Classification: VERIFIED FACT; ranking effect undocumented
- Surface: Shopping / Search
- Source: About the Top Quality Store badge — Google (Google Shopping Help) — https://support.google.com/googleshopping/answer/11115998?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt: > "To make a store Top Quality, Google asks businesses for data on certain experience categories when you shop, like shipping and returns policies, among others. Google also checks user ratings and the business’s website to measure its quality and accessibility."
- Excerpt: > "To estimate the expected quality of a shopping experience, Google considers all of that info together. The businesses with the highest ratings earn the Top Quality Store badge."
- Establishes: Google computes a merchant-quality estimate. It is displayed as a badge.
- Limitations: Page does not say the quality estimate affects ranking on any surface. Treating it as a ranking factor would be an UNVERIFIED HYPOTHESIS.

## Per-surface summary (index into findings; no new claims)

| Question | Gemini app | AI Mode | AI Overviews | Shopping tab / Search |
|---|---|---|---|---|
| What shows | Product cards, theme groups, comparisons, links, Buy button on web (GA-16, GA-17) | Shoppable images, comparison tables, price/reviews/inventory, sponsored + organic product list items (GA-37, GA-15, GA-12) | Ranked lists stated non-sponsored; ads in labeled sections (GA-19, GA-24) | Ranked listings, Top recommendations, Try-On, price tracking (GA-20, GA-21, GA-35, GA-34) |
| Data source stated | Shopping Graph (GA-16, GA-05); some answers grounded on Search (GA-28) | Shopping Graph (GA-37, GA-39); fan-out across data sources (GA-31, GA-40) | Shopping Graph for gen-AI features (GA-19); fan-out (GA-40) | Seller feeds via Merchant Center / Manufacturer Center (GA-19, GA-20) |
| Ranking factors documented | None product-specific | None product-specific; organic = "Search quality and ranking systems" (GA-24) | Same statement as AI Mode (GA-24) | Relevance, search terms, activity; Top recommendations = relevance, ratings, price, features; ads = bid + relevance (GA-20, GA-21, GA-22) |
| Checkout | UCP Buy (web), Universal Cart (U.S.) (GA-17, GA-18) | Agentic checkout (U.S.), UCP Buy, Universal Cart (U.S.) (GA-33, GA-06, GA-01) | Not documented | Agentic checkout via price tracking (GA-33) |
| Ads | Chats "not being used to show you ads" (GA-27) | Sponsored ads, Direct Offers, Highlighted Answers test, multiturn ads (U.S.) (GA-12, GA-25, GA-26) | Sponsored ads within/above/below (GA-24) | Sponsored Shopping ads (GA-20, GA-22) |
| India | Shopping: yes (EN, HI) (GA-15, GA-16); checkout: Flipkart test only, press (GA-43) | Yes; shopping EN, Hindi "soon" as of 2026-04-07 (GA-15); ads since 2026-10-28 (GA-12) | Yes; ads within, English (GA-24, GA-32) | Price tracking, Try-On, saved preferences: yes (GA-34, GA-35, GA-23); agentic checkout: no (GA-33) |

## Contradictions and superseded information

- Shopping Graph size: "more than 50 billion" listings / "more than 2 billion" refreshed hourly (GA-39 2025-05-20; GA-37 2025-11-13; GA-05 2026-01-11; Google India GA-15 2026-04-07) vs. "over 60 billion" (GA-03, 2026-05-19) and "60+ billion continually refreshed" (GA-01, 2026-10-15). The 60B figure supersedes. No hourly-refresh number is restated after April 2026. The India post predates the 60B figure by six weeks, so it is outdated now, not contradictory at publication.
- Universal Cart U.S. timing: "this summer" (GA-04, 2026-05-19) vs. actual U.S. launch 2026-10-15 (GA-01).
- AI Overviews vs. AI Mode: UI merged into "one, seamless AI Search experience" (GA-13, 2026-05-20), but Search Central says they "may use different models and techniques" (GA-40, 2025-12-10). The UI merge does not establish a shared retrieval or ranking pipeline.
- Agentic checkout country scope: the same Google Pay help page says "US and Australia" in its header and "only in the US" in its troubleshooting section (GA-33). One section is stale; which one is unknown.
- UCP checkout status: Merchant Center help says users "may see this checkout experience soon" (GA-45) vs. 2026-09-16 blog "already enables direct checkout for hundreds of thousands of brands and retailers" (GA-08). The help-page wording is outdated.
- UCP in Australia: press reports a live launch around 2026-06-17 (GA-44, Tier 3) vs. Google 2026-09-16 "Australia and Canada to follow early next year" for Merchant Center UCP hub capabilities (GA-08). The two may describe different features (checkout vs. hub tooling). Unresolved.
- "Ranked lists and info you find in AI Overviews and more aren’t sponsored" (GA-19) vs. ads appearing "within" AI Overviews in "Sponsored" sections (GA-24). Consistent only if read as: organic ranked lists are unpaid, and ads sit in separate labeled sections. The GA-19 sentence alone can mislead.
- Ads/organic separation vs. ad-format design: Google states ads do not influence organic AI answers (GA-24). Highlighted Answers puts ads "on that list" of AI Mode recommendations, and Direct Offers "naturally surface in the AI Mode response" (GA-26). Not a logical contradiction (the label stays), but the visual boundary between organic and paid items narrows.
- Gemini app shopping availability: "all Gemini users in the U.S." (GA-37, 2025-11-13) → 21 countries/regions incl. India (GA-16, current page). Superseded.
- AI Mode Personal Intelligence: Pro/Ultra subscribers first (GA-30, January 2026) → "no subscription required", nearly 200 countries (GA-14, May 2026). Superseded.

## Knowledge gaps

- No Google source documents product-level ranking or selection factors for AI Mode, AI Overviews or the Gemini app. The only factor lists (GA-20, GA-21, GA-22) cover Google Shopping and Search shopping recommendations. Whether AI surfaces reuse them is unknown.
- No source states whether the Gemini app and AI Mode share one product-retrieval or ranking pipeline. Shared assets are documented (Shopping Graph, Universal Cart, UCP, Merchant Center attributes), not a shared ranker.
- Gemini app grounding for product queries: Google documents Shopping Graph use (GA-16) and generic Search grounding (GA-28). No source says whether product answers also use web search results, or how the two combine.
- Shopping Graph inputs beyond direct feeds: the help page names Merchant Center and Manufacturer Center (GA-19). Try-On uses Image Search (GA-35); "Let Google Call" uses phone calls (GA-36). No current Google consumer source fetched here states that the Shopping Graph crawls merchant websites or ingests YouTube or review sites. Not found in this session; not proof of absence.
- Hourly refresh volume after April 2026: not restated.
- How Personal Intelligence (Gmail, Search history, Wallet) changes which products are shown or their order: undocumented for AI Mode and the Gemini app.
- Location and shopping results: only "The price may vary based on your location" (GA-21) and "near me" calls (GA-36). No AI Mode or Gemini statement on location-based product selection.
- India: no Google statement that UCP checkout, Universal Cart, agentic checkout or Direct Offers is generally available in India. No statement on INR pricing, UPI, or Indian-language shopping support beyond Hindi (Gemini app shopping EN/HI; AI Mode shopping EN with Hindi "soon" as of 2026-04-07). Hindi AI Mode shopping launch: not found. Expansion of the Flipkart Buy test in October 2026: not verified.
- Gemini app ads: no Google announcement found either way beyond the Privacy Hub statement (GA-27).
- Direct Offers: no Google Ads help page fetched. Country scope, eligibility and exact live label text ("Sponsored" vs. "Sponsored deal") are not confirmed.
- Canada and U.K. UCP checkout live status: not confirmed by any fetched source.
- Gemini Spark payments and AP2 live status: announced (GA-47), not confirmed live.
- Help-center page dates: support.google.com renders "Last updated" with JavaScript. Dates were not captured by curl, except the Gemini Apps Privacy Hub (2026-10-26). Re-check in a browser before registry promotion.
- "60+ billion" counts listings, not unique products or merchants. No merchant-count figure found.

## Unfetched sources

- Google Australia (blog.google/intl/en-au) primary post for the reported June 2026 UCP launch: not located (en-au RSS shows only recent items; WebSearch returned press only). Alternate used: Inside Retail (Tier 3), GA-44.
- Google Ads Help page for Direct Offers: not located via WebSearch. Not fetched.
- Google statement on the Flipkart Buy test, and the September 2026 India "agentic" partner announcement that TechCrunch references ("Earlier this month"): not located. Alternate used: Think with Google India page (GA-42).
- support.google.com "Last updated" dates: JavaScript-rendered; not captured by curl. The pages themselves returned HTTP 200.
- No page returned HTTP 403 or failed outright in this session. No instructions addressed to AI agents were observed on any fetched page.

## Source list

Tier 1 — The Keyword (blog.google)
1. An intelligent new shopping cart — 2026-10-15 — https://blog.google/products-and-platforms/products/shopping/universal-cart-launch/ (GA-01, GA-02)
2. Introducing the Universal Cart and more ways to help you shop — 2026-05-19 — https://blog.google/products-and-platforms/products/shopping/google-shopping-cart/ (GA-03, GA-04)
3. The AI platform shift and the opportunity ahead for retail (NRF 2026) — 2026-01-11 — https://blog.google/company-news/inside-google/message-ceo/nrf-2026-remarks/ (GA-05, GA-06)
4. AI shopping gets simpler with Universal Commerce Protocol updates — 2026-03-19 (modified 2026-04-07) — https://blog.google/products-and-platforms/products/shopping/ucp-updates/ (GA-07)
5. Boost your holiday sales with these agentic commerce updates — 2026-09-16 — https://blog.google/products-and-platforms/products/shopping/google-shopping-updates-holiday-shopping/ (GA-08, GA-09, GA-10)
6. How we’re helping retailers thrive with new Universal Commerce Protocol features and AI tools on Google — 2026-05-20 — https://blog.google/products-and-platforms/products/shopping/shopping-updates-google-marketing-live/ (GA-10, GA-11)
7. Ads in AI Mode expand to new markets. — 2026-10-28 — https://blog.google/products/ads-commerce/ads-in-ai-mode-global/ (GA-12)
8. 100 things we announced at Google I/O 2026 — 2026-05-20 (modified 2026-06-01) — https://blog.google/innovation-and-ai/technology/ai/google-io-2026-all-our-announcements/ (GA-13, GA-14, GA-47)
9. New ways Google is using AI to make shopping easier (Google India) — 2026-04-07 — https://blog.google/intl/en-in/products/explore-communicate/new-ways-google-is-using-ai-to-make-shopping-easier/ (GA-15)
10. Let AI do the hard parts of your holiday shopping — 2025-11-13 — https://blog.google/products-and-platforms/products/shopping/agentic-checkout-holiday-ai-shopping/ (GA-36, GA-37)
11. New tech and tools for retailers to succeed in an agentic shopping era — 2026-01-11 — https://blog.google/products/ads-commerce/agentic-commerce-ai-tools-protocol-retailers-platforms/ (GA-25, GA-38)
12. A new generation of ads for the AI era of Search — 2026-05-20 — https://blog.google/products/ads-commerce/google-marketing-live-search-ads/ (GA-26)
13. The latest AI news we announced in January — 2026-02-04 — https://blog.google/innovation-and-ai/products/google-ai-updates-january-2026/ (GA-30)
14. The latest AI news we announced in July 2026 — 2026-08-04 — https://blog.google/innovation-and-ai/technology/ai/google-ai-updates-july-2026/ (GA-47)
15. Shop with AI Mode, use AI to buy and try clothes on yourself virtually — 2025-05-20 — https://blog.google/products-and-platforms/products/shopping/google-shopping-ai-mode-virtual-try-on-update/ (GA-39)
16. Supercharging Search for India: New Languages in AI Mode & Search Live debuts — 2025-10-08 — https://blog.google/intl/en-in/products/supercharging-search-for-india-new-languages-in-ai-mode-search-live-debuts/ (GA-41)
17. Bringing Gemini in Chrome with auto browse to India — 2026-10-07 — https://blog.google/intl/en-in/products/bringing-gemini-in-chrome-with-auto-browse-to-india/ (GA-46)

Tier 1 — Google Help Centers (dates not captured unless stated)
18. Get help with your shopping in Gemini Apps — https://support.google.com/gemini/answer/16730149?hl=en (GA-16, GA-17)
19. Manage your universal cart — https://support.google.com/gemini/answer/17085590?hl=en (GA-18)
20. Gemini Apps Privacy Hub — last updated 2026-10-26 — https://support.google.com/gemini/answer/13594961?hl=en (GA-27, GA-28)
21. Use & manage Connected Apps in Gemini — https://support.google.com/gemini/answer/13695044?hl=en (GA-28)
22. Connect your Google apps to personalize your Gemini experience — https://support.google.com/gemini/answer/16598406?hl=en (GA-29)
23. About personalization with Connected Apps — https://support.google.com/gemini/answer/16836988?hl=en (GA-29)
24. Sources of shopping info — https://support.google.com/googleshopping/answer/14336735?hl=en (GA-19)
25. How Google Shopping works — https://support.google.com/googleshopping/answer/9128904?hl=en (GA-20)
26. Understand how shopping results are generated — https://support.google.com/googleshopping/answer/15456476?hl=en (GA-21)
27. How shopping recommendations work on Google Search — https://support.google.com/googleshopping/answer/10269376?hl=en (GA-22)
28. Recommendations & personalization — https://support.google.com/googleshopping/answer/9116422?hl=en (GA-22)
29. Manage shopping preferences on Google — https://support.google.com/googleshopping/answer/13005558?hl=en (GA-23)
30. About price tracking on Google — https://support.google.com/googleshopping/answer/13971184?hl=en (GA-33, GA-34)
31. How the Google Try-On tool works — https://support.google.com/googleshopping/answer/16253678?hl=en (GA-35)
32. Ask Google to call nearby stores for you — https://support.google.com/googleshopping/answer/16742225?hl=en (GA-36)
33. About the Top Quality Store badge — https://support.google.com/googleshopping/answer/11115998?hl=en (GA-48)
34. About Agentic checkout with Google Pay — https://support.google.com/googlepay/answer/16421147?hl=en (GA-33)
35. About ads in AI-powered experiences in Google Search — https://support.google.com/google-ads/answer/18826097?hl=en (GA-24)
36. Get AI-powered responses with AI Mode in Google Search — https://support.google.com/websearch/answer/16011537?hl=en (GA-30, GA-31)
37. Find information in faster & easier ways with AI Overviews in Google Search — https://support.google.com/websearch/answer/14901683?hl=en (GA-32)
38. About the Universal Commerce Protocol (UCP) and UCP-powered checkout feature on Google — https://support.google.com/merchants/answer/16837055?hl=en (GA-45)

Tier 1 — other Google-owned
39. AI features and your website — Google Search Central — last updated 2025-12-10 — https://developers.google.com/search/docs/appearance/ai-features (GA-40)
40. Google Marketing Live: What’s next for marketers in India — Think with Google APAC — September 2026 — https://business.google.com/en-all/think/future-of-marketing/google-marketing-live-india-ai-search/ (GA-42)

Tier 3 — press (used only where no primary source was found)
41. Google tests buying from Walmart-owned Flipkart through Gemini and AI Mode in India — TechCrunch — 2026-09-26 — https://techcrunch.com/2026/09/26/google-tests-buying-from-walmart-owned-flipkart-through-gemini-and-ai-mode-in-india/ (GA-43)
42. Google taps top Aussie retailers in AI shopping rollout — Inside Retail Australia — 2026-06-17 — https://insideretail.com.au/digital/ecommerce/google-taps-top-aussie-retailers-in-ai-shopping-rollout-202606 (GA-44)

Fetched but not cited as findings (context only): "More ways to connect with the web from Search" (2026-10-15, no shopping content); "4 tips for styling outfits with Gemini" (2026-10-19, image-generation styling, not a shopping feature); Google India "Decoding India’s two-speed festive shopper" (2026-10-08, Ipsos survey statistics, no feature facts); blog.google May 2026 and September 2026 AI recaps (no shopping facts beyond cited posts).
