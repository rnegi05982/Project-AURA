# Registry — RES (independent research)

Schema: `evidence/README.md`. All entries accessed 2026-10-30. arXiv excerpts were string-matched against arXiv HTML by agent E. Lead re-checked RES-012 to RES-015 on arXiv.

Rule for this file: a result on an API model or a mock store is a VERIFIED FACT about that system only. What it implies for production ChatGPT is at most an EVIDENCE-BASED INFERENCE.

---

## Agent choice experiments (mock stores, API models)

### RES-001 — Position bias in LLM shopping agents is large and flips between model versions
- **Claim:** In the ACES mock store, every agent showed strong position effects. GPT-4.1 and GPT-5.1 preferred opposite grid slots.
- **Classification:** VERIFIED FACT (API models tested) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** LLM agents / ranking
- **Source:** "What Is Your AI Agent Buying? Evaluation, Biases, Model Dependence, & Emerging Implications for Agentic E-Commerce" — Allouah, Besbes, Figueroa, Kanoria, Kumar — https://arxiv.org/abs/2508.02630
- **Published:** v1 2025-08-04; v3 2025-12-17 (arXiv preprint) · **Accessed:** 2026-10-30
- **Method:** 8-product grid; positions, tags, prices, ratings randomized; ~500 scenarios × 8 categories per model; conditional logit.
- **Excerpt:** > "the preferred position by one is the least preferred by the other and vice versa"
- **Establishes:** Position effects are causal and model-specific.
- **Limitations:** API models, single-page choice, no conversation. Not ChatGPT's shopping UI.
- **Related:** RES-004, RES-015
- **Origin:** notes/e-…#E-01 · **Checked:** pending

### RES-002 — A "Sponsored" tag lowers agent selection; an endorsement badge raises it
- **Claim:** With position fixed, "Sponsored" lowered a 10% baseline to 7.9–8.9%. "Overall Pick" raised it to 19.9–42.6%.
- **Classification:** VERIFIED FACT (API models) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** LLM agents / ads
- **Source:** Allouah et al. (as RES-001) — https://arxiv.org/html/2508.02630v3
- **Published:** 2025-12-17 · **Accessed:** 2026-10-30
- **Excerpt:** > "Sponsored tags are penalized while Platform Endorsement is substantially rewarded."
- **Establishes:** Labels in an agent's context change choices.
- **Limitations:** ACES-specific badges.
- **Related:** RES-023
- **Origin:** notes/e-…#E-02 · **Checked:** pending

### RES-003 — Agents prefer cheaper, higher-rated, more-reviewed items; magnitudes differ by model
- **Claim:** Implied price elasticities were −1.6 to −2.2. Late-2025 models almost never missed a dominant cheaper or better-rated option.
- **Classification:** VERIFIED FACT (API models) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** LLM agents / ranking signals
- **Source:** Allouah et al. (as RES-001) — https://arxiv.org/html/2508.02630v3
- **Published:** 2025-12-17 · **Accessed:** 2026-10-30
- **Excerpt:** > "our elasticity estimates (-1.6 to -2.2) are broadly in the same range"
- **Establishes:** Price, rating and review count move agent choices in the expected direction.
- **Limitations:** Small perturbations; generic persona.
- **Related:** CGPT-011, RES-006
- **Origin:** notes/e-…#E-03 · **Checked:** pending

### RES-004 — Model upgrades reshuffle which products agents choose by tens of points
- **Claim:** Fitbit Inspire's share fell from ~25% (GPT-4.1) to 6% (GPT-5.1). One phone-case brand went from 62.6% to 5%.
- **Classification:** VERIFIED FACT (API models) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** LLM agents / volatility
- **Source:** Allouah et al. (as RES-001) — https://arxiv.org/html/2508.02630v3
- **Published:** 2025-12-17 · **Accessed:** 2026-10-30
- **Excerpt:** > "while it fell (from 25%) to only 6% with GPT-5.1"
- **Establishes:** Visibility baselines must record model version and date.
- **Limitations:** Selection rate under one prompt, not demand.
- **Related:** RES-001
- **Origin:** notes/e-…#E-04 · **Checked:** pending

### RES-005 — One query-matched description rewrite raised selection share in 5 of 6 models
- **Claim:** Gains ranged from +3.66 to +14.89 percentage points; one model showed no significant change. Gains came mainly from front-loading query terms.
- **Classification:** VERIFIED FACT (API models) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** LLM agents / product text
- **Source:** Allouah et al. (as RES-001) — https://arxiv.org/html/2508.02630v3
- **Published:** 2025-12-17 · **Accessed:** 2026-10-30
- **Excerpt:** > "+14.89 (1.05) p.p. for GPT-5.1"
- **Establishes:** Text an agent reads at decision time can change its pick.
- **Limitations:** Whether ChatGPT shopping reads merchant descriptions at that step is unknown (CGPT-013 says titles may be rewritten).
- **Related:** RES-010
- **Origin:** notes/e-…#E-05 · **Checked:** pending

### RES-006 — Agents react to ratings, price, order and nudges far more than humans
- **Claim:** Across 17 models, higher ratings raised selection 30–80 pp in 14 models. Humans showed 4–10 pp effects.
- **Classification:** VERIFIED FACT (models tested, incl. GPT-4.1, GPT-5, o3) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** LLM agents / ranking signals
- **Source:** "A Framework for Studying AI Agent Behavior: Evidence from Consumer Choice Experiments" (ABxLab) — Cherep et al. — https://arxiv.org/abs/2509.25609
- **Published:** v2 2026-02-24 (ICLR) · **Accessed:** 2026-10-30
- **Excerpt:** > "Higher product ratings consistently increased selection probability by 30-80pp across 14 of 17 models"
- **Establishes:** Ratings are a strong lever for LLM agents generally.
- **Limitations:** Pairwise synthetic shop.
- **Related:** RES-003
- **Origin:** notes/e-…#E-06 · **Checked:** pending

