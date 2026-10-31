# Agent GC — How Shopify stores and other store platforms get products into Google's AI surfaces (Gemini app, AI Mode, AI Overviews)

- Scope: Shopify → Google AI Mode / Gemini through Agentic Storefronts (discovery source, direct checkout, eligibility, fees, buyer countries); Shopify's Google & YouTube sales channel (Merchant Center sync, fields, free listings); whether Google consumes Shopify Catalog or a store's `/.well-known/ucp`; Shopify field → Merchant Center attribute mapping; other platforms' Google AI paths (WooCommerce, BigCommerce/Feedonomics, Salesforce, commercetools, Adobe Commerce, Wix, Squarespace); Google documentation for platforms integrating UCP.
- Out of scope (reused, not re-researched): Shopify Catalog eligibility, Catalog field set, Agentic Storefronts admin model, robots.txt/agents.md/`/.well-known/ucp` defaults, JSON-LD defaults, other platforms' ChatGPT paths. These are cited by ID from `research/ai-platforms/chatgpt/notes/c-shopify-and-independent-platforms.md` (IDs C-01 … C-37).
- Research date: 2026-10-30.
- Method: Raw HTML fetched with `curl` (help.shopify.com, shopify.com, apps.shopify.com, support.google.com/merchants, developers.google.com/merchant/ucp, blog.google, vendor sites). Text extracted locally with an HTML-to-text script. Excerpts are copied from those extractions character-for-character. Publication dates come from page metadata (`datePublished`, `article:published_time`) or the devsite "Last updated" footer. Tier 3 trade press is used only to locate primary sources and is labelled.
- Coordination: Google Merchant Center / UCP / consumer-doc facts are cited by GB-ID from `research/ai-platforms/gemini/notes/gb-merchant-center-ucp.md` (GB-01 … GB-45) where GB covers them. This file records only Shopify-path and platform-path evidence.
- Access dates: all pages were fetched on 2026-10-30 (storefront response headers show `Date: Fri, 30 Oct 2026 21:59 GMT`). No page was re-fetched after the 2026-10-31 date change.
- Status: complete (35 findings). Excerpts copied from curl extractions were machine-checked against the saved text; in-app-browser captures (Wayback, BigCommerce release, Adobe, Squarespace) were copied from the browser's page text.

---

## 1. Findings

### GC-01 Shopify → Google AI Mode/Gemini: product discovery comes from Google Merchant Center, not from Shopify Catalog access
- Claim: For Google AI Mode and Gemini, Shopify does not syndicate products through a Shopify Catalog access setting. Products reach Google through the Google & YouTube sales channel or any other Merchant Center feed. Shopify states that Merchant Center powers product discovery for this channel.
- Classification: VERIFIED FACT
- Source: Selling on Google AI Mode and Gemini — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google ; Data sharing and privacy for selling with agentic storefronts — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/data-privacy ; Shopify agentic storefronts — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Products are made available to Google AI Mode and Gemini through the Google & YouTube sales channel or Google Merchant Center."
  > "Product discovery for Google AI Mode and Gemini is powered by Google Merchant Center. Your products must be available in Google Merchant Center to be discoverable."
  > "The agentic storefront for ChatGPT has only the Catalog access setting. Selling through direct checkout with Microsoft Copilot requires Shopify Catalog access. For Google AI Mode and Gemini and Meta, product discovery is powered by individual sales channels rather than a Shopify Catalog access setting."
  > "Your products are made available to AI channels through Shopify Catalog or through the Google & YouTube sales channel or Google Merchant Center for Google AI Mode and Gemini."
- Establishes: The Google path differs from the ChatGPT path (C-01, C-06). ChatGPT receives Shopify Catalog data. Google receives Merchant Center data. A Shopify store with no Merchant Center feed has no documented Shopify-managed discovery path into AI Mode or Gemini.
- Limitations: The Shopify pages describe the agentic channel only. They do not describe how Google ranks or retrieves Merchant Center offers inside AI Mode.

### GC-02 Direct checkout in AI Mode/Gemini is on by default for eligible stores; merchants opt out per channel
- Claim: Shopify-powered direct checkout in Google AI Mode and Gemini is active by default for eligible stores. Merchants turn it off in Sales channels > Agentic. With checkout off, products stay discoverable and buyers are sent to the online store. On the Agentic plan, direct checkout is off by default.
- Classification: VERIFIED FACT
- Source: Selling on Google AI Mode and Gemini — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google ; Setting up agentic storefronts for stores on the Agentic plan — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/agentic-plan-setup
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Purchasing in direct checkouts is activated by default for eligible stores, but you can deactivate direct checkout and have customers complete their purchase on your online store instead."
  > "If you opt out of direct checkout with Google AI Mode and Gemini, then your products can still be discovered and included in Google AI Mode and Gemini's search results through Google Merchant Center, but they can't be purchased through a direct checkout."
  > "From your Shopify admin, go to Sales channels > Agentic. Deactivate Allow Shopify to manage for me. Click Google AI Mode and Gemini. Activate or deactivate Direct checkout. Click Save."
  > "For Google AI Mode and Gemini, Meta, and Microsoft Copilot, direct checkout is deactivated by default on the Agentic plan. You need to set up the channel, and then activate direct checkout."
- Establishes: Default-on (opt-out) checkout for standard plans. The Google channel exposes a Direct checkout toggle only. It has no Shopify Catalog access toggle (compare C-02 for ChatGPT, which has only a Catalog access toggle).
- Limitations: Step list was rendered as separate list items; joined here with spaces. The agentic-home page also says "Direct checkout is also deactivated when Shopify Catalog access is turned off" for the global setting; Shopify does not say whether this global switch affects the Google channel (see Section 2).

### GC-03 Eligibility for Google AI Mode/Gemini direct checkout: buyers in US, Canada or Australia; Merchant Center; Catalog-eligible products; terms; policies
- Claim: The store must sell to customers in the United States, Canada or Australia and may be based in any country. It needs a valid Merchant Center account that meets Google's free-listing and return-policy requirements. Products must be in Merchant Center (Google & YouTube channel with product and shipping auto-sync, or a third-party feed or manual upload). Products must also be eligible for Shopify Catalog. The merchant must accept the Agentic Storefronts Supplemental Terms and complete three store policies.
- Classification: VERIFIED FACT
- Source: Selling on Google AI Mode and Gemini — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "You must sell to customers in the United States, Canada, or Australia. Your store can be based in any country."
  > "You must have a valid Google Merchant Center account, and you must meet all Google requirements in Google Merchant Center."
  > "Use the Google & YouTube sales channel, with the Automatically sync products and Automatically sync shipping information settings activated in the Product feed section of the sales channel."
  > "Connect to Google Merchant Center directly through a third-party feed provider or manual upload."
  > "Your products must be eligible for Shopify Catalog."
  > "You must have your Terms of service, Privacy policy, and Return and refund policy completed in Settings > Policies in your Shopify admin."
- Establishes: Buyer-country gate (US/CA/AU), Merchant Center gate, and Shopify Catalog gate (C-05) all apply. No Shopify plan gate beyond Catalog's Starter-or-higher rule (C-05) is stated. Shopify Payments is not listed as a requirement on this page.
- Limitations: India is not a supported buyer country. An India-based store qualifies only if it sells to US, Canadian or Australian buyers (EVIDENCE-BASED INFERENCE from "Your store can be based in any country"). The page does not name a payment-provider requirement; whether third-party payment gateways work with the direct checkout is not stated.

### GC-04 Direct checkout mechanics and unsupported features
- Claim: Buyers click Buy in AI Mode or Gemini, enter shipping and payment details in a Shopify-powered checkout, and pay by credit or debit card. Shopify Functions and discounts run. Subscriptions-only products, bundles, customizable products and B2B-only products are not supported. Client-side pixels and Google Analytics do not fire. Local delivery and pickup are not supported. Merchants cannot force sign-in. Only blocking-capable checkout blocks may load.
- Classification: VERIFIED FACT
- Source: Selling on Google AI Mode and Gemini — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Customers can fill out their shipping and payment details in Google AI Mode and Gemini's Shopify-powered direct checkout, and then complete their purchase without visiting your online store by clicking a Pay now button and paying with a credit card or debit card."
  > "Shopify Functions, such as shipping, discount, and cart and checkout validation functions, are supported or run in Google AI Mode and Gemini's direct checkout."
  > "Products that are sold only as subscriptions. If a product offers both a one-time purchase and a subscription, then customers can buy it as a one-time purchase in Google AI Mode and Gemini's direct checkout, but they can't select the subscription."
  > "Google Analytics and custom pixels won't fire in Google AI Mode and Gemini's direct checkout. The checkout fires only server-to-server pixels (started, completed), so none of the standard or custom client side pixels fire."
  > "Local delivery, pickup in store, and pickup points aren't supported as delivery methods in Google AI Mode and Gemini's direct checkout."
  > "In Google AI Mode and Gemini's direct checkout, only customizations that support blocking checkout, and have checkout blocking enabled in their settings, are eligible to load."
- Establishes: The checkout runs on Shopify's checkout engine (Functions, discounts) but renders in Google's surface with a reduced block set.
- Limitations: "Shopify-powered" is Shopify's wording; Google calls the same experience UCP-powered native checkout (GC-15). Neither side documents the exact API calls between them for Shopify stores.

### GC-05 Fees: none for Google AI Mode/Gemini direct checkout
- Claim: Shopify charges no channel fee for sales through Google AI Mode and Gemini direct checkout. Only standard payment processing fees apply.
- Classification: VERIFIED FACT
- Source: Selling on Google AI Mode and Gemini — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "There are no fees associated with selling in Google AI Mode and Gemini's direct checkout. You pay only your standard payment processing fees."
- Establishes: Zero channel fee as of Oct 2026.
- Limitations: The Agentic Storefronts Supplemental Terms (updated Oct 6, 2026) let Shopify add per-channel fees and list Participating Channel Terms for Google (C-04). Google's own UCP checkout terms page links a "Checkout Addendum" (US only); it contains no fee clause (GC-18).

