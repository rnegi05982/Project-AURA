# Registry — GEM (Gemini app, AI Mode, AI Overviews: consumer surfaces)

Schema: `evidence/README.md`. Google merchant-side and search-infrastructure claims are in `goog.md`; the protocol is in `ucp.md`. Accessed 2026-10-30 unless stated. Google help-center pages render dates with JavaScript; "not stated" means not captured.

Surfaces:
- **Gemini app:** gemini.google.com and mobile apps.
- **AI Mode:** Google Search's conversational mode.
- **AI Overviews (AIO):** generated summaries on the Search results page.

---

## Data source and pipeline

### GEM-001 — Gemini app shopping uses the Shopping Graph and is available in 21 countries, including India
- **Claim:** Gemini Apps Help says Gemini uses Shopping Graph information to find and compare products. Shopping is available in 21 listed countries/regions, including India. It can personalize recommendations with Personal Intelligence.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Gemini app / data sources, regions
- **Source:** "Get help with your shopping in Gemini Apps" — Gemini Apps Help — https://support.google.com/gemini/answer/16730149?hl=en
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Gemini uses information from Google's Shopping Graph to help you find products, compare options, and make purchase decisions."
- **Establishes:** The Gemini app's product data comes from the Shopping Graph. Countries: Argentina, Australia, Brazil, Canada, Chile, Colombia, Hong Kong, India, Japan, Indonesia, Malaysia, Mexico, New Zealand, Philippines, Saudi Arabia, Singapore, Taiwan, Thailand, UAE, US, Vietnam.
- **Limitations:** No ranking factors documented. Buy-button countries not stated on this page.
- **Related:** GEM-003, GOOG-020
- **Origin:** notes/ga-…#GA-16; notes/gb-…#GB-15 · **Checked:** 2026-10-31

### GEM-002 — India: Gemini app shopping in English and Hindi; AI Mode shopping in English, Hindi "soon" (2026-04-07)
- **Claim:** Google India says Gemini-app shopping (product listings, comparisons, prices, places to buy) is available in English and Hindi. AI Mode shopping (price, reviews, inventory, comparison tables) is available in English, with Hindi "soon".
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Gemini app, AI Mode / regions
- **Source:** "New ways Google is using AI to make shopping easier" — Google India (The Keyword) — https://blog.google/intl/en-in/products/explore-communicate/new-ways-google-is-using-ai-to-make-shopping-easier/
- **Published:** 2026-04-07 · **Accessed:** 2026-10-30
- **Excerpt:** > "Shopping in Gemini is powered by the Shopping Graph so you can trust you’re seeing fresh information and unmatched selection. This experience is currently available in English and Hindi." / > "This experience is currently available in English and we'll be rolling out in Hindi soon."
- **Establishes:** Google documents AI shopping surfaces for Indian users. ChatGPT does not (CGPT-046).
- **Limitations:** No INR, UPI or checkout statement. Hindi AI Mode shopping launch not confirmed later.
- **Related:** GEM-001, CGPT-046
- **Origin:** notes/ga-…#GA-15 · **Checked:** 2026-10-31

### GEM-003 — AI Mode shopping combines Gemini with the Shopping Graph and uses query fan-out
- **Claim:** Google describes AI Mode shopping as Gemini plus the Shopping Graph. AI Mode runs several simultaneous searches (query fan-out) to derive product criteria, then suggests products.
- **Classification:** VERIFIED FACT (statement); the fan-out-to-ranking mechanism is undocumented · **Confidence:** High · **Tier:** 1
- **Subject / topic:** AI Mode / retrieval
- **Source:** "Shop with AI Mode, use AI to buy and try clothes on yourself virtually" — The Keyword — https://blog.google/products-and-platforms/products/shopping/google-shopping-ai-mode-virtual-try-on-update/ ; "Let AI do the hard parts of your holiday shopping" — https://blog.google/products-and-platforms/products/shopping/agentic-checkout-holiday-ai-shopping/
- **Published:** 2025-05-20; 2025-11-13 · **Accessed:** 2026-10-30
- **Excerpt:** > "AI Mode will start a query fan-out, which means it runs several simultaneous searches to figure out what makes a bag good for rainy weather and long journeys, and then use those criteria to suggest waterproof options with easy access to pockets." / > "And because AI Mode is powered by the Shopping Graph…"
- **Establishes:** AI Mode retrieval = fan-out searches + Shopping Graph listings.
- **Limitations:** 2025 posts; UI may have changed.
- **Related:** GEM-004, GOOG-020
- **Origin:** notes/ga-…#GA-37, #GA-39; notes/gb-…#GB-31 · **Checked:** pending

