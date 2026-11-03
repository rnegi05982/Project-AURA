# Gemini, AI Mode and AI Overviews — how Google discovers, retrieves and recommends products

- **Research question:** How do Google's AI surfaces discover, retrieve and recommend products from Amazon, Flipkart, Shopify stores and independent sites?
- **Scope:** three Google surfaces, reported separately: the **Gemini app**, **AI Mode** (conversational Google Search) and **AI Overviews** (AIO, generated summaries on the results page). Google states AI Mode and AIO "may use different models and techniques" <sup>[GEM-004]</sup>.
- **Status as of:** 2026-10-31. Sources accessed 2026-10-30.
- **Evidence:** registry files `evidence/registry/{gem,goog,ucp,shop,mkt,res}.md`. Raw captures: `notes/ga-` to `notes/ge-`.
- **Comparison with ChatGPT:** `reports/platform-comparisons.md`.

---

## 1. Answer

- All three surfaces draw product data from Google's **Shopping Graph** (Google's index of 60+ billion product listings) <sup>[GEM-001, GEM-003, GOOG-019]</sup>.
- The Shopping Graph is fed by **Merchant Center** feeds, Manufacturer Center, and what retailers post on the web <sup>[GOOG-020]</sup>. Crawled products can appear on Google without Merchant Center or schema.org markup <sup>[GOOG-010]</sup>.
- AI Mode retrieves by **query fan-out**: several simultaneous searches to derive product criteria <sup>[GEM-003]</sup>. The Gemini app also grounds some answers on Google Search <sup>[GEM-006]</sup>.
- **Ranking is undocumented for the AI surfaces.** Google says organic AI Mode and AIO answers come from "Search quality and ranking systems" and that ads do not influence them <sup>[GEM-007]</sup>.
- The only factor list Google publishes is for Google Shopping's "Top recommendations": relevance, ratings, price, product features <sup>[GOOG-022]</sup>. Google does not say the AI surfaces use it.
- Checkout through Google's Universal Commerce Protocol (UCP) is ranking-neutral, per Google <sup>[GOOG-003]</sup>.
- **India:** Gemini-app shopping (English, Hindi) and AI Mode shopping (English) are live <sup>[GEM-002]</sup>. Ads in AI Mode reached India on 2026-10-28 <sup>[GEM-008]</sup>. Buy buttons and Universal Cart are US-only for consumers <sup>[GEM-014]</sup>.
- **Shopify:** Google AI Mode and Gemini discover Shopify products through **Merchant Center**, not Shopify Catalog <sup>[SHOP-025]</sup>. Direct checkout is on by default for stores selling to US, Canadian or Australian buyers <sup>[SHOP-026, SHOP-027]</sup>.
- **Amazon** blocks Google-Extended (the Gemini grounding/training token) but not Googlebot or Google's Shopping crawler <sup>[MKT-022]</sup>. **Flipkart** explicitly allows Google's Shopping crawler and is Google's only named Indian UCP partner <sup>[MKT-025, GEM-016]</sup>.

Mechanism, in one line: shopping intent → query fan-out over Search and the Shopping Graph (fed by Merchant Center feeds and crawl) → model selects products under "Search quality and ranking systems" → product cards, comparisons and labeled ads → Buy on Google (US) or hand-off to the merchant site.

---

## 2. Timeline

| Date | Change | Evidence |
|---|---|---|
| 2025-05-20 | AI Mode shopping = Gemini + Shopping Graph; query fan-out | GEM-003 |
| 2025-09-16 | AP2 announced | UCP-005 |
| 2025-11-13 | Gemini app shopping (US); agentic checkout on merchant sites (US) | GEM-003, GEM-015 |
| 2026-01-11 | UCP launched with Shopify, Etsy, Wayfair, Target, Walmart; Flipkart endorses; Business Agent; Direct Offers pilot | UCP-001, GOOG-008, GEM-009 |
| 2026-02-11 | UCP checkout rolling out in AI Mode and Gemini (Etsy, Wayfair) | MKT-024 |
| 2026-04-07 | India: Gemini-app shopping (EN, HI); AI Mode shopping (EN) | GEM-002 |
| 2026-05-20 | AIO and AI Mode merged into one UI; Gemini 3.5 Flash default; conversational attributes global; Highlighted Answers ads | GEM-005, GOOG-012, GEM-009 |
| 2026-08-31 | Search Console "Search generative AI control" worldwide | GOOG-028 |
| 2026-09 | Google says UCP checkout covers "hundreds of thousands" of brands; Shopify stores auto-enrolled; Flipkart named as India partner | GEM-015, SHOP-026, GEM-016 |
| 2026-10-15 | Universal Cart (US) | GEM-014 |
| 2026-10-28 | Ads in AI Mode reach India and 9 other countries | GEM-008 |
| 2026-10-19 → 10-30 | Shopify widens Google checkout eligibility to US/CA/AU buyers, stores anywhere | SHOP-027 |

