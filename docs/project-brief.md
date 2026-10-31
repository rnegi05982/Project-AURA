# AURA — Global AI Commerce Discovery & Product Recommendation Research

Original project brief, saved verbatim on 2026-10-30. This is the scope authority. `CLAUDE.md` condenses its working rules.

## 1. Project Overview

- **Project Name:** AURA
- **Project Type:** Proof of Concept (POC) / Technical Research
- **Primary Focus:** AI-powered product discovery, retrieval, ranking, and recommendations across global e-commerce ecosystems.
- **Primary Implementation Perspective:** Shopify merchants and independent e-commerce stores.

### Mission

AURA is a research initiative designed to investigate how AI-powered applications discover, retrieve, evaluate, rank, and recommend products from across the internet.

The research will cover AI applications such as:

- ChatGPT
- Google Gemini
- Claude
- Perplexity
- Microsoft Copilot
- Other emerging AI-powered shopping and discovery applications.

The research must investigate product sources across the global commerce ecosystem, including:

- Shopify-powered stores
- Amazon
- Flipkart
- Walmart
- eBay
- Etsy
- AliExpress
- Alibaba
- Mercado Libre
- Rakuten
- Regional and country-specific marketplaces
- Independent e-commerce websites
- Other product catalogs and merchant platforms.

Important: Shopify is the primary perspective from which we want to derive actionable implementation recommendations. However, the research itself must remain platform-independent and cover the entire global commerce ecosystem.

We want to understand how products from different commerce platforms compete for visibility and recommendations inside AI applications.

## 2. Core Research Objective

The main objective is to understand the complete lifecycle of product discovery and recommendation inside AI-powered applications.

We want to answer:

1. How do AI applications discover products?
2. Where do they obtain product information?
3. Do they use search engines, web crawling, scraping, APIs, merchant feeds, product catalogs, third-party providers, or proprietary databases?
4. Do they maintain their own product indexes or use external product indexes?
5. How do they retrieve products relevant to a customer's query?
6. How do they evaluate and rank competing products?
7. What determines which merchant or marketplace gets recommended?
8. How do AI applications retrieve current pricing, availability, images, specifications, and product URLs?
9. What role do commerce protocols and product catalog integrations play?
10. What can an independent Shopify merchant implement to increase product discoverability and recommendation eligibility?

The ultimate goal is to convert research findings into practical, evidence-backed recommendations for Shopify merchants.

## 3. Primary Use Case

Consider a customer asking ChatGPT:

> "I am looking for a premium ceramic coffee mug under ₹1,000. Recommend some good options."

ChatGPT might recommend products from:

- Amazon
- Flipkart
- A Shopify-powered independent store
- Walmart
- Other merchant websites.

AURA must investigate the mechanisms behind this process.

### Questions to investigate

**Product discovery**

- How did the AI application discover these products?
- Did it discover them through web search, crawling, product feeds, APIs, or another mechanism?
- Does it use a dedicated product catalog?
- Does it rely on third-party commerce providers?

**Product retrieval**

- How does it identify products matching the customer's requirements?
- How does it understand product attributes such as material, price, size, and intended use?
- Does it use keyword search, semantic search, vector retrieval, or a combination?

**Product evaluation and ranking**

- How does it compare competing products?
- Does it consider price, reviews, availability, merchant reputation, relevance, or other factors?
- Which ranking mechanisms are publicly documented?
- Which mechanisms remain unknown?

**Merchant visibility**

- Why does one merchant appear while another does not?
- What information does a merchant need to expose?
- What technical integrations can improve product discoverability?
- Can an independent Shopify store compete with established marketplaces?

**Shopify implementation**

- What should the Shopify merchant implement?
- What product data should be available?
- What structured data is required or recommended?
- Are product feeds or commerce protocols supported?
- What storefront, indexing, and integration changes are beneficial?

The research must investigate these questions separately for each AI application.

## 4. Research Scope

### A. AI Applications

Investigate each platform independently.

1. ChatGPT / OpenAI
2. Google Gemini
3. Claude / Anthropic
4. Perplexity
5. Microsoft Copilot
6. Other relevant AI shopping and discovery applications.

For every platform, investigate:

- Product discovery architecture.
- Web search and browsing capabilities.
- Search engine integrations.
- Product catalog access.
- Merchant integrations.
- Product feeds.
- Product retrieval mechanisms.
- Product ranking and recommendation mechanisms.
- Product information sources.
- Real-time pricing and availability.
- Shopping-specific experiences.
- Commerce protocols.
- Merchant eligibility requirements.
- Technical documentation and published specifications.

Do not assume that all AI applications use the same architecture.

### B. Global Commerce Platforms

Research product sources across multiple countries and commerce ecosystems.

