# Agent GD: Google crawl and structured-data rules for AI surfaces; how marketplace products reach Gemini / AI Mode

- Scope: (Part 1) Google's crawler docs and Search Central docs: which crawlers feed AI Overviews / AI Mode, what Google-Extended controls, shopping and agent user agents, "AI features" guidance and controls, Product structured data. (Part 2) 14 marketplaces: robots.txt treatment of Google tokens; official relationships with Google AI shopping (UCP, Gemini, AI Mode, investment), India focus.
- Date: 2026-10-30 (fetches); file completed 2026-10-31. All sources were accessed 2026-10-30. Status: complete for this pass (see Knowledge gaps).
- Method:
  - Google docs: raw HTTP GET with `curl` (default curl User-Agent) of developers.google.com, support.google.com and blog.google pages on 2026-10-30, converted to text locally with a Python HTML-to-text script. Excerpts are copied from the converted text. "Last updated" dates are the page footers ("Last updated YYYY-MM-DD UTC"). blog.google dates come from the page's `datePublished` field.
  - robots.txt: raw HTTP GET with `curl` default User-Agent on 2026-10-30 between 17:06 and 17:10 UTC. No crawler User-Agent was spoofed. Groups were split RFC 9309-style (consecutive `User-agent` lines form one group) by a local script; every group naming a Google token was printed with original line numbers. Exact lines are quoted from the saved files.
  - A curl retry with a desktop-browser User-Agent for hosts that refused plain curl was blocked by this session's permission policy and was not performed. Those files (Myntra, Mercado Libre) were then read in the in-app browser in this agent's own tab; text taken from `document.body.innerText`, status from Navigation Timing `responseStatus` (GD-35).
  - Wayback Machine `id_` captures via curl where a page returned 403 (Etsy newsroom).
  - Cross-references: ChatGPT marketplace notes use `D-NN` (`research/ai-platforms/chatgpt/notes/d-marketplaces-and-chatgpt.md`); Merchant Center / UCP notes use `GB-NN` (`research/ai-platforms/gemini/notes/gb-merchant-center-ucp.md`, which covers Merchant Center, free listings, Shopping Graph and the "AI features and your website" page as GB-27, GB-28, GB-30).
- Limits of robots.txt evidence: a file shows declared crawl policy on the access date. It does not show what Gemini, AI Mode or AI Overviews display, whether Google honors the file for a given agent, or whether product data reaches Google through Merchant Center feeds, UCP or partnerships.

## 1. Summary table

Legend: "No group" = no `User-agent` line names that token; Google's common crawlers then follow the `*` group (GD-02). "Empty/allow" = group exists with no effective disallow.

