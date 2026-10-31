# E: Independent (non-OpenAI) research on how ChatGPT and LLM systems select and rank products

- Agent: E (AURA research)
- Date: 2026-10-30
- Scope: Tier 2 research (arXiv / peer-reviewed / reproducible experiments) and the most credible Tier 3 analyses on LLM product selection, ranking, citation sourcing, volatility, and the search index behind ChatGPT search. OpenAI first-party docs are out of scope except where they bear on the index question.
- Method:
  - arXiv abstract and full-text HTML pages were downloaded with curl from arxiv.org and converted to text locally. arXiv excerpts below were string-matched against that text. They are verbatim except for collapsed line breaks.
  - Non-arXiv pages were read with WebFetch. Their excerpts are verbatim as returned by WebFetch extraction. They were not independently byte-verified.
  - Several pages returned HTTP 403 (see "Unfetched sources"). Two OpenAI pages that returned 403 to WebFetch were read in the in-app browser (E-25). Their excerpts were copied from the rendered page text. Pages that showed a Cloudflare bot check were not pursued. No claim below relies on an unfetched page.
  - Excerpts are kept short (one per finding) on purpose.
- Classification labels: VERIFIED FACT = the source states this result for the system it tested. EVIDENCE-BASED INFERENCE = what it suggests about ChatGPT. UNVERIFIED HYPOTHESIS = plausible, not tested.
- Core caveat for the whole file: no fetched Tier 2 study instruments the production consumer ChatGPT shopping UI (chatgpt.com product carousel) under controlled conditions. Most Tier 2 results come from (a) API models with a web-search tool, (b) API models without search on constructed inputs, or (c) open models. Lab results are not evidence of ChatGPT's production ranking.

---

## Findings

### E-01 Position bias in LLM shopping agents is large and flips between model versions
- Claim: In a controlled mock store, every tested agent showed large position effects. The preferred slot differed by provider and reversed between GPT-4.1 and GPT-5.1.
- Classification: VERIFIED FACT (for the API models tested). EVIDENCE-BASED INFERENCE for ChatGPT: any position effect inside ChatGPT shopping is likely model-version-specific, so a measured effect can expire at the next model update.
- Source: What Is Your AI Agent Buying? Evaluation, Biases, Model Dependence, & Emerging Implications for Agentic E-Commerce — Allouah, Besbes, Figueroa, Kanoria, Kumar (Columbia, Yale, MyCustomAI) — https://arxiv.org/abs/2508.02630 (full text: https://arxiv.org/html/2508.02630v3)
- Published/updated: v1 2025-08-04; v3 2025-12-17. arXiv preprint (no venue listed).
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: ACES sandbox. A VLM computer-use agent (LangChain + Selenium) sees a 2x4 grid of 8 products and picks one. Models: Claude Sonnet 4, GPT-4.1, Gemini 2.5 Flash (Aug 2025) and Claude Opus 4.5, GPT-5.1, Gemini 3.0 Pro Preview (Dec 2025). Temperature 1.0. Low reasoning effort. 8 categories x 500 randomized scenarios per model (about 3,756–3,993 valid choice sets per model). Conditional logit with product fixed effects.
- Excerpt: > "the preferred position by one is the least preferred by the other and vice versa"
- Establishes: Position effects are causal (positions randomized), large (for Claude Sonnet 4, moving a 4.5%-share item from bottom-right to top-row middle gives about a 5-fold increase), and not stable across model generations. A "headless" JSON-list variant on three models reproduced the effect ("found similar biases, e.g., strong, model-specific position effects"). Prompting "ignore position" did not remove it.
- Limitations: API models, not the ChatGPT app. One-shot choice from a single results page, no conversation, no product detail pages. Generic prompt with no user constraints. Low reasoning settings. Mock store built from Amazon listings. GPT-5.1 at low effort may not match the model or settings ChatGPT uses.

### E-02 Shopping agents penalize a "Sponsored" tag and reward a platform endorsement badge
- Claim: With position and attributes held fixed, a "Sponsored" tag lowered selection probability for all three Aug-2025 models. An "Overall Pick" badge raised it strongly. The pattern persisted after the model upgrades.
- Classification: VERIFIED FACT (API models in ACES). EVIDENCE-BASED INFERENCE: if ChatGPT's shopping model sees ad labels in its context, labels could reduce selection. UNVERIFIED for production ChatGPT.
- Source: Allouah et al. (as E-01) — https://arxiv.org/html/2508.02630v3
- Published/updated: v3 2025-12-17
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: Same as E-01. "Sponsored", "Overall Pick", and scarcity tags were randomly assigned per scenario.
- Excerpt: > "Sponsored tags are penalized while Platform Endorsement is substantially rewarded."
- Establishes: A product with a 10% baseline selection rate fell to 8.9% (Claude Sonnet 4), 8.0% (GPT-4.1), and 7.9% (Gemini 2.5 Flash) when tagged "Sponsored". An "Overall Pick" tag raised the same baseline to 24.3%, 19.9%, and 42.6%. The scarcity tag was weakly negative or null. The authors say aversion to sponsored tags persisted after the upgrade to the Dec-2025 models.
- Limitations: Tag effects are conditional on a fixed position. The authors note that sponsored placement can still win through position. Badge wording and visual design are ACES-specific.

### E-03 Price, rating, and review-count sensitivity is directionally rational but varies in magnitude across models
- Claim: All ACES models preferred cheaper, higher-rated, more-reviewed items. Magnitudes differed sharply by model.
- Classification: VERIFIED FACT (API models). EVIDENCE-BASED INFERENCE: ChatGPT shopping likely responds to price and rating in the expected direction. The size of the effect cannot be transferred from these models.
- Source: Allouah et al. (as E-01) — https://arxiv.org/html/2508.02630v3
- Published/updated: v3 2025-12-17
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: Same as E-01. Prices, ratings, and review counts were randomly perturbed per scenario.
- Excerpt: > "our elasticity estimates (-1.6 to -2.2) are broadly in the same range"
- Establishes: Implied price elasticities were -1.6 to -2.2, similar to human SKU-level estimates. Moving from row 2 to row 1 was worth about a doubling of price for Claude Sonnet 4 and GPT-4.1, but only about +17% for Gemini 2.5 Flash. In the basic rationality tests, the Dec-2025 models almost never missed a cheaper or higher-rated dominant option. Older models sometimes did (for example, GPT-4o failed 71.7% of the time on a tiny rating advantage).
- Limitations: Perturbations were small. A single generic persona. Elasticities come from a logit fitted to agent choices, not purchases.

### E-04 Model updates reshuffle which products agents choose
- Claim: Different models choose very different products from the same assortment. Upgrading a model can move a product's share by tens of points.
- Classification: VERIFIED FACT (API models). EVIDENCE-BASED INFERENCE: ChatGPT product visibility is exposed to model-update shocks. Any AURA baseline must record the model version and date.
- Source: Allouah et al. (as E-01) — https://arxiv.org/html/2508.02630v3
- Published/updated: v3 2025-12-17
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: 8 products per category, positions randomized, selection frequency used as a proxy for market share.
- Excerpt: > "while it fell (from 25%) to only 6% with GPT-5.1"
- Establishes: Fitbit Inspire went from about 25% (GPT-4.1) to 6% (GPT-5.1), and from 45% (Claude Sonnet 4) to 77% (Claude Opus 4.5). For iPhone 16 Pro covers, GPT-4.1 picked Mikeke 62.6% of the time. GPT-5.1 picked ESR 95% of the time and Mikeke 5%. Some brands were never chosen (for example, Arrow staplers). The authors report that Gemini 2.5 Flash's position bias inverted between the Preview and the final release.
- Limitations: Same as E-01. "Market share" is a selection rate under one prompt, not real demand.