---

## 3. Architecture by surface

| Question | Gemini app | AI Mode | AI Overviews |
|---|---|---|---|
| Product data source (documented) | Shopping Graph <sup>[GEM-001]</sup>; some answers grounded on Search <sup>[GEM-006]</sup> | Shopping Graph + query fan-out <sup>[GEM-003]</sup> | Search index via core ranking systems; Shopping Graph powers generative AI shopping features <sup>[GOOG-020, GOOG-029]</sup> |
| What a shopper sees | Product cards, theme groups, comparisons, links, Buy (web, US) <sup>[GEM-001, GEM-014]</sup> | Shoppable images, comparison tables, price/reviews/inventory, sponsored and organic product list items <sup>[GEM-002, GEM-008]</sup> | Summary with cited links; ads in labeled sections <sup>[GEM-007]</sup> |
| Ranking documented | None product-specific | "Search quality and ranking systems" only <sup>[GEM-007]</sup> | Same <sup>[GEM-007]</sup> |
| Ads | Chats not used for ads; no ad format found <sup>[GEM-010]</sup> | Sponsored items, Direct Offers, Highlighted Answers <sup>[GEM-008, GEM-009]</sup> | Sponsored sections <sup>[GEM-007]</sup> |
| Personalization | Personal Intelligence: Search, Shopping, Gmail, Photos, Wallet (US) <sup>[GEM-011]</sup> | Search Services History; Gmail/Photos opt-in <sup>[GEM-011]</sup> | Not documented for products |
| India | Shopping live, EN/HI <sup>[GEM-001, GEM-002]</sup> | Shopping live, EN; ads since 2026-10-28 <sup>[GEM-002, GEM-008]</sup> | Live in Indian languages <sup>[GEM-017]</sup> |

### 3.1 Product data paths into Google