### RES-007 — GPT-4 Turbo leaned on product names more than page content in RAG product ranking
- **Claim:** In RAG-style product recommendation, GPT-4 Turbo relied heavily on known product names. All tested LLMs favored documents placed earlier in context.
- **Classification:** VERIFIED FACT (2024 models) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** LLM ranking / brand priors
- **Source:** "Ranking Manipulation for Conversational Search Engines" — Pfrommer, Bai, Gautam, Sojoudi — https://arxiv.org/abs/2406.03589
- **Published:** v3 2024-09-25 (EMNLP 2024) · **Accessed:** 2026-10-30
- **Excerpt:** > "GPT-4 Turbo particularly attends to the product name"
- **Establishes:** Brand-name priors were measurable in OpenAI models.
- **Limitations:** 2024 models; retrieval bypassed.
- **Related:** RES-015, RES-017
- **Origin:** notes/e-…#E-09 · **Checked:** pending

### RES-008 — On production Bing Copilot (2024), real brands were recommended ~2× as often as a fictitious one
- **Claim:** Real camera brands beat a fictitious camera about two to one. An injected page reversed this.
- **Classification:** VERIFIED FACT (Bing Copilot, Perplexity, 2024) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** LLM search / brand priors
- **Source:** "Adversarial Search Engine Optimization for Large Language Models" — Nestaas, Debenedetti, Tramèr — https://arxiv.org/abs/2406.18382
- **Published:** v2 2024-07-02 · **Accessed:** 2026-10-30
- **Excerpt:** > "recommended nearly twice as often (presumably due to brand name recognition)"
- **Establishes:** Brand-familiarity effects exist in production LLM search systems.
- **Limitations:** Not ChatGPT; adversarial content.
- **Related:** RES-017
- **Origin:** notes/e-…#E-10 · **Checked:** pending

## Content optimization claims

### RES-009 — GEO: content edits raised visibility up to ~40% in a simulated GPT-3.5 engine
- **Claim:** Adding citations, quotations and statistics raised source visibility. Keyword stuffing did not.
- **Classification:** VERIFIED FACT (simulated engine) · **Confidence:** Low for ChatGPT · **Tier:** 2
- **Subject / topic:** Content / visibility
- **Source:** "GEO: Generative Engine Optimization" — Aggarwal et al. — https://arxiv.org/abs/2311.09735
- **Published:** v3 2024-06-28 (KDD 2024) · **Accessed:** 2026-10-30
- **Excerpt:** > "can improve the visibility of websites by up to 40%"
- **Establishes:** Content effects exist when retrieval is fixed.
- **Limitations:** 80% informational queries; 2023 model; retrieval fixed.
- **Related:** RES-010, RES-012
- **Origin:** notes/e-…#E-11 · **Checked:** pending

### RES-010 — C-SEO Bench: most conversational-SEO methods were ineffective; retrieval rank mattered more
- **Claim:** Across QA and product recommendation, most published content methods were ineffective or harmful. Improving a source's context position worked better. Gains fell as competitors adopted the same tactics.
- **Classification:** VERIFIED FACT (benchmark LLMs) · **Confidence:** Medium (abstract only) · **Tier:** 2
- **Subject / topic:** Content / visibility
- **Source:** "C-SEO Bench: Does Conversational SEO Work?" — Puerto et al. — https://arxiv.org/abs/2506.11097
- **Published:** v3 2025-10-20 (NeurIPS 2025 D&B) · **Accessed:** 2026-10-30
- **Excerpt:** > "most current C-SEO methods are not only largely ineffective"
- **Establishes:** Contradicts the size of GEO gains (RES-009).
- **Limitations:** Fixed-context setup.
- **Related:** RES-009, RES-012
- **Origin:** notes/e-…#E-12 · **Checked:** pending

## ChatGPT search behaviour (API and consumer UI)

### RES-011 — OpenAI's search API model cited mostly third-party review media for "best X" consumer queries (2025)
- **Claim:** gpt-4o-search-preview cited 93.5% earned media, 6.5% brand sites and no social sources for consumer ranking queries.
- **Classification:** VERIFIED FACT (API, 2025) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** ChatGPT search / sources
- **Source:** "Generative Engine Optimization: How to Dominate AI Search" — Chen, Wang, Chen, Koudas — https://arxiv.org/abs/2509.08919
- **Published:** 2025-09-10 · **Accessed:** 2026-10-30
- **Excerpt:** > "ChatGPT skewed even further, with 93.5% Earned, 6.5% Brand, and no Social"
- **Establishes:** For superlative product queries, review publishers dominated citations in that setup.
- **Limitations:** API, not the app. RES-024 and RES-025 found different mixes.
- **Related:** RES-024, RES-025
- **Origin:** notes/e-…#E-13 · **Checked:** pending

### RES-012 — For the OpenAI web-search API, retrieval explains far more of citation than page features
- **Claim:** Over 90 days, every page ChatGPT's API engine cited was first retrieved by its own search. Retrieval explained 32% of within-site citation variance; 14 page features explained 2.8%. FAQ blocks and schema.org markup showed slightly lower odds.
- **Classification:** VERIFIED FACT (gpt-5.4-nano + web_search, 2026, US home-internet questions) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** ChatGPT search / ranking
- **Source:** "What Drives AI Citations? Content, Retrieval and Model Knowledge in Generative Engine Optimization (GEO)" — Mahe Chen, Nick Koudas (University of Toronto) — https://arxiv.org/abs/2610.15033
- **Published:** v1 2026-10-10 · **Accessed:** 2026-10-30
- **Method:** 651 questions daily, 2026-06-24 to 2026-09-21; 143,249 answers; API replay.
- **Excerpt:** > "Every page ChatGPT cites is one its own search retrieved"
- **Establishes:** Getting retrieved matters more than on-page formatting, for this system.
- **Limitations:** Authors: the APIs "need not behave like their consumer applications". Services market, not physical goods.
- **Related:** RES-013, RES-014, RES-015
- **Origin:** notes/e-…#E-15 · **Checked:** 2026-10-30

### RES-013 — ChatGPT's API search retrieves pages that almost never appear in Google's or Bing's top 10
- **Claim:** Only 0.5% (Bing) and 0.7% (Google) of retrieved pages were in those engines' top 10 for ChatGPT's own sub-queries. 97% were absent from Google's top 50.
- **Classification:** VERIFIED FACT (API, 2026) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** ChatGPT search / index
- **Source:** Chen & Koudas (as RES-012) — https://arxiv.org/html/2610.15033v1
- **Published:** 2026-10-10 · **Accessed:** 2026-10-30
- **Excerpt:** > "97% of ChatGPT’s retrieved pages are absent from Google’s top 50 and 99% from Bing’s top 30"
- **Establishes:** Classic Google/Bing rank is a poor proxy for ChatGPT retrieval, at page level.
- **Limitations:** Does not identify the index. Site-level overlap is higher (51%).
- **Related:** CGPT-002, RES-020
- **Origin:** notes/e-…#E-16 · **Checked:** 2026-10-30