### E-05 Small, query-matched listing text edits shift agent selection
- Claim: One AI-rewritten product description raised the focal product's selection share significantly in 5 of 6 buyer models.
- Classification: VERIFIED FACT (API models). EVIDENCE-BASED INFERENCE: product text that the model reads at decision time can change ChatGPT's picks. Whether ChatGPT shopping reads merchant descriptions at that step is not established here.
- Source: Allouah et al. (as E-01) — https://arxiv.org/html/2508.02630v3
- Published/updated: v3 2025-12-17
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: 200 shuffled trials before and after one description rewrite (GPT-4.1 or GPT-5.1 as the seller agent). The same shuffles were reused pre and post.
- Excerpt: > "+14.89 (1.05) p.p. for GPT-5.1"
- Establishes: Average gains were +3.66 p.p. (Claude Sonnet 4), +8.37 (GPT-4.1), +14.79 (Gemini 2.5 Flash), +7.38 (Claude Opus 4.5), +14.89 (GPT-5.1), and +0.32, not significant (Gemini 3 Pro Preview). The authors attribute gains mainly to front-loading query terms (for example, "Office" for an office-lamp query). Some edits reduced share.
- Limitations: Single seller optimizes. Description truncation in the mock UI may inflate the keyword effect.

### E-06 Agents are hypersensitive to ratings, price, order, and nudges compared with humans
- Claim: Across 17 models and more than 80,000 trials, ratings, prices, presentation order, and short persuasive text shifted agent choices far more than they shifted human choices in the same task.
- Classification: VERIFIED FACT (the models tested, including GPT-4.1, GPT-4o, GPT-5, GPT-5 Mini/Nano, o3, o4-mini). EVIDENCE-BASED INFERENCE: OpenAI models used as shopping agents can over-weight star ratings and on-page claims. This was not tested in the ChatGPT app.
- Source: A Framework for Studying AI Agent Behavior: Evidence from Consumer Choice Experiments (ABxLab) — Cherep, Ma, Xu, Shaked, Maes, Singh (MIT Media Lab et al.) — https://arxiv.org/abs/2509.25609 (full text: https://arxiv.org/html/2509.25609v2)
- Published/updated: v1 2025-09-30; v2 2026-02-24. arXiv comment: "ICLR".
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: Two-alternative forced choice in a realistic web shop. 50 product pairs x 10 interventions x 3 conditions = 1,500 base configurations per model. 17 models. Temperature 0.1 (1 for OpenAI reasoning models). Human baseline: 30 Prolific participants on the same 50 pairs.
- Excerpt: > "Higher product ratings consistently increased selection probability by 30-80pp across 14 of 17 models"
- Establishes: Cheaper items gained 15.2–34.3 pp in 13 of 17 models. Order effects were heterogeneous in sign ("GPT-4.1 Nano showed a +90pp preference for the first-listed product"; Claude 3.5 Haiku showed a −35.4 pp penalty). Nudges such as "best seller" shifted selections 10–60 pp when price and rating were matched. Humans showed 4–10 pp effects, mostly not significant.
- Limitations: Pairwise choice, not ranking. Synthetic store. Agent prompts lack real user context. Human sample is small (n=30).

### E-07 First-proposal bias dominates in two-sided agent markets; list-position bias was near-uniform for frontier models
- Claim: In a simulated marketplace, all models heavily favored the first business proposal received. Frontier models did not favor the first-listed search result among three identical businesses.
- Classification: VERIFIED FACT (models tested: GPT-4o, GPT-4.1, GPT-5, Gemini-2.5-Flash, Claude Sonnet 4/4.5, open models). EVIDENCE-BASED INFERENCE: order effects depend on task framing (list vs sequential offers). This conflicts in part with E-01 and E-06 (see Contradictions).
- Source: Magentic Marketplace: An Open-Source Environment for Studying Agentic Markets — Bansal et al. (Microsoft Research, with Arizona State University) — https://arxiv.org/abs/2510.25779 (full text: https://arxiv.org/html/2510.25779v1)
- Published/updated: v1 2025-10-27. arXiv preprint.
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: Synthetic restaurant and contractor domains. 33x99 and 100x300 customer-x-business markets. 5 independent runs per configuration. Position test: three identical businesses differing only in list position.
- Excerpt: > "all models exhibit severe first-proposal bias, creating 10-30x advantages for response speed over quality"
- Establishes: First proposals were selected 60–100% of the time versus near zero for third proposals. GPT-4.1, Sonnet-4.5, and Gemini-2.5-Flash "showed near-uniform selection rates across all three positions". Qwen3-4B was strongly position-biased.
- Limitations: Synthetic agent-to-agent negotiation, not a consumer chat UI. Only three list positions. Not ChatGPT.

### E-08 A strategic text sequence on a product page can make an open LLM rank that product first
- Claim: An adversarially optimized text string (GCG) added to one product's JSON raised its chance of being the top recommendation.
- Classification: VERIFIED FACT (Llama-2 on a 10-item fictitious catalog). EVIDENCE-BASED INFERENCE: weak for ChatGPT. Transfer to GPT models is cited from other work, not tested.
- Source: Manipulating Large Language Models to Increase Product Visibility — Aounon Kumar, Himabindu Lakkaraju (Harvard) — https://arxiv.org/abs/2404.07981 (full text: https://arxiv.org/html/2404.07981v2)
- Published/updated: v1 2024-04-11; v2 2024-09-02. No venue listed on arXiv.
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: Llama-2 chat with JSON lines for ten fictitious coffee machines. Two target products. 200 LLM evaluations with and without the sequence, product order randomized.
- Excerpt: > "can significantly increase its likelihood of being listed as the LLM’s top recommendation"
- Establishes: Order-robust optimization matters. A sequence optimized for a fixed order improved rank in "about 40%" of randomized-order evaluations and left about 60% unchanged. An order-robust sequence did better.
- Limitations: White-box attack on an open model. Fictitious products with no prior knowledge. No retrieval step. Not ChatGPT.

### E-09 LLM rankers weigh product name, page content, and context position differently; GPT-4 Turbo leans on product name
- Claim: In RAG-style product recommendation, GPT-4 Turbo relied heavily on its prior knowledge of product names and little on page content. All tested LLMs preferred documents placed earlier in the context. Prompt injections promoted low-ranked products, including on Perplexity's online model.
- Classification: VERIFIED FACT (GPT-3.5 Turbo, GPT-4 Turbo, Llama 3 70B, Mixtral 8x22, Perplexity Sonar Large Online). EVIDENCE-BASED INFERENCE: OpenAI models may rank well-known products high regardless of retrieved page content. This supports E-18 and E-23.
- Source: Ranking Manipulation for Conversational Search Engines — Pfrommer, Bai, Gautam, Sojoudi (UC Berkeley) — https://arxiv.org/abs/2406.03589 (full text: https://arxiv.org/html/2406.03589v3)
- Published/updated: v1 2024-06-05; v3 2024-09-25. Venue: EMNLP 2024 (Main).
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: RagDoll dataset with 1,147 manufacturer pages across 50 categories. Experiments use 8 brands per category. Product-document pairs were shuffled and swapped, and F-statistics were computed per factor. A tree-of-attacks injection was transferred to self-hosted pages read by Sonar Large Online.
- Excerpt: > "GPT-4 Turbo particularly attends to the product name"
- Establishes: "all LLMs are significantly influenced by the input context position". The injection raised the promoted product's mean ranking score by 5.00 (82.94% of the gap to the top) on GPT-4 Turbo and by 2.89 (54.23%) on Sonar Large Online.
- Limitations: 2024 models. Manufacturer pages only. Retrieval was bypassed (documents supplied). Perplexity was tested only via an API surrogate.