| # | Path | Who | How | Evidence |
|---|---|---|---|---|
| G1 | Merchant Center feed → free listings → Shopping Graph | Any merchant with an approved account | Direct upload, Content/Merchant API, or platform app (Shopify's Google & YouTube app) | GOOG-009, GOOG-010, SHOP-029 |
| G2 | Web crawl → Shopping Graph | Any crawlable store | Googlebot / Storebot-Google; no feed needed | GOOG-010, GOOG-020, GOOG-031 |
| G3 | Manufacturer Center | Brands | Brand data feed | GOOG-020 |
| G4 | Search index (web pages) → AIO/AI Mode citations | Any indexed, snippet-eligible page | Googlebot + Search Console AI control "include" | GOOG-011, GOOG-026, GOOG-028 |
| G5 | Model knowledge | Known brands | Not controllable | RES-032 |
| G6 | UCP | Checkout, cart, identity — not documented as a discovery input on Google | Google approval; platform integrations | GOOG-004, UCP-004 |

Google calls Merchant Center "central to our ecosystem" <sup>[GOOG-004]</sup>. Its AI optimization guide names Merchant Center feeds, not structured data, as the way products become visible in AI responses <sup>[GOOG-029]</sup>.

---

## 4. Retrieval

Documented:
- AI Mode runs a query fan-out: it splits a question into subtopics and searches each "across multiple data sources" <sup>[GEM-003]</sup>.
- AIO and AI Mode ground on the Search index through "core Search ranking systems" <sup>[GOOG-029]</sup>.
- The Gemini app grounds "some" responses on Search and uses the Shopping Graph for shopping <sup>[GEM-001, GEM-006]</sup>.

Not documented: how Shopping Graph listings and web results are combined; whether feed or crawl data wins when they disagree; how attribute constraints are parsed.

Independent evidence:
- AIO, the Gemini API and organic Google share few sources: URL Jaccard 0.11–0.18, lowest for product queries <sup>[RES-039]</sup>.
- Grounded Gemini (API) cites pages mostly outside Google's top 10 for its own sub-queries <sup>[RES-031]</sup>.
- The Gemini **app** and Gemini **API** share only 14.8% of source domains for the same product question <sup>[RES-034]</sup>. API studies do not describe the app.
- AIO triggers on only 14–17% of short product-keyword searches when logged out in the US <sup>[RES-038]</sup>; logged in from Italy it triggered on 97% of queries <sup>[RES-043]</sup>.
- A vendor study finds only 1.28% of Shopping-carousel products also appear in AI Mode for the same query <sup>[RES-046]</sup>. Google says both use the same data source. Tier 3.

---

## 5. Ranking and recommendation

### 5.1 What Google documents

| Statement | Scope | Evidence |
|---|---|---|
| Organic AI answers come from "Search quality and ranking systems"; ads don't influence them | AI Mode, AIO | GEM-007 |
| Shopping tab: relevance to search terms + personalization from recent activity | Shopping tab | GOOG-022 |
| "Top recommendations": relevance, ratings, price, product features | Google Shopping | GOOG-022 |
| Shopping recommendations: popularity/trending; personal history | Search shopping recs | GOOG-022 |
| Store Quality (shipping, returns) "may boost" visibility | Shopping tab only | GOOG-021 |
| Store ratings "can help" free-listing performance | Free listings | GOOG-023 |
| UCP native checkout "does not influence how we rank your offers" | Product listings | GOOG-003 |
| Saved favorite brands "show up more often" (US, CA, AU, IN) | Search, Shopping | GEM-012 |

Google publishes **no** marketplace-versus-brand rule <sup>[GOOG-035]</sup>. OpenAI does ("maker or primary seller", CGPT-015).

### 5.2 Feed attributes and ranking

- Google says feed data is used "to match your products to the right queries" and missing data can limit eligibility <sup>[GOOG-009]</sup>.
- Six optional conversational attributes target AI Mode, including Q&A and a merchant-declared `popularity_rank` <sup>[GOOG-012, GOOG-013, GOOG-014]</sup>.
- In one lululemon test, these attributes were used in 50% of relevant AI Mode recommendations <sup>[GEM-013]</sup>. That is use in answer text. No source says the fields change which products are selected or their order.
- Classification: "feed completeness improves AI Mode ranking" is an UNVERIFIED HYPOTHESIS. "Feed data reaches AI Mode answers" is VERIFIED <sup>[GEM-013]</sup>.

### 5.3 Independent research

All Tier 2 results come from Gemini **API** models, mock stores or Swiss/Dutch consumer UIs. None measures AI Mode product cards under controlled conditions.
- **Version shocks:** a Gemini preview-to-GA update inverted position bias and moved product shares ~25 points <sup>[RES-026]</sup>.
- **Labels:** Gemini agents penalize "Sponsored" tags and strongly reward platform badges <sup>[RES-027]</sup>. AI Mode now mixes sponsored and organic items <sup>[GEM-008]</sup>.
- **Price and ratings:** Gemini agents pick dominant cheaper or better-rated options <sup>[RES-028]</sup>; Gemini 3 Flash switches brands on a tiny rating edge <sup>[RES-037]</sup>.
- **Brand priors:** for known brands, Gemini's model sets most of the order before retrieval <sup>[RES-032]</sup>. LLMs favor global over local brands <sup>[RES-018]</sup>.
- **Markup:** schema.org and FAQ blocks show no citation effect for grounded Gemini <sup>[RES-033]</sup>; a vendor quasi-experiment found no AI Mode gain from adding JSON-LD <sup>[RES-044]</sup>.
- **Volatility:** AI Mode sources change across same-day runs <sup>[RES-035, RES-045]</sup>; device changes AIO sources more than city <sup>[RES-040]</sup>.

---

## 6. Prices, availability, freshness

- Google claimed 2 billion listings refreshed hourly (to April 2026); later posts say only "continually refreshed" <sup>[GOOG-019]</sup>.
- The Shopify Google & YouTube app re-syncs on change and within Google's 30-day expiry <sup>[SHOP-029]</sup>.
- Google warns that JavaScript-generated Product markup makes Shopping crawls "less frequent and less reliable" for price and availability <sup>[GOOG-031]</sup>.
- A vendor reports AI Mode's lead offer is often not the lowest price <sup>[RES-046]</sup>. Tier 3.

---

## 7. Integrations and protocols

### 7.1 Merchant Center
- Free listings are on by default and can appear on Gemini <sup>[GOOG-010]</sup>.
- Merchant Center is mandatory for the Shopping tab, optional for Search <sup>[GOOG-011]</sup>.
- AI performance report (share of voice on AI Mode and AIO) covers India for English queries <sup>[GOOG-017]</sup>.
- No AI-surface-specific opt-out exists for listings or ads <sup>[GOOG-018]</sup>.

### 7.2 UCP and AP2
- UCP: Google- and Shopify-led open spec; Google holds proxy votes for open council seats until Dec 2028 <sup>[UCP-002, UCP-003]</sup>.
- On Google, UCP powers checkout and cart transfer, gated by approval and a per-item `native_commerce` flag (default off) <sup>[GOOG-001, GOOG-005]</sup>.
- Discovery on Google is "powered by our Shopping Graph", not by merchant UCP catalog endpoints <sup>[GOOG-004, UCP-004]</sup>.
- AP2 is the payment layer for autonomous purchases; not confirmed in production <sup>[UCP-005]</sup>.

### 7.3 Business Agent
- A brand chat agent on Search for US stores with 50+ approved free listings. It answers brand queries; it is not a discovery surface for non-brand queries <sup>[GOOG-008]</sup>.

---

## 8. Crawlers and controls

| Control | What it governs | Evidence |
|---|---|---|
| Googlebot (robots.txt) | Search, including AIO and AI Mode citations | GOOG-026 |
| Search Console "Search generative AI control" | Inclusion in AIO, AI Mode, Discover AI features; default include | GOOG-028 |
| Google-Extended (robots.txt token) | Gemini app and Vertex AI grounding and training; not Search | GOOG-027 |
| Storebot-Google | All Google Shopping surfaces | GOOG-031 |
| Google-Agent | User-triggered agent fetches; "generally ignore robots.txt" | GOOG-032 |
| nosnippet / max-snippet | Use of page text as direct input to AIO/AI Mode | GOOG-030 |

Notes:
- Storebot-Google falls back to `*`, not to a Googlebot group, so custom robots.txt files can split Search and Shopping access <sup>[GOOG-034]</sup>.
- Sites that block Google-Extended were never cited by grounded Gemini in one study <sup>[RES-039]</sup>.

---

## 9. Structured data

- Google: structured data "isn't required" for generative AI search, and Google Search does not use llms.txt <sup>[GOOG-029]</sup>.
- Merchant listing markup needs the page to be the point of sale. Google recommends markup plus a Merchant Center feed for eligibility and verification <sup>[GOOG-033]</sup>.
- The only sentence linking markup to AI inputs: in-page structured data is exempt from `max-snippet` limits <sup>[GOOG-030]</sup>.
- Shopify themes output Product/ProductGroup JSON-LD without ratings, shipping or returns <sup>[SHOP-022]</sup>.
- Classification: "structured data improves Gemini/AI Mode ranking" is UNVERIFIED and contradicted by RES-033 and RES-044. Markup still matters for Shopping crawl reliability <sup>[GOOG-031]</sup>.

---

## 10. How each source type reaches Google's AI surfaces

| Source | Googlebot / Storebot | Google-Extended | Merchant Center / Graph | UCP / checkout | Evidence |
|---|---|---|---|---|---|
| Amazon (.com, .in) | Allowed (`*`) | Blocked | Not stated | None; Tech Council seat | MKT-022, MKT-023 |
| Flipkart | Storebot explicitly allowed to `/viewcart` | Allowed | Not stated | Named UCP partner; Buy test (Tier 3) | MKT-025, GEM-016 |
| Shopify store selling to US/CA/AU | Allowed by default | Allowed by default | Via Google & YouTube app | Direct checkout default-on | SHOP-025, SHOP-026, SHOP-027 |
| Shopify store selling only in India | Allowed by default | Allowed | Via app; India is a supported country | Not eligible | SHOP-032, SHOP-027 |
| Other independent stores | Per their robots.txt | Per their robots.txt | Platform app or feed | Opt-in per platform | MKT-028 |
| Walmart, Etsy, Target | Allowed | Allowed | Not stated | UCP co-developers; live in US | MKT-024 |
| eBay, Mercado Libre, Meesho, JioMart, Myntra | Allowed | Allowed | Not stated | None found | MKT-026, MKT-029 |

### The brief's use case: "premium ceramic coffee mug under ₹1,000", asked from India

- Google documents Gemini-app and AI Mode shopping for Indian users <sup>[GEM-002]</sup>. The product data comes from the Shopping Graph <sup>[GEM-001]</sup>.
- An Indian Shopify store can enter that graph through the Google & YouTube app, with India as a sync and free-listings country <sup>[SHOP-032]</sup>.
- Amazon.in is not blocked for Google Search or Shopping crawling; it is blocked for Gemini grounding <sup>[MKT-022]</sup>. Whether Amazon.in products appear in Gemini or AI Mode product cards is untested. TechCrunch saw Amazon listings without a Buy button (Tier 3) <sup>[GEM-016]</sup>.
- Indian users may see sponsored product items in AI Mode <sup>[GEM-008]</sup>.
- EVIDENCE-BASED INFERENCE: for this query, Google can show product cards built from Merchant Center and crawl data. ChatGPT documents no such surface for India (CGPT-046).
- Test case: `experiments/test-cases/gemini-coffee-mug.md`.

---

## 11. Knowledge gaps

1. Product-level ranking factors for AI Mode, AIO and the Gemini app.
2. Whether the Gemini app and AI Mode share a product retrieval or ranking pipeline.
3. Feed-versus-crawl precedence inside the Shopping Graph.
4. Whether crawl-only products (no Merchant Center) appear as AI Mode or Gemini product cards.
5. Whether conversational attributes, `popularity_rank`, store ratings or Store Quality affect AI-surface ranking.
6. How AI Mode chooses between a marketplace offer and a brand offer for one product.
7. Whether the Search Console AI control removes Merchant Center listings from AI Mode.
8. Whether Amazon products appear in AI Mode or Gemini product cards despite the Google-Extended block.
9. How personal context (Search history, Gmail) changes product selection.
10. Whether Hindi AI Mode shopping has launched; whether India gets UCP checkout beyond the Flipkart test.
11. Which model versions run AI Mode, AIO and Gemini shopping at any given time.
12. Whether sponsored item placement in AI Mode lists affects organic selection.

---

## 12. Contradictions and outdated sources

| Topic | Conflict | Resolution |
|---|---|---|
| Google-Extended scope | Crawler doc: no effect on Search. Search Console help: use it to limit training of Search generative AI models | Unresolved wording conflict <sup>[GOOG-027]</sup> |
| AI features controls | "AI features" page (2025-12-10) lists no extra requirements; Search Console AI control (2026-08-31) adds one | Newer control wins <sup>[GOOG-028]</sup> |
| Google checkout countries | Shopify: US/CA/AU buyers. Google Search Help: US only. Merchant Center hub: CA/AU "next year" | Unresolved; record buyer country in tests <sup>[SHOP-027, GEM-014]</sup> |
| UCP Buy in Gemini mobile app | FAQ: web and mobile. Landing page: "app coming soon" | FAQ is newer <sup>[GOOG-004]</sup> |
| Shopify discovery for Google | Jan 2026 Shopify post: Catalog reaches Google. Oct 2026 help: Merchant Center powers discovery | Oct 2026 wins <sup>[SHOP-025]</sup> |
| AIO overlap with organic | 0.18 URL Jaccard vs 48% top-10 domain share vs 68% top-100 aggregate | Different units; all agree much AIO sourcing is outside the top 10 <sup>[RES-039, RES-041]</sup> |
| Gemini repeatability | Gemini most repeatable (Swiss UI) vs less than AIO (Dutch UI) | Locale and prompt type differ <sup>[RES-034, RES-035]</sup> |
| Shopping Graph size | 50B (2025) → 60B+ (May 2026) | 60B+ is current <sup>[GOOG-019]</sup> |

---

## 13. Shopify implications

Full action list: `shopify/gemini.md`. Summary:
- **Mandatory for Google AI discovery:** a Merchant Center feed with approved free listings (for Shopify, the Google & YouTube app) <sup>[SHOP-025, GOOG-010]</sup>; Googlebot allowed and the Search Console AI control on "include" <sup>[GOOG-026, GOOG-028]</sup>.
- **Mandatory for Google checkout:** US/CA/AU buyers, Catalog eligibility, three policies, Merchant Center return policy <sup>[SHOP-027, SHOP-031]</sup>.
- **Recommended:** complete feed fields (GTIN, category, variants in English, General shipping profile), store ratings and Store Quality data, conversational attributes, video, 500×500 images before 2027-01-31 <sup>[SHOP-030, GOOG-012, GOOG-016, GOOG-021, GOOG-023]</sup>.
- **Unverified for Google AI ranking:** JSON-LD enrichment, llms.txt, UCP checkout as a ranking lever.

---

## 14. Method and limits

- Five research agents gathered sources on 2026-10-30 (three resumed on 2026-10-31 after a usage limit). Raw captures are in `notes/`.
- Google pages were fetchable by curl and WebFetch. Help-center dates render by JavaScript and were not captured.
- The lead researcher re-checked these on the live pages: Gemini shopping countries, Google India shopping post, ads-in-AI-Mode post, UCP FAQ ranking statement, Search Console AI control, Google-Extended crawler doc, Shopify's Google channel page, and the Gemini app-vs-API paper. Registry `Checked` fields record which entries.
- No queries were run on any Google surface. Statements about what Google displays come from documentation or third-party studies.