**Global marketplaces:** Amazon, eBay, Walmart, Etsy, AliExpress, Alibaba.

**Indian marketplaces:** Flipkart, Amazon India, Myntra, Meesho, JioMart, other relevant Indian commerce platforms.

**Other regional marketplaces:** Mercado Libre (Latin America), Rakuten (Japan), Shopee (Southeast Asia), Lazada (Southeast Asia), Allegro (Europe), other relevant regional platforms.

**Independent commerce infrastructure:** Shopify, WooCommerce, BigCommerce, Magento / Adobe Commerce, custom-built e-commerce websites.

Investigate how products from these different sources become discoverable to AI applications.

The list is not exhaustive. Expand it when new relevant platforms or commerce integrations are identified.

## 5. Technical Research Areas

### 5.1 Product Discovery and Search

Research: search engine indexing; web crawling; product discovery APIs; search engine result retrieval; semantic search; vector search; product indexing; third-party product discovery services; proprietary product databases; real-time web retrieval.

Determine which mechanisms are explicitly documented by each AI application.

### 5.2 Product Catalogs and Feeds

Investigate: Google Merchant Center; product data feeds; XML product feeds; CSV product feeds; JSON product catalogs; merchant APIs; product catalog integrations; third-party product data providers; product inventory synchronization.

Determine whether and how each AI application consumes these sources.

### 5.3 Commerce Protocols

Investigate relevant commerce protocols and standards, including: Universal Commerce Protocol (UCP); Model Context Protocol (MCP); agentic commerce integrations; OpenAI-supported commerce integrations; other emerging agent-to-commerce protocols.

For each protocol, establish:

- What problem it solves.
- Who developed or maintains it.
- Which applications support it.
- How merchants can integrate it.
- Whether it affects product discovery, product retrieval, checkout, or purchasing.
- Whether support is publicly documented or merely proposed.

Do not assume that adopting a protocol automatically improves product ranking or recommendations.

### 5.4 Structured Product Data

Investigate: Schema.org; Product schema; Offer schema; AggregateRating; Review; ProductGroup; JSON-LD; Open Graph metadata; product-specific metadata; canonical URLs; sitemap configuration.

Understand how structured data is consumed by search engines and whether there is evidence of its use by individual AI applications.

### 5.5 Product Ranking and Recommendation

Investigate: query understanding; product relevance; semantic matching; product attribute matching; ranking signals; merchant reputation; reviews and ratings; pricing; availability; product popularity; personalization; search-result selection; recommendation generation.

Clearly distinguish documented ranking factors from industry assumptions.

### 5.6 Merchant and Storefront Accessibility

Investigate: search engine crawler accessibility; robots.txt; XML sitemaps; JavaScript rendering; product page accessibility; structured content; product page metadata; storefront performance; product image accessibility; public product information; crawl restrictions and bot policies.

Determine which aspects are relevant to each platform.

## 6. Shopify-Specific Research

Although the research is global, Shopify implementation is our primary practical outcome. Investigate the following areas in detail.

**Product Page Optimization:** product titles; product descriptions; product specifications; product attributes; product variants; pricing; availability; images; reviews; product identifiers such as GTIN, UPC, EAN, and MPN; shipping and return information.

**Technical Store Optimization:** Shopify product URLs; product structured data; JSON-LD implementation; sitemap availability; robots.txt configuration; canonical URLs; storefront accessibility; crawlability; JavaScript rendering; duplicate product content.

**Commerce Integrations:** Shopify product feeds; Google Merchant Center; supported AI shopping integrations; UCP compatibility; MCP-based integrations; product catalog synchronization; inventory synchronization; merchant APIs.

**Content and Brand Discoverability:** product-specific landing pages; buying guides; comparison articles; FAQs; product use cases; brand information; merchant trust signals; external references and mentions.

For every recommendation, explain:

1. What should the Shopify merchant implement?
2. Why should they implement it?
3. Which AI applications or discovery systems does it affect?
4. What evidence supports the recommendation?
5. Is it mandatory, recommended, experimental, or unverified?
6. How can its impact be tested?

## 7. Strict Evidence and Source Requirements

This is one of the most important requirements of AURA.

Every factual research claim must have supporting evidence.

The project must not become a collection of generic SEO recommendations, assumptions, or AI-generated explanations.

### Preferred source hierarchy

**Tier 1 — Primary sources:** official AI platform documentation; official engineering blogs; official merchant integration documentation; official API documentation; official protocol specifications; official search engine documentation; published technical papers from platform developers.

**Tier 2 — Research and technical publications:** peer-reviewed research papers; university research; independent technical research; reputable engineering publications; technical experiments with reproducible methodologies.