### GEM-004 — Google: AI Overviews and AI Mode "may use different models and techniques"
- **Claim:** Search Central says both surfaces may fan out across subtopics and data sources, but may use different models and techniques, so their responses and links vary.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** AI Mode, AIO / retrieval
- **Source:** "AI features and your website" — Google Search Central — https://developers.google.com/search/docs/appearance/ai-features
- **Published:** last updated 2025-12-10 · **Accessed:** 2026-10-30
- **Excerpt:** > "AI Mode and AI Overviews may use different models and techniques, so the set of responses and links they show will vary."
- **Establishes:** The two surfaces must be measured separately, even after the May 2026 UI merge (GEM-005).
- **Limitations:** Predates the merge. Product selection not described.
- **Related:** GEM-005, RES-039
- **Origin:** notes/ga-…#GA-40 · **Checked:** pending

### GEM-005 — AI Overviews and AI Mode merged into one UI flow (2026-05-20); AI Mode >1B monthly users; Gemini 3.5 Flash default
- **Claim:** Google merged AIO and AI Mode into "one, seamless AI Search experience" worldwide and moved AI Mode to Gemini 3.5 Flash as default.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** AI Mode, AIO
- **Source:** "100 things we announced at Google I/O 2026" — The Keyword — https://blog.google/innovation-and-ai/technology/ai/google-io-2026-all-our-announcements/
- **Published:** 2026-05-20 · **Accessed:** 2026-10-30
- **Excerpt:** > "And today we’re upgrading the experience with Gemini 3.5 Flash as the new default model, globally."
- **Establishes:** Model version is a recordable variable (RES-026 shows version changes move results).
- **Limitations:** A shared UI does not mean shared retrieval or ranking (GEM-004).
- **Related:** GEM-004
- **Origin:** notes/ga-…#GA-13 · **Checked:** pending

### GEM-006 — The Gemini app grounds some responses on Google Search
- **Claim:** Google states some Gemini responses are grounded on Search results, and Gemini can always use public Google Search information, even signed out.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Gemini app / retrieval
- **Source:** "Gemini Apps Privacy Hub" — https://support.google.com/gemini/answer/13594961?hl=en ; "Use & manage Connected Apps in Gemini" — https://support.google.com/gemini/answer/13695044?hl=en
- **Published:** Privacy Hub last updated 2026-10-26 · **Accessed:** 2026-10-30
- **Excerpt:** > "We rely on other Google services and infrastructure to provide Gemini Apps. For example, some Gemini responses are grounded on Search results."
- **Establishes:** Two data paths may feed Gemini product answers: Shopping Graph (GEM-001) and Search grounding.
- **Limitations:** How the two combine for product queries is undocumented.
- **Related:** GEM-001, RES-034
- **Origin:** notes/ga-…#GA-28 · **Checked:** pending

## Ranking, ads and personalization

### GEM-007 — Organic AI Mode and AI Overviews answers come from "Search quality and ranking systems"; ads don't influence them
- **Claim:** Google Ads Help says organic AIO and AI Mode responses are generated by Google's Search quality and ranking systems, ads are labeled "Sponsored", and buying ads does not influence organic answers. Ads match the query or the query plus the AI response.
- **Classification:** VERIFIED FACT (stated policy) · **Confidence:** High · **Tier:** 1
- **Subject / topic:** AI Mode, AIO / ranking, ads
- **Source:** "About ads in AI-powered experiences in Google Search" — Google Ads Help — https://support.google.com/google-ads/answer/18826097?hl=en
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "No. Organic AI Overviews and AI Mode responses are generated independently using Google's Search quality and ranking systems. Buying ads doesn't influence organic AI answers, and whether your site is cited organically doesn't affect your ad auction eligibility."
- **Establishes:** The only Google statement on organic ranking in AI surfaces. No product-level factors are named.
- **Limitations:** Policy statement. Within-answer ads serve in English in the US, AU, CA, IN and others.
- **Related:** GEM-008, GOOG-022
- **Origin:** notes/ga-…#GA-24; notes/gb-…#GB-35 · **Checked:** pending