### RES-014 — ChatGPT's search queries and citations change on every run
- **Claim:** Two same-day runs shared 2.7% of search queries (Jaccard) and 15% of cited pages. ChatGPT added a brand the user did not name to 28% of queries.
- **Classification:** VERIFIED FACT (API, 2026) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** ChatGPT search / volatility
- **Source:** Chen & Koudas (as RES-012) — https://arxiv.org/html/2610.15033v1
- **Published:** 2026-10-10 · **Accessed:** 2026-10-30
- **Excerpt:** > "between two runs on the same day, ChatGPT’s queries overlap by 2.7% (Jaccard) and its cited pages by 15%"
- **Establishes:** Single-run observations are not evidence.
- **Limitations:** API; one market.
- **Related:** RES-016
- **Origin:** notes/e-…#E-17 · **Checked:** 2026-10-30

### RES-015 — The model behind ChatGPT's API engine favors first-shown sources and reorders identical products by brand name
- **Claim:** A source shown first was cited 17.6 points more often than when shown last. Revealing brand names on identical product profiles changed top-3 rates 2.1× more than repetition noise. 47% of citations came from websites the model names without searching.
- **Classification:** VERIFIED FACT (gpt-5.4-nano, constructed inputs) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** ChatGPT model / brand priors
- **Source:** Chen & Koudas (as RES-012) — https://arxiv.org/html/2610.15033v1
- **Published:** 2026-10-10 · **Accessed:** 2026-10-30
- **Excerpt:** > "controlled experiments show that brand names reorder its rankings of products with identical facts"
- **Establishes:** Model priors about brands act alongside retrieval (matches CGPT-012's "model responses … before it considers any new search results").
- **Limitations:** Small model; B2B/ISP markets.
- **Related:** CGPT-012, RES-017
- **Origin:** notes/e-…#E-18 · **Checked:** 2026-10-30

### RES-016 — In the consumer ChatGPT UI, cited sources and brands vary heavily across same-day repeats
- **Claim:** Scraping ChatGPT's web UI from Switzerland, same-day source sets overlapped at mean Jaccard 0.233 and brand sets at 0.437. 57.8% of runs had no citations. About 7–8 runs per prompt bring per-brand detection SE below 0.10.
- **Classification:** VERIFIED FACT (ChatGPT consumer UI, Swiss locale, Jan–Mar 2026) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** ChatGPT / volatility, methodology
- **Source:** "Don't Measure Once: Measuring Visibility in AI Search (GEO)" — Schulte, Bleeker, Kaufmann (University of St. Gallen) — https://arxiv.org/abs/2604.07585
- **Published:** v1 2026-04-08 · **Accessed:** 2026-10-30
- **Excerpt:** > "leaving 57.8% of its runs with zero citations"
- **Establishes:** The closest Tier 2 evidence to production ChatGPT. Sets AURA's repetition floor.
- **Limitations:** German prompts; 32 prompts; model not pinned.
- **Related:** RES-014
- **Origin:** notes/e-…#E-20 · **Checked:** pending

### RES-017 — With identical specs, a known brand wins; a tiny rating edge removes the advantage
- **Claim:** A real skincare brand won 100% of 670 trials against fictional brands with identical specs. A competitor rating edge under +0.1 star broke this. Product parameters explained 82.4% of variance, position 6.5%, brand 1.2%.
- **Classification:** VERIFIED FACT (API models incl. GPT-4o-mini; direct prompts) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** LLM ranking / brand priors
- **Source:** "Incumbent Advantage: Brand Bias and Cognitive Manipulation Dynamics in LLM Recommendation Systems" — Xi Chu, Yupeng Hou — https://arxiv.org/abs/2606.17443
- **Published:** v3 2026-10-10 · **Accessed:** 2026-10-30
- **Excerpt:** > "Brand identity explains only 1.2%."
- **Establishes:** Brand acts as a tie-breaker; visible attributes dominate when they differ.
- **Limitations:** No web search in main experiments.
- **Related:** RES-015
- **Origin:** notes/e-…#E-23 · **Checked:** pending

### RES-018 — LLMs associate global brands with positive attributes more than local brands
- **Claim:** LLMs linked global brands to positive attributes disproportionately.
- **Classification:** VERIFIED FACT (models tested) · **Confidence:** Low (abstract only; 2024 models) · **Tier:** 2
- **Subject / topic:** LLM / brand priors
- **Source:** ""Global is Good, Local is Bad?": Understanding Brand Bias in LLMs" — Kamruzzaman, Nguyen, Kim — https://arxiv.org/abs/2406.13997
- **Published:** v2 2024-09-27 (EMNLP 2024) · **Accessed:** 2026-10-30
- **Excerpt:** > "disproportionately associating global brands with positive attributes"
- **Establishes:** A prior that may disadvantage small or local brands, such as Indian D2C stores.
- **Limitations:** No web search.
- **Related:** RES-015, RES-017
- **Origin:** notes/e-…#E-24 · **Checked:** pending

## Reporting and vendor studies (Tier 3)

### RES-019 — Press report: OpenAI partially used Google results scraped by SerpApi (Aug 2025)
- **Claim:** The Information reported that OpenAI partially used Google search results obtained via SerpApi.
- **Classification:** UNVERIFIED HYPOTHESIS for current production · **Confidence:** Low · **Tier:** 3
- **Subject / topic:** ChatGPT search / index
- **Source:** "Report: ChatGPT Using SerpApi To Scrape Google Search Results" — Search Engine Roundtable — https://www.seroundtable.com/chatgpt-serpapi-scrape-google-39989.html
- **Published:** 2025-08-25 · **Accessed:** 2026-10-30
- **Excerpt:** > "OpenAI has been partially using Google search results scraped by a startup called SerpApi"
- **Establishes:** Credible reporting of a Google-sourced component exists.
- **Limitations:** Secondhand summary of a paywalled report; no OpenAI confirmation.
- **Related:** CGPT-002, RES-021
- **Origin:** notes/e-…#E-26 · **Checked:** pending

### RES-020 — Industry overlap studies disagree on ChatGPT vs Bing/Google
- **Claim:** Seer Interactive (2025-02) found 87%+ of ChatGPT citations matched Bing's top results. Ahrefs (2025-08) found ~8% top-10 overlap with both Google and Bing.
- **Classification:** VERIFIED FACT (each vendor's result); they contradict · **Confidence:** Low · **Tier:** 3
- **Subject / topic:** ChatGPT search / index
- **Source:** https://www.seerinteractive.com/insights/87-percent-of-searchgpt-citations-match-bings-top-results ; https://ahrefs.com/blog/ai-search-overlap/
- **Published:** 2025-02-06; 2025-08-11 · **Accessed:** 2026-10-30
- **Excerpt:** > "we aren’t seeing much differentiation in how ChatGPT surfaces both Google and Bing results" (Ahrefs)
- **Establishes:** Index identity cannot be settled by overlap studies. Tier 2 (RES-013) sides with low overlap.
- **Limitations:** Different eras and methods.
- **Related:** RES-013
- **Origin:** notes/e-…#E-27 · **Checked:** pending

### RES-021 — Vendor study: 83% of ChatGPT carousel products strongly match Google Shopping's top 40
- **Claim:** Peec AI reports 83% of 43,000+ carousel products matched Google Shopping organic top-40 results, vs 11% for Bing.
- **Classification:** VERIFIED FACT (as the vendor reports). That ChatGPT sources carousel candidates from Google Shopping is an UNVERIFIED HYPOTHESIS. · **Confidence:** Low · **Tier:** 3
- **Subject / topic:** ChatGPT shopping / data sources
- **Source:** "How ecommerce managers can optimize ChatGPT product rankings step by step" — Peec AI — https://peec.ai/blog/how-ecommerce-managers-can-optimize-chatgpt-product-rankings-step-by-step
- **Published:** 2026-03-17 (byline) · **Accessed:** 2026-10-30
- **Excerpt:** > "83% were strong matches to products in Google's top 40 organic shopping results."
- **Establishes:** A testable hypothesis: Google Merchant Center presence may matter for ChatGPT carousels.
- **Limitations:** Vendor with commercial interest; method not public. OpenAI names Microsoft and Shopify, not Google (CGPT-002).
- **Related:** CGPT-002, CGPT-012, RES-019
- **Origin:** notes/e-…#E-28 · **Checked:** pending

### RES-022 — Vendor study: carousel order behaves like a shuffle; Walmart and Target lead buy links; Amazon nearly absent
- **Claim:** Profound reports ~95% of product titles appeared in under 30% of runs for the same prompt. Walmart held 8.78% of rank-1 offers. Amazon was poorly represented.
- **Classification:** VERIFIED FACT (as the vendor reports) · **Confidence:** Low · **Tier:** 3
- **Subject / topic:** ChatGPT shopping / volatility, marketplaces
- **Source:** "Which retailers does ChatGPT actually send shoppers to?" — Profound — https://www.tryprofound.com/blog/chatgpt-retail-target-walmart
- **Published:** 2026-03-26 · **Accessed:** 2026-10-30
- **Excerpt:** > "~95% of product titles appeared in fewer than 30% of runs for the same prompt."
- **Establishes:** Consistent with Amazon's crawler blocks (MKT-001). Inclusion frequency is the stable metric, not position.
- **Limitations:** Undisclosed sampling; vendor data.
- **Related:** MKT-001, RES-016
- **Origin:** notes/e-…#E-29 · **Checked:** pending

### RES-023 — LLM persuasion raised sponsored-product choice by humans; labels did not stop it
- **Claim:** Promoting chat agents raised sponsored-product selection from 22.4% (search) to 61.2%. "Sponsored" labels did not significantly reduce this.
- **Classification:** VERIFIED FACT (systems tested) · **Confidence:** Medium (abstract only) · **Tier:** 2
- **Subject / topic:** Ads / persuasion
- **Source:** "Commercial Persuasion in AI-Mediated Conversations" — Salvi, Cuevas, Ribeiro — https://arxiv.org/abs/2604.04263
- **Published:** 2026-04-05 · **Accessed:** 2026-10-30
- **Excerpt:** > "Explicit \"Sponsored\" labels do not significantly reduce persuasion"
- **Establishes:** Why separating ads from answers matters (CGPT-042).
- **Limitations:** eBooks; not ChatGPT's ads.
- **Related:** RES-002, CGPT-042
- **Origin:** notes/e-…#E-30 · **Checked:** pending

### RES-024 — In a services market, ChatGPT's API engine cited providers' own sites most (64%)
- **Claim:** For US home-internet questions, 64.3% of ChatGPT citations went to provider websites.
- **Classification:** VERIFIED FACT (API, 2026) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** ChatGPT search / sources
- **Source:** Chen & Koudas (as RES-012) — https://arxiv.org/html/2610.15033v1
- **Published:** 2026-10-10 · **Accessed:** 2026-10-30
- **Excerpt:** > "64% of its citations go to the providers’ own websites"
- **Establishes:** Source mix depends on market and query type; contradicts RES-011's pattern.
- **Limitations:** Services, not physical retail.
- **Related:** RES-011
- **Origin:** notes/e-…#E-19 · **Checked:** pending

### RES-025 — GPT-4o web answers overlapped Google's top 10 at 4%; popular-entity rankings resisted evidence shuffling
- **Claim:** Over 1,000 consumer ranking queries, web-enabled GPT-4o had 4.0% domain overlap with Google's top 10. Shuffling snippets changed popular-entity ranks only mildly (2.30 vs 4.15 for niche entities).
- **Classification:** VERIFIED FACT (GPT-4o API) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** ChatGPT search / brand priors
- **Source:** "Navigating the Shift: A Comparative Analysis of Web Search and Generative AI Response Generation" — Chen, Wang, Chen, Koudas — https://arxiv.org/abs/2601.16858
- **Published:** v2 2026-05-16 (EDBT/ICDT 2026 Workshops) · **Accessed:** 2026-10-30
- **Excerpt:** > "GPT-4o shows the lowest mean overlap at 4.0% (std = 6.6%)"
- **Establishes:** Niche entities are more sensitive to retrieved evidence than popular ones.
- **Limitations:** GPT-4o retired from ChatGPT (2026-02-13).
- **Related:** RES-013, RES-015
- **Origin:** notes/e-…#E-22 · **Checked:** pending

## Gemini, AI Mode and AI Overviews

Origin file for this section: `research/ai-platforms/gemini/notes/ge-independent-research.md` (GE-xx). Rule: a Gemini API result is not evidence about the Gemini app, AI Mode or AI Overviews (RES-034).

### RES-026 — Gemini agents show position effects that change shape across versions; a preview-to-GA update inverted them
- **Claim:** In ACES, Gemini 2.5 Flash preferred the top row and columns 3–4; Gemini 3 Pro Preview had the strongest top-row preference of the Dec-2025 models (coefficient 2.146). Replacing Gemini 2.5 Flash Preview with GA flipped its row bias and moved some products' shares by about 25 points.
- **Classification:** VERIFIED FACT (Gemini API agents) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** Gemini models / ranking, volatility
- **Source:** "What Is Your AI Agent Buying?…" — Allouah et al. — https://arxiv.org/html/2508.02630v3
- **Published:** v3 2025-12-17 · **Accessed:** 2026-10-30
- **Excerpt:** > "inverted the model’s position bias from the bottom row to the top row"
- **Establishes:** A silent model update can move product visibility with no merchant change.
- **Limitations:** Mock store, API models.
- **Related:** RES-001, RES-004, GEM-005
- **Origin:** notes/ge-…#GE-01, #GE-02, #GE-03 · **Checked:** pending

### RES-027 — Gemini agents penalize "Sponsored" tags and strongly reward platform badges
- **Claim:** "Sponsored" cut a 10% baseline to 7.9% for Gemini 2.5 Flash; "Overall Pick" raised it to 42.6%. Gemini 3 Pro Preview had the largest sponsored penalty of the Dec-2025 models.
- **Classification:** VERIFIED FACT (API agents) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** Gemini models / ads
- **Source:** Allouah et al. (as RES-026) — https://arxiv.org/html/2508.02630v3
- **Published:** 2025-12-17 · **Accessed:** 2026-10-30
- **Excerpt:** > "falls to 8.9% under Claude Sonnet 4, 8.0% under GPT-4.1, and 7.9% under Gemini 2.5 Flash"
- **Establishes:** Labels in a Gemini model's context change its picks. Relevant to AI Mode's mixed sponsored/organic lists (GEM-008, GEM-009).
- **Limitations:** Whether AI Mode passes labels into the model is unknown.
- **Related:** RES-002, GEM-009
- **Origin:** notes/ge-…#GE-04 · **Checked:** pending

### RES-028 — Gemini agents are price- and rating-rational; Gemini 3 Pro weights ratings least
- **Claim:** Gemini 2.5 Flash and 3 Pro Preview almost never missed a dominant cheaper or better-rated option. Gemini 3 Pro Preview's rating coefficient (4.224) was under half of GPT-5.1's (9.247).
- **Classification:** VERIFIED FACT (API agents) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** Gemini models / ranking signals
- **Source:** Allouah et al. (as RES-026) — https://arxiv.org/html/2508.02630v3
- **Published:** 2025-12-17 · **Accessed:** 2026-10-30
- **Excerpt:** > "An increment of +0.1 in ratings, allows a seller to increase their price by a quarter with Gemini 2.5 Flash"
- **Establishes:** Price and rating move Gemini picks in the expected direction; weights differ by version.
- **Limitations:** API agents only.
- **Related:** RES-003, RES-037
- **Origin:** notes/ge-…#GE-05 · **Checked:** pending

### RES-029 — One listing rewrite moved Gemini 2.5 Flash +14.79 points and Gemini 3 Pro Preview not at all
- **Claim:** An AI-rewritten description raised share by +14.79 p.p. for Gemini 2.5 Flash and +0.32 (not significant) for Gemini 3 Pro Preview.
- **Classification:** VERIFIED FACT (API agents) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** Gemini models / product text
- **Source:** Allouah et al. (as RES-026) — https://arxiv.org/html/2508.02630v3
- **Published:** 2025-12-17 · **Accessed:** 2026-10-30
- **Excerpt:** > "for Gemini 2.5 Flash, +6.5 p.p. in mousepad, and +52.0 p.p. in office lamp, +29.1 p.p. in toothpaste and +12.0 p.p. in washing machine"
- **Establishes:** Text-optimization gains on Gemini models are version-specific.
- **Limitations:** Mock UI truncation may inflate effects.
- **Related:** RES-005
- **Origin:** notes/ge-…#GE-06 · **Checked:** pending

### RES-030 — Grounded Gemini (API) cites ~10 pages per answer, 83% third-party, Reddit 13% (services market)
- **Claim:** For US home-internet questions, Gemini 3.1 Flash Lite with Google grounding cited 10.1 pages per answer; 83% were third-party sites.
- **Classification:** VERIFIED FACT (API, Jun–Sep 2026) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** Gemini API / sources
- **Source:** "What Drives AI Citations?…" — Chen & Koudas — https://arxiv.org/html/2610.15033v1
- **Published:** 2026-10-10 · **Accessed:** 2026-10-30
- **Excerpt:** > "Gemini cites 10.1 pages, 83% of them on third-party websites (Reddit alone 13%)"
- **Establishes:** Grounded Gemini cites broadly; ChatGPT's API cited 2.0 pages (RES-024).
- **Limitations:** API; services, not retail.
- **Related:** RES-024, RES-031
- **Origin:** notes/ge-…#GE-08 · **Checked:** pending

### RES-031 — Pages cited by grounded Gemini rarely appear in Google's own top 10 (5.6%)
- **Claim:** Only 5.6% of pages cited by grounded Gemini were in Google's top 10 for Gemini's own sub-queries; 93% were absent from the top 50.
- **Classification:** VERIFIED FACT (API) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** Gemini API / retrieval
- **Source:** Chen & Koudas (as RES-030) — https://arxiv.org/html/2610.15033v1
- **Published:** 2026-10-10 · **Accessed:** 2026-10-30
- **Excerpt:** > "5.6% of those Gemini cites are in the top 10, although Gemini is grounded on Google"
- **Establishes:** Google organic rank is a poor proxy for grounded Gemini citation.
- **Limitations:** API; page-level.
- **Related:** RES-013, RES-039
- **Origin:** notes/ge-…#GE-09 · **Checked:** pending

### RES-032 — Gemini's model shows no source-order effect, but brand names reorder its product rankings 3.3× repetition noise
- **Claim:** Gemini cited a source at 57–59% in every position. Revealing brand names on identical profiles changed top-3 rates 3.3× repetition noise (ChatGPT 2.1×). For large brands, one score per brand predicted 92% of Gemini's pairwise orders from memory alone.
- **Classification:** VERIFIED FACT (gemini-3.1-flash-lite, constructed inputs) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** Gemini models / brand priors
- **Source:** Chen & Koudas (as RES-030) — https://arxiv.org/html/2610.15033v1
- **Published:** 2026-10-10 · **Accessed:** 2026-10-30
- **Excerpt:** > "one score per brand predicts 75% of the pairs for ChatGPT and 92% for Gemini"
- **Establishes:** For known brands, Gemini-family rankings are largely set before retrieval. Unknown brands depend more on evidence.
- **Limitations:** Small model; non-retail markets.
- **Related:** RES-015, RES-017
- **Origin:** notes/ge-…#GE-10, #GE-11 · **Checked:** pending

### RES-033 — For grounded Gemini, title match and inbound links associate with citations; schema.org and FAQ blocks show no effect; JS-only text gets fewer
- **Claim:** Within websites, better title match (+16.8%/SD) and more referring sites (+33.7%/SD) went with more Gemini citations. FAQ blocks and schema.org markup had no effect. Pages needing JavaScript for main text got 10.6% fewer citations.
- **Classification:** VERIFIED FACT (observational, API) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** Gemini API / page features
- **Source:** Chen & Koudas (as RES-030) — https://arxiv.org/html/2610.15033v1
- **Published:** 2026-10-10 · **Accessed:** 2026-10-30
- **Excerpt:** > "FAQ blocks and schema.org markup have no effect for any engine."
- **Establishes:** Server-rendered text matters; markup does not show a citation effect.
- **Limitations:** Observational; services market; web pages, not Merchant Center data.
- **Related:** GOOG-029, GOOG-031, RES-012
- **Origin:** notes/ge-…#GE-13 · **Checked:** pending

### RES-034 — The Gemini consumer app and the Gemini API show different sources for the same product question (14.8% domain overlap)
- **Claim:** For 117 product-recommendation queries, the logged-out Gemini web app and the Gemini API (grounded) shared 14.8% of displayed domains and 11.9% of pages on average. AI Overviews recommended more consistent products than the Gemini app (Jaccard 0.421 vs 0.287).
- **Classification:** VERIFIED FACT (Gemini UI and API, Netherlands, Sept 2026) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** Gemini / methodology
- **Source:** ""If I Had to Buy Just ONE: Galaxy S26 Ultra": Auditing AI-Generated Product Recommendations" — Uberti-Bona Marin et al. — https://arxiv.org/abs/2609.18729
- **Published:** 2026-09-16 · **Accessed:** 2026-10-30
- **Excerpt:** > "with mean domain overlaps of 12.0% for ChatGPT and 14.8% for Gemini"
- **Establishes:** API studies do not describe the Gemini app. AURA must test the consumer surfaces directly.
- **Limitations:** One country; logged out; AI Mode not tested.
- **Related:** RES-012, RES-042, GEM-006
- **Origin:** notes/ge-…#GE-27, #GE-28 · **Checked:** 2026-10-31 (abstract)

### RES-035 — In consumer UIs, Gemini's sources were the most repeatable of four engines; AI Mode concentrated citations most
- **Claim:** Scraped from Swiss consumer interfaces, Gemini had within-24h source Jaccard 0.505 and AI Mode 0.318; AI Mode had the highest citation concentration (Gini 0.782).
- **Classification:** VERIFIED FACT (consumer UIs, Swiss, Jan–Mar 2026) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** Gemini app, AI Mode / volatility
- **Source:** "Don't Measure Once…" — Schulte, Bleeker, Kaufmann — https://arxiv.org/html/2604.07585v1
- **Published:** 2026-04-08 · **Accessed:** 2026-10-30
- **Excerpt:** > "Google AI Mode exhibits the highest citation concentration (Gini = 0.782)"
- **Establishes:** Repeat runs are needed on Google surfaces too.
- **Limitations:** German prompts; contradicts RES-034's lower Gemini repeatability.
- **Related:** RES-016, RES-034
- **Origin:** notes/ge-…#GE-14 · **Checked:** pending

### RES-036 — Grounded Gemini cites more brand-owned sources than ChatGPT; ~11% domain overlap with Google's top 10
- **Claim:** For well-known brands, Gemini 2.5 Flash with grounding cited 63.4% earned, 25.1% brand and 11.5% social domains (ChatGPT 93.5% earned). Its mean domain overlap with Google's top 10 was 11.1%. For transactional intent, all AI systems raised brand citations to 52–68%.
- **Classification:** VERIFIED FACT (API, 2025) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** Gemini API / sources
- **Source:** Chen, Wang, Chen, Koudas — https://arxiv.org/html/2509.08919v1 ; https://arxiv.org/html/2601.16858v2
- **Published:** 2025-09-10; 2026-05-16 · **Accessed:** 2026-10-30
- **Excerpt:** > "Gemini stood between these extremes, balancing 63.4% Earned, 25.1% Brand, and 11.5% Social."
- **Establishes:** Brand-owned pages get more share in Gemini than in ChatGPT.
- **Limitations:** API; LLM-labeled domains.
- **Related:** RES-011
- **Origin:** notes/ge-…#GE-15, #GE-17 · **Checked:** pending

### RES-037 — Gemini 3 Flash switches from an incumbent brand on a tiny rating edge (83% of trials)
- **Claim:** With identical specs, a fictional competitor's minimal rating advantage won 83% of trials for Gemini 3 Flash (Claude 22%). Authority-style claims moved Gemini to near 100% selection.
- **Classification:** VERIFIED FACT (gemini-3-flash-preview API, direct prompts) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** Gemini models / ranking signals
- **Source:** "Incumbent Advantage…" — Chu & Hou — https://arxiv.org/html/2606.17443v3
- **Published:** 2026-10-10 · **Accessed:** 2026-10-30
- **Excerpt:** > "Gemini is near baseline at subtle intensity (11.7%) but saturates near 100% from moderate intensity onward (99.3%/100%)."
- **Establishes:** Gemini models react strongly to small visible attribute differences and claim wording.
- **Limitations:** No search; fabricated claims in stimuli.
- **Related:** RES-017, RES-028
- **Origin:** notes/ge-…#GE-18 · **Checked:** pending

### RES-038 — AI Overviews rarely trigger on product-keyword searches (14–17%)
- **Claim:** AIOs appeared on 17.4% of Amazon product-keyword queries (vs 51.5% of representative queries) in a SIGIR 2026 study and on 14.6% of US trending Shopping queries in an IMC 2026 study. Question-form and longer queries triggered far more often. Real-user data (Pew, March 2025) found AI summaries on 18% of searches, 8% for 1–2-word searches.
- **Classification:** VERIFIED FACT · **Confidence:** High (three independent studies agree) · **Tier:** 2
- **Subject / topic:** AI Overviews / triggering
- **Source:** Grossman et al. — https://arxiv.org/abs/2604.27790 ; Xu, Iqbal, Montgomery — https://arxiv.org/abs/2605.14021 ; Pew Research Center — https://www.pewresearch.org/short-reads/2025/07/22/google-users-are-less-likely-to-click-on-links-when-an-ai-summary-appears-in-the-results/
- **Published:** 2026-04-30; 2026-10-01; 2025-07-22 · **Accessed:** 2026-10-30
- **Excerpt:** > "94.6% of ELI5 queries, compared to just 17.4% of Amazon Retail queries, result in an AIO"
- **Establishes:** For short product searches, AIO is often absent; AI Mode and Shopping units matter more.
- **Limitations:** Logged-out, US; a logged-in Milan study saw 97% (RES-043).
- **Related:** RES-043
- **Origin:** notes/ge-…#GE-19, #GE-23, #GE-29, #GE-37 · **Checked:** pending

### RES-039 — AIO, Gemini and Google organic share few sources; Gemini never cited sites that block Google-Extended
- **Claim:** URL-level Jaccard was 0.18 (AIO vs SERP), 0.16 (Gemini vs SERP) and 0.11 (AIO vs Gemini); Amazon product queries were lowest (0.06–0.08). Gemini (API) never cited Facebook, Yelp, Tripadvisor, Consumer Reports and others that block Google-Extended. AIOs favored google.com and youtube.com.
- **Classification:** VERIFIED FACT (AIO via SerpApi; Gemini 2.5 Flash API) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** Google AI surfaces / sources
- **Source:** "How Generative AI Disrupts Search…" — Grossman et al. — https://arxiv.org/html/2604.27790v1
- **Published:** 2026-04-30 (SIGIR 2026) · **Accessed:** 2026-10-30
- **Excerpt:** > "In particular, the product and service queries (i.e., Amazon Retail and Localized query subsets) result in the lowest similarity for each pairing of search engines."
- **Establishes:** Google-Extended blocking associates with Gemini exclusion (consistent with GOOG-027).
- **Limitations:** Observational; one date.
- **Related:** GOOG-027, MKT-022, RES-031
- **Origin:** notes/ge-…#GE-20, #GE-21 · **Checked:** pending

### RES-040 — Device changes AI Overview sources more than city does
- **Claim:** Same-config AIO runs had source RBO 0.69. Changing device dropped RBO by 0.16; changing US city changed it by 0.01–0.02. Cosmetic query edits dropped it to 0.49.
- **Classification:** VERIFIED FACT · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** AI Overviews / methodology
- **Source:** Grossman et al. (as RES-039) — https://arxiv.org/html/2604.27790v1
- **Published:** 2026-04-30 · **Accessed:** 2026-10-30
- **Excerpt:** > "the retrieved sources are more inconsistent between different devices than between different locations"
- **Establishes:** Experiments must fix and record device.
- **Limitations:** US only; small robustness samples.
- **Related:** RES-038
- **Origin:** notes/ge-…#GE-22 · **Checked:** pending

### RES-041 — About 30–53% of AIO-cited domains sit outside the organic first page or top 10; AIO sources drift heavily over two months
- **Claim:** In an IMC 2026 study, 29.8% of AIO reference domains were absent from the first results page. In a Findings of ACL 2026 study, 53% of AIO domains were outside the organic top 10, and run-to-run overlap two months apart was 18% (organic 45%).
- **Classification:** VERIFIED FACT · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** AI Overviews / retrieval
- **Source:** Xu et al. — https://arxiv.org/html/2605.14021v2 ; Kirsten et al. — https://arxiv.org/html/2510.11560v2
- **Published:** 2026-10-01; 2026-05-31 · **Accessed:** 2026-10-30
- **Excerpt:** > "only 31.5% of AIO reference domains overlap with the top-5 first-page results, rising to 48.0% at top-10 and 70.2% across the full first page."
- **Establishes:** AIO is not a re-ranking of the visible SERP.
- **Limitations:** Domain-level; trending and mixed query sets.
- **Related:** RES-039, RES-048
- **Origin:** notes/ge-…#GE-24, #GE-25 · **Checked:** pending

### RES-042 — For product questions, AI Overviews mix retailers, brands and community pages more than the Gemini app
- **Claim:** AIO source types for product answers: editorial/review 25.4%, UGC/social 22.2%, retailers/marketplaces 17.8%, manufacturers/brands 16.1%. AIO appeared on 38.2% of these product queries. 61.7% of AIOs combined three or more source types (Gemini 19.0%).
- **Classification:** VERIFIED FACT (Netherlands, Sept 2026) · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** AI Overviews, Gemini app / sources
- **Source:** Uberti-Bona Marin et al. (as RES-034) — https://arxiv.org/html/2609.18729v1
- **Published:** 2026-09-16 · **Accessed:** 2026-10-30
- **Excerpt:** > "AI Overviews displayed reddit.com (35.0%) and youtube.com (30.0%) most often."
- **Establishes:** Retailer pages are a minority of AIO product sources.
- **Limitations:** Small AIO sample; LLM-labeled types.
- **Related:** RES-034
- **Origin:** notes/ge-…#GE-28 · **Checked:** pending

### RES-043 — Logged in from Italy, Google showed an AI overview for 97% of queries
- **Claim:** With a logged-in account (Milan), Google generated overviews for 97.0% of English MS MARCO queries.
- **Classification:** VERIFIED FACT · **Confidence:** Medium · **Tier:** 2
- **Subject / topic:** AI Overviews / methodology
- **Source:** "Auditing Source Exposure in Baidu and Google AI Search" — Li et al. — https://arxiv.org/html/2609.24407v1
- **Published:** 2026-09-21 · **Accessed:** 2026-10-30
- **Excerpt:** > "Google generated overviews for 97.6 % of Chinese queries and 97.0 % of English queries."
- **Establishes:** Account state, location and language can move AIO trigger rates far from logged-out US figures.
- **Limitations:** Cause not isolated; small sample.
- **Related:** RES-038
- **Origin:** notes/ge-…#GE-31 · **Checked:** pending

### RES-044 — Vendor quasi-experiment: adding JSON-LD did not raise AI Mode or AIO citations
- **Claim:** Ahrefs tracked 1,885 pages that added JSON-LD against matched controls. AIO citations changed −4.6% (significant); AI Mode +2.4% and ChatGPT +2.2% (not significant).
- **Classification:** VERIFIED FACT (as reported by the vendor) · **Confidence:** Low · **Tier:** 3
- **Subject / topic:** AI Mode, AIO / structured data
- **Source:** "We Tracked 1,885 Pages Adding Schema. AI Citations Barely Moved." — Ahrefs — https://ahrefs.com/blog/schema-ai-citations/
- **Published:** 2026-05-11 · **Accessed:** 2026-10-30
- **Excerpt:** > "No platform showed a meaningful citation increase after schema was added." (Search Engine Journal summary)
- **Establishes:** Agrees with Google's guidance (GOOG-029) and RES-033.
- **Limitations:** Vendor data; heavily cited pages only; says nothing about Merchant Center feeds.
- **Related:** GOOG-029, RES-033
- **Origin:** notes/ge-…#GE-33 · **Checked:** pending

### RES-045 — Vendor study: AI Mode sources change across same-day runs (9.2% three-run URL overlap)
- **Claim:** For 10,000 US keywords run three times on one day, AI Mode's exact-URL overlap across all runs averaged 9.2%. AI Mode vs AIO URL overlap was 10.7%.
- **Classification:** VERIFIED FACT (as reported by the vendor) · **Confidence:** Low · **Tier:** 3
- **Subject / topic:** AI Mode / volatility
- **Source:** "AI Mode research…" — SE Ranking — https://seranking.com/blog/ai-mode-research/
- **Published:** 2025-08-29 · **Accessed:** 2026-10-30
- **Excerpt:** > "Volatility is high. Even the same query run multiple times on the same day often yields different sources."
- **Establishes:** Consistent with RES-035.
- **Limitations:** June 2025, early AI Mode.
- **Related:** RES-035
- **Origin:** notes/ge-…#GE-34 · **Checked:** pending

### RES-046 — Vendor study: AI Mode shows few products, almost none from the regular Shopping carousel, often at a higher lead price
- **Claim:** Productrise reports AI Mode showed products on ~23% of shopping queries (vs ~88% for standard search), and only 1.28% of carousel products also appeared in AI Mode. When both showed a product, AI Mode's lead seller differed 49.6% of the time and its lead price averaged 21.6% higher. Google said both use the same data source.
- **Classification:** VERIFIED FACT (as reported by the vendor; Google statement as quoted by SEJ) · **Confidence:** Low · **Tier:** 3
- **Subject / topic:** AI Mode / product selection
- **Source:** PPC Land — https://ppc.land/ai-mode-shows-the-same-products-21-6-more-expensive-productrise-finds/ ; Search Engine Journal — https://www.searchenginejournal.com/google-ai-mode-prices-differ-from-product-carousel-for-same-items/588227/
- **Published:** 2026-09-03 · **Accessed:** 2026-10-30
- **Excerpt:** > "only 1.28% of products ranking in traditional search also appeared in AI Mode for the same search on the same day."
- **Establishes:** Shopping-tab rank is a poor proxy for AI Mode inclusion; lowest price is not the dominant lead-offer rule (inference).
- **Limitations:** Vendor sample and method not public.
- **Related:** GOOG-022, GEM-003
- **Origin:** notes/ge-…#GE-35, #GE-36 · **Checked:** pending

### RES-047 — Vendor data: Walmart leads Gemini's cited US retailers; Amazon absent
- **Claim:** LLM Pulse's Gemini table for US non-branded shopping questions lists walmart.com first (0.92% of citations) and no Amazon.
- **Classification:** VERIFIED FACT (as reported by the vendor) · **Confidence:** Low · **Tier:** 3
- **Subject / topic:** Gemini / marketplaces
- **Source:** "Gemini · Top US Retailers cited by AI" — LLM Pulse — https://llmpulse.ai/data-studies/top-us-retailers/gemini
- **Published:** updated 2026-10-29 · **Accessed:** 2026-10-30
- **Excerpt:** [paraphrase — table values, no prose excerpt]
- **Establishes:** Consistent with Amazon's Google-Extended block (MKT-022, RES-039).
- **Limitations:** Surface (app vs API) not stated; internal inconsistencies.
- **Related:** MKT-022
- **Origin:** notes/ge-…#GE-38 · **Checked:** pending

### RES-048 — Vendor data: share of AIO citations from the organic top 10 fell from 76% (Jul 2025) to 38% (Mar 2026)
- **Claim:** Ahrefs reported 76.1% of AIO-cited pages in the top 10 in July 2025 and 37.9% in March 2026.
- **Classification:** VERIFIED FACT (as reported by the vendor) · **Confidence:** Low (method changed between the two) · **Tier:** 3
- **Subject / topic:** AI Overviews / retrieval
- **Source:** "Update: 38% of AI Overview Citations Pull From The Top 10" — Ahrefs — https://ahrefs.com/blog/ai-overview-citations-top-10/
- **Published:** 2026-03-02 · **Accessed:** 2026-10-30
- **Excerpt:** > "Google is selecting far fewer pages straight from the original SERP."
- **Establishes:** Consistent with RES-041.
- **Limitations:** Not a clean time series.
- **Related:** RES-041
- **Origin:** notes/ge-…#GE-32 · **Checked:** pending