### GC-06 Rollout status (Oct 2026): channel and direct checkout still "rolling out"; buyer access gradual in US, Canada, Australia
- Claim: Shopify says the Google AI Mode and Gemini channel is rolling out to eligible stores, and direct checkout is rolling out to Google users. Buyers in the US, Canada and Australia get direct checkout gradually. Buyers without direct checkout still see the products and are redirected to the online store.
- Classification: VERIFIED FACT
- Source: Selling on Google AI Mode and Gemini — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google ; Shopify Catalog and product discovery for agentic storefronts — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/products
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Google AI Mode and Gemini is rolling out to eligible stores through Shopify's agentic storefronts. Direct checkout is also rolling out to Google users and might not yet be available in your store."
  > "Google AI Mode and Gemini's direct checkout is rolling out gradually to customers based in the United States, Canada, and Australia. Customers who don't have access to direct checkout can still discover your products, but they're redirected to your online store to complete their purchase."
- Establishes: As of 2026-10-30 the Shopify → Google direct checkout is not universally live. Discovery (via Merchant Center) does not depend on checkout availability.
- Limitations: Google's own UCP onboarding docs (updated 2026-10-19) say the Merchant Center UCP integration hub is US-only, "with Australia and Canada to follow early next year" (GB-12, GC-24). Those docs describe the direct-merchant path; Shopify's CA/AU statement describes the Shopify-managed path. See Section 2. A Sept 22, 2026 trade article reported the Shopify requirement then as US-based stores selling to US customers (GC-07), so the eligibility text changed between Sept 22 and Oct 30, 2026 (EVIDENCE-BASED INFERENCE; the earlier help-page version was not captured — see Section 5).

### GC-07 Sept 2026: Google notified Merchant Center users that their Shopify store "was matched" to Merchant Center, enabling native checkout by default
- Claim: Around Sept 18–22, 2026 Google emailed Merchant Center users on Shopify that native checkout was enabled for eligible products, with nothing to set up, and pointed to the Shopify admin for opt-out. The email text is known only through trade press.
- Classification: UNVERIFIED HYPOTHESIS (email wording; Google email not seen directly). The default-on behaviour itself is VERIFIED FACT via Shopify (GC-02).
- Source: Google Merchant Center Auto Enables Native Checkout: Buy On AI Mode & Gemini — Search Engine Roundtable — https://www.seroundtable.com/google-native-checkout-emails-42140.html ; Google opens native AI checkout to eligible Shopify merchants — Search Engine Land — https://searchengineland.com/google-opens-native-ai-checkout-to-eligible-shopify-merchants-490407
- Published/updated: 2026-09-22 (both, page metadata)
- Accessed: 2026-10-30
- Tier: 3
- Excerpt:
  > "Your Shopify store was matched to your Merchant Center, enabling native checkout on Google Al Mode and Gemini. Customers can now buy your products in Al Mode on Google Search, Gemini, and more. This seamless checkout feature is powered by the Universal Commerce Protocol (UCP)." (email as quoted by Search Engine Roundtable; "Al" spelling as published)
  > "To be eligible, your products must be published on your Shopify storefront and available in Merchant Center. Eligible products are automatically included. There's nothing for you to set up." (email as quoted)
  > "Shopify merchants must be based in the U.S. and sell to U.S. customers, have a valid Merchant Center account, and make eligible products available through Merchant Center, among other requirements." (Search Engine Land, Sept 22, 2026)
- Establishes: The mechanism Google describes is a match between a Shopify store and a Merchant Center account. Merchant Center offers then become checkout-eligible through Shopify's UCP integration (EVIDENCE-BASED INFERENCE).
- Limitations: Tier 3 relay of a private email. No Google help page fetched describes the "store matching" step. Search Engine Roundtable says UCP checkout "launched in February" and was pushed to more retailers "last Friday" (Sept 18, 2026) — trade-press claim, not verified.

### GC-08 The Google & YouTube sales channel is built and supported by Google, not Shopify
- Claim: Google LLC develops and supports the Google & YouTube app. Shopify's Help Center defers setup guidance to Google Merchant Center Help. Google's Merchant Center Help lists Shopify as a platform "supported by Google", unlike BigCommerce, WooCommerce, Wix and others.
- Classification: VERIFIED FACT
- Source: Google & YouTube — Shopify App Store — https://apps.shopify.com/google ; Google & YouTube — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/google ; How to find support if you use a non-Google platform — Google Merchant Center Help — https://support.google.com/merchants/answer/12048683?hl=en
- Published/updated: app "Launched November 28, 2017"; help pages not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "App support provided by Google LLC."
  > "The Google & YouTube sales channel is managed by Google. Refer to Google Merchant Center Help for setup guides."
  > "Sync your products, deals, and shipping to Merchant Center to turn shoppers into customers."
  > "Note: Shopify is supported by Google."
- Establishes: The Shopify → Merchant Center feed is a Google-owned integration. Field behaviour is defined by Google's app and documented in Merchant Center Help.
- Limitations: The app listing does not mention AI Mode, Gemini or UCP.

### GC-09 What the Google & YouTube channel syncs, and how often
- Claim: The channel syncs the store domain, products available to the online store, and shipping and tax settings to Merchant Center. Connecting an existing Merchant Center account overwrites an existing product feed. Products re-sync on change and within Google's 30-day expiry window. Merchants choose automatic or manual sync. Shopify discounts can sync as Merchant Center promotions. Google reviews new products within 3–5 business days.
- Classification: VERIFIED FACT
- Source: Google & YouTube channel requirements — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/marketplaces/google/requirements ; Syncing your products — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/marketplaces/google/getting-setup/syncing-products ; Syncing your products — Google Merchant Center Help — https://support.google.com/merchants/answer/13427434?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Your online store domain" / "Product information for the products that are available to your online store" / "Relevant Shopify store settings like shipping and taxes" (list items that "sync from your Shopify store to Google")
  > "If you already have a product feed set up, then it's overwritten to avoid conflicts between your Shopify store and your Merchant Center account."
  > "Google sets a strict 30-day expiry policy on synced product data, so the Google & YouTube channel updates your products automatically within that 30-day period to avoid account suspension or loss of product data."
  > "A product sync will be initiated after a merchant has successfully connected their Merchant Center account and updates required product information. Products will continue to sync automatically when any information changes."
  > "Some promotions (percentage, fixed amount, automatic discount) created in your Shopify admin automatically sync to Google Ads and to show organically across Google."
  > "Review time: Google reviews new products within 3-5 business days after initial sync."
- Establishes: The feed that powers Shopify discovery in AI Mode/Gemini (GC-01) is change-triggered plus a 30-day refresh.
- Limitations: Sync latency after a change is not stated. The Google page's FAQ says the Content API → Merchant API migration is handled by Google with no merchant action.

### GC-10 Shopify fields that map to Merchant Center attributes
- Claim: GTIN comes from the variant barcode. Products without a GTIN need MPN plus brand in the channel, or a "custom product" flag. Google product category is added in the channel; if absent, Google assigns one. Apparel needs age group, gender, color, size. The channel can send the SEO title and meta description instead of product title and description. Channel mapping lets any text field source from product, variant or metafield data; a channel's brand field "might use your product vendor by default". Google-specific data is stored in `mm-google-shopping` metafields. Product options must be in English.
- Classification: VERIFIED FACT
- Source: Google & YouTube channel requirements — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/marketplaces/google/requirements ; Syncing your products — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/marketplaces/google/getting-setup/syncing-products ; Syncing your products — Google Merchant Center Help — https://support.google.com/merchants/answer/13427434?hl=en ; Customizing product data for sales channels — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/channel-mapping
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "If a product has a GTIN (Global Trade Item Number), then you need to add it before you can publish the product. You can add a GTIN in the details of a product variant."
  > "Add a barcode (GTIN): In your Shopify admin, go to Products, open the product, and add the barcode in the Inventory section."
  > "For products without a GTIN, you need to add an MPN (Manufacturer Part Number) and brand to the product data in the Google & YouTube channel."
  > "If you don't add a product category, then Google automatically assigns a category to the product, but you might encounter errors."
  > "Optional: If your product doesn't have a GTIN or MPN because it's a custom product, then check This is a custom product."
  > "Optional: Add custom labels for Age, Gender, or Condition."
  > "You might want to use the search engine listing title tag and meta description so that you can include more keywords for search engine optimization on Google Shopping without changing the product information in your online store."
  > "For example, a channel's brand field might use your product vendor by default."
  > "If you added Google product data, such as age group or gender, in the Google & YouTube sales channel, then that data is stored in metafields with the mm-google-shopping namespace."
  > "Product options, including variants, need to be in English to sync with Google."
- Establishes: Mapping (Shopify → Merchant Center): variant barcode → `gtin`; vendor → `brand` (default, per example wording); channel field → `mpn`; channel/metafield → `google_product_category`, `age_group`, `gender`; product or SEO title → `title`; description or meta description → `description`; General shipping profile → `shipping`; Shopify discounts → promotions.
- Limitations: Shopify publishes no full default mapping table. Whether Shopify's Standard Product Taxonomy category auto-maps to `google_product_category` is not stated on these pages (gap). "Condition" appears only as a custom-label option; whether it fills the Merchant Center `condition` attribute is not stated.