### GEM-008 — Ads in AI Mode reached India on 2026-10-28; AI Mode mixes sponsored and organic product list items
- **Claim:** Google scaled ads in AI Mode to India and nine other countries. It says click-through rates are similar between sponsored and organic product list items in AI Mode.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** AI Mode / ads, regions
- **Source:** "Ads in AI Mode expand to new markets." — The Keyword — https://blog.google/products/ads-commerce/ads-in-ai-mode-global/
- **Published:** 2026-10-28 · **Accessed:** 2026-10-30
- **Excerpt:** > "In fact, click-through rates are already similar between sponsored and organic product list items within AI Mode." / > "Now we're scaling ads in AI Mode in Australia, Canada, India, Kenya, Malaysia, New Zealand, Nigeria, Pakistan, the Philippines, and Singapore."
- **Establishes:** Indian AI Mode users can see sponsored product items beside organic ones. Experiments must label them.
- **Limitations:** Relative placement of sponsored items not documented.
- **Related:** GEM-007, GEM-009
- **Origin:** notes/ga-…#GA-12 · **Checked:** 2026-10-31

### GEM-009 — Direct Offers and Highlighted Answers put labeled ads inside AI Mode responses and recommendation lists
- **Claim:** Direct Offers (pilot since January 2026) shows advertiser discounts in AI Mode. In May 2026 Google said Direct Offers will "naturally surface in the AI Mode response". Highlighted Answers lets ads appear on AI Mode recommendation lists. Both are labeled "Sponsored".
- **Classification:** VERIFIED FACT (announcements; live status of tests unconfirmed) · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** AI Mode / ads
- **Source:** "A new generation of ads for the AI era of Search" — The Keyword — https://blog.google/products/ads-commerce/google-marketing-live-search-ads/
- **Published:** 2026-05-20 · **Accessed:** 2026-10-30
- **Excerpt:** > "Now, when AI Mode provides a list of recommendations — like the best language apps for an upcoming trip — highly relevant, high-quality ads are eligible to appear on that list as a Highlighted Answer."
- **Establishes:** The visual boundary between organic and paid items in AI Mode is a label, not a separate zone.
- **Limitations:** No Direct Offers help page found. Country scope undocumented.
- **Related:** GEM-008, RES-027 (sponsored-tag effects on Gemini agents)
- **Origin:** notes/ga-…#GA-25, #GA-26; notes/gb-…#GB-36 · **Checked:** pending

### GEM-010 — Gemini app chats are not used to show ads; cart data can be
- **Claim:** The Gemini Apps Privacy Hub (2026-10-26) says Gemini chats are not used to show ads. Cart and order data added from Gemini go to Google Wallet and can be used for personalization and ads, per settings.
- **Classification:** VERIFIED FACT (statement). No Gemini-app ad format was found: EVIDENCE-BASED INFERENCE. · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Gemini app / ads
- **Source:** "Gemini Apps Privacy Hub" — https://support.google.com/gemini/answer/13594961?hl=en
- **Published:** last updated 2026-10-26 · **Accessed:** 2026-10-30
- **Excerpt:** > "Your Gemini Apps chats are not being used to show you ads. If this changes, we will clearly communicate it to you."
- **Establishes:** As of the access date, Gemini app product answers have no documented ad unit.
- **Limitations:** Narrower than "no ads in Gemini".
- **Related:** GEM-007
- **Origin:** notes/ga-…#GA-27 · **Checked:** pending