| Marketplace | Official Google AI relationship (finding) | Googlebot | Google-Extended | Storebot-Google | GoogleAgent-* | robots.txt fetch (plain curl) |
|---|---|---|---|---|---|---|
| Amazon.com | No Gemini/AI Mode catalog or checkout integration found. Amazon holds a UCP Shopping Tech Council seat (GD-26). Amazon listings reported in Gemini without Buy button (GD-30, Tier 3) | No group (`*`; `/dp/<ASIN>` not disallowed) (GD-17) | `Disallow: /` | No group (follows `*`, GD-34) | `GoogleAgent-Mariner` and `GoogleAgent-Shopping`: `Disallow: /` | 200 |
| Amazon.in | None found (same as above; India test report GD-30) | No group (`*`) | `Disallow: /` | No group (follows `*`) | Mariner + Shopping: `Disallow: /` | 200 |
| Walmart | UCP co-developer (GD-23); Walmart-built experience in Gemini via UCP, announced 2026-01-11 (GD-25); named Universal Cart checkout merchant, US launch 2026-10-15 (GD-28, GD-33) | No group | No group | No group | No group | 200 |
| Etsy | UCP co-developer (GD-23); US checkout in AI Mode and Gemini rolling out 2026-02-11 (GD-27) | No group | No group | No group | No group | 200 |
| eBay | None found (GD-37) | Own group, rules identical to `*` (GD-18) | No group (absent from eBay's AI block group) | No group (follows `*`) | No group | 200 |
| Target | UCP co-developer (GD-23); Target says it has shopping in Google Search incl. AI Mode and the Gemini app (D-11); named Universal Cart checkout merchant (GD-28, GD-33). US | No group | No group | No group | No group | 200 |
| Flipkart | UCP endorser 2026-01-11 (GD-23); Google: "Merchants like Flipkart are already partnering" on UCP agentic shopping in India, 2026-09-18 (GD-29); Flipkart checkout test in Gemini/AI Mode (GD-30, Tier 3); Google VP named Flipkart as APAC partner, Mar 2026 (GD-36, Tier 3); Google minority investment 2024 (Tier 3 only) | No group | No group | Own group: `Allow: /viewcart` only (GD-19) | No group | 200 |
| Myntra | None found (GD-37) | No group (single `*` group) (GD-35) | No group | No group | No group | curl: connection reset ×2; in-app browser: 200 |
| Meesho | None found (GD-37) | No group | No group | No group | No group | 200 |
| JioMart | None found (GD-37) | No group | No group | No group | No group | 200 |
| Mercado Libre (MX/BR/AR) | None found (GD-37) | No group (GD-35) | No group | No group | No group | curl: 403 ×3; in-app browser: 200 ×3 (+ articulo.mercadolibre.com.mx 200) |
| Rakuten Ichiba (JP) | None found (GD-37) | Own group: `Disallow: /*?lang=`, `/*&lang=` (GD-20) | No group | No group (follows `*`) | No group | 200 |
| Shopee (8 markets) | Sea × Google expanded partnership, 2026-02-19: joint "agentic shopping prototype" (GD-32); Google VP named Shopee as APAC partner, Mar 2026 (GD-36, Tier 3) | Group shared with Googlebot-Mobile and Bingbot (GD-21) | No group | No group (follows `*`) | No group | 200 |
| Lazada (SG/MY/TH/PH/VN) | None found (GD-37) | No group (GD-22) | No group | No group | No group | 200 |
| Lazada (ID) | None found (GD-37) | No group (empty `Googlebot-Image` group only) | No group | No group | No group | First try failed; retry 200 |
| Allegro (PL) | None found (GD-37) | No group (GD-22) | No group | No group | No group | 200 |

Cross-cutting (Part 1): Googlebot is the crawl control for AI Overviews and AI Mode (GD-02). Google-Extended controls Gemini Apps / Vertex AI training and grounding, not Search (GD-01). Since 2026-08-31 a Search Console setting controls inclusion in AI Overviews, AI Mode and Discover AI features (GD-04). Storebot-Google affects "all surfaces of Google Shopping" (GD-07) and, per Google's spec, falls back to `*`, never to a Googlebot group (GD-34). No marketplace in scope except Amazon names Google-Extended; none except Flipkart names Storebot-Google. Google's documented agent fetcher is `Google-Agent`, a user-triggered fetcher that "generally" ignores robots.txt; `GoogleAgent-Mariner` and `GoogleAgent-Shopping` do not appear in Google's current fetcher list (GD-09).

## 2. Findings

### Part 1 — Google crawler and Search Central rules

### GD-01 Google-Extended controls Gemini Apps / Vertex AI training and grounding; it does not affect Google Search inclusion or ranking
- Claim: Google-Extended is a robots.txt product token with no own HTTP user agent. It controls whether crawled content may be used to train future Gemini models (Gemini Apps, Vertex AI API for Gemini) and for grounding in Gemini Apps and Grounding with Google Search on Vertex AI. It does not affect inclusion in Google Search and is not a Search ranking signal. A note added on 2026-10-30 says Google intends to support the AIPREF training-preference signal in early 2027.
- Classification: VERIFIED FACT
- Source: List of Google's common crawlers — Google Crawling infrastructure docs — https://developers.google.com/crawling/docs/crawlers-fetchers/google-common-crawlers (the old URL https://developers.google.com/search/docs/crawling-indexing/google-common-crawlers redirects here)
- Published/updated: Last updated 2026-10-30 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Google-Extended doesn't have a separate HTTP request user agent string. Crawling is done with existing Google user agent strings; the robots.txt user-agent token is used in a control capacity."

  > "Google-Extended is a standalone product token that web publishers can use to manage whether content Google crawls from their sites may be used for training future generations of Gemini models that power Gemini Apps and Vertex AI API for Gemini and for grounding (providing content from the Google Search index to the model at prompt time to improve factuality and relevancy) in Gemini Apps and Grounding with Google Search on Vertex AI."

  > "Google-Extended does not impact a site's inclusion in Google Search nor is it used as a ranking signal in Google Search."

  > "Note: Google intends to support the AIPREF shared machine-readable training preference signal (with "user-agent: __usage_ai-training") in early 2027."
- Also: Crawling changelog (https://developers.google.com/crawling/docs/changelog, Last updated 2026-10-30): "October 30 … Updated common crawlers page to mention future AI training control support". The changelog also records "April 25 [2025] Updated the description of the Google-Extended product token … Based on publisher feedback".
- Establishes: Blocking Google-Extended removes a site from Gemini Apps grounding (per Google's wording) but leaves AI Overviews and AI Mode untouched (those are Search features; see GD-02, GD-03).
- Limitations: The doc does not define how Gemini Apps answers that do not use grounding treat a Google-Extended-blocked site, or whether Shopping Graph product data (Merchant Center, GD-14) reaches Gemini Apps regardless of Google-Extended. See contradiction C-1 (Search Console help says Google-Extended limits training of Search generative AI models).

### GD-02 Googlebot robots.txt rules are the crawl control for AI Overviews and AI Mode; common crawlers obey robots.txt
- Claim: Googlebot preferences affect Google Search including "all Google Search features". Google's AI features page says robots.txt directives for Googlebot are the crawl control for Search, because AI is "integral" to Search. Common crawlers "always obey robots.txt rules when crawling automatically."
- Classification: VERIFIED FACT
- Sources:
  - List of Google's common crawlers — https://developers.google.com/crawling/docs/crawlers-fetchers/google-common-crawlers — Last updated 2026-10-30 UTC
  - AI features and your website — Google Search Central — https://developers.google.com/search/docs/appearance/ai-features — Last updated 2025-12-10 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Google's common crawlers are used to find information for building Google's search indexes, perform other product specific crawls, and for analysis. They always obey robots.txt rules when crawling automatically."

  > "Crawling preferences addressed to the Googlebot user agent affect Google Search (including Discover and all Google Search features), as well as other products such as Google Images, Video mode, Google News, and Discover."

  > "AI is built into Search and integral to how Search functions, which is why robots.txt directives for Googlebot is the control for site owners to manage access to how their sites are crawled for Search. To limit the information shown from your pages in Search, use nosnippet, data-nosnippet, max-snippet, or noindex controls."

  > "To limit AI training and grounding in some of Google's other systems, read more about Google-Extended."
- Establishes: No separate crawler feeds AI Overviews or AI Mode; they draw on the Search index built by Googlebot. A site that allows Googlebot and blocks Google-Extended stays eligible for AI Overviews / AI Mode.
- Limitations: Since 2026-08-31 a non-robots.txt control also exists (GD-04). The AI features page predates it.

### GD-03 AI features page (2025-12-10): eligibility = indexed + snippet-eligible; "no additional technical requirements"; no special schema.org
- Claim: To be a supporting link in AI Overviews or AI Mode, a page must be indexed and eligible for a snippet. The page lists no extra requirement, no AI text files and no special structured data. It lists "structured data matches the visible text" and up-to-date Merchant Center / Business Profile among SEO fundamentals.
- Classification: VERIFIED FACT (page text). Partly OUTDATED: see GD-04 and C-2.
- Source: AI features and your website — Google Search Central — https://developers.google.com/search/docs/appearance/ai-features
- Published/updated: Last updated 2025-12-10 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "The best practices for SEO remain relevant for AI features in Google Search (such as AI Overviews and AI Mode). There are no additional requirements to appear in AI Overviews or AI Mode, nor other special optimizations necessary."

  > "To be eligible to be shown as a supporting link in AI Overviews or AI Mode, a page must be indexed and eligible to be shown in Google Search with a snippet, fulfilling the Search technical requirements. There are no additional technical requirements."

  > "Making sure your structured data matches the visible text on the page"

  > "Checking that your Merchant Center and Business Profile information is up-to-date"

  > "You don't need to create new machine readable files, AI text files, or markup to appear in these features. There's also no special schema.org structured data that you need to add."

  > "Both AI Overviews and AI Mode may use a "query fan-out" technique — issuing multiple related searches across subtopics and data sources — to develop a response."
- Establishes: Google's documented eligibility gate for AI Overviews / AI Mode links is the ordinary Search gate (index + snippet). Same page is captured as GB-28 in the Merchant Center notes.
- Limitations: Describes supporting links, not product listings or checkout units in AI Mode.

### GD-04 New in 2026: "Search generative AI control" in Search Console (worldwide since 2026-08-31) includes or excludes a site from AI Overviews, AI Mode and Discover AI features
- Claim: Search Console has a per-property setting that excludes a site's links and content from Search generative AI features (AI Overviews, AI Mode, generative AI features in Discover). Default is include. Exclusion also stops crawled content from grounding those answers. It does not affect AI training (Google-Extended does), is not a ranking signal for other Search features, and "doesn't override" participation in Merchant Center or Google Ads. Google's AI optimization guide (2026-07-10) states that inclusion via this control is an eligibility requirement.
- Classification: VERIFIED FACT
- Sources:
  - Search generative AI control — Search Console Help — https://support.google.com/webmasters/answer/16908024 — date not stated on page; contains "As of August 31, 2026, we’ve rolled out this control to all websites worldwide."
  - Optimizing your website for generative AI features on Google Search — Google Search Central — https://developers.google.com/search/docs/fundamentals/ai-optimization-guide — Last updated 2026-07-10 UTC (guide added 2026-05-15 per the Search Central updates log)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Note: As of August 31, 2026, we’ve rolled out this control to all websites worldwide."

  > "Use the Search generative AI control to manage your site's inclusion in the following generative AI features on Google Search. We expect to update this list over time as we develop Google Search."

  > "Exclude my site's links and content from Search generative AI features: Your site's content is prevented from being visible to users in Search generative AI features, including being linked to within these features and helping with grounding AI responses in these features."

  > "This control only affects whether your content can appear in certain Search generative AI features; this control isn't used as a ranking or inclusion signal affecting other parts of Search. This control doesn't override publishers' other choices to participate in particular services, such as Merchant Center and Google Ads."

  > "This control doesn't affect AI training; to limit training of the models used to generate responses in Search generative AI features, use Google-Extended."

  > (AI optimization guide) "In addition to the technical requirements for Search, a site must be included in Search generative AI features in Search Console to be eligible for display in generative AI features on Google Search."
- Establishes: Since 2026 there are three separate levers: Googlebot robots.txt (crawl for Search, GD-02), the Search Console generative AI control (display/grounding in AI Overviews, AI Mode, Discover AI), and Google-Extended (Gemini Apps / Vertex grounding and training, GD-01). The Merchant Center carve-out means a merchant's feed-based product data is governed separately from this control.
- Limitations: The help page does not say how the control treats Shopping Graph product listings inside AI Mode that come from Merchant Center rather than from crawled pages. "Doesn't override … Merchant Center" is the only statement. Gemini app is not listed among controlled features. See C-1, C-2.

### GD-05 AI optimization guide (2026): structured data "isn't required"; Merchant Center feeds help products appear in AI responses; UCP named for agents
- Claim: Google's generative-AI guide says AI Overviews / AI Mode use RAG ("grounding") and query fan-out over the Search index. It says structured data is not required and no special schema.org markup is needed. It says AI responses can include product listings and that Merchant Center feeds and Business Profiles help visibility in AI responses. It names Business Agent and UCP.
- Classification: VERIFIED FACT
- Source: Optimizing your website for generative AI features on Google Search — Google Search Central — https://developers.google.com/search/docs/fundamentals/ai-optimization-guide
- Published/updated: Last updated 2026-07-10 UTC; added 2026-05-15 (Search Central updates log, https://developers.google.com/search/updates, Last updated 2026-10-26 UTC); llms.txt note added 2026-06-15 (same log)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Retrieval-augmented generation (RAG): A technique (also known as grounding) used to improve the quality, accuracy, and freshness of AI responses by relying on our core Search ranking systems to retrieve relevant, up-to-date web pages from our Search index."

  > "Where appropriate, generative AI responses can include product listings, product information, and information about local businesses. Using products like Merchant Center (such as Merchant Center feeds) and Google Business Profiles can help your products and services to be visible in both AI responses and other Google Search results."

  > "Overfocusing on structured data: Structured data isn't required for generative AI search, and there's no special schema.org markup you need to add. However, it's a good idea to continue using it as part of your overall SEO strategy, as it helps with being eligible for rich results on Google Search."

  > "LLMS.txt files and other "special" markup: You don't need to create new machine readable files, AI text files, markup, or Markdown to appear in Google Search (including its generative AI capabilities), as Google Search itself doesn't use them."

  > "Protocols like Universal Commerce Protocol (UCP) are emerging that will allow Search agents to do more."
- Establishes: Google's own statement linking commerce data to AI responses names Merchant Center feeds, not Product structured data.
- Limitations: "Can help" is not a ranking statement. The guide does not describe how product listings are selected in AI Mode.

### GD-06 nosnippet and max-snippet apply to AI Overviews and AI Mode; max-snippet does not limit in-page structured data use
- Claim: `nosnippet` prevents content from being used as "a direct input" for AI Overviews and AI Mode. `max-snippet` limits how much content may be used as direct input. The max-snippet limit does not apply where a publisher supplies in-page structured data or has a license agreement. `data-nosnippet` excludes marked `span`, `div` and `section` elements from snippets.
- Classification: VERIFIED FACT
- Source: Robots meta tag, data-nosnippet, and X-Robots-Tag specifications — Google Search Central — https://developers.google.com/search/docs/crawling-indexing/robots-meta-tag
- Published/updated: Last updated 2026-03-24 UTC (AI Mode added 2025-03-05 per updates log)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "This applies to all forms of search results (at Google: web search, Google Images, Discover, AI Overviews, AI Mode) and will also prevent the content from being used as a direct input for AI Overviews and AI Mode." (nosnippet)

  > "This applies to all forms of search results (such as Google web search, Google Images, Discover, Assistant, AI Overviews, AI Mode) and will also limit how much of the content may be used as a direct input for AI Overviews and AI Mode. However, this limit does not apply in cases where a publisher has separately granted permission for use of content. For instance, if the publisher supplies content in the form of in-page structured data or has a license agreement with Google, this setting does not interrupt those more specific permitted uses." (max-snippet)

  > "You can designate textual parts of an HTML page not to be used as a snippet. This can be done on an HTML-element level with the data-nosnippet HTML attribute on span, div, and section elements."
- Establishes: Structured data on a page is treated as separately permitted data that max-snippet does not restrict. This is the only Google sentence found that ties structured data to AI Overviews/AI Mode input handling.
- Limitations: Does not say AI Mode uses structured data for ranking or product units.

### GD-07 Storebot-Google: common crawler that obeys robots.txt; affects "all surfaces of Google Shopping"
- Claim: Storebot-Google is listed as a common crawler (desktop and mobile UAs). Its only robots.txt token is `Storebot-Google` (no fallback token listed, unlike Googlebot-Image which also matches `Googlebot`). Google says its preferences affect all Google Shopping surfaces. The crawler overview says Storebot-Google "only supports caching in certain conditions". The merchant-listing doc warns that JavaScript-generated Product markup makes "Shopping crawls less frequent and less reliable".
- Classification: VERIFIED FACT. "Storebot-Google feeds AI Mode shopping units" is UNVERIFIED HYPOTHESIS (Google does not name AI Mode in the Storebot entry).
- Sources: List of Google's common crawlers (Last updated 2026-10-30 UTC); Overview of Google crawlers and fetchers — https://developers.google.com/crawling/docs/crawlers-fetchers/overview-google-crawlers (Last updated 2026-06-12 UTC); Merchant listing structured data — https://developers.google.com/search/docs/appearance/structured-data/merchant-listing (Last updated 2026-09-08 UTC)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Crawling preferences addressed to the Storebot-Google user agent affect all surfaces of Google Shopping (for example, the Shopping tab in Google Search and Google Shopping)."

  > "For example, Googlebot supports caching when re-crawling URLs for Google Search, and Storebot-Google only supports caching in certain conditions."

  > "For JavaScript-generated Product markup: Be aware that dynamically-generated markup can make Shopping crawls less frequent and less reliable, which can be an issue for fast-changing content like product availability and price."
- Establishes: Shopping has its own crawler token, separate from Googlebot. A site can treat Search and Shopping crawling differently.
- Limitations: Google does not state whether AI Mode shopping results or Gemini shopping use Storebot-Google crawls, Googlebot crawls, Merchant Center feeds, or all three.

### GD-08 GoogleOther and Google-CloudVertexBot: no effect on Google Search; Vertex bot is site-owner-requested
- Claim: GoogleOther "don't affect any specific product" (generic, internal R&D crawls). Google-CloudVertexBot preferences affect crawls requested by site owners for building Vertex AI Agents and have "no effect on Google Search or other products". Both are listed as common crawlers (obey robots.txt).
- Classification: VERIFIED FACT
- Source: List of Google's common crawlers — https://developers.google.com/crawling/docs/crawlers-fetchers/google-common-crawlers
- Published/updated: Last updated 2026-10-30 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Crawling preferences addressed to the GoogleOther user agent don't affect any specific product. GoogleOther is the generic crawler that may be used by various product teams for fetching publicly accessible content from sites. For example, it may be used for one-off crawls for internal research and development."

  > "Crawling preferences addressed to the Google-CloudVertexBot user agent affect crawls requested by the site owners' for building Vertex AI Agents. It has no effect on Google Search or other products."
- Establishes: Amazon's disallows of GoogleOther and Google-CloudVertexBot (GD-17) have no documented effect on Search, AI Overviews or AI Mode.
- Limitations: The robots.txt token list for Google-CloudVertexBot also shows `Googlebot` as a matching token (page lists "Google-CloudVertexBot / Googlebot"); the page does not explain the fallback.

### GD-09 Google-Agent (added 2026-03-20) is the documented Google agent fetcher; user-triggered fetchers "generally ignore robots.txt"; no GoogleAgent-Mariner or GoogleAgent-Shopping in Google's list
- Claim: Google lists `Google-Agent` as a user-triggered fetcher "used by agents hosted on Google infrastructure to navigate the web and perform actions upon user request", with IP ranges in `user-triggered-agents.json` and experimental Web Bot Auth (`https://agent.bot.goog`). User-triggered fetchers "generally ignore robots.txt rules". Google-Agent has no robots.txt token on the page. The current list contains no `GoogleAgent-Mariner` or `GoogleAgent-Shopping` entry. `Google-NotebookLM` became `Google-GeminiNotebook` (old agent "supported until August 2026").
- Classification: VERIFIED FACT (page contents). "GoogleAgent-Mariner / GoogleAgent-Shopping were never documented by Google" is UNVERIFIED (archived copies of the fetcher page were empty shells; history not checked).
- Sources:
  - List of Google user-triggered fetchers — https://developers.google.com/crawling/docs/crawlers-fetchers/google-user-triggered-fetchers (https://developers.google.com/crawling/docs/crawlers-fetchers/google-agent redirects to its #google-agent anchor) — Last updated 2026-08-19 UTC
  - Changelog — Google Crawling infrastructure — https://developers.google.com/crawling/docs/changelog — Last updated 2026-10-30 UTC
  - user-triggered-agents.json — https://developers.google.com/static/crawling/ipranges/user-triggered-agents.json — "creationTime": "2026-10-30T15:46:18.000000"
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Because the fetch was requested by a user, these fetchers generally ignore robots.txt rules."

  > "Google-Agent is used by agents hosted on Google infrastructure to navigate the web and perform actions upon user request. It uses IP ranges from user-triggered-agents.json."

  > "Note: Google is also experimenting with the Web Bot Auth protocol, using the https://agent.bot.goog identity."

  > (changelog, March 20 [2026]) "The Google-Agent user agent is rolling out over the next few weeks, and will be used by Google agents hosted on Google infrastructure to navigate the web and perform actions upon user request."

  > (changelog, July 16 [2026]) "Updated the NotebookLM user agent to be Google-GeminiNotebook."
- Establishes: A robots.txt group for `GoogleAgent-Mariner` / `GoogleAgent-Shopping` (Amazon, GD-17) names tokens that Google's current docs do not list. Google's documented agent (`Google-Agent`) is described as generally not following robots.txt; identification is by UA string, IP ranges and Web Bot Auth.
- Limitations: "Generally" is not "always". The page does not say which Google products (Gemini agent mode, AI Mode agentic checkout, Project Mariner) use Google-Agent.

### GD-10 UCP traffic is identified by headers, not by a crawler token
- Claim: Google's UCP FAQ says UCP requests carry a `UCP-Agent` header and a User-Agent beginning `Google/UCP`; health checks use `Google-UCP-Prober/1.0`. Choosing native UCP checkout "does not influence how we rank your offers".
- Classification: VERIFIED FACT
- Source: Frequently asked questions — Google Universal Commerce Protocol (UCP) Guide — Google for Developers — https://developers.google.com/merchant/ucp/faq
- Published/updated: Last updated 2026-10-16 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "HTTP Headers: You can identify incoming UCP requests at the network level by verifying that the request meets two conditions: a header with the label UCP-Agent:Profile is present, and the User-Agent value begins with Google/UCP."

  > "These health check requests will include a specific User-Agent header: User-Agent: Google-UCP-Prober/1.0."

  > "No. Opting for our Native integration does not influence how we rank your offers in product listings. The user experience for listings remains consistent; however, offers integrated with UCP will feature the direct purchase option."

  > "Merchant Center remains central to our ecosystem. You must ensure your product feeds, brand assets, return policies, and business contact information are complete and up-to-date there."
- Establishes: UCP is an API integration between Google and the merchant's endpoints, layered on Merchant Center feeds. It is not crawling and is not governed by robots.txt.
- Limitations: FAQ addresses merchants that integrate; it does not cover marketplaces with third-party sellers.

### GD-11 Product structured data: product snippets vs merchant listings; merchant listings need the page to sell the product
- Claim: Google defines two classes. Product snippets: pages where people cannot buy directly (e.g., reviews). Merchant listings: pages where customers can purchase from you. Merchant listings require an `Offer` (not `AggregateOffer`) because "the merchant has to be the seller". Only pages where a shopper can purchase are eligible; pages linking to other sellers are not. Google recommends combining structured data with Merchant Center feeds.
- Classification: VERIFIED FACT
- Sources:
  - Introduction to Product structured data — https://developers.google.com/search/docs/appearance/structured-data/product — Last updated 2025-12-10 UTC
  - Merchant listing (Product, Offer) structured data — https://developers.google.com/search/docs/appearance/structured-data/merchant-listing — Last updated 2026-09-08 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Product snippets: For product pages where people can't directly purchase the product."

  > "Merchant listings: For pages where customers can purchase products from you."

  > "Product snippets accept an Offer or AggregateOffer but merchant listings require an Offer as the merchant has to be the seller of the product in order to be eligible for merchant listing experiences."

  > "Only pages where a shopper can purchase a product are eligible for merchant listing experiences, not pages with links to other sites that sell the product. Google may attempt to verify merchant listing product data before showing the information in search results."

  > "Providing both structured data on web pages and a Merchant Center feed maximizes your eligibility to experiences and helps Google correctly understand and verify your data."
- Establishes: Google's markup model ties merchant-listing eligibility to the page being the point of sale. A marketplace product page (buyable on the marketplace) and a brand page (buyable on the brand site) can both qualify; an affiliate or comparison page cannot.
- Limitations: None of the four fetched Product pages mentions AI Overviews, AI Mode or Gemini (text search for "AI Mode", "AI Overview", "Gemini", "agentic" returned zero hits in each). The doc does not say how Google picks between a marketplace offer and a brand offer for the same product.

### GD-12 Merchant listing property requirements (2026-09-08)
- Claim: Required: `Product.name`, `Product.image`, `Product.offers` (Offer); `Offer.price` (or `priceSpecification.price`, >0) and `priceCurrency`. Recommended Product properties include `aggregateRating`, `audience`, `brand.name`, `category` (text or `CategoryCode` with Google Product Taxonomy, added 2026-07-07), `color`, `description`, `gtin`/`gtin8`/`gtin12`/`gtin13`/`gtin14`/`isbn`, `hasAdultConsideration` (added 2026-05-20), `hasCertification`, `inProductGroupWithID`, `isVariantOf`, `material`, `mpn`, `pattern`, `review`, `size`, `sku`, `subjectOf` (3DModel). Recommended Offer properties include `availability`, `hasMerchantReturnPolicy`, `itemCondition`, `priceValidUntil`, `shippingDetails`, `url`, `validFrom`, `validThrough`. Google recommends return and shipping policies at Organization level, with Offer-level properties only as overrides.
- Classification: VERIFIED FACT
- Source: Merchant listing (Product, Offer) structured data — https://developers.google.com/search/docs/appearance/structured-data/merchant-listing ; Search Central documentation updates — https://developers.google.com/search/updates
- Published/updated: Last updated 2026-09-08 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Unlike product snippets, merchant listing experiences require a price greater than zero."

  > "We recommend you provide a global return policy for your business under Organization markup instead, as documented under the Organization documentation and the Merchant return policy documentation. Only if some of your products have specific return policies for which you need to override your global return policy, or if you don't provide standard return policy for your business, use this property under Offer."

  > "We recommend you provide a global shipping policy for your business under Organization markup instead, as documented under the Organization documentation and the Merchant shipping policy documentation."

  > "Include all applicable global identifiers; these are described at schema.org/Product. While you can use the generic gtin property for all GTINs, we recommend that you use the most specific GTIN that applies to your product"

  > (updates log, July 7 [2026]) "Updated the Merchant listing documentation to detail how the Product.category property can be used with both Text and CategoryCode types. This aligns with the Google Merchant Center feed specifications for the product_type and google_product_category attributes."
- Establishes: The current required/recommended split. gtin, shippingDetails, hasMerchantReturnPolicy and aggregateRating are recommended, not required. 2026 changes align markup with Merchant Center feed attributes.
- Limitations: Requirements govern rich-result eligibility in Search, not AI Mode ranking.

### GD-13 Product snippet requirements; ProductGroup variant requirements
- Claim: Product snippets require `name` plus one of `review`, `aggregateRating` or `offers`. ProductGroup requires `name`; recommended include `aggregateRating`, `brand`, `description`, `hasAdultConsideration`, `hasVariant`, `productGroupID`, `review`, `url`, `variesBy` (color, size, suggestedAge, suggestedGender, material, pattern).
- Classification: VERIFIED FACT
- Sources: Product snippet structured data — https://developers.google.com/search/docs/appearance/structured-data/product-snippet ; Product variant structured data (ProductGroup, Product) — https://developers.google.com/search/docs/appearance/structured-data/product-variants
- Published/updated: both Last updated 2026-09-08 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "You must include one of the following properties: review aggregateRating offers"

  > "To help Google better understand which products are variations of the same parent product, use the ProductGroup class with associated properties variesBy, hasVariant, and productGroupID to group such variants together, in addition to Product structured data."

  > "The identifier of the product group (also known as the parent sku). This identifier must be provided for the ProductGroup property or, alternatively, using inProductGroupWithID property for variants of the ProductGroup property."
- Establishes: Variant grouping is a recommended, not required, layer.
- Limitations: Same as GD-12.

### GD-14 Merchant Center, not crawl, is Google's named commerce data path into AI Mode / Gemini; new conversational attributes and AI performance insights (2026)
- Claim: Google announced (2026-01-11) "dozens of new data attributes in Merchant Center designed for easy discovery … on surfaces like AI Mode, Gemini and Business Agent". On 2026-05-20 it announced "conversational attributes" for product descriptions and an "AI performance insights" tool in Merchant Center rolling out in Australia, Canada, India, New Zealand and the US. The Product structured data intro says data can come from structured data, Merchant Center feeds (free listings), or both, and that some experiences combine them.
- Classification: VERIFIED FACT
- Sources:
  - New tech and tools for retailers to succeed in an agentic shopping era — Google (The Keyword) — https://blog.google/products/ads-commerce/agentic-commerce-ai-tools-protocol-retailers-platforms/ — datePublished 2026-01-11
  - How we’re helping retailers thrive with new Universal Commerce Protocol features and AI tools on Google — Google (The Keyword) — https://blog.google/products-and-platforms/products/shopping/shopping-updates-google-marketing-live/ — datePublished 2026-05-20
  - Introduction to Product structured data — Last updated 2025-12-10 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "That’s why we’re announcing dozens of new data attributes in Merchant Center designed for easy discovery in the conversational commerce era, on surfaces like AI Mode, Gemini and Business Agent."

  > "The new AI performance insights tool in Merchant Center gives you a clear view into how your brand is performing on AI surfaces by comparing your share of voice against similar brands. It's rolling out in Australia, Canada, India, New Zealand and the U.S. in the coming months."

  > "Some experiences combine data from structured data and Google Merchant Center feeds if both are available. For example, product snippets may use pricing data from your merchant feed if it's not present in the structured data on the page."

  > (Sundar Pichai, NRF, https://blog.google/company-news/inside-google/message-ceo/nrf-2026-remarks/ , 2026-01-11) "Since 2021, our Shopping Graph provides information on products in real time. It has over 50 billion product listings, including inventory, prices and reviews. More than 2 billion of those listings are refreshed every single hour."

  > (same) "And last year, we brought the Shopping Graph to the Gemini app, so it’s a lot more helpful for people asking shopping-related questions, too."
- Establishes: Google names the Shopping Graph and Merchant Center as the product data layer for AI Mode and Gemini shopping. This is the documented route by which marketplace and brand products reach Gemini/AI Mode, separate from Google-Extended and the Search generative AI control (GD-04). Related findings in the Merchant Center notes: free listings "may show on … Gemini" and crawled products can show without Merchant Center (GB-27); Shopping Graph sources include Merchant Center, Manufacturer Center and web crawl (GB-30); AI performance report covers AU, CA, IN, NZ, US (GB-26); Merchant Center is "mandatory" only for the Shopping tab (GB-28).
- Limitations: The posts do not say whether the Shopping Graph ingests a given marketplace's listings from crawling, feeds, or both, or how a marketplace's third-party-seller offers are attributed.

### GD-15 Google states no marketplace-versus-brand rule; the closest statements are seller-of-record and "merchant has to be the seller"
- Claim: No fetched Google document states how Search, Shopping, AI Mode or Gemini rank a marketplace offer against a brand-site offer. Related statements: merchant listings require the page owner to be the seller (GD-11); UCP keeps "the retailer" as merchant/seller of record (GD-23, GD-28); native UCP does not change offer ranking (GD-10); Business Agent requires a "US-based e-commerce store" and a claimed brand profile. Google's consumer ranking statements for Shopping (relevance, bids for ads, "Top recommendations" on relevance, ratings, price, features) are captured in GB-32 and name no seller type.
- Classification: VERIFIED FACT (absence across documents fetched in this session and in GB-32). That no such rule exists at Google: UNVERIFIED.
- Source: documents in GD-10, GD-11, GD-23, GD-28; GB-32; Get started with Business Agent — Google Help — https://support.google.com/brandprofile/answer/16410382 (date not stated)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Have a US-based e-commerce store." (Business Agent eligibility)

  > "Starting in 2025, a conversational feature was made available on merchant brand profiles in the US, Canada, Australia, and India that provides responses to customers' questions based on product and brand information stored in Merchant Center."
- Establishes: Unlike OpenAI (D-21 "maker or primary seller"), Google has not published a seller-type ranking factor in the documents fetched.
- Limitations: Google Merchant Center Help (not fetched in this pass) may contain marketplace-specific feed rules (e.g., multi-seller accounts).

### Part 2 — Marketplaces: robots.txt (all fetched 2026-10-30, plain curl, Tier 1, Published/updated: not stated unless noted)

### GD-16 Robots.txt fetch log
- Claim: HTTP results for plain curl (default User-Agent), 2026-10-30 ~17:06–17:10 UTC.
- Classification: VERIFIED FACT
- Results: 200 — amazon.com (7,947 B), amazon.in (9,320 B), walmart.com, etsy.com, ebay.com, target.com, flipkart.com, meesho.com, jiomart.com, rakuten.co.jp, item.rakuten.co.jp, search.rakuten.co.jp, shopee.sg/.co.id/.co.th/.ph/.vn/.com.my/.tw/.com.br, lazada.sg/.com.my/.co.th/.com.ph/.vn, allegro.pl. 403 (text/html, 2,585 B) — mercadolibre.com.mx, mercadolivre.com.br, mercadolibre.com.ar. Failed — myntra.com (curl 000, then "Recv failure: Connection was reset" on retry). lazada.co.id — first request curl 000, retry 200.
- Establishes: Same access pattern as agent D for Mercado Libre (403 to curl UA, D-16 table) and Myntra (curl UA connection failure).
- Limitations: Mercado Libre and Myntra Google groups not captured this session.

### GD-17 Amazon.com and Amazon.in: no Googlebot or Storebot-Google group; Google-Extended, GoogleAgent-Mariner, GoogleAgent-Shopping, GoogleOther, Google-CloudVertexBot, Google-NotebookLM, Google-Firebase all `Disallow: /`
- Claim: Each Google AI/agent token has its own one-line group disallowing `/`. Googlebot and Storebot-Google have no group, so they follow `*`. The `*` group disallows sub-paths such as `/dp/shipping/` and `/dp/product-availability/` but not `/dp/` itself.
- Classification: VERIFIED FACT (file contents). "Googlebot may crawl Amazon product detail pages" is EVIDENCE-BASED INFERENCE from group matching.
- Source: https://www.amazon.com/robots.txt (101 groups) ; https://www.amazon.in/robots.txt (103 groups)
- Accessed: 2026-10-30 · Tier: 1
- Excerpt (amazon.com lines 153–160, 213–214, 345–346; amazon.in lines 188–195, 248–249, 380–381 identical):
  > "User-agent: Google-Extended
  > Disallow: /"

  > "User-agent: GoogleAgent-Mariner
  > Disallow: /"

  > "User-agent: GoogleAgent-Shopping
  > Disallow: /"

  > "User-agent: Google-CloudVertexBot
  > Disallow: /"

  > "User-agent: GoogleOther
  > Disallow: /"
- Also: "User-agent: Google-NotebookLM / Disallow: /" (amazon.com l.201–202) and "User-agent: Google-Firebase / Disallow: /" (l.342–343).
- Establishes: Amazon allows Google Search crawling (Googlebot, hence AI Overviews / AI Mode eligibility per GD-02) and Shopping crawling (Storebot-Google) under `*`, while opting out of Gemini Apps / Vertex grounding and training (Google-Extended, GD-01) and naming two agent tokens Google does not currently document (GD-09).
- Limitations: Does not show what Gemini app shows for Amazon products; Shopping Graph data may come from feeds or crawls (GD-14). Google-Agent (the documented agent) is not named in the file, and Google says user-triggered fetchers generally ignore robots.txt (GD-09). Amazon's Agent Terms (D-17) are a separate contractual control.

### GD-18 eBay: Googlebot group is byte-identical to `*`; Google-Extended not in eBay's AI block group
- Claim: eBay (file version "# v30.2_COM_August_2026") has a `User-agent: Googlebot` group (lines 265–499) whose rules match the `*` group (lines 30–264) exactly after removing blank lines (234 rule lines each; `cmp` reports identical). Its "LLM / AI bot" block group (lines 760–769, D-02) lists Bytespider, CCBot, ChatGLM-Spider, ClaudeBot, PerplexityBot, anthropic-ai, AmazonBot, meta-externalagent, GPTBot, Applebot-Extended; Google-Extended is absent. Other Google group: AdsBot-Google (line 719).
- Classification: VERIFIED FACT
- Source: https://www.ebay.com/robots.txt
- Accessed: 2026-10-30 · Tier: 1
- Excerpt:
  > "User-agent: Googlebot
  > Disallow: /*_kw"
  > (first two lines of the Googlebot group; group continues with the same rules as `*`, including "Disallow: /sch/" and item-page sub-path disallows such as "Disallow: /itm/addToCart")
- Establishes: eBay does not opt out of Google-Extended; Gemini Apps grounding/training may use eBay content under Google's stated rule (GD-01). eBay blocks Applebot-Extended and GPTBot but not Google-Extended.
- Limitations: Header says checkouts are for humans and bans "buy-for-me agents" (D-02); that contract text applies to Google-Agent too but is not a robots.txt rule.

### GD-19 Flipkart: `Storebot-Google` has its own group that only allows `/viewcart`
- Claim: Flipkart's file has groups for Mediapartners-Google, Adsbot-Google, Googlebot-Image (each `Disallow:` empty) and a Storebot-Google group with one rule. Googlebot and Google-Extended are not named.
- Classification: VERIFIED FACT (contents). "Storebot-Google is effectively unrestricted on Flipkart, including paths `*` blocks such as `/search?`" is EVIDENCE-BASED INFERENCE from Google's documented group selection (GD-34: only the most specific matching group applies; "User agent specific groups and global groups (*) are not combined").
- Source: https://www.flipkart.com/robots.txt
- Accessed: 2026-10-30 · Tier: 1
- Excerpt (lines 10–16):
  > "# cart
  > User-agent: *
  > Disallow: /viewcart
  >
  > # Allow Store bot
  > User-agent: Storebot-Google
  > Allow: /viewcart"
- Establishes: Flipkart is the only marketplace in scope that names Storebot-Google, and it does so to allow cart access for Google Shopping's crawler.
- Limitations: Intent of the rule is not stated beyond the comment "# Allow Store bot".

### GD-20 Rakuten Ichiba: Googlebot group blocks only `lang` parameters; no Google AI tokens
- Classification: VERIFIED FACT
- Source: https://www.rakuten.co.jp/robots.txt (item.rakuten.co.jp and search.rakuten.co.jp: `*` only)
- Accessed: 2026-10-30 · Tier: 1
- Excerpt (lines 17–22):
  > "User-Agent: AdsBot-Google
  > Disallow: /com/
  >
  > User-agent: Googlebot
  > Disallow: /*?lang=
  > Disallow: /*&lang="
- Establishes: Googlebot on www.rakuten.co.jp follows only these two rules (not the `*` group, which disallows `/shops/`). Google-Extended, Storebot-Google, GoogleOther and GoogleAgent-* are not named. Per Google's spec (GD-34), Storebot-Google does not inherit the Googlebot group; it follows `*` (EVIDENCE-BASED INFERENCE), so Googlebot and Storebot-Google get different rules here.
- Limitations: Item pages live on item.rakuten.co.jp, whose file has no Google group.

### GD-21 Shopee (8 markets): one group for Googlebot, Googlebot-Mobile and Bingbot, with `Crawl-delay:0.1`; no Google AI tokens
- Classification: VERIFIED FACT
- Source: https://shopee.sg/robots.txt (same structure in .co.id, .co.th, .ph, .vn, .com.my, .tw, .com.br; each file has 2 groups)
- Accessed: 2026-10-30 · Tier: 1
- Excerpt (shopee.sg lines 1–6):
  > "User-Agent:Googlebot
  > User-Agent:Googlebot-Mobile
  > User-Agent:Bingbot
  > Crawl-delay:0.1
  > Disallow: /cart/
  > Disallow: /checkout/"
- Establishes: Shopee gives Google's search crawler its own rule set and does not name Google-Extended, Storebot-Google or agent tokens. Storebot-Google therefore follows the shorter `*` group (shopee.sg lines 40–59), which omits about 14 `/search…` and `/shop/…` disallows present in the Googlebot group (local `diff`; EVIDENCE-BASED INFERENCE from GD-34).
- Limitations: Google does not support `crawl-delay` (GD-34), so `Crawl-delay:0.1` has no effect on Googlebot.

### GD-22 No Google-specific group (for Googlebot, Google-Extended, Storebot-Google, GoogleOther or GoogleAgent-*): Walmart, Etsy, Target, Meesho, JioMart, Lazada, Allegro
- Classification: VERIFIED FACT
- Source: https://www.walmart.com/robots.txt ; https://www.etsy.com/robots.txt ; https://www.target.com/robots.txt ; https://www.meesho.com/robots.txt ; https://www.jiomart.com/robots.txt ; https://www.lazada.sg/robots.txt (and .com.my, .co.th, .com.ph, .vn, .co.id) ; https://allegro.pl/robots.txt
- Accessed: 2026-10-30 · Tier: 1
- Google tokens that do appear: Walmart — "User-agent: Adsbot-Google" and "User-agent: Mediapartners-Google" (lines 110–112, empty rule set, grouped with Slurp's `Crawl-delay: 5`). Etsy — "User-agent: AdsBot-Google-Mobile" (line 4, `/people` disallows). Allegro — "user-agent: Mediapartners-Google" (line 39). Lazada ID — "User-agent: Googlebot-Image" (last line, no rules). JioMart (167 groups) and Meesho, Target: no Google token at all. Lazada SG/MY/TH/PH/VN name only OpenAI tokens (D-03).
- Establishes: These marketplaces do not opt out of Google-Extended. Their product pages fall under `*` for Googlebot and Storebot-Google.
- Limitations: Only Google tokens were checked; path-level crawlability of product URLs was not tested here (see D-16 for key paths).

### Part 2 — Marketplaces: official relationships with Google AI shopping

### GD-23 UCP launched 2026-01-11: co-developed with Shopify, Etsy, Wayfair, Target and Walmart; endorsed by 20+ including Flipkart
- Claim: Google launched UCP as an open standard for agentic commerce. It names co-developers and endorsers. Checkout was to start with "eligible U.S. retailers" in AI Mode and the Gemini app; retailers remain seller of record.
- Classification: VERIFIED FACT
- Sources:
  - New tech and tools for retailers to succeed in an agentic shopping era — Google — https://blog.google/products/ads-commerce/agentic-commerce-ai-tools-protocol-retailers-platforms/ — 2026-01-11
  - The AI platform shift and the opportunity ahead for retail (Sundar Pichai, NRF) — Google — https://blog.google/company-news/inside-google/message-ceo/nrf-2026-remarks/ — 2026-01-11
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "UCP was co-developed with industry leaders including Shopify, Etsy, Wayfair, Target and Walmart, and endorsed by more than 20 others across the ecosystem like Adyen, American Express, Best Buy, Flipkart, Macy’s Inc., Mastercard, Stripe, The Home Depot, Visa and Zalando."

  > "To start, UCP will soon power a new checkout feature on eligible Google product listings in AI Mode in Search and the Gemini app, allowing shoppers to check out from eligible U.S. retailers right as they’re researching on Google."

  > (Pichai) "Throughout this process, the retailer remains the merchant of record, allowing them to own and shape the customer relationship."
- Establishes: Official UCP status for marketplaces in scope as of launch: Etsy, Target, Walmart = co-developers; Flipkart = endorser. Amazon, eBay, Mercado Libre, Rakuten, Shopee, Lazada, Allegro, Myntra, Meesho, JioMart are not named in the launch post.
- Limitations: The full 20+ endorser list was an image ("Support of the Universal Commerce Protocol from across the ecosystem.") and was not captured as text.

### GD-24 UCP checkout scope in Google's merchant docs: US only (Merchant Center hub), Canada/Australia next
- Claim: Google's UCP Merchant Center guide says the integration hub is rolling out in the US, with Australia and Canada "early next year", and applies only to products sold in the US. Google's May 2026 post says UCP checkout will reach Canada and Australia "in the coming months", then the UK. Native checkout is the default; embedded (iframe) checkout is for "specific, approved merchants".
- Classification: VERIFIED FACT
- Sources:
  - About Universal Commerce Protocol (UCP) integration hub in Merchant Center — https://developers.google.com/merchant/ucp/guides/merchant-center/overview — Last updated 2026-10-19 UTC
  - Getting started with Universal Commerce Protocol on Google — https://developers.google.com/merchant/ucp — Last updated not captured
  - Google blog 2026-05-20 (GD-14)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Important: the UCP integration hub is gradually rolling out in the United States, with Australia and Canada to follow early next year."

  > "Scope: this applies only to products sold within the United States."

  > "UCP-powered checkout will roll out across Canada and Australia in the coming months, and later to the U.K."

  > "UCP unlocks access to users on surfaces like AI Mode in Google Search and Gemini web (app coming soon)."
- Establishes: As documented, Google-hosted UCP checkout is a US program; India is not in the published rollout list. See C-3 for the Flipkart test.
- Limitations: Dates in the two sources conflict ("in the coming months" on 2026-05-20 vs "early next year" on 2026-10-19).

### GD-25 Walmart × Google (2026-01-11): Walmart-built experience inside Gemini via UCP, US first
- Claim: Walmart and Google announced a Gemini shopping experience for Walmart and Sam's Club, "built by Walmart" and accessed in Gemini through UCP, launching first in the US.
- Classification: VERIFIED FACT
- Source: Walmart and Google Turn AI Discovery Into Effortless Shopping Experiences — Walmart Inc. — https://corporate.walmart.com/news/2026/01/11/walmart-and-google-turn-ai-discovery-into-effortless-shopping-experiences
- Published/updated: Jan. 11, 2026
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "The new experience — built by Walmart and accessible directly within Gemini using the Universal Commerce Protocol — addresses several key customer needs:"

  > "The new experience will first launch directly within Gemini in the U.S. and internationally thereafter."
- Also: Walmart's 2026-10-21 release lists "conversational commerce integrations with Muse, ChatGPT, Gemini and others" (D-09). Google's Universal Cart launch (GD-28) names Walmart among checkout merchants.
- Establishes: Walmart reaches Gemini through a Walmart-built, UCP-connected experience, not through crawl rules (Walmart's robots.txt names no Google AI token, GD-22).
- Limitations: Launch date of the Gemini experience is not stated in the release. Dashes in the quote are em dashes (raw bytes E2 80 94 in the fetched HTML).

### GD-26 Amazon sits on the UCP Shopping Tech Council (2026); no Amazon catalog integration with Gemini/AI Mode found
- Claim: UCP's maintainer file lists an Amazon representative on the Shopping Tech Council, with Google, Shopify, Etsy, Meta, Microsoft, Salesforce, Stripe, Target and Wayfair. ucp.dev lists Amazon among "Co-developed by industry leaders" logos for Shopping. A Google/Shopify press release distributed by Newsfile on 2026-04-24 (Tier 3 copy) says Amazon, Meta, Microsoft, Salesforce and Stripe joined the Tech Council.
- Classification: VERIFIED FACT (council membership file and ucp.dev logos). "Amazon products can be bought in Gemini/AI Mode" is UNVERIFIED (no source). TechCrunch (GD-30) reports Amazon listings appeared in Gemini without a Buy button (Tier 3).
- Sources:
  - UCP Maintainers — Universal-Commerce-Protocol/.github — https://github.com/Universal-Commerce-Protocol/.github/blob/main/MAINTAINERS.md (raw fetched); last commit touching the file 2026-10-12
  - Universal Commerce Protocol — ucp.dev — https://ucp.dev/ (date not stated)
  - "Amazon, Meta, Microsoft, Salesforce, and Stripe Join the Universal Commerce Protocol Tech Council" — Yahoo Finance copy of a Newsfile Corp. release dated April 24, 2026 — https://finance.yahoo.com/sectors/technology/articles/amazon-meta-microsoft-salesforce-stripe-150500021.html (Tier 3; original https://www.newsfilecorp.com/release/294133 returned HTTP 202 with empty body to curl)
- Accessed: 2026-10-30
- Tier: 1 (repo, ucp.dev) / 3 (release copy)
- Excerpt:
  > "| Jordan Williams | Amazon     |" (Shopping Tech Council table)

  > "The Shopping Tech Council is responsible for the technical direction and overall design of the protocol for Shopping Domain."

  > (GOVERNANCE.md) "Includes 16 members, 4 permanent members from each founding organization (Google & Shopify), each with 1 vote (total 8 votes)."

  > (Yahoo copy, via WebFetch) "Amazon, Meta, Microsoft, Salesforce, and Stripe are now a part of the Universal Commerce Protocol (UCP) Tech Council"
- Establishes: Amazon participates in governing the protocol that powers Gemini/AI Mode checkout, while its robots.txt blocks Google-Extended and two GoogleAgent-* tokens (GD-17). These are different layers (protocol governance vs crawl policy).
- Limitations: Council membership does not show Amazon implementing UCP for its own store. Walmart (a UCP co-developer) is not on the Shopping Tech Council list.

### GD-27 Etsy × Google (2026-01-11): Etsy co-develops UCP; US signed-in Google users can buy some Etsy items in AI Mode and Gemini; live from 2026-02-11
- Classification: VERIFIED FACT
- Sources:
  - Etsy Partners with Google to Make Sellers’ Items Available for Purchase on AI Surfaces — Etsy, Inc. — https://www.etsy.com/news/etsy-partners-with-google-on-ai-powered-shopping (direct: HTTP 403; read via Wayback https://web.archive.org/web/20260213122144id_/https://www.etsy.com/news/etsy-partners-with-google-on-ai-powered-shopping , captured 2026-02-13) — Jan 11, 2026
  - What to expect in digital advertising and commerce in 2026 — Google — https://blog.google/products/ads-commerce/digital-advertising-commerce-2026/ — datePublished 2026-02-11
- Accessed: 2026-10-30
- Tier: 1 (Etsy via archive)
- Excerpt:
  > "Starting soon, signed-in Google users in the U.S. will be able to purchase some Etsy items directly in AI Mode in Google Search and the Gemini app. This integration, powered by the new Universal Commerce Protocol, helps the Etsy brand, our sellers, and their items show up across both new and familiar surfaces"

  > (Google, 2026-02-11) "In fact, UCP-powered checkout is rolling out now, letting US shoppers buy items from Etsy and Wayfair, right in AI Mode in Search and the Gemini app (with Shopify, Target, and Walmart coming soon)."
- Establishes: Etsy is the first marketplace in scope with Google-hosted checkout in AI Mode/Gemini (US).
- Limitations: "some Etsy items" is not defined.

### GD-28 Google agentic checkout (2025-11-13) and Universal Cart (US launch 2026-10-15) name Target and Walmart among merchants
- Claim: In Nov 2025 Google started "agentic checkout" (Google buys on the merchant site after price-tracking, with user confirmation) for eligible US merchants. On 2026-10-15 Universal Cart launched in the US across Search and Gemini, with Google Pay checkout or transfer to the merchant's cart; named merchants include Target and Walmart. Gemini app shopping (Shopping Graph listings) became available to all US Gemini users on 2025-11-13.
- Classification: VERIFIED FACT
- Sources:
  - Google Shopping launches agentic checkout and more AI shopping tools — Google — https://blog.google/products-and-platforms/products/shopping/agentic-checkout-holiday-ai-shopping/ — 2025-11-13
  - Google’s new Universal Cart launches today in the U.S. — Google — https://blog.google/products-and-platforms/products/shopping/universal-cart-launch/ — 2026-10-15
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Agentic checkout is starting to roll out now on Search, including in AI Mode, from eligible merchants in the U.S. like Wayfair, Chewy, Quince and select Shopify merchants, with many more coming soon."

  > "This is available to all Gemini users in the U.S. starting today — simply ask a shopping-related question to get started."

  > "Try these simplified checkout experiences with merchants like Nike, Sephora, Target, Ulta Beauty, Walmart, Wayfair, and many Shopify merchants. Either way, you will receive direct confirmations and customer support from the merchant, and they will remain the seller of record."
- Establishes: As of 2026-10-30, Target and Walmart are named checkout merchants in Google's US Universal Cart. Target's own fact sheet (D-11, 2026-06-18) says it has shopping experiences in "Google Search, including AI Mode, and the Gemini app".
- Limitations: Names are examples ("merchants like"). Amazon and eBay are not named.

### GD-29 Flipkart (India): Google says "Merchants like Flipkart are already partnering with Google" on UCP-based agentic shopping (Sep 2026)
- Claim: Google's Think with Google recap of Google Marketing Live India names Flipkart as a merchant partnering with Google to offer UCP agentic experiences to Indian shoppers.
- Classification: VERIFIED FACT
- Source: Google Marketing Live: What’s next for marketers in India — Google (business.google.com, Think) — https://business.google.com/en-all/think/future-of-marketing/google-marketing-live-india-ai-search/
- Published/updated: "September 2026"; datePublished 2026-09-18
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Agentic commerce: To enable Gemini users’ agents to securely complete checkout and buy your eligible products in Google, we’ve introduced the Universal Commerce Protocol (UCP), an open standard for agentic commerce. The UCP acts as a universal translator between merchants’ inventories and AI agents. Merchants like Flipkart are already partnering with Google to offer this agentic experience to Indian shoppers, and help brands grow sales."

  > "AI Overviews has over 2.5 billion monthly users, while AI Mode has surpassed 1 billion monthly users."
- Establishes: Flipkart is the only Indian marketplace in scope that Google names as an agentic-commerce partner.
- Limitations: Marketing page; it does not describe the integration, launch date or availability. See C-3 (US-only UCP scope in developer docs).

### GD-30 Flipkart checkout test inside Gemini and AI Mode in India (reported 2026-09-26, Tier 3); Google's stake in Flipkart
- Claim: TechCrunch reports a limited test in which some Indian users see a Buy button on select Flipkart listings in Gemini and AI Mode that opens a Flipkart-branded checkout; Amazon listings appeared without the button. Google's spokesperson gave a generic statement. TechCrunch states Google invested about $350 million in Flipkart in 2024.
- Classification: UNVERIFIED at primary source (Tier 3 report; Google's quoted statement neither confirms nor denies). The 2024 investment: UNVERIFIED in this session at primary source (Flipkart/Google announcement not fetched).
- Source: Google tests buying from Walmart-owned Flipkart through Gemini and AI Mode in India — TechCrunch — https://techcrunch.com/2026/09/26/google-tests-buying-from-walmart-owned-flipkart-through-gemini-and-ai-mode-in-india/
- Published/updated: datePublished 2026-09-27T01:30:00Z (URL date 2026-09-26)
- Accessed: 2026-10-30
- Tier: 3
- Excerpt:
  > "Users in the test see a Buy button on select Flipkart product listings appearing in Gemini and Google’s AI Mode, which takes them directly to a Flipkart checkout flow without leaving the AI interface, according to people familiar with the matter and as seen by TechCrunch."

  > "Google plans to roll out the experience more broadly later in October, ahead of India’s festive shopping season, one of the people said."

  > "In the experience seen by TechCrunch, listings from rivals, including Amazon, appeared alongside Flipkart products but did not offer the option to purchase directly through the AI interface."
- Establishes: Lead only. If accurate, Amazon India products are shown in Gemini/AI Mode listings despite Amazon's Google-Extended block (GD-17); this would fit Google's rules (Shopping Graph / Search, not Google-Extended, GD-01–GD-04) but is not verified here.
- Limitations: Anonymous sources; rollout "later in October" not confirmed by any primary source found.

### GD-31 India: Google's AI shopping in Gemini (English, Hindi) and AI Mode shopping upgrade (2026-04-07)
- Claim: Google India announced Gemini app shopping (Shopping Graph listings, comparison tables, prices, places to buy; English and Hindi) and its "biggest upgrade to shopping in AI Mode in Search in India" (English; Hindi "soon").
- Classification: VERIFIED FACT
- Source: New ways Google is using AI to make shopping easier — Google India Team (blog.google/intl/en-in) — https://blog.google/intl/en-in/products/explore-communicate/new-ways-google-is-using-ai-to-make-shopping-easier/
- Published/updated: 07 Apr, 2026 (datePublished 2026-04-07)
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "You can move beyond simple text suggestions and get shoppable product listings, comparison tables, prices from across the web and places to buy right in the Gemini app. Shopping in Gemini is powered by the Shopping Graph so you can trust you’re seeing fresh information and unmatched selection. This experience is currently available in English and Hindi."

  > "We’ve rolled out our biggest upgrade to shopping in AI Mode in Search in India, making it more conversational and seamless."
- Establishes: Shopping Graph product listings appear in Gemini and AI Mode in India since April 2026. India's documented path for marketplace products is the Shopping Graph (discovery), plus the Flipkart agentic partnership (GD-29). India is also in the Merchant Center AI performance insights rollout (GD-14) and the 2025 brand-profile conversational feature (GD-15).
- Limitations: The post names no merchant or marketplace.

### GD-32 Sea (Shopee) × Google (2026-02-19): joint exploration of an "AI agentic shopping prototype" across Shopee and Google; AP2 collaboration via Monee
- Classification: VERIFIED FACT (announcement). Live integration: UNVERIFIED (none found).
- Source: Sea and Google Deepen Partnership to Deliver AI-Powered Innovations for Consumers Globally — Sea Limited — https://www.sea.com/news/384
- Published/updated: 19 February, 2026
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Advancing Agentic Commerce: Shopee and Google will jointly explore the building of an AI agentic shopping prototype that can seamlessly integrate across Shopee and Google platforms to enhance the e-commerce discovery, engagement, and transaction experience."
- Establishes: Shopee has an announced exploratory Google agentic-commerce relationship (in addition to its ChatGPT app, D-24).
- Limitations: "Explore" language; no product, market or date.

### GD-33 Walmart and Target also appear in Google's GML 2026 checkout list; checkout expansion beyond US
- Claim: Google's 2026-05-20 post says shoppers can try select checkout features "soon" across Nike, Sephora, Target, Ulta Beauty, Walmart, Wayfair and Shopify merchants, and names Universal Cart, Direct Offers, YouTube Shopping ads with UCP checkout.
- Classification: VERIFIED FACT
- Source: GD-14 (blog.google, 2026-05-20)
- Accessed: 2026-10-30 · Tier: 1
- Excerpt:
  > "Shoppers can try these select checkout features soon across retailers like Nike, Sephora, Target, Ulta Beauty, Walmart, Wayfair and Shopify merchants such as Fenty and Steve Madden. Regardless of how a shopper chooses to buy, the retailer always remains the merchant of record."
- Establishes: Target and Walmart move from co-developers (Jan) to named checkout merchants (May, Oct).
- Limitations: Superseded in detail by the 2026-10-15 launch post (GD-28).

### GD-34 Google's robots.txt group selection: one group per crawler; Storebot-Google falls back to `*`, not to Googlebot; `crawl-delay` unsupported
- Claim: Google's crawlers use only the most specific matching group. Specific groups and `*` are never combined. Google's own example states Storebot-Google follows `*` when no Storebot-Google group exists, even if a Googlebot group exists. Google does not support `crawl-delay`.
- Classification: VERIFIED FACT
- Source: How Google interprets the robots.txt specification — Google Crawling infrastructure docs — https://developers.google.com/crawling/docs/robots-txt/robots-txt-spec
- Published/updated: Last updated 2026-10-23 UTC
- Accessed: 2026-10-30
- Tier: 1
- Excerpt:
  > "Only one group is valid for a particular crawler. Google's crawlers determine the correct group of rules by finding in the robots.txt file the group with the most specific user agent that matches the crawler's user agent. Other groups are ignored."

  > "If there's more than one specific group declared for a user agent, all the rules from the groups applicable to the specific user agent are combined internally into a single group. User agent specific groups and global groups (*) are not combined."

  > "Storebot-Google follows group 2, because there is no specific Storebot-Google group." (group 2 is `user-agent: *` in Google's example, with a separate `user-agent: googlebot` group 3)

  > "Google supports the following fields (other fields such as crawl-delay aren't supported):"
- Establishes: Interpretation key for Part 2. On eBay, Rakuten and Shopee, Googlebot (Search, hence AI Overviews / AI Mode) and Storebot-Google (Shopping) can receive different rules. On Flipkart, the Storebot-Google group replaces `*` entirely. Google-Extended is a control token, not a crawler (GD-01); the spec page does not say how it is matched, but a Google-Extended group only matters where it exists (Amazon).
- Limitations: Google's spec governs Google's crawlers; it does not cover user-triggered fetchers such as Google-Agent, which "generally ignore robots.txt" (GD-09).

### GD-35 Myntra and Mercado Libre (MX, BR, AR, articulo.MX): no Google token in robots.txt; Mercado Libre blocks Amazonbot, Perplexity, Claude and OpenAI agents but not Google-Extended
- Claim: Read in the in-app browser (own tab) after plain curl failed (GD-16). Myntra's file has one group (`User-agent: *`, 24,173 characters) and no Google token. Mercado Libre's three country files and the product host articulo.mercadolibre.com.mx have no Google token. Their first group blocks seven non-Google AI agents; Bingbot has its own group; `*` comes last.
- Classification: VERIFIED FACT (rendered file text; HTTP status from the browser's Navigation Timing `responseStatus` = 200 for all five). "Mercado Libre allows Google-Extended, Googlebot and Storebot-Google under `*`" is EVIDENCE-BASED INFERENCE from GD-34.
- Sources: https://www.myntra.com/robots.txt ; https://www.mercadolibre.com.mx/robots.txt ; https://www.mercadolivre.com.br/robots.txt ; https://www.mercadolibre.com.ar/robots.txt ; https://articulo.mercadolibre.com.mx/robots.txt
- Published/updated: not stated
- Accessed: 2026-10-30
- Tier: 1
- Excerpt (mercadolibre.com.ar lines 1–8; MX and BR identical; articulo.MX identical lines 1–8):
  > "User-agent: Amazonbot
  > User-agent: PerplexityBot
  > User-agent: Perplexity-User
  > User-agent: ClaudeBot
  > User-agent: Claude-User
  > User-agent: GPTBot
  > User-agent: ChatGPT-User
  > Disallow: /"
- Other `User-agent` lines: MX/AR/BR — FacebookExternalHit, FacebookBot, Twitterbot, LinkedInBot (`Allow: /`), Bingbot (line 16), `*` (MX l.57, BR l.67, AR l.58). articulo.MX — Twitterbot (l.10), Bingbot (l.13, `Crawl-delay: 5`), `*` (l.96). Myntra line 1–2: "User-agent: *" / "Allow: /".
- Establishes: Mercado Libre's AI blocking (D-04) targets Amazon, Perplexity, Anthropic and OpenAI agents and leaves every Google token (including Google-Extended) under `*`. Myntra names no bot at all.
- Limitations: Rendered `innerText`, not raw bytes; whitespace may differ from the file. Not fetched with curl.

### GD-36 Google VP (Mar 2026, Tier 3): working with "partners in APAC like Flipkart and Shopee" to bring UCP capability "in the coming months"
- Claim: Storyboard18 reports that Dan Taylor, Vice President, Global Ads at Google, said at a roundtable that Google was working with APAC partners including Flipkart and Shopee to bring UCP capability to the region.
- Classification: UNVERIFIED at primary source (Tier 3 report of oral remarks). Consistent with GD-29 (Google page naming Flipkart) and GD-32 (Sea release).
- Source: Google to debut Universal Commerce Platform in India with Flipkart in coming months — Storyboard18 — https://storyboard18.com/digital/google-and-flipkart-to-launch-universal-commerce-platform-soon-91935.html
- Published/updated: March 12, 2026, 11:03:40 IST
- Accessed: 2026-10-30 (via WebFetch; fragments only)
- Tier: 3
- Excerpt (fragments returned verbatim by WebFetch):
  > "We are working with some partners in APAC like Flipkart and Shopee"

  > "to bring this capability to customers in the region in the coming months."

  > "Google is planning to launch its Universal Commerce Platform with IPO-bound Flipkart in the coming months."
- Establishes: Lead that Google planned UCP checkout in India (Flipkart) and Southeast Asia (Shopee) from early 2026.
- Limitations: The article misnames UCP as "Universal Commerce Platform" and says the US launch "occurred in 2025", which conflicts with Google's 2026-01-11 launch (GD-23). Full quote not captured.

### GD-37 No official Google AI-shopping relationship found for eBay, Mercado Libre, Rakuten, Lazada, Allegro, Myntra, Meesho or JioMart
- Claim: Searches (English; Google, marketplace newsrooms, UCP materials) found no announcement of UCP participation, Gemini/AI Mode integration, or AI-shopping partnership with Google for these eight marketplaces. None appears in Google's UCP launch post (GD-23), ucp.dev co-developer logos or the UCP Shopping Tech Council file (GD-26), or Google's checkout merchant lists (GD-27, GD-28, GD-33).
- Classification: UNVERIFIED HYPOTHESIS that none exists (negative search). Absence from the named Google/UCP documents: VERIFIED FACT.
- Source: documents in GD-23, GD-26, GD-28, GD-33; web searches 2026-10-30 (no qualifying result)
- Accessed: 2026-10-30
- Tier: n/a
- Establishes: As of 2026-10-30 these marketplaces' documented path into Gemini / AI Mode is the general one: Search index (Googlebot) and Shopping Graph (crawl and/or Merchant Center, GB-27, GB-30). None blocks Google-Extended (GD-18, GD-20, GD-22, GD-35).
- Limitations: Searches were not run in Japanese, Polish, Spanish, Portuguese or Hindi. Merchant Center participation (free listings) by these marketplaces is not publicly stated and was not tested. A Tier 3 search summary speculated JioMart may follow Flipkart; no source supports it.

## 3. Contradictions and superseded information

- C-1 (scope of Google-Extended): Google's crawler doc (GD-01, updated 2026-10-30) says Google-Extended covers Gemini Apps and Vertex AI training/grounding and "does not impact a site's inclusion in Google Search". The Search Console help page (GD-04) says "to limit training of the models used to generate responses in Search generative AI features, use Google-Extended." The two are compatible only if the Gemini models used in AI Overviews/AI Mode are "future generations of Gemini models" covered by the training clause; the crawler doc does not name Search. Record as unresolved wording conflict.
- C-2 (AI features page outdated): The AI features page (last updated 2025-12-10) says "There are no additional technical requirements" and names robots.txt for Googlebot plus snippet controls as the controls. The AI optimization guide (2026-07-10) adds a Search Console inclusion requirement, and the Search generative AI control rolled out worldwide on 2026-08-31 (GD-04). The AI features page has not been updated to mention it.
- C-3 (UCP geography): Google's UCP developer docs (updated 2026-10-19) say the Merchant Center hub "applies only to products sold within the United States", with Canada/Australia next (GD-24). Google's India marketing page (2026-09-18) says Flipkart is "already partnering" on UCP agentic experiences for Indian shoppers (GD-29), and TechCrunch reports a Flipkart-branded checkout test in India (GD-30). Possible resolution (UNVERIFIED HYPOTHESIS): India runs as a partner-specific pilot outside the self-serve Merchant Center program.
- C-4 (UCP rollout timing): 2026-05-20 post says Canada/Australia checkout "in the coming months"; the 2026-10-19 developer guide says the hub reaches Australia and Canada "early next year".
- C-5 (UCP membership framing): ucp.dev shows Amazon, Microsoft, Meta, Salesforce and Stripe under "Co-developed by industry leaders" (GD-26). Google's Jan 2026 launch post lists only Shopify, Etsy, Wayfair, Target and Walmart as co-developers (GD-23). The later additions joined the Tech Council in April 2026 (Tier 3 release). Walmart is a named co-developer but not on the Shopping Tech Council file.
- C-6 (Amazon stance): Amazon blocks Google-Extended and GoogleAgent-* in robots.txt (GD-17) and enforces Agent Terms against third-party agents (D-17), yet holds a UCP Shopping Tech Council seat (GD-26). Different layers; not a factual contradiction.
- C-7 (agent tokens): Amazon names `GoogleAgent-Mariner` and `GoogleAgent-Shopping`; Google's fetcher list names `Google-Agent` (GD-09). The Amazon rules therefore do not target the token Google documents.
- SUPERSEDED: Gemini-app shopping was US-only on 2025-11-13 (GD-28); India got it on 2026-04-07 (GD-31).
- SUPERSEDED: UCP checkout "soon" for Target and Walmart (2026-02-11, GD-27) → named in the US Universal Cart launch (2026-10-15, GD-28).
- C-8 (press error, Tier 3): Storyboard18 (2026-03-12, GD-36) says UCP's US launch "occurred in 2025" and calls it "Universal Commerce Platform". Google's primary posts date the UCP launch to 2026-01-11 (GD-23) and US checkout rollout to 2026-02-11 (GD-27). Google's separate "agentic checkout" (Google buys on the merchant site) did start in Nov 2025 (GD-28); the press item likely conflates the two (EVIDENCE-BASED INFERENCE).
- C-9 (ChatGPT notes vs this pass): D-16 recorded Myntra 200 with a Chrome User-Agent and Mercado Libre 200 with a Chrome User-Agent; this pass got connection reset / 403 with curl's default User-Agent and 200 in the in-app browser. Content (Google tokens absent; Mercado Libre first group) is consistent with D-04 and D-16.

## 4. Knowledge gaps

- No Google document fetched says how AI Mode or Gemini choose between a marketplace offer and a brand-site offer for the same product, or how third-party marketplace sellers are attributed. Google has no published equivalent of OpenAI's "maker or primary seller" factor (D-21).
- Which data sources feed Gemini/AI Mode product listings for a given marketplace (Storebot-Google crawl, Googlebot crawl, Merchant Center feed, partner API) is not documented per marketplace.
- Whether the Search generative AI control (GD-04) removes a site's Merchant Center product listings from AI Mode is not stated; the help page only says it "doesn't override" Merchant Center participation.
- Whether Gemini app answers (as opposed to Gemini grounding) can show products from a Google-Extended-blocked site (Amazon): no primary statement. TechCrunch (Tier 3) reports Amazon listings in Gemini (GD-30).
- GoogleAgent-Mariner / GoogleAgent-Shopping: no Google documentation found; archived copies of Google's fetcher page could not be read (empty shells), so prior documentation cannot be ruled out.
- Flipkart: Google's 2024 investment and Flipkart's own statement on the Gemini/AI Mode test were not fetched at primary source. Status of the "later in October" rollout: unknown.
- Myntra, Meesho, JioMart, eBay, Mercado Libre, Rakuten, Lazada, Allegro × Google AI shopping: no relationship found (GD-37; English searches only).
- Whether any marketplace in scope submits Merchant Center feeds / free listings: not publicly stated; not tested.
- India: no Google primary source states that Google-hosted UCP checkout is live in India; developer docs say US only (GD-24). The Flipkart test (GD-30) and the "later in October" broader rollout are Tier 3 only.
- Whether Google treats `GoogleAgent-Mariner` / `GoogleAgent-Shopping` robots.txt groups as binding for any product: no Google statement.
- Mercado Libre and Myntra robots.txt were read as rendered browser text, not raw bytes (GD-35).

## 5. Unfetched sources

- https://www.mercadolibre.com.mx/robots.txt , https://www.mercadolivre.com.br/robots.txt , https://www.mercadolibre.com.ar/robots.txt — HTTP 403 (curl default UA). curl retry with a browser User-Agent blocked by session permission policy ("Bot Check Circumvention"); not performed. Read successfully in the in-app browser (GD-35).
- https://www.myntra.com/robots.txt — curl 000 twice ("Recv failure: Connection was reset"). Read successfully in the in-app browser (GD-35).
- https://storyboard18.com/digital/google-and-flipkart-to-launch-universal-commerce-platform-soon-91935.html — read via WebFetch only; full Taylor quote not captured (fragments).
- Flipkart Stories (stories.flipkart.com) — no 2024 Google-investment or 2026 Google/Gemini statement found; WordPress API path returned 404.
- https://www.lazada.co.id/robots.txt — first attempt curl 000; retry 200 (used).
- https://www.etsy.com/news/etsy-partners-with-google-on-ai-powered-shopping — HTTP 403; used Wayback 20260213122144.
- https://www.newsfilecorp.com/release/294133 — HTTP 202, empty body (curl); WebFetch returned no content. Used Yahoo Finance copy (Tier 3).
- https://developers.google.com/search/docs/specialty/ecommerce/where-ecommerce-content-can-appear-on-google — HTTP 404.
- https://developers.google.com/crawling/updates — HTTP 404 (changelog lives at /crawling/docs/changelog).
- Wayback captures of Google's user-triggered fetcher page (2025-08-14, 2025-11-04, 2026-03-08, 2026-04-15) — content not present in `id_` captures (shell pages); history check failed.
- Not attempted: Google Merchant Center Help articles on marketplaces/multi-seller accounts (Merchant Center coverage is in GB notes); non-English searches for Rakuten, Allegro, Mercado Libre, Indian marketplaces.

## 6. Source list

Tier 1 — Google crawling and Search Central (all accessed 2026-10-30)
- List of Google's common crawlers — https://developers.google.com/crawling/docs/crawlers-fetchers/google-common-crawlers — updated 2026-10-30
- List of Google's special-case crawlers — https://developers.google.com/crawling/docs/crawlers-fetchers/google-special-case-crawlers — updated 2026-09-17
- List of Google user-triggered fetchers — https://developers.google.com/crawling/docs/crawlers-fetchers/google-user-triggered-fetchers — updated 2026-08-19
- Overview of Google crawlers and fetchers — https://developers.google.com/crawling/docs/crawlers-fetchers/overview-google-crawlers — updated 2026-06-12
- Crawling changelog — https://developers.google.com/crawling/docs/changelog — updated 2026-10-30
- user-triggered-agents.json — https://developers.google.com/static/crawling/ipranges/user-triggered-agents.json — creationTime 2026-10-30
- AI features and your website — https://developers.google.com/search/docs/appearance/ai-features — updated 2025-12-10
- Optimizing your website for generative AI features on Google Search — https://developers.google.com/search/docs/fundamentals/ai-optimization-guide — updated 2026-07-10
- Search Central documentation updates — https://developers.google.com/search/updates — updated 2026-10-26
- Robots meta tag, data-nosnippet, and X-Robots-Tag specifications — https://developers.google.com/search/docs/crawling-indexing/robots-meta-tag — updated 2026-03-24
- Introduction to Product structured data — https://developers.google.com/search/docs/appearance/structured-data/product — updated 2025-12-10
- Product snippet structured data — https://developers.google.com/search/docs/appearance/structured-data/product-snippet — updated 2026-09-08
- Merchant listing structured data — https://developers.google.com/search/docs/appearance/structured-data/merchant-listing — updated 2026-09-08
- Product variant structured data — https://developers.google.com/search/docs/appearance/structured-data/product-variants — updated 2026-09-08
- Merchant shipping policy / return policy structured data — https://developers.google.com/search/docs/appearance/structured-data/shipping-policy ; https://developers.google.com/search/docs/appearance/structured-data/return-policy — both updated 2026-09-08 (fetched; not quoted)
- Best practices for ecommerce sites; Share your product data with Google — https://developers.google.com/search/docs/specialty/ecommerce ; https://developers.google.com/search/docs/specialty/ecommerce/share-your-product-data-with-google — updated 2025-12-10 (fetched; not quoted)
- How Google interprets the robots.txt specification — https://developers.google.com/crawling/docs/robots-txt/robots-txt-spec — updated 2026-10-23
- Search generative AI control — https://support.google.com/webmasters/answer/16908024
- Generative AI performance report (Search) — https://support.google.com/webmasters/answer/16984139 (fetched; "As of August 31, 2026, we’ve rolled out these insights to all websites worldwide.")
- Get started with Business Agent — https://support.google.com/brandprofile/answer/16410382

Tier 1 — Google commerce / UCP
- Getting started with UCP on Google — https://developers.google.com/merchant/ucp
- UCP FAQ — https://developers.google.com/merchant/ucp/faq — updated 2026-10-16
- UCP integration hub in Merchant Center — https://developers.google.com/merchant/ucp/guides/merchant-center/overview — updated 2026-10-19
- ucp.dev — https://ucp.dev/
- UCP MAINTAINERS.md and GOVERNANCE.md — https://github.com/Universal-Commerce-Protocol/.github
- Google, 2025-11-13 — https://blog.google/products-and-platforms/products/shopping/agentic-checkout-holiday-ai-shopping/
- Google, 2026-01-11 (UCP launch) — https://blog.google/products/ads-commerce/agentic-commerce-ai-tools-protocol-retailers-platforms/
- Google, 2026-01-11 (Pichai NRF) — https://blog.google/company-news/inside-google/message-ceo/nrf-2026-remarks/
- Google, 2026-02-11 — https://blog.google/products/ads-commerce/digital-advertising-commerce-2026/
- Google India, 2026-04-07 — https://blog.google/intl/en-in/products/explore-communicate/new-ways-google-is-using-ai-to-make-shopping-easier/
- Google, 2026-05-20 (GML) — https://blog.google/products-and-platforms/products/shopping/shopping-updates-google-marketing-live/
- Google, 2026-09-18 (GML India, Think) — https://business.google.com/en-all/think/future-of-marketing/google-marketing-live-india-ai-search/
- Google, 2026-10-15 (Universal Cart) — https://blog.google/products-and-platforms/products/shopping/universal-cart-launch/

Tier 1 — marketplaces and partners
- robots.txt files listed in GD-16 (accessed 2026-10-30)
- Walmart, 2026-01-11 — https://corporate.walmart.com/news/2026/01/11/walmart-and-google-turn-ai-discovery-into-effortless-shopping-experiences
- Etsy, 2026-01-11 — https://www.etsy.com/news/etsy-partners-with-google-on-ai-powered-shopping (via Wayback 20260213122144)
- Wayfair, 2026-01-12 — https://www.aboutwayfair.com/category/company-news/wayfair-partners-with-google-to-advance-ai-powered-shopping-for-the-home (context only; Wayfair is out of scope)
- Sea, 2026-02-19 — https://www.sea.com/news/384

Tier 3 — press
- TechCrunch, 2026-09-26 — https://techcrunch.com/2026/09/26/google-tests-buying-from-walmart-owned-flipkart-through-gemini-and-ai-mode-in-india/
- Storyboard18, 2026-03-12 — https://storyboard18.com/digital/google-and-flipkart-to-launch-universal-commerce-platform-soon-91935.html

Tier 1 — robots.txt read in the in-app browser (accessed 2026-10-30)
- https://www.myntra.com/robots.txt ; https://www.mercadolibre.com.mx/robots.txt ; https://www.mercadolivre.com.br/robots.txt ; https://www.mercadolibre.com.ar/robots.txt ; https://articulo.mercadolibre.com.mx/robots.txt
- Yahoo Finance (Newsfile copy), 2026-04-24 — https://finance.yahoo.com/sectors/technology/articles/amazon-meta-microsoft-salesforce-stripe-150500021.html