### GC-11 Shipping sync: General profile only; carrier-calculated rates for AU, DE, US
- Claim: Only rates in the General shipping profile sync. Custom profiles cause errors. Carrier-calculated rates sync only for certain carriers in Australia, Germany and the US. Transit time feeds Google's delivery estimate; handling time defaults to the Shopify average. The Shopify → Google AI Mode path requires shipping auto-sync when the Google & YouTube channel is used (GC-03).
- Classification: VERIFIED FACT
- Source: Google & YouTube channel requirements — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/marketplaces/google/requirements ; Set up Shipping (for Shopify users) — Google Merchant Center Help — https://support.google.com/merchants/answer/14232591?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Only shipping rates in your General shipping profile can sync to Google Merchant Center. If you use custom shipping profiles, then rates will sync incorrectly with Google Merchant Center and cause errors."
  > "The Google & YouTube channel supports carrier-calculated shipping rates for certain shipping carriers and services in Australia, Germany, and the United States."
  > "By default, your handling time is based on the average handling time for Shopify merchants."
  > "Updates to your shipping settings made using the automated API, including that by a third-party platform such as Shopify, may overwrite manual updates from Merchant Center."
- Establishes: Shipping data in Merchant Center derives from the Shopify General profile.
- Limitations: How AI Mode displays shipping is not documented on these pages.

### GC-12 Return policy: Google's Shopify guide prescribes setting it in Shopify and again in Merchant Center
- Claim: Google's Shopify-specific help says to add the return policy in Shopify and separately in Merchant Center. Shopify's Google AI Mode page asks merchants to keep both consistent. Google's UCP checkout requires a Merchant Center return policy with cost, window and link, plus customer-support contact info.
- Classification: VERIFIED FACT
- Source: Set up your return policies (for Shopify users) — Google Merchant Center Help — https://support.google.com/merchants/answer/14232691?hl=en ; Selling on Google AI Mode and Gemini — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google ; Merchant Center (UCP guide) — Google for Developers — https://developers.google.com/merchant/ucp/guides/merchant-center
- Published/updated: help pages not stated; developer guide "Last updated 2026-10-29 UTC"
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "This article explains how to set up your return policy in your Shopify admin and in Merchant Center. Adding your return policy in both locations helps ensure that Google accurately represents your policies in search results and Shopping ads."
  > "To help ensure that customers get accurate information, keep your product data and store policies, including your return and refund policy, up to date in Shopify so that they match what's in Google Merchant Center."
  > "You must define your return policies in Merchant Center, as it is a Merchant of Record requirement and will be referenced on the checkout screen."
  > "You must include return cost, return speed (window), and a link to the full policy."
  > "You must set your customer support information in Merchant Center. This information is used to generate the "Contact Merchant" link on the order confirmation page."
- Establishes: Returns are a separate Merchant Center step for Shopify merchants; shipping is synced by the app (GC-11), returns are not described as synced.
- Limitations: Google's article does not say "not synced" in those words; it prescribes two separate steps (EVIDENCE-BASED INFERENCE that the app does not sync return policy). Merchant Center may suggest a policy "based on information collected from your website" (same article). Google-side UCP Merchant Center requirements are recorded in GB-04 and GB-05.

### GC-13 Free listings through the Google & YouTube app: automatic opt-in; Google's country list includes India; Shopify's page names only the US
- Claim: Google says the Google & YouTube app automatically opts Shopify stores into free listings on Google surfaces. Opt-in is automatic only when the Merchant Center account was created through the app. Google's supported free-listing countries include India. Shopify's Help Center describes the free display only "for eligible stores selling in the United States".
- Classification: VERIFIED FACT
- Source: Show your products for free on Google — Google Merchant Center Help — https://support.google.com/merchants/answer/13692890?hl=en ; Google & YouTube — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/google
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "When you use the Google & YouTube app on Shopify, you’re automatically opted in to show products from your Shopify store for free on surfaces across Google, such as on the Shopping tab, YouTube, Google Search (.com), Google Images, and Google Lens."
  > "If you created your Merchant Center account by using the Google & YouTube app on Shopify and your store meets eligibility requirements, then your approved products can automatically start appearing on the Shopping tab in relevant search results."
  > "You can list your products for free on Google in the following countries and regions:" (table includes "India")
  > "For eligible stores selling in the United States, products synced to Google Merchant Center using the Google & YouTube channel can display in relevant Google Shopping tab search listings for free."
- Establishes: Free listings are the organic layer that Merchant Center data enters. Google's general free-listings page also names Gemini as a free-listing surface (GB-27). AI Mode/Gemini direct checkout additionally requires free-listing approval (GB-04).
- Limitations: Neither page names AI Mode or AI Overviews. Shopify's US-only wording is narrower than Google's country list (Section 2).

### GC-14 Google & YouTube app country sync: India is a supported sync country; multi-market countries become standalone data sources
- Claim: Merchants choose which countries the app syncs to. Google's supported list includes India (languages en, hi). A country that sits in several Shopify Markets is synced as a "Standalone Country" in its own Merchant Center data source.
- Classification: VERIFIED FACT
- Source: Syncing your products — Google Merchant Center Help — https://support.google.com/merchants/answer/13427434?hl=en
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Select the country or countries you wish to sync your products to on Google platforms:"
  > "India | IN | en, hi" (table row as rendered)
  > "Note that if you have configured a single country to be part of multiple Shopify markets, the app will now treat it as a "Standalone Country" to prevent data conflicts."
  > "Ensure your Shopify markets are enabled and have general shipping rates configured for these locations to properly sync your country information to Google."
- Establishes: An India-based Shopify store can sync products to Merchant Center for India and other target countries. Country targets derive from Shopify Markets plus General-profile shipping rates.
- Limitations: Sync country support is not AI Mode/Gemini checkout support. Direct checkout buyers are limited to US/CA/AU (GC-03).

### GC-15 Shopify Catalog and the Google & YouTube feed are two separate pipes; a Shopify merchant needs both for Google direct checkout
- Claim: Shopify Catalog syndicates to ChatGPT, Copilot and Shop (C-01, C-06, C-15). Google discovery uses Merchant Center (GC-01). Google direct checkout requires both a Merchant Center feed and Shopify Catalog eligibility (GC-03). Shopify Catalog inclusion is automatic and cannot be opted out (C-05). So the merchant action for Google is the Merchant Center feed; Catalog eligibility comes with meeting Catalog requirements. Removing Shopify Catalog access does not remove products from Google discovery, because Google uses web crawling and Merchant Center.
- Classification: VERIFIED FACT (each component); "a merchant needs both" = EVIDENCE-BASED INFERENCE from the combined requirements
- Source: Selling on Google AI Mode and Gemini — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google ; Shopify Catalog and product discovery for agentic storefronts — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/products ; Setting up agentic storefronts for stores on the Agentic plan — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/agentic-plan-setup
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Products are made available to Google AI Mode and Gemini through the Google & YouTube sales channel, and to Meta surfaces through the Facebook and Instagram by Meta sales channel."
  > "Even when you opt out of Shopify Catalog access with Shopify's agentic storefronts, your products can still be found in AI channels in the same way that they're listed in traditional search engines such as Google. For example, if one of your products can be discovered in a Google web search, then the same product could also be found by a customer using Google Gemini."
  > "If your products are eligible for Shopify Catalog, they're then available to the ChatGPT and Microsoft Copilot AI channels."
  > "To make your products available to the Google AI Mode and Gemini channel with agentic storefronts, you need to install the Google & YouTube sales channel, and have your products and shipping information automatically synced."
- Establishes: For Google, the Google & YouTube feed is the discovery input. Shopify Catalog is an eligibility gate, not the Google discovery feed. Channel mapping can be set separately for Shopify Catalog and for Google & YouTube (GC-10; C-07), so the two pipes can carry different titles and descriptions.
- Limitations: Shopify does not explain why Catalog eligibility is required for Google. One hypothesis is that Shopify uses Catalog to resolve the product inside its checkout API; this is an UNVERIFIED HYPOTHESIS.