**Tier 3 — Industry publications:** reputable industry blogs; technical SEO research; e-commerce research publications; credible industry analysis.

**Tier 4 — Community observations:** Reddit discussions; developer forums; merchant experiences; community experiments.

Tier 4 sources can help identify research questions and practical observations, but must not independently establish proprietary internal mechanisms.

### Evidence classification

Every finding must be classified as one of the following:

- **VERIFIED FACT** — Directly supported by an authoritative source.
- **EVIDENCE-BASED INFERENCE** — A reasonable conclusion supported by documented facts, but not explicitly confirmed by the platform.
- **UNVERIFIED HYPOTHESIS** — A possible explanation that requires further investigation or experimentation.
- **EXPERIMENTALLY OBSERVED** — A behavior reproduced through controlled experiments, with methodology and limitations documented.

Never present an inference or hypothesis as an officially confirmed internal mechanism.

### Required citation information

Every research finding must include: claim; source title; publisher; original URL; publication date, if available; access or verification date; relevant excerpt or supporting passage; evidence classification; explanation of what the source establishes; research limitations.

Never invent sources, URLs, quotations, or technical specifications.

If an article does not support the claim being made, do not cite it as evidence.

Prefer original sources over articles that merely repeat other articles.

## 8. Research Methodology

Follow this workflow for each research topic.

1. **Define the research question.** Write a specific question rather than researching broad topics without direction. Example: "Does ChatGPT use merchant product feeds to discover products from independent Shopify stores?"
2. **Search for primary documentation.** Official documentation, engineering articles, API specifications, technical announcements, research papers, official merchant integration guides.
3. **Identify the actual mechanism.** Determine what the evidence establishes (e.g. product discovery through web search, merchant catalog integration, product feed consumption, product retrieval through an API). Do not assume one mechanism explains every product recommendation.
4. **Document the evidence.** Record the claim, source, relevant passage, classification, and limitations.
5. **Identify Shopify implications.** Determine whether the finding creates a technical or operational action for Shopify merchants.
6. **Identify knowledge gaps.** Document what is not publicly known. Do not fill gaps with assumptions.
7. **Design experiments.** Where possible, design controlled tests to validate observable behavior.
8. **Produce actionable recommendations.** Convert validated findings into platform-specific implementation guidance.

## 9. Experimental Research

AURA should not rely exclusively on documentation. It should also perform reproducible experiments.

### Example: Coffee Mug Experiment

Select a group of products from Shopify stores, Amazon, Flipkart, and independent merchant websites.

Create a consistent set of product queries. Examples:

1. Best ceramic coffee mug under ₹1,000.
2. Premium handmade coffee mug.
3. Microwave-safe coffee mug.
4. Best coffee mug for office use.
5. Minimalist coffee mug with a wooden handle.

Run these queries against different AI applications.

Record: whether the product appears; merchant or marketplace; product URL; displayed price; product attributes; product images; citations or references; query wording; date and time; application and model; shopping or browsing mode; whether the product information is accurate.

Repeat experiments to identify variability.

### Experimental rules

- Keep query conditions consistent.
- Record the application version where possible.
- Separate personalized and non-personalized tests.
- Distinguish organic recommendations from sponsored placements.
- Record regional differences.
- Do not claim that a single experiment reveals the internal algorithm.
- Maintain raw observations separately from interpretations.

## 10. Expected Research Deliverables

- **A. Platform Research Reports** — one per AI application: architecture and documented mechanisms; product discovery; product retrieval; merchant integrations; product data sources; ranking and recommendations; technical requirements; evidence and limitations.
- **B. Commerce Ecosystem Research** — comparative study of Amazon, Flipkart, Walmart, eBay, Etsy, Shopify, other marketplaces and independent stores; how products from each become discoverable to AI applications.
- **C. Technology Research** — UCP, MCP, Schema.org, product feeds, merchant APIs, search indexing, agentic commerce, other emerging standards.
- **D. Shopify Implementation Guide** — technical checklist; product data requirements; structured data; catalog and feed integrations; storefront accessibility; content; platform-specific guidance.
- **E. Evidence Database** — claims, sources, classifications, research dates, platform associations, excerpts, confidence and limitations.
- **F. Experimental Results** — reproducible product recommendation experiments and results.
- **G. Final Recommendations** — "What should a Shopify merchant do today to maximize the likelihood that their products are discovered and recommended by AI applications?" Separated into: confirmed platform requirements; evidence-backed improvements; experimental recommendations; unverified possibilities.

## 11. Suggested Repository Structure