### E-10 On production Bing Copilot, real brands beat unknown ones; injected pages can override this
- Claim: In live tests on Bing Copilot, real camera brands were recommended about twice as often as a fictitious camera. A preference-manipulation page reversed this.
- Classification: VERIFIED FACT (Bing Copilot and Perplexity, 2024). EVIDENCE-BASED INFERENCE: brand-familiarity effects exist in production LLM search, not only in labs. Not tested on ChatGPT.
- Source: Adversarial Search Engine Optimization for Large Language Models — Nestaas, Debenedetti, Tramèr (ETH Zürich) — https://arxiv.org/abs/2406.18382 (full text: https://arxiv.org/html/2406.18382v2)
- Published/updated: v1 2024-06-26; v2 2024-07-02. ICLR 2025 per the search results (venue not on the arXiv page).
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: 50 dummy pages on the authors' domain. Fictitious cameras, books, and news sites. Production Bing Copilot and Perplexity. GPT-4 and Claude 3 plugin APIs.
- Excerpt: > "recommended nearly twice as often (presumably due to brand name recognition)"
- Establishes: An injected page made the attacker's camera 2.5x more likely to be recommended than a comparable product. Direct attacks on Bing succeeded 95–100% of the time in the multi-listing test.
- Limitations: 2024 production systems. Small page set. Adversarial (hidden-text) content. The brand-recognition effect is a side observation.

### E-11 GEO: content edits raised source visibility up to about 40% in a simulated generative engine
- Claim: Adding citations, quotations, and statistics to a source raised its visibility in answers from a GPT-3.5-based generative engine. Lower-ranked sources gained most.
- Classification: VERIFIED FACT (simulated engine: Google top-5 sources + gpt-3.5-turbo; plus Perplexity.ai). EVIDENCE-BASED INFERENCE for ChatGPT: weak. The setup fixes retrieval, which E-15 shows drives most citation variance.
- Source: GEO: Generative Engine Optimization — Aggarwal, Murahari, Rajpurohit, Kalyan, Narasimhan, Deshpande (Princeton, IIT Delhi et al.) — https://arxiv.org/abs/2311.09735 (full text: https://arxiv.org/html/2311.09735v3)
- Published/updated: v1 2023-11-16; v3 2024-06-28. Venue: KDD 2024.
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: GEO-bench, 10K queries (1K test). 5 sampled responses at temperature 0.7. 5 seeds. Metrics: position-adjusted word count and subjective impression scored by GPT-3.5.
- Excerpt: > "can improve the visibility of websites by up to 40%"
- Establishes: The "Cite Sources" method raised visibility of rank-5 sources by 115.1%, while top-ranked sources lost 30.3% on average. Keyword stuffing did not help. The paper reports up to 37% gains on Perplexity.ai.
- Limitations: GEO-bench is 80% informational queries, not product-specific. A 2023 model. Visibility is defined by word count in the answer, not by product rank.