### GEM-011 — Personal Intelligence can personalize shopping in Gemini and AI Mode (Search history, Shopping, Gmail, Photos)
- **Claim:** Gemini's Personal Intelligence can draw on Search services (incl. Shopping), Gmail, Photos and Wallet (US) and make recommendations from preferences; not in EEA, UK, Switzerland, Nigeria. AI Mode personalization uses Search Services History; Google named shopping recommendations as a use. AI Mode Personal Intelligence reached ~200 countries in May 2026.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Gemini app, AI Mode / personalization
- **Source:** "Connect your Google apps to personalize your Gemini experience" — https://support.google.com/gemini/answer/16598406?hl=en ; "Get AI-powered responses with AI Mode in Google Search" — https://support.google.com/websearch/answer/16011537?hl=en
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Personal Intelligence in AI Mode references previous searches and activity saved in your Search Services History to provide suggestions tailored to your tastes and preferences."
- **Establishes:** Signed-in history changes AI shopping answers. Experiments need logged-out baselines.
- **Limitations:** Mechanism (rewrite vs re-rank) undocumented.
- **Related:** GEM-012
- **Origin:** notes/ga-…#GA-14, #GA-29, #GA-30 · **Checked:** pending

### GEM-012 — Saved shopping preferences make favorite brands "show up more often" (US, CA, AU, India)
- **Claim:** Users in the US, Canada, Australia and India can save brand and style preferences. Saved brands appear more often in results across Search, Shopping, Discover and other surfaces.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** Search, Shopping / personalization
- **Source:** "Manage shopping preferences on Google" — Google Shopping Help — https://support.google.com/googleshopping/answer/13005558?hl=en
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Products from your favorite brands will show up more often in your search results."
- **Establishes:** A documented user-side brand boost exists in India.
- **Limitations:** AI Mode and Gemini are not named.
- **Related:** GEM-011
- **Origin:** notes/ga-…#GA-23 · **Checked:** pending

### GEM-013 — Brand-submitted conversational attributes appeared in 50% of relevant AI Mode recommendations (lululemon test)
- **Claim:** Google says conversational attributes from lululemon were incorporated 50% of the time in relevant AI Mode product recommendations during testing.
- **Classification:** VERIFIED FACT (statement about one test) · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** AI Mode / product data
- **Source:** "Boost your holiday sales with these agentic commerce updates" — The Keyword — https://blog.google/products-and-platforms/products/shopping/google-shopping-updates-holiday-shopping/
- **Published:** 2026-09-16 · **Accessed:** 2026-10-30
- **Excerpt:** > "During testing with lululemon, conversational attributes submitted from the brand were incorporated 50% of the time in relevant product recommendations in AI Mode, providing shoppers with more precise and helpful answers."
- **Establishes:** Merchant Center text reaches AI Mode answer text.
- **Limitations:** "Incorporated" = used in answer text. It does not say attributes change which products are selected or their order. One brand, no method.
- **Related:** GOOG-012
- **Origin:** notes/ga-…#GA-09 · **Checked:** pending

## Checkout and agentic features

### GEM-014 — Buy buttons and Universal Cart are US-only for consumers
- **Claim:** AI Mode checkout is for signed-in 18+ users in the US, in English. Universal Cart (live 2026-10-15) is US-only; it checks out with Google Pay for participating merchants or fills the merchant-site cart for others.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** AI Mode, Gemini app / checkout, regions
- **Source:** "Make purchases and manage orders directly from AI Mode in Google Search" — https://support.google.com/websearch/answer/16833721?hl=en ; "Manage your universal cart" — https://support.google.com/gemini/answer/17085590?hl=en ; "An intelligent new shopping cart" — https://blog.google/products-and-platforms/products/shopping/universal-cart-launch/
- **Published:** cart launch 2026-10-15 · **Accessed:** 2026-10-30
- **Excerpt:** > "This feature is only available for signed in 18+ users in the US, in English." / > "Important: This feature is currently available only in the United States."
- **Establishes:** Indian users can discover products in Google AI surfaces but not buy through Google's checkout.
- **Limitations:** Press reports UCP checkout in Australia (Tier 3) and a Flipkart test in India (GEM-016).
- **Related:** GEM-015, GOOG-001
- **Origin:** notes/gb-…#GB-09, #GB-16; notes/ga-…#GA-01, #GA-18 · **Checked:** pending