```
aura/
├── CLAUDE.md
├── README.md
├── research/
│   ├── ai-platforms/{chatgpt,gemini,claude,perplexity,copilot}/
│   ├── commerce-platforms/{amazon,flipkart,walmart,ebay,etsy,shopify,other-marketplaces}/
│   ├── technologies/{ucp,mcp,schema-org,product-feeds,merchant-apis,agentic-commerce}.md
│   └── research-topics/{product-discovery,product-retrieval,product-ranking,product-data-sources}.md
├── shopify/{product-optimization,structured-data,storefront-accessibility,catalog-integrations,implementation-guide}.md
├── experiments/{methodology.md,test-cases/,raw-observations/,findings/}
├── evidence/{evidence-registry,verified-facts,inferences,hypotheses}.md
└── reports/{platform-comparisons,commerce-ecosystem,final-recommendations}.md
```

This is an initial organizational structure. Modify it when there is a clear research or maintainability benefit.

## 12. Instructions for the AI Research Agent

You are acting as the principal technical research agent for AURA. Your responsibility is to conduct deep, evidence-focused research into AI-powered product discovery and recommendations across the global commerce ecosystem.

### Mandatory rules

1. Never invent technical mechanisms or platform capabilities.
2. Never claim to know proprietary internal algorithms without direct evidence.
3. Always prioritize primary sources.
4. Attach citations to individual factual claims.
5. Clearly distinguish verified facts, inferences, hypotheses, and experimental observations.
6. Investigate global marketplaces, not just Shopify.
7. Treat Shopify as the primary implementation perspective.
8. Research each AI application independently.
9. Investigate the complete product discovery lifecycle, not just SEO.
10. Keep track of publication dates and whether documentation is current.
11. Identify contradictions between sources.
12. Document knowledge gaps explicitly.
13. Do not recommend an implementation simply because it is commonly discussed in GEO or SEO articles.
14. Explain why every Shopify recommendation matters and which evidence supports it.
15. Do not assume that product visibility guarantees product recommendations.

### Research quality expectations

Research should be detailed enough that a developer can understand: what the mechanism does; how it works according to available evidence; which platform uses it; what source proves it; what remains unknown; what implementation action follows from it.

Do not prioritize producing large quantities of documents over research quality. A small number of deeply researched, well-cited findings is more valuable than hundreds of unsupported claims.

## 13. Initial Research Roadmap

Do not attempt to investigate every topic simultaneously. Follow this sequence:

1. **Phase 1 — Understand AI Commerce:** define AI-powered product discovery; identify the major AI applications; understand the global commerce ecosystem; map the possible product discovery mechanisms.
2. **Phase 2 — Investigate Individual AI Applications:** ChatGPT first, then Gemini, Claude, Perplexity, others.
3. **Phase 3 — Investigate Product Sources:** Amazon and other major marketplaces; Shopify and independent stores; regional marketplaces; merchant catalogs and feeds; third-party product discovery providers.
4. **Phase 4 — Investigate Technical Infrastructure:** search and crawling; product feeds; structured data; merchant APIs; UCP and MCP; retrieval and ranking.
5. **Phase 5 — Translate Findings into Shopify Actions:** platform-specific requirements; common improvements; Shopify implementation checklist; separate verified requirements from recommendations.
6. **Phase 6 — Validate Through Experiments:** standardized product datasets; repeatable queries; compare AI applications; analyze product visibility; document reproducible findings.

## 14. First Task: Begin with ChatGPT Product Discovery

Research question: How does ChatGPT discover, retrieve, and recommend products from different e-commerce sources, including Amazon, Shopify stores, Flipkart, and independent merchant websites?

Investigate:

1. ChatGPT shopping and product discovery capabilities.
2. Officially documented product search and retrieval mechanisms.
3. Product information sources.
4. Merchant catalog integrations.
5. Product feeds and commerce protocols.
6. Product information and structured data.
7. Product ranking and recommendation mechanisms.
8. Merchant eligibility and technical requirements.
9. What a Shopify merchant can implement to improve product discoverability.
10. What remains unknown about ChatGPT's internal mechanisms.

Prioritize official OpenAI documentation, engineering publications, technical specifications, and credible research papers. Do not stop at introductory blog posts. Produce a detailed, source-cited research report and a corresponding evidence registry.

Once the ChatGPT research is established, use the same methodology to investigate the other AI applications.

## Final Project Principle

AURA is not an SEO checklist generator, a generic GEO guide, or a product recommendation engine.

It is a technical research initiative focused on understanding the intersection of: artificial intelligence; product discovery; search and retrieval systems; e-commerce marketplaces; merchant catalogs; agentic commerce; product ranking and recommendations.

The ultimate objective is to understand how the global commerce ecosystem becomes discoverable to AI applications and translate that understanding into evidence-backed actions that help independent Shopify merchants compete for visibility in AI-powered shopping experiences.