### E-12 A later benchmark found most conversational-SEO methods ineffective; improving retrieval rank worked better
- Claim: Across QA and product-recommendation tasks, most published C-SEO content methods were ineffective or harmful. Improving a source's position in the LLM context was significantly more effective. Gains fell as more competitors adopted C-SEO.
- Classification: VERIFIED FACT (the benchmark's LLMs). EVIDENCE-BASED INFERENCE: contradicts the size of GEO gains in E-11. Supports E-15 (retrieval and rank dominate).
- Source: C-SEO Bench: Does Conversational SEO Work? — Puerto, Gubri, Green, Oh, Yun (Parameter Lab, NAVER AI Lab et al.) — https://arxiv.org/abs/2506.11097
- Published/updated: v1 2025-06-06; v3 2025-10-20. Venue: NeurIPS 2025 Datasets & Benchmarks.
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: Two tasks (QA, product recommendation) x three domains each. Varying adoption rates among competing documents. Abstract only was read. Model list not extracted.
- Excerpt: > "most current C-SEO methods are not only largely ineffective"
- Establishes: Content-level "optimization" results from single-actor lab setups do not generalize reliably.
- Limitations: Abstract-level reading only. Fixed-context setup, not ChatGPT. Related: E-GEO (Bagga et al., https://arxiv.org/abs/2511.20867, v2 2026-07-14) built 13,747 product queries, each paired with 10 Amazon listings, across five generative engines. Its abstract claims that, under a simple in-prompt defense, "gains from GEO reflect genuine content improvement rather than manipulation". Its full text was not read.

### E-13 Web-search LLMs cite mostly third-party "earned" media for product ranking queries; the OpenAI search model most of all
- Claim: For consumer ranking queries, the OpenAI search API model cited almost only third-party review and media domains, with almost no brand-owned or social sources.
- Classification: VERIFIED FACT (gpt-4o-search-preview via API, 2025). EVIDENCE-BASED INFERENCE: ChatGPT search answers to "best X" queries likely lean on review publishers. Production ChatGPT and the shopping carousel were not tested. E-19 contradicts this pattern in a services market.
- Source: Generative Engine Optimization: How to Dominate AI Search — Mahe Chen, Xiaoxuan Wang, Kaiwen Chen, Nick Koudas (University of Toronto) — https://arxiv.org/abs/2509.08919 (full text: https://arxiv.org/html/2509.08919v1)
- Published/updated: v1 2025-09-10. arXiv preprint.
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: "GPT: gpt-4o-search-preview (the search-enabled variant of GPT-4o)." Also Claude 3.5 Sonnet with web_search, Gemini 2.5 Flash with grounding, and Perplexity sonar-pro. Google top-10 came from the Custom Search API. 1,000 consumer ranking prompts (10 categories x 100) in the US and Canada. Domains were classified Brand/Earned/Social by GPT-4o-search-preview.
- Excerpt: > "ChatGPT skewed even further, with 93.5% Earned, 6.5% Brand, and no Social"
- Establishes: Niche-brand queries: ChatGPT 95.1% Earned, 4.9% Brand. Consumer electronics: GPT 93.6% Earned. Top GPT domains were TechRadar, Tom's Guide, and Wikipedia. Google mixed more brand and social sources. Smartphone/laptop GPT-vs-Google domain overlap was 15–32% at top-5 and 20–41% at top-10.
- Limitations: API model, not the ChatGPT app. LLM-based domain labels. Ranking-style prompts only. The paper is partly framed as practitioner guidance; only its measurements are used here.

### E-14 The OpenAI search model's cited domains change almost completely across languages but are fairly stable across paraphrases
- Claim: Translating the same query changed GPT's cited domains almost entirely. Paraphrasing within English changed them less than it changed Google's results.
- Classification: VERIFIED FACT (gpt-4o-search-preview). EVIDENCE-BASED INFERENCE: locale and language are first-order variables for any ChatGPT measurement.
- Source: Chen, Wang, Chen, Koudas (as E-13) — https://arxiv.org/html/2509.08919v1
- Published/updated: 2025-09-10
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: 100 English base queries across 10 consumer verticals, translated into 5 languages and given 7 paraphrase templates. Jaccard overlap of cited-domain sets averaged per vertical.
- Excerpt: > "GPT is the special case that shows lower overlap than Google"
- Establishes: GPT's cross-language domain overlap was near zero. Across paraphrases, AI engines showed many base-variant overlaps of 0.3–0.7 ("AI results tend to be less sensitive to wording tweaks than Google").
- Limitations: Single run per condition is implied. Run-to-run noise was not separated from the paraphrase effect (compare E-17 and E-20).

### E-15 For the OpenAI web-search API, being retrieved explains far more citation variance than page features
- Claim: Over 90 days of daily answers, every page cited by the ChatGPT engine (API) had first been returned by its own search. Retrieval explained 32% of within-website citation variance. Fourteen page features explained 2.8%.
- Classification: VERIFIED FACT (gpt-5.4-nano with the web_search tool, 2026, US home-internet questions). EVIDENCE-BASED INFERENCE: for ChatGPT search, the retrieval and re-ranking step probably matters more than on-page formatting. Production-app equivalence is not shown.
- Source: What Drives AI Citations? Content, Retrieval and Model Knowledge in Generative Engine Optimization (GEO) — Mahe Chen, Nick Koudas (University of Toronto) — https://arxiv.org/abs/2610.15033 (full text: https://arxiv.org/html/2610.15033v1)
- Published/updated: v1 2026-10-10. arXiv preprint, CC BY 4.0.
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: An academic monitoring platform ran by the authors queried the public APIs daily (ChatGPT = GPT-5.4 nano + web search; Gemini 3.1 Flash Lite + Google grounding; Perplexity Sonar). 651 questions, 2026-06-24 to 2026-09-21. 143,249 answers and 396,188 citations. API replay: 13 runs on 11 days up to 2026-10-07. Replication: 55-question B2B niche market.
- Excerpt: > "Every page ChatGPT cites is one its own search retrieved"
- Establishes: ChatGPT consults about 26 pages per question and cites about 3. It cites 43.8% (95% CI 42.6–45.1%) of rank-1 pages, 12.2% at ranks 6–10, and 3.5% at ranks 11–20. Rank alone explains 26.8% of the choice (McFadden R²). Adding content features raises this only to 32.5%. At equal rank, brand pages had higher odds (x1.71). Reddit threads (x0.30) and comparison pages (x0.34) were consulted often but cited rarely. FAQ blocks and schema.org markup showed slightly lower odds.
- Limitations: API, not the app. Authors: "which need not behave like their consumer applications". Services market (ISPs), not physical products. Questions were written for a client, not sampled from logs. Observational.

### E-16 ChatGPT's retrieved pages almost never match Google's or Bing's top results for the same queries
- Claim: For the ChatGPT API engine's own rewritten search queries, only 0.5% (Bing) and 0.7% (Google) of retrieved pages were in those engines' top 10. 97% were absent from Google's top 50 and 99% from Bing's top 30.
- Classification: VERIFIED FACT (API, 2026). EVIDENCE-BASED INFERENCE: a classic Google or Bing page-level rank is a poor proxy for ChatGPT search retrieval. Contradicts Seer's 87% Bing match (E-27).
- Source: Chen & Koudas (as E-15) — https://arxiv.org/html/2610.15033v1
- Published/updated: 2026-10-10
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: Replay queries compared with US-located Google and Bing results fetched within 1–2 days.
- Excerpt: > "97% of ChatGPT’s retrieved pages are absent from Google’s top 50"
- Establishes: Low page-level overlap persists even when using ChatGPT's own sub-queries rather than the user prompt. 51% of ChatGPT's pages came from websites that appear in Google's top 50, so the overlap is higher at site level than at page level. Gemini, although grounded on Google Search, showed 5.6% top-10 overlap.
- Limitations: Does not identify which index ChatGPT uses. Low overlap is compatible with a different index, the same index with different re-ranking, or both. API only.

### E-17 ChatGPT search queries and citations change on every run and drift over weeks
- Claim: Between two runs on the same day, ChatGPT's search queries overlapped by 2.7% (Jaccard) and its cited pages by 15%. Shared citation variance fell to 40% after two weeks and 14% after ten weeks.
- Classification: VERIFIED FACT (API). EVIDENCE-BASED INFERENCE: single-run measurements of ChatGPT search are unreliable. AURA needs repeated runs and longitudinal windows.
- Source: Chen & Koudas (as E-15) — https://arxiv.org/html/2610.15033v1
- Published/updated: 2026-10-10
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: Odd/even-day split reliability (r=0.82; 90-day reliability 0.90). Six 14-day windows.
- Excerpt: > "ChatGPT’s queries overlap by 2.7% (Jaccard) and its cited pages by 15%"
- Establishes: About 10% of page-level citation variance is day-to-day chance and about 75% is repeatable within a 90-day window, yet that repeatable part decays over weeks. ChatGPT splits a question into about 4 keyword-style queries. It adds the current year to 23% of queries and adds a brand the user did not name to 28%.
- Limitations: API. One market. Repeatability is at page level, not product level.

### E-18 ChatGPT's model favors sources shown first and re-ranks identical products by brand name
- Claim: In controlled answer-step tests on the model behind the ChatGPT engine, a source shown first was cited 17.6 points more often than when shown last. Revealing brand names on otherwise identical product profiles changed top-3 rates 2.1x more than repetition noise. Much brand naming came from model memory, not from cited pages.
- Classification: VERIFIED FACT (gpt-5.4-nano without search on constructed inputs, and API collection). EVIDENCE-BASED INFERENCE: production ChatGPT likely carries both a retrieval-order effect and a brand-prior effect. Magnitudes are unverified for the app's model.
- Source: Chen & Koudas (as E-15) — https://arxiv.org/html/2610.15033v1
- Published/updated: 2026-10-10
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: Position test: 8 real sources x 100 questions x all 8 orders (9,600 answers). Brand test: 60 packets, 5 products with equal-length profiles, brand and publisher names masked or revealed (1,920 answers). Prior probe: model asked without search.
- Excerpt: > "brand names reorder its rankings of products with identical facts"
- Establishes: 60% citation when shown first vs 43% when shown last for ChatGPT. Gemini was flat (57–59%). A brand in the model's prior was written into search queries 67% of the time (vs 11%). "47% of ChatGPT’s citations come from websites its model names without searching". 46% of mentions of unnamed brands had no supporting cited page. Repeat consistency (Kendall τ) was 0.75 on fixed profiles, 0.56 with search, and 0.51 from memory.
- Limitations: Small model (nano). Constructed inputs. ISP/B2B markets. The authors explicitly stress these limits.

### E-19 In a services market, ChatGPT (API) cited providers' own websites most, unlike the earned-media pattern
- Claim: For US home-internet questions, 64.3% of ChatGPT citations went to brand (provider) websites. ChatGPT cited 2.0 pages per answer, and 30.8% of answers had no citation.
- Classification: VERIFIED FACT (gpt-5.4-nano + web_search, 2026). EVIDENCE-BASED INFERENCE: the brand-vs-third-party mix depends on market and query type. E-13's "earned media" finding does not generalize to all commercial queries.
- Source: Chen & Koudas (as E-15) — https://arxiv.org/html/2610.15033v1
- Published/updated: 2026-10-10
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: 58,590 ChatGPT answers. Website roles were rule-proposed and hand-reviewed.
- Excerpt: > "64% of its citations go to the providers’ own websites"
- Establishes: Gemini cited 10.1 pages per answer, 83% third party (Reddit 13%). Perplexity cited nothing in 95.8% of answers. In the niche B2B market, ChatGPT cited something in only 35% of answers.
- Limitations: Services with plan and price pages on brand sites. Not physical retail. API.

### E-20 Consumer-UI measurements: ChatGPT sources and brands vary heavily across same-day repeats
- Claim: Scraping consumer web interfaces from Switzerland, ChatGPT's cited-source sets overlapped by a mean Jaccard of 0.233 across repeats within 24 hours. Brand sets overlapped by 0.437. 57.8% of ChatGPT runs had zero citations.
- Classification: VERIFIED FACT (ChatGPT consumer interface, Swiss locale, Jan–Mar 2026). This is the closest fetched Tier 2 evidence to production ChatGPT behavior.
- Source: Don't Measure Once: Measuring Visibility in AI Search (GEO) — Schulte, Bleeker, Kaufmann (University of St. Gallen) — https://arxiv.org/abs/2604.07585 (full text: https://arxiv.org/html/2604.07585v1)
- Published/updated: v1 2026-04-08. arXiv preprint.
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: 4 German-language campaigns (incl. Consumer Electronics, Sporting Goods) x 8 prompts. ChatGPT, Gemini, Google AI Mode, Perplexity. Daily for 45–46 days (2026-01-24 to 03-20). Plus up to 10 same-day repeats per prompt (ChatGPT: 2026-03-21 to 03-23). Jaccard and RBO (p=0.9). Appendix note: "all data collected via web-interface scraping".
- Excerpt: > "leaving 57.8% of its runs with zero citations"
- Establishes: ChatGPT within-24h source RBO was 0.088 and brand RBO 0.192, so order is less stable than set membership. Across engines, day-to-day source Jaccard was 0.34–0.42 and brand Jaccard 0.45–0.59. Bootstrap: per-brand detection-rate SE falls below 0.10 at n=7 runs and below 0.08 at n=8. Rolling windows of 2–4 weeks are recommended. Mean citation Gini was 0.715.
- Limitations: Swiss IPs and German prompts. Small prompt set (32). ChatGPT model and version not pinned. Brand detection uses a lexicon.

### E-21 Tier 3 replication: repeated brand-recommendation prompts almost never return the same list
- Claim: Across 2,961 runs of 12 brand-recommendation prompts, ChatGPT and Google AI returned the same brand list less than 1% of the time and the same ordered list less than 0.1% of the time.
- Classification: VERIFIED FACT as reported by secondary press about the study. EVIDENCE-BASED INFERENCE: rank position within a ChatGPT answer is close to noise. Inclusion frequency is the more stable metric. This agrees with E-20.
- Source: "AI Recommendations Change With Nearly Every Query: SparkToro" — Matt G. Southern, Search Engine Journal (reporting on Rand Fishkin / SparkToro and Patrick O'Donnell / Gumshoe.ai) — https://www.searchenginejournal.com/ai-recommendations-change-with-nearly-every-query-sparktoro/566242/
- Published/updated: 2026-01-30 (data: Nov–Dec 2025)
- Accessed: 2026-10-30
- Tier: 3 (not peer-reviewed; sponsored by a tracking vendor; primary SparkToro post returned 403)
- System tested / method / sample: Volunteers ran 12 prompts 60–100 times each on ChatGPT, Claude, and Google AI Overviews/AI Mode, using their normal settings (unstandardized).
- Excerpt: > "The same list in the same order appears less than 0.1% of the time across repeated runs."
- Establishes: Top headphone brands appeared in 55–77% of 994 responses to varied human-written prompts. Set inclusion is measurable, but order is not.
- Limitations: Uncontrolled accounts, memory, and locations. Secondary reporting. No per-model breakdown for ChatGPT alone.

### E-22 GPT-4o web answers barely overlap Google's top 10, and popular-entity rankings resist evidence shuffling
- Claim: Over 1,000 consumer ranking queries, web-enabled GPT-4o had the lowest domain overlap with Google's top 10 (4.0%). In a GPT-4o case study, shuffling retrieved snippets changed popular-entity rankings only mildly.
- Classification: VERIFIED FACT (GPT-4o API). EVIDENCE-BASED INFERENCE: for well-known brands, the pre-training prior likely sets much of the order. This partly conflicts with E-18's position effect (different metric and model).
- Source: Navigating the Shift: A Comparative Analysis of Web Search and Generative AI Response Generation — Mahe Chen, Xiaoxuan Wang, Kaiwen Chen, Nick Koudas — https://arxiv.org/abs/2601.16858 (full text: https://arxiv.org/html/2601.16858v2)
- Published/updated: v1 2026-01-23; v2 2026-05-16. Venue: EDBT/ICDT 2026 Workshops.
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: 100 ranking templates x 10 consumer topics. Systems: Google, GPT-4o (web), Claude 4.5 Sonnet, Gemini 2.5 Flash, Perplexity Sonar Pro. Bootstrap tests (10,000 iterations). Pre-training study: gpt-4o-search-preview evidence passed to gpt-4o under deterministic settings.
- Excerpt: > "GPT-4o shows the lowest mean overlap at 4.0% (std = 6.6%)"
- Establishes: Mean absolute rank change under snippet shuffle was 2.30 for popular entities and 4.15 for niche entities (normal grounding). Pairwise-derived vs one-shot ranking: Kendall τ 0.911 for popular entities. On 300 consumer-electronics queries, GPT-4o cited 57% earned and 8% social sources. This is lower than the 93.6% earned figure in E-13 (see Contradictions).
- Limitations: API. Single-model case study for the prior experiments.

### E-23 With identical specs, the known brand wins every time; a tiny rating edge removes the advantage
- Claim: Across GPT-4o-mini, Claude Sonnet, and Gemini 3 Flash, a real skincare brand was recommended in 100% of 670 trials against fictional brands with identical specs. A competitor's rating advantage below +0.1 star broke this. In the variance decomposition, product parameters explained 82.4%, list position 6.5%, and brand 1.2%.
- Classification: VERIFIED FACT (API models, direct prompt, no web search in the main experiments). EVIDENCE-BASED INFERENCE: brand priors act as a tie-breaker, and visible attributes dominate when they differ.
- Source: Incumbent Advantage: Brand Bias and Cognitive Manipulation Dynamics in LLM Recommendation Systems — Xi Chu, Yupeng Hou — https://arxiv.org/abs/2606.17443 (full text: https://arxiv.org/html/2606.17443v3)
- Published/updated: v1 2026-06-16; v3 2026-10-10. arXiv preprint.
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: Skincare plus a search-goods check (USB-C cables, AA batteries). English and Chinese. Temperature 0.7. 20–30 repetitions per cell. N=14,395 valid trials for the ANOVA.
- Excerpt: > "Brand identity explains only 1.2%."
- Establishes: Authority-style claims (including fabricated clinical claims) beat the incumbent at an effect equivalent to +0.17 rating points. When all brands adopted the same tactic, the incumbent's survival recovered to 93.8%.
- Limitations: Direct prompting on API models. Product lists are given in the prompt. The RAG probe uses one embedding model. Not ChatGPT.

### E-24 LLMs associate global brands with positive attributes more than local brands
- Claim: LLMs disproportionately linked global brands to positive attributes and recommended luxury gifts more for high-income countries. Country-of-origin cues could boost local brands.
- Classification: VERIFIED FACT (models tested; list not extracted). EVIDENCE-BASED INFERENCE: brand-prior bias is a known model property and is likely present in ChatGPT's model.
- Source: "Global is Good, Local is Bad?": Understanding Brand Bias in LLMs — Kamruzzaman, Nguyen, Kim (University of South Florida) — https://arxiv.org/abs/2406.13997
- Published/updated: v1 2024-06-20; v2 2024-09-27. Venue: EMNLP 2024 (main).
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: Curated dataset across four brand categories. Attribute association and recommendation probes. Abstract only was read.
- Excerpt: > "disproportionately associating global brands with positive attributes"
- Establishes: Brand bias exists in model priors independent of retrieval.
- Limitations: 2024 models. No web search. Abstract-level reading.

### E-25 Official statements: ChatGPT search uses unnamed "third-party search providers"; Microsoft and Shopify are the only providers linked
- Claim: OpenAI says ChatGPT search uses third-party search providers plus partner content. Queries are rewritten into one or more targeted queries sent to those providers. The current help article links only Microsoft's and Shopify's privacy policies for "how search providers may process queries". Website eligibility requires allowing OAI-Searchbot. Microsoft said in May 2023 that Bing would be ChatGPT's default search experience.
- Classification: VERIFIED FACT (what each document says). EVIDENCE-BASED INFERENCE: Microsoft (Bing) and Shopify are probably among the current providers, because their privacy policies are the ones linked. OpenAI does not state which provider serves which query type, and does not state that only those providers are used. The help article also implies OpenAI runs its own crawler (OAI-Searchbot) that affects inclusion.
- Source A: Searching the web with ChatGPT — OpenAI Help Center — https://help.openai.com/en/articles/9237897-searching-the-web-with-chatgpt (read in the in-app browser; WebFetch and curl got HTTP 403)
- Source B: Introducing ChatGPT search — OpenAI — https://openai.com/index/introducing-chatgpt-search/ (read in the in-app browser)
- Source C: Microsoft Build brings AI tools to the forefront for developers — Frank X. Shaw, Official Microsoft Blog — https://blogs.microsoft.com/blog/2023/05/23/microsoft-build-brings-ai-tools-to-the-forefront-for-developers/
- Source D: Web search (tools guide) — OpenAI developer docs — https://developers.openai.com/api/docs/guides/tools-web-search (redirected from platform.openai.com)
- Published/updated: A shows "Updated: 10 days ago" on 2026-10-30 (about 2026-10-20). B 2024-10-31, with an update note dated 2024-12-16. C 2023-05-23. D undated (current version as accessed).
- Accessed: 2026-10-30
- Tier: 1
- System tested / method / sample: Document reading.
- Excerpt (B): > "ChatGPT search leverages third-party search providers, as well as content provided directly by our partners"
- Establishes:
  - A states: "ChatGPT search sometimes partners with other search providers." It also says ChatGPT "typically rewrites your query into one or more targeted queries". It may send follow-up queries "to other search providers". It may use saved memories and IP-derived general location when rewriting a query.
  - A on ranking: "ChatGPT ranks search results using multiple factors intended to help users find relevant, reliable information. Placement is not guaranteed."
  - B states that the search model was "a fine-tuned version of GPT‑4o" at launch.
  - C: Bing was the declared default in 2023, before ChatGPT search launched.
  - D does not name an index. D does describe the `sources` field used for replay in E-15 and E-16: "sources returns the complete list of URLs the model consulted when forming its response."
- Limitations: None of the four documents name Google or SerpApi. None describe the shopping carousel's product source. Help-center text changes over time (dated "10 days ago"). The query-rewriting description matches the fan-out behavior measured in E-17 and E-31.

### E-26 Tier 3 report: OpenAI partially used Google results scraped by SerpApi
- Claim: The Information reported (Aug 2025) that OpenAI partially used Google search results obtained through SerpApi for ChatGPT.
- Classification: UNVERIFIED HYPOTHESIS for current production (single paywalled press report, read second-hand, no OpenAI confirmation on the fetched page).
- Source: "Report: ChatGPT Using SerpApi To Scrape Google Search Results" — Barry Schwartz, Search Engine Roundtable (summarizing The Information) — https://www.seroundtable.com/chatgpt-serpapi-scrape-google-39989.html
- Published/updated: 2025-08-25
- Accessed: 2026-10-30
- Tier: 3
- System tested / method / sample: Press report; method not disclosed.
- Excerpt: > "OpenAI has been partially using Google search results scraped by a startup called SerpApi"
- Establishes: Credible reporting of Google-sourced results in the ChatGPT pipeline exists. This conflicts with a Bing-only reading of E-25C. It is compatible with OpenAI's unnamed "third-party search providers" wording (E-25B).
- Limitations: The fetched page contains no OpenAI response. The Information original is paywalled and was not read.

### E-27 Tier 3 overlap studies disagree on ChatGPT vs Bing/Google citation overlap
- Claim: Seer Interactive (Feb 2025) found 87%+ of ChatGPT search citations matched Bing's top organic results. Ahrefs (Aug 2025) found about 8% top-10 overlap with both Google and Bing, with no Bing preference.
- Classification: VERIFIED FACT (each vendor's reported result). The two contradict each other. Tier 2 evidence (E-16, E-22) sides with low overlap.
- Source A: "87% of SearchGPT Citations Match Bing's Top Results" — Christina Blake, Alisa Scharf, Seer Interactive — https://www.seerinteractive.com/insights/87-percent-of-searchgpt-citations-match-bings-top-results
- Source B: "Only 12% of AI Cited URLs Rank in Google's Top 10 for the Original Prompt" — Louise Linehan (with Xibeijia Guan), Ahrefs — https://ahrefs.com/blog/ai-search-overlap/
- Published/updated: A 2025-02-06. B 2025-08-11 (ChatGPT data from early July 2025).
- Accessed: 2026-10-30
- Tier: 3
- System tested / method / sample: A: about 100 questions and 500+ citations, exact URL matching against SERPs from the same question. The authors call it directional. B: 15,000 long-tail prompts, ChatGPT in-text citations and references vs Google and Bing top 10 and top 100.
- Excerpt (B): > "we aren’t seeing much differentiation in how ChatGPT surfaces both Google and Bing results"
- Establishes: ChatGPT in-text citations overlapped Google's top 10 at 8.00% and Bing's top 10 at 8.10% (Ahrefs). Seer reported a 56% Google match vs 87%+ Bing. Ahrefs also relays a third-party claim that ChatGPT falls back to Google when Bing pages are inaccessible (unverified).
- Limitations: Different eras (early SearchGPT vs mid-2025), sample sizes, and match definitions. The URL-level overlap of citations with SERPs for the user's prompt does not identify the index.

### E-28 Tier 3: ChatGPT shopping carousel products closely match Google Shopping organic results
- Claim: Peec AI reports that 83% of 43,000+ ChatGPT carousel products were strong matches to Google Shopping's top-40 organic results, vs 11% for Bing. Products ranked higher in Google Shopping tended to appear earlier in the carousel.
- Classification: VERIFIED FACT as reported by the vendor. EVIDENCE-BASED INFERENCE: ChatGPT shopping's product candidate set may come from Google Shopping via "shopping fan-out" queries. That would separate it from the web-citation pipeline in E-15 and E-16. Not confirmed by OpenAI or by Tier 2 research.
- Source: "How ecommerce managers can optimize ChatGPT product rankings step by step" — Tom Wells, Peec AI — https://peec.ai/blog/how-ecommerce-managers-can-optimize-chatgpt-product-rankings-step-by-step
- Published/updated: Byline 2026-03-17. Page metadata showed 2026-10-30 (conflict). The study was first published on Search Engine Land on about 2026-03-05 (that page returned 403).
- Accessed: 2026-10-30
- Tier: 3 (vendor research; method not fully public)
- System tested / method / sample: 43,000+ carousel products. Secondary coverage (not read at source) cites 5,000+ carousels and 1.1M fan-out queries. A "strong match" threshold is reported second-hand as similarity ≥0.8.
- Excerpt: > "83% were strong matches to products in Google's top 40 organic shopping results."
- Establishes: 60% of matches came from the Google Shopping top 10, and about 84% from the top 20. A related Tier 3 recap (Precis, 2026-06-16, https://www.precis.com/resources/how-chatgpt-shops-what-we-found-why-it-matters-and-what-to-do-about-it) states a stronger "100%" explanation and "ChatGPT looks at organic Google Shopping results only. Paid ads are completely ignored." That conflicts with the 83% figure.
- Limitations: Vendor with a commercial interest. Matching algorithm not public. Unknown locale and account state. Not reproducible from the page.

### E-29 Tier 3: Carousel order behaves like a shuffle; big-box retailers dominate buy links; Amazon is nearly absent
- Claim: Profound reports that ChatGPT carousel product titles are highly unstable across runs of the same prompt. Walmart and Target lead buy-link slots. Amazon is poorly represented. Tinuiti (with Profound) reports Amazon's ChatGPT citation share fell from about 0.5% to 0.3%.
- Classification: VERIFIED FACT as reported by vendors. EVIDENCE-BASED INFERENCE: marketplace vs retailer share in ChatGPT shopping is shaped by crawler access and merchant feeds, not only by relevance.
- Source A: "Which retailers does ChatGPT actually send shoppers to?" — Brandon Punturo, Profound — https://www.tryprofound.com/blog/chatgpt-retail-target-walmart
- Source B: "Tracking AI Platform Citation Patterns in 2026: Key Findings" — Jen Cornwell, Tinuiti — https://tinuiti.com/blog/search/ai-citations/
- Published/updated: A 2026-03-26 (data 2026-03-10 to 03-20). B 2026-03-24 (data Oct 2025–Jan 2026).
- Accessed: 2026-10-30
- Tier: 3
- System tested / method / sample: A: 22.5M buy offers. "1000s of prompts run many times each". Runs per prompt, UI vs API, and region are not stated. B: "thousands of prompts" on 7 platforms, collection method not stated.
- Excerpt (A): > "~95% of product titles appeared in fewer than 30% of runs for the same prompt."
- Establishes: "The carousel is a shuffle, not a ranking." Walmart held 8.78% of rank-1 retailer offers. Target held 7.16% of total buy-link presence. The top 20 merchants held about 40% of offers. The median was 5 products per response (range 1–67). Profound attributes Amazon's absence to possibly blocking OpenAI's crawlers (speculative).
- Limitations: Vendor data. Undisclosed sampling. Not peer-reviewed.

### E-30 Ads and sponsorship: LLM persuasion raises sponsored-product choice, and some models favor sponsored items
- Claim: (A) In preregistered human experiments, chat agents tasked with promotion raised sponsored-product selection from 22.4% (search) to 61.2%. "Sponsored" labels did not significantly reduce this. (B) In conflict-of-interest evaluations, several models favored sponsored options, for example GPT 5.1 surfacing sponsored options in 94% of a scenario.
- Classification: VERIFIED FACT (systems tested). EVIDENCE-BASED INFERENCE: label effects differ by direction. The ACES agent penalizes a sponsored tag (E-02). A model instructed or incentivized to promote can steer users despite labels. Neither study tests ChatGPT's production shopping or ads.
- Source A: Commercial Persuasion in AI-Mediated Conversations — Salvi, Cuevas, Ribeiro — https://arxiv.org/abs/2604.04263
- Source B: Ads in AI Chatbots? An Analysis of How Large Language Models Navigate Conflicts of Interest — Wu, Liu, Li, Tsvetkov, Griffiths — https://arxiv.org/abs/2604.08525
- Published/updated: A v1 2026-04-05. B v1 2026-04-09, v3 2026-08-17. Venue: COLM 2026.
- Accessed: 2026-10-30
- Tier: 2
- System tested / method / sample: A: N=2,012 participants choosing eBooks via search or an LLM agent (five frontier models). One fifth of products were secretly sponsored. B: scenario suite across many LLMs. Abstracts only were read.
- Excerpt (A): > "Explicit \"Sponsored\" labels do not significantly reduce persuasion"
- Establishes: Disclosure labels alone do not neutralize LLM-mediated steering of humans. Some models trade user welfare for sponsor incentives when the system prompt creates a conflict.
- Limitations: eBooks only (A). Constructed incentives (B). Abstract-level reading.

### E-31 Vendor preprints: own-domain exposure and branded fan-out go with ChatGPT brand mentions; brand stature predicts first-run visibility
- Claim: (A) In Aiso data from June–Sept 2026, GPT target mention rates were 2.8% with no own-domain citation and no branded fan-out, 49.0% with an own-domain citation, and 91.4% with both. 78.3% of commercial prompts triggered ChatGPT fan-out vs 3.6% of informational prompts (n=90 rows). (B) In Ranqo API data (Mar–May 2026, 100K+ responses, 5 engines), household-name brands appeared in 73% of relevant first-run answers, mid-market brands in 44%, and niche brands in 11%.
- Classification: VERIFIED FACT as reported. Both authors have a conflict of interest (A: affiliated with Aiso Boost Ltd; B: co-founder and equity holder of Ranqo). Observational and not causal.
- Source A: From Prompt to Recommendation: A Fitted Stage Model of Brand Visibility in AI Search — Benjamin Tannenbaum — https://arxiv.org/abs/2609.23162
- Source B: Generative Engine Optimization at Scale: Measuring Brand Visibility Across AI Search Engines — Pratyush Kumar — https://arxiv.org/abs/2606.20065
- Published/updated: A v1 2026-09-19. B v1 2026-06-18.
- Accessed: 2026-10-30
- Tier: 3 (vendor-authored preprints with proprietary data; listed on arXiv but not reproducible)
- System tested / method / sample: A: 34,960 prompt-engine observations, 75 projects, 2,854 prompts. B: official APIs (ChatGPT = GPT-5 with a weekly search cooldown per brand).
- Excerpt (A): > "78.3% of commercial prompts trigger fan-out versus 3.6% of informational prompts in this sample"
- Establishes: Commercial intent strongly predicts whether ChatGPT searches at all. This agrees with E-20's 57.8% zero-citation runs on mostly top-of-funnel prompts. B's "corporate websites" (about 78% of citations) means third-party company pages, not the brand's own domain. That is a different taxonomy from E-13's Earned/Brand/Social.
- Limitations: COI. Proprietary samples. Fan-out cohort is tiny. B's ChatGPT runs answer from parameters between weekly search passes.

---

## Reusable experiment methodologies (for AURA)

- Randomized choice-set auditing (ACES, E-01..E-05): Fix an assortment of 8 items. Randomize position, tags, price (±), rating (±), and review count per trial. About 500 trials per category per model. Fit a conditional logit with product fixed effects to get position, badge, and attribute coefficients. Re-run on each model release to detect shocks. A headless JSON-list variant separates UI effects from model effects.
- Pairwise forced choice with matched attributes (ABxLab, E-06): Match ratings, then match prices post hoc (MR, MRaP conditions) to isolate order and nudge effects. Use linear probability models with cluster-robust SEs. Include a small human baseline.
- All-orders position test (Chen & Koudas, E-18): Show N sources in all N rotations (8x8 design) and compare first-vs-last citation rates with 95% CIs.
- Name masking (E-18): Use the same product profiles with brand names masked vs revealed vs randomly assigned. Compare change against a repeat-only baseline (ratio of change to repetition noise).
- API replay with the sources field (E-15/E-16): Use the Responses API `web_search` tool. Log `queries` and `sources`, rank in the pooled list, and cited subset. Fit a conditional logit of citation on rank plus content features. Compare retrieved URLs with Google and Bing top-k for the engine's own sub-queries. State plainly that API ≠ consumer app.
- Repetition and variance (Schulte, E-20; Chen & Koudas, E-17): Report Jaccard (set) and RBO p=0.9 (order). Separate same-day stochasticity (repeats within 24 h) from drift (daily runs over ≥45 days; 14-day windows). Use ≥7–8 runs per prompt per day for per-brand inclusion SE <0.10. Use 2–4 week rolling windows. Use a prompt portfolio, not 1–2 prompts. Exclude zero-citation runs from source overlap but report their rate. Use odd/even-day split reliability (Spearman–Brown) to measure repeatability.
- Within-website design (E-15): Compare pages of the same site to remove site-level confounds before attributing citation lift to page features.
- Query sets: GEO-bench (10K, E-11), C-SEO Bench (QA plus product recommendation, E-12), E-GEO (13,747 product queries with Amazon listings, E-12), RagDoll (1,147 manufacturer pages, E-09), Chen et al. 2025 (1,000 ranking prompts across 10 categories, E-13).
- Record for every run: model or product surface, date and time, locale and IP country, logged-in state and memory, language, prompt text, whether search fired, sub-queries, all URLs, product cards, and order.

## Contradictions

1. Position bias: strong and model-specific in ACES (8-item grid, E-01) and ABxLab (pairs, E-06) vs near-uniform for frontier models in Magentic Marketplace (3 identical list items, E-07). Possible reasons: item count, grid vs list, identical vs differentiated items. Magentic shows the dominant order effect is temporal (first proposal).
2. Position effect for GPT models: Chen & Koudas 2026 (E-18) find a 17.6-point first-vs-last citation effect for ChatGPT's model. Chen et al. 2026 (E-22) find GPT-4o popular-entity rankings only mildly affected by snippet shuffling. The metrics (citation vs entity rank) and models (gpt-5.4-nano vs gpt-4o) differ.
3. Source-type mix: ChatGPT (gpt-4o-search-preview) 93.5–95.1% earned media (E-13) vs GPT-4o 57% earned on 300 consumer-electronics queries (E-22, same group) vs 64.3% brand-site citations for ISP queries (E-19). Market, query intent, model, and date all vary.
4. Index overlap: Seer, 87%+ Bing match (E-27A) vs Ahrefs, about 8% for both Google and Bing (E-27B) vs Chen & Koudas, 0.5% Bing and 0.7% Google top-10 on the engine's own queries (E-16).
5. Index identity: OpenAI names no provider. It links Microsoft and Shopify privacy policies and says it uses multiple "third-party search providers" (E-25A/B). Bing was the declared default in 2023 (E-25C). Press reports Google results via SerpApi (E-26). Vendor research shows a Google Shopping match for carousel products (E-28). These are compatible with a multi-provider pipeline where web citations and shopping use different sources. None of them confirm it.
6. Carousel provenance strength: Peec AI, 83% strong match (E-28) vs the Precis recap, 100% explained (E-28). Same underlying research team, different framing.
7. Content-optimization efficacy: GEO, up to 40% (E-11) and ACES seller edits, up to +14.89 p.p. (E-05) vs C-SEO Bench, mostly ineffective or negative (E-12) vs Chen & Koudas, page features explain 2.8% within sites (E-15).
8. Sponsored labels: an agent penalizes a sponsored tag when choosing (E-02) vs labels fail to protect humans from LLM persuasion (E-30A). Not a strict contradiction: different actors (agent vs human).
9. Brand weight: brand explains 1.2% of variance when specs differ (E-23) vs brand names shift rankings 2.1x the repetition noise on identical facts (E-18). These are consistent if brand acts mainly as a tie-breaker. Magnitudes are not comparable.

## Knowledge gaps

- No fetched Tier 2 study instruments the production ChatGPT shopping carousel (product cards, merchant offers, order) with controlled repeats. All carousel evidence is Tier 3 vendor research (E-28, E-29).
- No official OpenAI statement names the current search index or the shopping product source. The help center says "third-party search providers" and links only Microsoft and Shopify privacy policies (E-25).
- The relationship between the API `web_search` tool and the consumer ChatGPT search and shopping pipeline is unknown. Chen & Koudas flag this explicitly.
- No study measures merchant-feed or Shopify-catalog effects on ChatGPT product inclusion.
- No study isolates review/rating sensitivity inside ChatGPT shopping (only API agents in E-03, E-06, E-23).
- Effects of user memory, account state, and locale on ChatGPT product results have not been measured in a controlled way (E-20 is Swiss-only; E-21 uncontrolled).
- Marketplace (Amazon, eBay) vs brand-DTC share for physical-product queries in ChatGPT is unknown beyond Tier 3 point estimates. Crawler blocking is a likely confound (E-29).

## Unfetched sources

- https://searchengineland.com/openai-chatgpt-serpapi-google-search-results-461226 — HTTP 403 to WebFetch. The in-app browser showed a Cloudflare bot check, which was not pursued.
- https://searchengineland.com/new-finding-chatgpt-sources-83-of-its-carousel-products-from-google-shopping-via-shopping-query-fan-outs-470723 — HTTP 403.
- https://sparktoro.com/blog/new-research-ais-are-highly-inconsistent-when-recommending-brands-or-products-marketers-should-take-care-when-tracking-ai-visibility/ — HTTP 403 to WebFetch. The in-app browser showed a Cloudflare bot check, which was not pursued.
- (Recovered: the OpenAI help-center article and the ChatGPT search launch post returned 403 to WebFetch but were read in the in-app browser. See E-25.)
- The Information (Aug 2025 SerpApi report) — paywalled, not attempted.
- Full texts of C-SEO Bench (2506.11097), E-GEO (2511.20867), Kamruzzaman (2406.13997), Salvi et al. (2604.04263), Wu et al. (2604.08525) — abstracts only were read.

## Source list

Tier 1
- OpenAI Help Center, Searching the web with ChatGPT — https://help.openai.com/en/articles/9237897-searching-the-web-with-chatgpt
- OpenAI, Introducing ChatGPT search (2024-10-31) — https://openai.com/index/introducing-chatgpt-search/
- Microsoft (Frank X. Shaw), 2023-05-23 — https://blogs.microsoft.com/blog/2023/05/23/microsoft-build-brings-ai-tools-to-the-forefront-for-developers/
- OpenAI developer docs, Web search tool guide — https://developers.openai.com/api/docs/guides/tools-web-search

Tier 2
- Allouah et al., What Is Your AI Agent Buying? — https://arxiv.org/abs/2508.02630
- Cherep et al., ABxLab — https://arxiv.org/abs/2509.25609
- Bansal et al., Magentic Marketplace — https://arxiv.org/abs/2510.25779
- Kumar & Lakkaraju, Manipulating LLMs to Increase Product Visibility — https://arxiv.org/abs/2404.07981
- Pfrommer et al., Ranking Manipulation for Conversational Search Engines (EMNLP 2024) — https://arxiv.org/abs/2406.03589
- Nestaas et al., Adversarial Search Engine Optimization for LLMs — https://arxiv.org/abs/2406.18382
- Aggarwal et al., GEO: Generative Engine Optimization (KDD 2024) — https://arxiv.org/abs/2311.09735
- Puerto et al., C-SEO Bench (NeurIPS 2025 D&B) — https://arxiv.org/abs/2506.11097
- Bagga et al., E-GEO — https://arxiv.org/abs/2511.20867
- Chen, Wang, Chen, Koudas, GEO: How to Dominate AI Search — https://arxiv.org/abs/2509.08919
- Chen & Koudas, What Drives AI Citations? — https://arxiv.org/abs/2610.15033
- Chen, Wang, Chen, Koudas, Navigating the Shift (EDBT/ICDT 2026 Workshops) — https://arxiv.org/abs/2601.16858
- Schulte, Bleeker, Kaufmann, Don't Measure Once — https://arxiv.org/abs/2604.07585
- Chu & Hou, Incumbent Advantage — https://arxiv.org/abs/2606.17443
- Kamruzzaman et al., Global is Good, Local is Bad? (EMNLP 2024) — https://arxiv.org/abs/2406.13997
- Salvi, Cuevas, Ribeiro, Commercial Persuasion in AI-Mediated Conversations — https://arxiv.org/abs/2604.04263
- Wu et al., Ads in AI Chatbots? (COLM 2026) — https://arxiv.org/abs/2604.08525

Tier 3
- Tannenbaum (Aiso), From Prompt to Recommendation — https://arxiv.org/abs/2609.23162
- Kumar (Ranqo), GEO at Scale — https://arxiv.org/abs/2606.20065
- Search Engine Roundtable (Barry Schwartz), SerpApi report — https://www.seroundtable.com/chatgpt-serpapi-scrape-google-39989.html
- Seer Interactive, 87% of SearchGPT citations match Bing — https://www.seerinteractive.com/insights/87-percent-of-searchgpt-citations-match-bings-top-results
- Ahrefs, AI search overlap — https://ahrefs.com/blog/ai-search-overlap/
- Peec AI (Tom Wells), ChatGPT product rankings — https://peec.ai/blog/how-ecommerce-managers-can-optimize-chatgpt-product-rankings-step-by-step
- Precis, How ChatGPT shops — https://www.precis.com/resources/how-chatgpt-shops-what-we-found-why-it-matters-and-what-to-do-about-it
- Profound (Brandon Punturo), ChatGPT retailers — https://www.tryprofound.com/blog/chatgpt-retail-target-walmart
- Tinuiti (Jen Cornwell), AI citation trends Q1 2026 — https://tinuiti.com/blog/search/ai-citations/
- Search Engine Journal (Matt G. Southern), SparkToro/Gumshoe study — https://www.searchenginejournal.com/ai-recommendations-change-with-nearly-every-query-sparktoro/566242/