### GEM-015 — Two Google buy mechanisms: agentic checkout on the merchant site (2025) and UCP checkout on Google (2026)
- **Claim:** Agentic checkout ("Buy for me with GPay") buys on the merchant's site after the user confirms, for select merchants that accept Google Pay (US; one help section also says Australia). UCP checkout happens on Google surfaces with the merchant as merchant of record. Google says UCP checkout covered "hundreds of thousands of brands and retailers" by September 2026.
- **Classification:** VERIFIED FACT · **Confidence:** Medium (country scope conflicts inside one page) · **Tier:** 1
- **Subject / topic:** Google AI surfaces / checkout
- **Source:** "About Agentic checkout with Google Pay" — https://support.google.com/googlepay/answer/16421147?hl=en ; "Boost your holiday sales…" — https://blog.google/products-and-platforms/products/shopping/google-shopping-updates-holiday-shopping/
- **Published:** 2026-09-16 (blog) · **Accessed:** 2026-10-30
- **Excerpt:** > "UCP already enables direct checkout for hundreds of thousands of brands and retailers across Google."
- **Establishes:** Google, unlike OpenAI (CGPT-021), is expanding in-surface checkout.
- **Limitations:** Merchant eligibility for agentic checkout is unpublished.
- **Related:** GOOG-001, GOOG-025
- **Origin:** notes/ga-…#GA-08, #GA-33; notes/gb-…#GB-02, #GB-38 · **Checked:** pending

### GEM-016 — India: Google says Flipkart is "partnering" on UCP; press reports a Flipkart Buy test in Gemini and AI Mode
- **Claim:** Google's India GML page (Sept 2026) says merchants like Flipkart are partnering with Google to offer the UCP agentic experience to Indian shoppers. TechCrunch reports a limited test from ~2026-09-26 with a Buy button on select Flipkart listings.
- **Classification:** VERIFIED FACT (Google statement; press report). Live availability in India: UNVERIFIED. · **Confidence:** Low · **Tier:** 1 (Google marketing page) / 3 (TechCrunch)
- **Subject / topic:** India / checkout
- **Source:** "Google Marketing Live: What's next for marketers in India" — Think with Google APAC — https://business.google.com/en-all/think/future-of-marketing/google-marketing-live-india-ai-search/ ; https://techcrunch.com/2026/09/26/google-tests-buying-from-walmart-owned-flipkart-through-gemini-and-ai-mode-in-india/
- **Published:** September 2026; 2026-09-26 · **Accessed:** 2026-10-30
- **Excerpt:** > "Merchants like Flipkart are already partnering with Google to offer this agentic experience to Indian shoppers, and help brands grow sales."
- **Establishes:** Flipkart is the only named Indian UCP partner.
- **Limitations:** Marketing page; anonymous press sourcing.
- **Related:** UCP-001, GEM-014
- **Origin:** notes/ga-…#GA-42, #GA-43 · **Checked:** pending

### GEM-017 — India availability beyond chat: price tracking, Try-On, AI Overviews and AI Mode in Indian languages, Gemini in Chrome auto browse
- **Claim:** Price tracking and Virtual Try-On are available in India. AI Mode supports Hindi and other Indian languages generally; AI Overviews are available in India. Gemini in Chrome's auto browse launched for AI Pro/Ultra subscribers in India (2026-10-07).
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** India / regions
- **Source:** https://support.google.com/googleshopping/answer/13971184?hl=en ; https://support.google.com/googleshopping/answer/16253678?hl=en ; https://support.google.com/websearch/answer/16011537?hl=en ; https://blog.google/intl/en-in/products/bringing-gemini-in-chrome-with-auto-browse-to-india/
- **Published:** 2026-10-07 (Chrome post); others not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Price tracking is available in the United States, Canada, Australia, Japan, and India."
- **Establishes:** India is a live market for most Google AI shopping discovery features.
- **Limitations:** General AI Mode language support ≠ shopping-module language support (GEM-002).
- **Related:** GEM-002
- **Origin:** notes/ga-…#GA-31, #GA-32, #GA-34, #GA-35, #GA-46 · **Checked:** pending