### GC-16 Google's own Shopify addendum: "Google Native Checkout" uses "Shopify's API"; item info flows "through Shopify's technology platform, or through the Google Channel App"
- Claim: Google publishes an Addendum to the Merchant Center Terms of Service for Shopify Merchants. It defines Google Native Checkout as Google using Shopify's API, and Embedded Checkout as Shopify's checkout shown as a layer. Purchase terms and item information reach Google through Shopify's platform or the Google & YouTube app. Order status and tracking reach Google through Shopify's platform. Shopify's Agentic Storefronts Supplemental Terms incorporate this addendum.
- Classification: VERIFIED FACT
- Source: Addendum to the Google Merchant Center Terms of Service for Shopify Merchants — Google for Developers — https://developers.google.com/merchant/terms/shopify ; Shopify Agentic Storefronts Supplemental Terms of Service — Shopify — https://www.shopify.com/legal/terms-agentic-storefronts
- Published/updated: Google addendum "Last updated 2026-01-06 UTC"; Shopify terms "Last updated: October 6, 2026"
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "1.3. "Google Channel App" means the Google-developed application, also known as the 'Google & YouTube' application, available via the Shopify App Store, which enables Merchant to conduct sales and/or other related commerce activity in the Service."
  > "1.4. "Google Native Checkout" means the checkout process where Google uses Shopify's API to enable the User to complete checkout directly in the Service without displaying a separate checkout layer."
  > "1.2. "Embedded Checkout" means a checkout feature where Merchant's checkout is used as a separate layer within the Program's native checkout experience."
  > "Merchant will provide to Google the applicable Purchase Terms and item information through Shopify's technology platform, or through the Google Channel App."
  > "Merchant will provide to Google (using Shopify's technology platform) order information including the following: delivery status ("ordered", "shipped", "delivered") and order tracking number."
  > "Addendum to the Google Merchant Center Terms of Service for Shopify Merchants" (listed under Participating Channel Terms in Shopify's Supplemental Terms)
- Establishes: Google's own document confirms a platform-level integration: Google calls Shopify's API for checkout, rather than each merchant building UCP endpoints. Shopify is the only commerce platform for which a Google-authored platform addendum was found in this pass.
- Limitations: The addendum does not name UCP, Shopify Catalog, `/.well-known/ucp` or the API's endpoints. Excerpts were extracted from the page with line breaks joined. The addendum was last updated before the Sept 2026 enrollment (GC-07).

### GC-17 Does Google consume Shopify Catalog or each store's `/.well-known/ucp`? No source says so explicitly
- Claim: No Shopify or Google page fetched states that Google AI Mode or Gemini reads Shopify Catalog (Global Catalog MCP) or a Shopify store's `/.well-known/ucp`. Shopify states Google discovery is powered by Merchant Center (GC-01). Google states its discovery is powered by the Shopping Graph and Merchant Center feeds (GB-08, GB-10, GB-42). For checkout, Google says it uses "Shopify's API" (GC-16). Live Shopify storefront UCP profiles declare a Google Pay payment handler (`com.google.pay`, spec on pay.google.com) with tokenization gateway `shopify`. Google's own UCP onboarding asks direct merchants to provide a `/.well-known/ucp` URL (GB-12, GB-14).
- Classification: VERIFIED FACT (absence of an explicit statement; profile contents as observed). "Google's Shopify checkout calls Shopify's UCP checkout service declared in these profiles" = EVIDENCE-BASED INFERENCE. "Google discovers Shopify products through Shopify Catalog" = not supported by any source.
- Source: live files https://kith.com/.well-known/ucp ; https://colourpop.com/.well-known/ucp ; https://www.brooklinen.com/.well-known/ucp ; https://www.allbirds.com/.well-known/ucp ; https://theme-horizon-demo.myshopify.com/.well-known/ucp ; https://theme-dawn-demo.myshopify.com/.well-known/ucp ; Shopify storefronts now support UCP 2026-08-25 — Shopify developer changelog — https://shopify.dev/changelog/08-25-is-now-supported
- Published/updated: profiles fetched with response header "Date: Fri, 30 Oct 2026 21:59:55 GMT"; changelog 2026-09-04
- Accessed: 2026-10-30
- Tier: 1 (primary artifacts)
- Excerpt (kith.com profile, keys and values verbatim; merchant IDs omitted):
  > `"payment_handlers": {"com.google.pay": [{"id": "gpay", "version": "2026-01-11", "spec": "https://pay.google.com/gp/p/ucp/2026-01-11/", "schema": "https://pay.google.com/gp/p/ucp/2026-01-11/schemas/config.json", ...`
  > `"tokenization_specification": {"type": "PAYMENT_GATEWAY", "parameters": {"gateway": "shopify", ...`
  > `"allowed_auth_methods": ["PAN_ONLY", "CRYPTOGRAM_3DS"]`
  > `"services": {"dev.ucp.shopping": [{"version": "2026-08-25", ... "transport": "mcp", "endpoint": "https://kithnyc.myshopify.com/api/ucp/mcp", ...}, {"version": "2026-08-25", ... "transport": "embedded", ...}]}`
  > Changelog: "Platforms and agents that speak UCP can use a compatible 2026-08-25 profile to negotiate supported capabilities with Shopify storefronts."
- Establishes: Payment handler keys observed: `com.google.pay`, `dev.shopify.card`, `dev.shopify.shop_pay` on kith.com, colourpop.com, brooklinen.com, allbirds.com and the Horizon demo. The Dawn demo store returns `"payment_handlers": {}`. Profiles also list `supported_versions` 2026-04-08 and 2026-01-23, which covers Google's 2026-04-08 Cart API requirement (GB-14). Google Pay's UCP handler is only needed by a Google Pay–based agent, so its presence fits a Google checkout integration (EVIDENCE-BASED INFERENCE).
- Limitations: The handler config matches Google's UCP FAQ, which says "UCP on Google's AI surfaces only supports PAN_ONLY for the allowed_auth_methods field. You can include other methods (such as CRYPTOGRAM_3DS), but they aren't used during the UCP checkout flow." (https://developers.google.com/merchant/ucp/faq, Last updated 2026-10-16 UTC, fetched 2026-10-30). Why the Dawn demo lacks the handler is unknown (possibly payment-provider setup; UNVERIFIED HYPOTHESIS). Whether the gateway `shopify` value means Shopify Payments is required for Google direct checkout is not stated anywhere (gap). Profiles may vary by requesting agent; these were fetched without a `UCP-Agent` header.

### GC-18 Google's UCP Checkout Addendum (US) defines "Third-Party Sellers" of an e-commerce service and requires Google Pay
- Claim: Google's Checkout Addendum to the Merchant Center Terms (US) requires Google Pay as the wallet in Native Checkout. It makes the Merchant the merchant of record, including for items sold by "Third-Party Sellers" — customers of the Merchant's e-commerce service. It names "AI Mode" in the Chrome browser as a Program surface. No fee clause appears in the addendum.
- Classification: VERIFIED FACT (text); "the Third-Party Sellers clause is how platforms other than Shopify can enrol their merchants" = EVIDENCE-BASED INFERENCE
- Source: Checkout Addendum to the Google Merchant Center Terms of Service — Google — https://merchants.google.com/files/tos/ucp_integration/US/1_00_tos.html (linked from https://support.google.com/merchants/answer/17515932?hl=en)
- Published/updated: "Last Updated: June 24, 2026"
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "“Third-Party Sellers” means, if applicable, a) a third-party customer of Merchant’s e-commerce service and b) who markets and sells their items using such e-commerce service."
  > "Merchant is the merchant of record for all items sold through the Program, including, if applicable, items sold by Third-Party Sellers."
  > "Google Pay’s payment wallet is required for the Program and the Google Pay button will appear in Native Checkout."
  > "The Program allows Users to purchase Merchant’s items on Google services or properties (including Google “AI Mode” in the Chrome browser) with checkout occurring in the Native Checkout."
- Establishes: Google's general UCP checkout terms anticipate an e-commerce service acting for many sellers. Shopify has its own Google addendum (GC-16).
- Limitations: No platform is named in this addendum. The wording "merchant of record … including … items sold by Third-Party Sellers" is unusual for a platform model; how it applies in practice is unknown.

### GC-19 Google's documentation for commerce platforms integrating UCP: none beyond "contact your platform" and a partner waitlist
- Claim: Google's UCP docs tell merchants on third-party platforms to ask their platform about UCP plans (GB-12). The UCP landing page offers a "Partner with us" waitlist. Google's developer blog addresses "AI platforms" (agent builders), not commerce platforms. Merchant Center Help lists BigCommerce, Cafe24, GoDaddy, LojaIntegrada, Prestashop, STORES, Wix and WooCommerce as non-Google platforms with their own support, and states Shopify "is supported by Google". No Google page fetched describes a platform or technology-partner onboarding process for UCP.
- Classification: VERIFIED FACT (statements); "no platform onboarding doc exists" = EVIDENCE-BASED INFERENCE (not found)
- Source: About Universal Commerce Protocol (UCP) integration hub in Merchant Center — Google for Developers — https://developers.google.com/merchant/ucp/guides/merchant-center/overview ; Getting started with Universal Commerce Protocol on Google — Google for Developers — https://developers.google.com/merchant/ucp ; Under the Hood: Universal Commerce Protocol (UCP) — Google Developers Blog — https://developers.googleblog.com/under-the-hood-universal-commerce-protocol-ucp/ ; How to find support if you use a non-Google platform — Google Merchant Center Help — https://support.google.com/merchants/answer/12048683?hl=en ; Universal Commerce Protocol Checkout Terms of Service (US only) — https://support.google.com/merchants/answer/17515932?hl=en
- Published/updated: hub overview "Last updated 2026-10-19 UTC"; developers blog 2026-01-11; others not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "If you work with a third-party service provider or platform, contact them directly to learn about their UCP integration plans."
  > "Join the waitlist to become part of an ecosystem of industry leaders adopting the protocol to drive the next generation of commerce."
  > "For AI platforms: With UCP, you can enable agentic shopping for your audiences. You can simplify business onboarding using standardized APIs while giving them flexibility to use MCP, A2A and existing agent frameworks of their choice."
  > "If you primarily use a platform other than Merchant Center (such as GoDaddy, WooCommerce, etc) to run your online retail business through Google, you may need to check that platform’s support offerings to help resolve issues with your account."
  > "Review the Checkout Addendum to the Google Merchant Center Terms of Service. This Terms of Service applies to the United States only."
- Establishes: Platform onboarding for Google UCP is negotiated privately (Shopify addendum, GC-16; BigCommerce, Salesforce, commercetools and Stripe announcements, GC-28–GC-31). Merchants on other platforms enter through the platform or through Google's own interest form and hub.
- Limitations: The "Partner with us" waitlist form was not opened. Google may have non-public partner docs.

### GC-20 Product-eligibility mismatch: Google's UCP exclusion list is broader than Shopify's unsupported list; the `checkout_eligibility` flag for Shopify offers is undocumented
- Claim: Google's UCP guide excludes subscriptions, personalized goods, used/refurbished, final-sale, pre-order, freight, age-restricted and other items from checkout and requires `native_commerce(checkout_eligibility)` = TRUE per item (default FALSE) (GB-05, GB-06). Shopify's Google page lists only subscription-only, bundles, customizable and B2B-only products as unsupported (GC-04). Shopify and Google's enrollment email say eligible Shopify products are included automatically with nothing to set up (GC-02, GC-07). No source states who sets `checkout_eligibility` for Shopify offers or whether Shopify-path offers use that attribute at all.
- Classification: VERIFIED FACT (both lists); mechanism = knowledge gap
- Source: Selling on Google AI Mode and Gemini — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google ; GB-05, GB-06 (Google UCP Merchant Center guide, https://developers.google.com/merchant/ucp/guides/overview/merchant-center, Last updated 2026-10-29 UTC)
- Published/updated: Shopify not stated; Google 2026-10-29
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "The following types of products aren't supported in Google AI Mode and Gemini's direct checkout:" … "Product bundles" / "Customizable products" / "B2B-only products" (Shopify)
  > "This opts a product into the checkout experience on Google." … "If set to FALSE or missing, the product won't be eligible for checkout (defaults to FALSE)." (Google UCP guide, fetched by GC on 2026-10-30; see GB-05)
- Establishes: The Shopify path and the direct UCP path have different documented eligibility rules.
- Limitations: Google's guide is written for direct merchants; it may not apply to the Shopify platform path (UNVERIFIED HYPOTHESIS).

### GC-21 Shopify newsroom (Jan 11, 2026): Google selling "rolling out soon", managed in Shopify Admin; Catalog data "surfaced everywhere, including … Google AI Mode, and Gemini"
- Claim: At UCP launch Shopify said native shopping on Google would roll out soon, managed from the Shopify Admin through Agentic Storefronts, and named Monos, Gymshark and Everlane as early brands. The same post said Agentic-plan data is surfaced in Google AI Mode and Gemini through Agentic Storefronts.
- Classification: VERIFIED FACT (statements). The "surfaced everywhere, including … Google AI Mode" sentence is superseded for discovery by the Oct 2026 help pages (GC-01) — EVIDENCE-BASED INFERENCE.
- Source: The agentic commerce platform: Shopify connects any merchant to every AI conversation — Shopify Newsroom — https://www.shopify.com/news/ai-commerce-at-scale
- Published/updated: datePublished 2026-01-11T14:58:43Z
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Native shopping on Google surfaces is rolling out soon, which means Shopify merchants can sell directly in AI Mode in Google Search and the Gemini app."
  > "In both Gemini app and AI Mode in Google Search, merchants will be able to sell in an embedded experience and manage it directly from the Shopify Admin."
  > "Brands like Monos, Gymshark, and Everlane will soon sell directly in AI Mode in Google Search and the Gemini app, and merchants like Keen and Pura Vida are using Copilot Checkout to reach their customers."
  > "Merchants set up their data once, and through Shopify's Agentic Storefronts, that data is surfaced everywhere, including ChatGPT, Microsoft Copilot, Google AI Mode, and Gemini."
- Establishes: January 2026 baseline: Google channel announced, not live. The Jan post described an "embedded experience"; Google's Shopify addendum defines both Native and Embedded checkout (GC-16).
- Limitations: The post does not say how product data reaches Google. Already cited for UCP co-development in C-16.

### GC-22 Shopify blog (Apr 2, 2026): "Shopify stores are UCP-enabled by default"; Google & YouTube channel is step one
- Claim: Shopify's blog says Google's agentic checkout runs on UCP and Shopify stores are UCP-enabled by default with no extra setup. It says Google AI shopping relies on Merchant Center data and lists installing the Google & YouTube channel as the first step. It describes the Google channel as "rolling out in early access".
- Classification: VERIFIED FACT (Shopify statements). Tier 1 vendor blog with marketing tone.
- Source: Google AI Shopping Features: How to Maximize Your Visibility (2026) — Shopify Blog — https://www.shopify.com/blog/google-ai-shopping
- Published/updated: datePublished 2026-04-02; dateModified 2026-04-02
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Google's agentic checkout capability, which is currently rolling out in the US and may not be available for all merchants, is powered by the Universal Commerce Protocol (UCP), an open standard co-developed by Shopify and Google."
  > "Shopify stores are UCP-enabled by default, so no additional setup is required to support agentic checkout."
  > "With Shopify Agentic Storefronts (currently rolling out in early access), merchants can sell directly in Google AI Mode and the Gemini app, allowing shoppers to move from conversation to checkout without leaving the experience."
  > "The Google & YouTube sales channel in Shopify syncs your products and store data with your Google Merchant Center account."
- Establishes: Shopify's own framing matches GC-01 (Merchant Center for data) and GC-17 (UCP built into every store).
- Limitations: The blog uses "agentic checkout" loosely; Google uses that term for merchant-site checkout and "UCP-powered checkout" for on-Google checkout (GB-02). Blog advice content is not recorded.

### GC-23 Google I/O (May 19, 2026): Universal Cart names Shopify merchants Fenty and Steve Madden; UCP checkout to Canada and Australia "in the coming months"
- Claim: Google's Universal Cart post lists Shopify merchants among those where select checkout features would be tried soon. Google said UCP-powered checkout would expand to Canada and Australia in the coming months and later the UK. Universal Cart rolls out in the US across Search and the Gemini app.
- Classification: VERIFIED FACT
- Source: Introducing the Universal Cart and more ways to help you shop — The Keyword (Google) — https://blog.google/products-and-platforms/products/shopping/google-shopping-cart/
- Published/updated: datePublished 2026-05-19
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "You can try these select checkout features soon across merchants like Nike, Sephora, Target, Ulta Beauty, Walmart, Wayfair and Shopify merchants such as Fenty and Steve Madden."
  > "Building on that momentum, we’re expanding our UCP-powered checkout experience on Google to Canada and Australia in the coming months and later to the U.K."
  > "Universal Cart is rolling out across Search and the Gemini app in the U.S. this summer, with YouTube and Gmail to follow."
- Establishes: Google's CA/AU plan (May) precedes Shopify's Oct 2026 CA/AU buyer expansion (GC-06). The parallel Google Marketing Live post (May 20) is GB-19; Universal Cart consumer rules are GB-16.
- Limitations: "Select checkout features" is not defined per merchant.

### GC-24 Google (Sept 16, 2026): UCP direct checkout for "hundreds of thousands of brands and retailers"; hub capabilities US-first; AI performance insights include India
- Claim: Google said UCP already enables direct checkout for hundreds of thousands of brands and retailers. New Merchant Center hub capabilities roll out in the US, with Australia and Canada early next year. AI performance insights became available in Australia, Canada, India, New Zealand and the US. Google reported conversational attributes from lululemon were used in 50% of relevant AI Mode recommendations in testing.
- Classification: VERIFIED FACT (Google statements); "the 'hundreds of thousands' figure is mostly Shopify merchants enrolled by default" = EVIDENCE-BASED INFERENCE (scale plus timing with GC-07; Google does not say so)
- Source: Boost your holiday sales with these agentic commerce updates — The Keyword (Google) — https://blog.google/products-and-platforms/products/shopping/google-shopping-updates-holiday-shopping/
- Published/updated: datePublished 2026-09-16
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "UCP already enables direct checkout for hundreds of thousands of brands and retailers across Google."
  > "The new capabilities are gradually rolling out in the U.S., with Australia and Canada to follow early next year."
  > "To help, AI performance insights in Merchant Center is now available to businesses across Australia, Canada, India, New Zealand, and the U.S."
  > "During testing with lululemon, conversational attributes submitted from the brand were incorporated 50% of the time in relevant product recommendations in AI Mode, providing shoppers with more precise and helpful answers."
- Establishes: Timeline anchor two days before the Shopify enrollment emails (GC-07). AI performance insights details are in GB-26.
- Limitations: "Hundreds of thousands" is not broken down by platform. Google's lululemon figure is a single-brand test.

### GC-25 AI Overviews: no Shopify-specific path documented
- Claim: No Shopify page fetched mentions AI Overviews. Shopify's agentic channel covers AI Mode and Gemini only. Google says AI Overviews need no extra technical requirements (GB-28), that crawled products can appear without Merchant Center (GB-27), and that AI performance insights cover AI Mode and AI Overviews (GB-26). For a Shopify store, the paths into AI Overviews are therefore the open-web crawl of the storefront (C-11, C-18, C-26) and Merchant Center/Shopping Graph data (GC-01, GC-09).
- Classification: VERIFIED FACT (absence on Shopify pages); path statement = EVIDENCE-BASED INFERENCE
- Source: Shopify agentic storefronts — Shopify Help Center — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts ; GB-26, GB-27, GB-28
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Shopify's agentic storefronts lets customers discover and purchase your products in AI channels, such as ChatGPT, Google AI Mode and Gemini, Microsoft Copilot, and Meta."
- Establishes: AI Overviews are outside Shopify's Agentic Storefronts product scope.
- Limitations: How AI Overviews select product results is outside this agent's scope (see GB notes).

### GC-26 India status (synthesis)
- Claim: Buyers in India cannot use Shopify-powered direct checkout in AI Mode or Gemini; only US, Canada and Australia buyers can (GC-03, GC-06). An India-based Shopify store can still qualify if it sells to US, Canadian or Australian buyers (GC-03). Indian shoppers can use Gemini shopping, which Google lists for India (GB-15). India is a supported Google & YouTube sync country (GC-14) and a free-listings country (GC-13). Merchant Center AI performance insights cover India (GC-24, GB-26). Google's UCP checkout terms are US-only (GC-19).
- Classification: VERIFIED FACT (components); synthesis = EVIDENCE-BASED INFERENCE
- Source: GC-03, GC-06, GC-13, GC-14, GC-24; GB-15, GB-26
- Published/updated: see component findings
- Accessed: 2026-10-30
- Tier: 1 (via components)
- Excerpt: see component findings.
- Establishes: For Indian buyers, Shopify products reach Gemini/AI Mode only as discovery (Merchant Center/Shopping Graph or crawl), with checkout on the merchant's site.
- Limitations: Before an unrecorded date between 2026-10-19 and 2026-10-30, Shopify required stores to be US-based (Section 2). No source gives an India roadmap for UCP checkout.

---

## Other platforms → Google AI surfaces

### GC-27 WooCommerce: discovery via Google for WooCommerce (Merchant Center); Google UCP marked "Coming soon"; WooCommerce AI exposes UCP endpoints but needs each service's onboarding
- Claim: Woo's agentic-commerce page (modified Oct 25, 2026) lists "Universal Commerce Protocol (UCP) — Google" as "Coming soon" and points to Google for WooCommerce, which syncs the catalog to Merchant Center. WooCommerce AI 0.8.0 ships UCP REST endpoints advertising UCP 2026-04-08, proxied through WordPress.com by default. Woo's docs say a store must also complete each shopping service's onboarding. Woo's Aug 2026 post says Google's UCP version "runs on Google Merchant Center". Woo also says Stripe ACS reaches Gemini.
- Classification: VERIFIED FACT (Woo statements); "no live Woo → Google UCP checkout as of Oct 2026" = EVIDENCE-BASED INFERENCE from "Coming soon"
- Source: Agentic Commerce — WooCommerce — https://woocommerce.com/agentic-commerce/ ; Integrate with the WooCommerce AI UCP REST API — WooCommerce Docs — https://woocommerce.com/document/woocommerce-ai/ucp-rest-api/ ; Enable agentic commerce in WooCommerce AI — WooCommerce Docs — https://woocommerce.com/document/woocommerce-ai/agentic-commerce/ ; From found to bought: Getting your store ready to sell through AI — WooCommerce — https://woocommerce.com/posts/selling-though-ai/
- Published/updated: agentic-commerce page published 2026-08-06, modified 2026-10-25; UCP REST doc 2026-10-23; agentic-commerce doc 2026-10-23; post published 2026-08-01, modified 2026-09-03 (page metadata)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Universal Commerce Protocol (UCP) — Google" / "Google’s protocol for AI-powered shopping. If you already sync to Google Merchant Center or use structured data, you have the foundation." (status label "Coming soon")
  > "Syncs your product catalog to Google Merchant Center, making your products visible to Google AI."
  > "This reference describes the UCP endpoints shipped in WooCommerce AI 0.8.0. The plugin advertises UCP version 2026-04-08."
  > "WordPress.com proxy mode is enabled by default."
  > "To use an external shopping service, your store also needs to complete that service’s onboarding and use a supported payment method."
  > "Still being built. Google’s version runs on Google Merchant Center and uses your structured product data."
  > "With Stripe’s Agentic Commerce Suite, one implementation is all it takes to find and buy your products across different AI assistants (like Copilot or Gemini)."
- Establishes: Woo → Google discovery = Merchant Center feed (same model as Shopify's GC-01). Woo → Google checkout = not live via Woo; possible via Stripe ACS (GC-32) or a merchant's own Google onboarding. ChatGPT-side Woo facts are C-30.
- Limitations: Third-party plugins (e.g., WebToffee "UCP Enabler for WooCommerce" on wordpress.org, seen but not analysed) are not Woo's own path.

### GC-28 BigCommerce / Commerce: UCP endorsement (Jan 11, 2026); Google UCP checkout in early access via Commerce AI Labs, "early Q4 2026, subject to Google approval"
- Claim: Commerce endorsed UCP on Jan 11, 2026 and said it is "building toward the protocol", with Feedonomics enriching feeds for Google. BigCommerce's Oct 2026 guide says the Google UCP checkout path is in early access through Commerce AI Labs ("Agentic Checkout with Google UCP") in Channel Manager, timed for early Q4 2026 subject to Google approval. Commerce's April 2026 Feedonomics ACE syndication to Google Gemini is C-31.
- Classification: VERIFIED FACT (vendor statements); live GA = UNVERIFIED
- Source: Commerce Supports Universal Commerce Protocol, Plans to Offer Buying Directly Across Google’s AI Surfaces — Commerce (GlobeNewswire) — https://investors.bigcommerce.com/news-releases/news-release-details/commerce-supports-universal-commerce-protocol-plans-offer-buying ; Google Agentic Checkout: How to Enable Buying in AI Mode and Gemini via UCP — BigCommerce — https://www.bigcommerce.com/articles/ecommerce/google-agentic-checkout/
- Published/updated: Jan. 11, 2026; article datePublished 2026-10-02, dateModified 2026-10-13
- Accessed: 2026-10-30 (press release: curl HTTP 403; text captured in the in-app browser)
- Tier: 1
- Excerpt:
  > "To start, UCP will soon enable a new checkout feature on product listings in AI Mode in Search and the Gemini app, allowing shoppers to buy directly from eligible US retailers and Commerce merchants right as they’re researching on Google."
  > "As part of the collaboration, Commerce is building toward the protocol to allow merchants to:"
  > "This layer structures and optimizes product feeds to align with Google’s schema, dynamically enhancing titles, attributes, and taxonomy to ensure high-quality data that boosts product visibility, improves match rates, and conversion with the Google ecosystem."
  > "For BigCommerce merchants, the Google UCP checkout path is available now in early access through the Commerce AI Labs program (“Agentic Checkout with Google UCP”), built into Channel Manager."
  > "Timing: early Q4 2026, subject to Google approval. Request early access through Commerce AI Labs."
- Establishes: BigCommerce = opt-in early access, Merchant Center feed via Feedonomics, no default-on enrolment (contrast GC-02).
- Limitations: The Oct 2026 article is a vendor explainer, not a release note. No BigCommerce source confirms general availability.

### GC-29 Salesforce Agentforce Commerce (B2C Commerce): UCP support (Jan 14, 2026) → "GA summer 2026" (C-32) → "arriving in the coming months" (Jul 6) → "now live" (Oct 26, 2026)
- Claim: Salesforce announced native UCP support for Google AI surfaces on Jan 14, 2026. In June it listed Google Search/AI Mode/Gemini as "GA summer 2026" (C-32). On July 6 it said the Google integration was "arriving in the coming months". Its October 2026 B2C Commerce release says UCP integration is now live and merchants can turn on UCP-powered checkout on Google.
- Classification: VERIFIED FACT
- Source: Salesforce Announces Support for Google’s Universal Commerce Protocol to Bring Product Discovery and Checkout into Conversational AI — Salesforce — https://www.salesforce.com/news/stories/google-universal-commerce-protocol-support-announcement/ ; As AI Agents Transform Commerce, Salesforce Unleashes Its Biggest Agentforce Commerce Release Yet (APAC) — Salesforce — https://www.salesforce.com/ap/news/press-releases/2026/07/06/as-ai-agents-transform-commerce-salesforce-unleashes-its-biggest-agentforce-commerce-release-yet/ ; Peak-Ready Precision: The October 2026 B2C Commerce Release — Salesforce Blog — https://www.salesforce.com/blog/b2c-commerce-october-26-release/
- Published/updated: 2026-01-14 (modified 2026-01-15); 2026-07-06; 2026-10-26 (page metadata)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "As part of this, Salesforce will empower Agentforce Commerce merchants with native UCP support, unlocking new AI-driven shopping journeys across Google’s AI surfaces, including AI Mode in Search and the Gemini app."
  > "Salesforce will share additional details on timelines and merchant onboarding as they are finalized."
  > "The agents are here: Shopper Agent, Buyer Agent, and Merchant Agent are generally available now — with native integration into ChatGPT; Google Search, including AI Mode; and the Gemini app arriving in the coming months."
  > "Integration with the Universal Commerce Protocol (UCP) is now live"
  > "Merchants can now turn on UCP-powered checkout on Google to enable shoppers to seamlessly discover and buy products directly on surfaces like the Gemini app and Google Search, including AI Mode — while staying the merchant of record."
- Establishes: Salesforce's Google path went live on or before Oct 26, 2026, later than the "summer 2026" target. Activation is merchant opt-in ("can now turn on"), not default-on.
- Limitations: The October post does not state countries, eligibility or whether Merchant Center feeds are required. Feed/catalog details for Google are not in the excerpts captured.

### GC-30 commercetools AI Hub (GA July 30, 2026): Gemini end-to-end via UCP; Stripe ACS named for Gemini too
- Claim: commercetools' AI Hub GA note says Gemini supports discovery through checkout via UCP with Adyen, Stripe, CyberSource or Worldpay Access (C-33). The same note says Stripe ACS enables agentic checkout across ChatGPT, Copilot, Gemini and Perplexity for Stripe merchants.
- Classification: VERIFIED FACT
- Source: AI Hub is now generally available — commercetools docs — https://docs.commercetools.com/api/releases/2026-07-30-ai-hub-is-now-generally-available
- Published/updated: 30 July 2026
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Google Gemini supports the end-to-end flow from discovery through checkout using the Universal Commerce Protocol (UCP), with payments through Adyen, Stripe, CyberSource, or Worldpay Access."
  > "The Stripe Agentic Commerce Suite (ACS) enables agentic checkout across ChatGPT, Copilot, Gemini, and Perplexity through a single integration for Stripe merchants."
- Establishes: commercetools names Gemini only (not AI Mode) and claims "discovery" through UCP; it does not say discovery bypasses Merchant Center.
- Limitations: AI Hub is an add-on (C-33). The note does not mention Merchant Center; whether commercetools merchants still need a Merchant Center feed is not stated (gap; Google's docs require one, GB-04).

### GC-31 Stripe Agentic Commerce Suite → Google: partnership "soon" (Apr 29, 2026); US entities "can already sell" via Gemini (Jun 30, 2026)
- Claim: Stripe announced a partnership with Google on Apr 29, 2026 so ACS businesses can sell inside AI Mode and the Gemini app via UCP, initially "soon". On Jun 30, 2026 Stripe said businesses with US entities can already sell to US customers via platforms including Gemini and Copilot. Stripe ACS is the stated Google path for Wix, BigCommerce, WooCommerce and others (C-37).
- Classification: VERIFIED FACT
- Source: Stripe builds out the economic infrastructure for AI with 288 launches — Stripe Newsroom — https://stripe.com/newsroom/news/sessions-2026 ; Everything we announced at Sessions 2026 — Stripe Blog — https://stripe.com/blog/everything-we-announced-at-sessions-2026 ; New tools from Stripe allow German businesses to sell globally—including to AI agents — Stripe Newsroom — https://stripe.com/newsroom/news/stripe-tour-berlin-2026
- Published/updated: 2026-04-29; 2026-04-29; 2026-06-30 (page metadata)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Today, Stripe announced a partnership with Google that will allow businesses to sell to consumers inside AI Mode and the Gemini app."
  > "Customers will soon be able to buy your products in AI Mode and the Gemini app via the Universal Commerce Protocol (UCP), through a new partnership between Stripe and Google."
  > "Businesses with entities in the US can already sell to customers in the US via platforms including Gemini and Copilot."
- Establishes: A second platform-level rail into Google checkout exists besides Shopify (Stripe as the "e-commerce service" model; compare GC-18).
- Limitations: The Jun 30 sentence is in a Germany-focused release; it does not say whether all ACS businesses or only selected ones are live on Gemini. Product discovery for Stripe-path merchants on Google is not described (Merchant Center still required per GB-04 — EVIDENCE-BASED INFERENCE).

### GC-32 Wix: Google & YouTube app on Wix sends products to Merchant Center with checkout on the Wix store; Stripe ACS is Wix's multi-agent path
- Claim: Wix's Google & YouTube app creates free listings across Google and sends shoppers back to the Wix store for checkout. Wix's agentic-commerce post says Stripe ACS (via Wix Payments) covers multiple agents including Gemini, and that browser co-pilots such as Gemini in Chrome read Wix sites directly. No Wix source found announces UCP-powered checkout in AI Mode.
- Classification: VERIFIED FACT (statements); "no Wix → Google UCP checkout announcement" = EVIDENCE-BASED INFERENCE (not found)
- Source: Google & YouTube — Wix App Market — https://www.wix.com/app-market/google-merchant-solutions ; Agentic commerce on Wix and how AI agents can sell your products — Wix Blog — https://www.wix.com/blog/agentic-commerce-on-wix
- Published/updated: app page not stated; blog published 2026-07-27, modified 2026-10-26
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Your products will be shown in search results across Google—from Google Search to Google Shopping and more. When a customer clicks on your listing, they’ll be brought back to your Wix store to complete checkout."
  > "You're not building one integration for ChatGPT and another for Gemini and another for Perplexity because Wix Payments does the heavy lifting."
  > "In the second, an AI agent (typically a browser co-pilot like Gemini in Chrome) visits your Wix site directly and reads it the way a careful shopper would."
- Establishes: Wix → Google = Merchant Center feed (discovery) + Stripe ACS (checkout, rollout per C-35) + on-site crawl.
- Limitations: Wix says the ACS integration is "rolling out gradually" (C-35). The app listing does not mention AI Mode or Gemini.

### GC-33 Squarespace: Merchant Center integration for physical products; no AI Mode or UCP statement found
- Claim: Squarespace syncs physical products automatically to Google Merchant Center on Core, Plus, Advanced, Commerce Basic and Commerce Advanced plans. The help article does not mention AI Mode, Gemini or UCP. Squarespace's AI Visibility report and Stripe ACS listing are C-36.
- Classification: VERIFIED FACT (statements); absence of a Google AI checkout path = EVIDENCE-BASED INFERENCE
- Source: Display your products in Google Shopping — Squarespace Help Center — https://support.squarespace.com/hc/en-us/articles/12131658984717-Display-your-products-in-Google-Shopping
- Published/updated: "Last updated September 9, 2026"
- Accessed: 2026-10-30 (curl returned a JavaScript shell; text captured in the in-app browser)
- Tier: 1
- Excerpt:
  > "Using our integration with Google Merchant Center, you can display your physical products in product listings across Google, like in Google Shopping, Google image searches, and on YouTube."
  > "This integration is available in Core, Plus, Advanced, Commerce Basic, and Commerce Advanced plans."
  > "You can’t sync only specific physical products, but you can choose which products display on Google from your Google Merchant Center account."
- Establishes: Squarespace stores reach Google AI surfaces only through Merchant Center/Shopping Graph and crawl, as far as found.
- Limitations: Squarespace newsroom not searched exhaustively.

### GC-34 Adobe Commerce: committed to UCP (Feb 18, 2026); no live Google UCP checkout found
- Claim: Adobe committed to support UCP and ACP and to make catalogs available to Gemini and ChatGPT (C-34). No Adobe source found in this pass announces live UCP checkout on AI Mode or Gemini.
- Classification: VERIFIED FACT (statement, via C-34 and re-read); absence = EVIDENCE-BASED INFERENCE
- Source: Adobe Commerce commits to agentic commerce standards — Adobe — https://business.adobe.com/blog/adobe-commerce-commits-to-agentic-commerce-standards
- Published/updated: 02-18-2026
- Accessed: 2026-10-30 (curl timed out; text read in the in-app browser)
- Tier: 1
- Excerpt:
  > "Adobe Commerce is moving towards supporting UCP and ACP by making merchant product catalogs, pricing, and inventory machine-readable by AI agents and available to the latest LLM surfaces like Gemini and ChatGPT."
  > "With support for UCP and ACP, and additional capabilities planned throughout the year, Adobe Commerce provides a foundation for agentic commerce, helping brands engage customers wherever and however intent emerges."
- Establishes: Adobe's Google path is stated as direction, not a shipped channel.
- Limitations: Adobe Experience League release notes were not searched exhaustively. Tier 3 search snippets mention a "Commerce MCP" (Apr 2026) — not verified.

### GC-35 Platform comparison: only Shopify is default-on for Google checkout
- Claim: Shopify enrolls eligible stores in Google direct checkout by default (GC-02, GC-07). Salesforce requires the merchant to turn it on (GC-29). BigCommerce is early access on request (GC-28). commercetools requires the AI Hub add-on (GC-30, C-33). WooCommerce marks Google UCP "Coming soon" (GC-27). Stripe ACS is a separate opt-in rail (GC-31). Wix, Squarespace and Adobe have no live Google UCP checkout found (GC-32–GC-34). All platforms found rely on Merchant Center for Google discovery where they state a discovery path (GC-01, GC-27, GC-28, GC-32, GC-33).
- Classification: EVIDENCE-BASED INFERENCE (comparison across findings)
- Source: GC-02, GC-07, GC-27–GC-34
- Published/updated: see component findings
- Accessed: 2026-10-30
- Tier: 1 (via components)
- Excerpt: see component findings.
- Establishes: The Shopify default makes Shopify merchants the largest likely population with Google checkout enabled (consistent with GC-24's "hundreds of thousands"; inference).
- Limitations: Default-on status for other platforms could change without a public announcement.

---

## 2. Contradictions and superseded information

- **Shopify eligibility changed in late Oct 2026 (superseded text).** Wayback snapshots of https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google dated 2026-09-21 (`20260921030354`) and 2026-10-19 (`20261019124501`), read in the in-app browser on 2026-10-30, say: "Your store must be based in the United States and you must sell to customers in the United States." and "Google AI Mode and Gemini's direct checkout is displayed only to customers based in the United States. Customers based elsewhere can still discover your products, but they're redirected to your online store to complete their purchase." The live page on 2026-10-30 says buyers in the US, Canada or Australia and stores based in any country (GC-03, GC-06). The same snapshots list "Subscriptions" as unsupported; the live page allows the one-time-purchase option of a subscription product (GC-04). The change date lies between 2026-10-19 and 2026-10-30. Search Engine Land (Sept 22, 2026) reflects the old text (GC-07).
- **Canada/Australia timing: Shopify vs Google.** Shopify (live, Oct 2026): direct checkout "rolling out gradually to customers based in the United States, Canada, and Australia" (GC-06). Google, May 19, 2026: CA/AU "in the coming months" (GC-23). Google, Sept 16 and Oct 19, 2026: Merchant Center UCP hub capabilities US first, "Australia and Canada to follow early next year" (GC-24, GB-12). Google Search Help: AI Mode checkout is US-only for buyers (GB-09). The Google hub dates concern the direct-merchant path; the Google Search Help buyer restriction conflicts with Shopify's CA/AU buyer statement unless that page is stale. Not resolved.
- **Shopify Catalog "surfaced everywhere, including … Google AI Mode" (Jan 2026) vs Merchant Center-powered discovery (Oct 2026).** Shopify's Jan 11, 2026 post (GC-21) implies Catalog data reaches Google AI Mode. Shopify's current Help Center says Google discovery is powered by Merchant Center, not a Shopify Catalog access setting (GC-01). Treat the January sentence as superseded for Google discovery.
- **Free listings country scope.** Shopify's Google & YouTube page says free display applies "for eligible stores selling in the United States" (GC-13). Google's Shopify free-listings page lists many countries including India (GC-13). The Shopify sentence is outdated or narrower than Google's.
- **Global Catalog switch vs Google channel.** agentic-home: "Direct checkout is also deactivated when Shopify Catalog access is turned off." data-privacy: for Google "product discovery is powered by individual sales channels rather than a Shopify Catalog access setting." Shopify does not say whether turning off global Catalog access disables Google direct checkout (GC-02).
- **Rollout labels.** Shopify blog (Apr 2, 2026): "currently rolling out in early access" (GC-22). Shopify Help (Oct 2026): "rolling out to eligible stores" (GC-06). Search Engine Roundtable (Tier 3): UCP checkout "launched in February" (GC-07). Google (Sept 16, 2026): direct checkout for "hundreds of thousands of brands and retailers" (GC-24).
- **Product eligibility lists differ.** Google's UCP exclusions (GB-06) include used, refurbished, final-sale, pre-order and personalized goods. Shopify's Google page lists only subscription-only, bundles, customizable and B2B-only (GC-20).
- **Salesforce timing slipped.** "GA summer 2026" (June 24, C-32) → "arriving in the coming months" (July 6) → "now live" (Oct 26) (GC-29).
- **Stripe timing.** "Soon" (Apr 29) → US entities "can already sell" via Gemini (Jun 30) (GC-31).
- **WooCommerce signals.** WooCommerce AI ships UCP endpoints (Oct 23, 2026) while Woo's protocol page marks Google UCP "Coming soon" (Oct 25, 2026) (GC-27). Not a contradiction: store-side UCP endpoints exist; the Google channel is not live.
- **Outdated URL.** https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/ai-channels-with-built-in-checkout (returned in search results) now 307-redirects to the Microsoft Copilot page.

## 3. Knowledge gaps

- Which "Shopify's API" Google calls for native checkout (GC-16): Shopify's UCP checkout service declared at `/.well-known/ucp`, a private API, or another endpoint. No source names it.
- Whether Google ever reads Shopify Catalog (Global or Storefront Catalog MCP) for discovery, ranking or enrichment. No source says it does (GC-17).
- How `native_commerce(checkout_eligibility)` is set (or bypassed) for Shopify offers in Merchant Center, given Google's default FALSE (GC-20, GB-05).
- How Google "matches" a Shopify store to a Merchant Center account (GC-07), and whether matching works for merchants who feed Merchant Center through a third-party feed tool instead of the Google & YouTube app.
- Whether Shopify Payments is required for Google direct checkout. Live profiles show a Google Pay handler with gateway `shopify` (GC-17); Shopify's requirements list no payment-provider rule (GC-03).
- Why Shopify Catalog eligibility is a requirement for the Google channel (GC-15).
- Exact date (between 2026-10-19 and 2026-10-30) of Shopify's CA/AU buyer and any-country store expansion.
- Whether the Google & YouTube app maps Shopify's Standard Product Taxonomy category to `google_product_category`, and whether its "Condition" label fills Merchant Center `condition` (GC-10).
- Whether the Google & YouTube app sends Google's new conversational attributes (`question_and_answer`, `popularity_rank`, `related_product`, GB-21–GB-24), `video_link` (GB-25) or `native_commerce` from Shopify data or metafields. No Shopify or Google page fetched says so.
- Whether Shopify-path orders appear in Merchant Center's UCP analytics tab.
- Google ranking effect of Shopify direct checkout: Google says native integration does not influence ranking (GB-07); nothing Shopify-specific.
- AI Overviews: no Shopify-specific documentation (GC-25).
- Live, generally available Google UCP checkout status for BigCommerce, Wix, WooCommerce, Squarespace and Adobe Commerce; countries and eligibility for Salesforce's live integration.
- India: no roadmap from Shopify or Google for UCP checkout buyers in India.

## 4. Unfetched sources

- `web.archive.org/web/<ts>id_/...` raw snapshots via curl — HTTP 429 on three attempts. The 2026-09-21 and 2026-10-19 snapshots were read in the in-app browser (standard replay) instead. The 2026-10-04 snapshots were not read.
- https://investors.bigcommerce.com/news-releases/news-release-details/commerce-supports-universal-commerce-protocol-plans-offer-buying — curl HTTP 403; read in the in-app browser.
- https://business.adobe.com/blog/adobe-commerce-commits-to-agentic-commerce-standards and https://business.adobe.com/blog/product-discovery-on-llm-surfaces-is-available-in-adobe-commerce — curl timed out; the first was read in the in-app browser; the second relies on C-34.
- https://support.squarespace.com/hc/en-us/articles/12131658984717-Display-your-products-in-Google-Shopping — curl returned a JavaScript shell; read in the in-app browser.
- Google UCP interest form and "Partner with us" waitlist — not opened (forms).
- Shopify Editions Summer '26 page — not located on shopify.com in this pass (seen only in Tier 3 search results).
- Tier 3, seen only in search results and not cited: techwyse.com, xgentech.net, theroberthu.com, digitalapplied.com, brandmediaworks.com, virtina.com, intuz.com, seresa.io, jumpfly.com, metizsoft.com, stellagent.ai (various Shopify/Google UCP explainers); pymnts.com and emarketer.com holiday coverage.
- Google Merchant Center Help pages on UCP and the UCP developer guides were fetched by this agent on 2026-10-30 but are cited through GB IDs per coordinator instruction where GB covers them.

## 5. Source list

Shopify (Tier 1)
- Shopify agentic storefronts — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts
- Selling on Google AI Mode and Gemini — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/google (live; Wayback 20260921030354 and 20261019124501)
- Managing agentic storefronts — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/agentic-home
- Data sharing and privacy for selling with agentic storefronts — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/data-privacy
- Shopify Catalog and product discovery for agentic storefronts — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/products
- Setting up agentic storefronts for stores on the Agentic plan — https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/agentic-plan-setup
- Google & YouTube — https://help.shopify.com/en/manual/online-sales-channels/google
- Google & YouTube channel requirements — https://help.shopify.com/en/manual/online-sales-channels/marketplaces/google/requirements
- Syncing your products (Shopify) — https://help.shopify.com/en/manual/online-sales-channels/marketplaces/google/getting-setup/syncing-products
- Customizing product data for sales channels — https://help.shopify.com/en/manual/online-sales-channels/channel-mapping
- Shopify Agentic Storefronts Supplemental Terms (Oct 6, 2026) — https://www.shopify.com/legal/terms-agentic-storefronts
- Newsroom, Jan 11, 2026 — https://www.shopify.com/news/ai-commerce-at-scale
- Blog, Apr 2, 2026 — https://www.shopify.com/blog/google-ai-shopping
- Google & YouTube app listing — https://apps.shopify.com/google
- shopify.dev changelog feed — https://shopify.dev/changelog/feed.xml ; entries: https://shopify.dev/changelog/08-25-is-now-supported ; https://shopify.dev/changelog/cart-and-checkout-permalinks-now-support-ucp-at-buy ; https://shopify.dev/changelog/global-catalog-rest-api-stops-serving-traffic-on-november-2-2026

Live storefront artifacts (fetched 2026-10-30, server Date 21:59 GMT)
- /.well-known/ucp: kith.com, colourpop.com, www.brooklinen.com, www.allbirds.com, theme-horizon-demo.myshopify.com, theme-dawn-demo.myshopify.com (+ /.well-known/ucp/2026-04-08); www.gymshark.com returned 404

Google (Tier 1)
- Addendum to the Google Merchant Center Terms of Service for Shopify Merchants — https://developers.google.com/merchant/terms/shopify
- Checkout Addendum to the Google Merchant Center Terms of Service (US) — https://merchants.google.com/files/tos/ucp_integration/US/1_00_tos.html
- Universal Commerce Protocol Checkout Terms of Service (US only) — https://support.google.com/merchants/answer/17515932?hl=en
- Syncing your products (Google & YouTube app on Shopify) — https://support.google.com/merchants/answer/13427434?hl=en
- Show your products for free on Google (Shopify) — https://support.google.com/merchants/answer/13692890?hl=en
- Set up Shipping (for Shopify users) — https://support.google.com/merchants/answer/14232591?hl=en
- Set up your return policies (for Shopify users) — https://support.google.com/merchants/answer/14232691?hl=en
- How to find support if you use a non-Google platform — https://support.google.com/merchants/answer/12048683?hl=en
- Merchant Center topics: https://support.google.com/merchants/topic/16837563 ; /topic/14190434 ; /topic/13402337 ; /topic/15190247
- UCP developer docs (fetched; cited via GB where covered): https://developers.google.com/merchant/ucp ; /faq ; /guides ; /guides/merchant-center ; /guides/ucp-profile ; /guides/tools/merchant-center/integration ; /guides/merchant-center/overview
- Merchant Center UCP help (fetched; cited via GB): https://support.google.com/merchants/answer/16837055 ; https://support.google.com/merchants/answer/16992327
- The Keyword: Jan 11, 2026 — https://blog.google/products/ads-commerce/agentic-commerce-ai-tools-protocol-retailers-platforms/ ; May 19, 2026 — https://blog.google/products-and-platforms/products/shopping/google-shopping-cart/ ; Sept 16, 2026 — https://blog.google/products-and-platforms/products/shopping/google-shopping-updates-holiday-shopping/
- Google Developers Blog, Jan 11, 2026 — https://developers.googleblog.com/under-the-hood-universal-commerce-protocol-ucp/

Other platforms (Tier 1 vendor sources)
- WooCommerce — https://woocommerce.com/agentic-commerce/ ; https://woocommerce.com/document/woocommerce-ai/agentic-commerce/ ; https://woocommerce.com/document/woocommerce-ai/ucp-rest-api/ ; https://woocommerce.com/posts/selling-though-ai/
- BigCommerce / Commerce — https://investors.bigcommerce.com/news-releases/news-release-details/commerce-supports-universal-commerce-protocol-plans-offer-buying ; https://www.bigcommerce.com/articles/ecommerce/google-agentic-checkout/
- Salesforce — https://www.salesforce.com/news/stories/google-universal-commerce-protocol-support-announcement/ ; https://www.salesforce.com/ap/news/press-releases/2026/07/06/as-ai-agents-transform-commerce-salesforce-unleashes-its-biggest-agentforce-commerce-release-yet/ ; https://www.salesforce.com/blog/b2c-commerce-october-26-release/
- commercetools — https://docs.commercetools.com/api/releases/2026-07-30-ai-hub-is-now-generally-available
- Stripe — https://stripe.com/newsroom/news/sessions-2026 ; https://stripe.com/blog/everything-we-announced-at-sessions-2026 ; https://stripe.com/newsroom/news/stripe-tour-berlin-2026
- Wix — https://www.wix.com/app-market/google-merchant-solutions ; https://www.wix.com/blog/agentic-commerce-on-wix
- Squarespace — https://support.squarespace.com/hc/en-us/articles/12131658984717-Display-your-products-in-Google-Shopping
- Adobe — https://business.adobe.com/blog/adobe-commerce-commits-to-agentic-commerce-standards

Tier 3 (located primary sources; cited only in GC-07)
- https://www.seroundtable.com/google-native-checkout-emails-42140.html (2026-09-22)
- https://searchengineland.com/google-opens-native-ai-checkout-to-eligible-shopify-merchants-490407 (2026-09-22)

Cross-references
- ChatGPT notes (C-IDs): `research/ai-platforms/chatgpt/notes/c-shopify-and-independent-platforms.md`
- Gemini Merchant Center/UCP notes (GB-IDs): `research/ai-platforms/gemini/notes/gb-merchant-center-ucp.md`
