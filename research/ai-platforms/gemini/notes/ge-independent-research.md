# GE: Independent (non-Google) evidence on how Gemini, AI Mode and AI Overviews select and rank products and sources

- Agent: GE (AURA research)
- Date: 2026-10-30
- Scope: Tier 2 research (arXiv, peer-reviewed, reproducible experiments) and the most credible Tier 3 analyses on how Google's AI surfaces select and rank products and sources. Surfaces: the Gemini API (with and without Google Search grounding), the Gemini consumer app, Google AI Overviews (AIO) and Google AI Mode. Google first-party docs are out of scope here, except where a study quotes them.
- Method:
  - arXiv HTML pages were downloaded with curl and converted to text locally. arXiv excerpts below were string-matched against that text. They are verbatim except for collapsed line breaks. Where the HTML renders a value from LaTeX math, the excerpt shows the rendered value (for example `53%` for `53\%`); this is noted per finding.
  - Non-arXiv pages were read with WebFetch. Their excerpts are verbatim as returned by WebFetch extraction. They were not byte-verified.
  - Papers already summarized in `research/ai-platforms/chatgpt/notes/e-independent-research.md` (E-xx IDs) were re-fetched in this session. Only their Gemini- or Google-specific results are extracted here.
- Classification labels: VERIFIED FACT = the source states this result for the system it tested. EVIDENCE-BASED INFERENCE = what it suggests about Gemini, AI Mode or AIO in production. UNVERIFIED HYPOTHESIS = plausible, not tested.
- Core caveat for the whole file: most Gemini results come from the Gemini API (often a small Flash or Flash-Lite model) with Google Search grounding, or from API models without search on constructed inputs. An API result is not evidence of the Gemini app's, AI Mode's or AIO's production ranking. AIO studies mostly use SerpApi or headless browsers, logged out, from one US location. No fetched Tier 2 study instruments AI Mode product cards or Google Shopping-backed product results under controlled conditions.

---

## Findings

### GE-01 Gemini 2.5 Flash as a shopping agent: position effects exist but are weaker and differently shaped than for Claude or GPT
- Claim: In the ACES mock store, Gemini 2.5 Flash preferred the top row and the third and fourth columns. Moving a product from row 2 to row 1 was worth only about +17% in price, against about a doubling for Claude Sonnet 4 and GPT-4.1.
- Classification: VERIFIED FACT (Gemini 2.5 Flash via API, VLM agent on a mock grid). EVIDENCE-BASED INFERENCE: if a Gemini model chooses among products on a page, slot position changes its choice. The size and shape do not transfer to the Gemini app or AI Mode.
- Surface/system tested: Gemini 2.5 Flash API (reasoning tokens omitted), computer-use agent on a 2x4 product grid. Also a "headless" JSON-list variant.
- Source: What Is Your AI Agent Buying? Evaluation, Biases, Model Dependence, & Emerging Implications for Agentic E-Commerce — Allouah, Besbes, Figueroa, Kanoria, Kumar — https://arxiv.org/html/2508.02630v3
- Published/updated: v1 2025-08-04; v3 2025-12-17. arXiv preprint.
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: 8 products per category, 8 categories. Positions, tags, prices, ratings and review counts randomized per trial. Conditional logit with product fixed effects. Gemini 2.5 Flash ran 100 headless experiments per category "due to latency" (500 for Claude and GPT).
- Excerpt: > "Gemini 2.5 Flash tilts toward the third and fourth columns"
- Establishes: All three Aug-2025 models showed a top-row premium. In the headless list, "Gemini 2.5 Flash peaks at Position 3 and is comparatively neutral or negative elsewhere." Prompting the agent to ignore position attenuated Gemini's top-row and column-2 coefficients but raised its column-3 bias. For Claude and GPT the same prompt had no significant effect.
- Limitations: Mock store from Amazon listings. One-shot choice, generic prompt, no conversation. Not the Gemini app, not AI Mode.

### GE-02 Gemini 3 Pro Preview has the strongest top-row preference of the tested frontier models
- Claim: For Gemini 3.0 Pro Preview, the Row 1 coefficient was 2.146, against 0.467 (Claude Opus 4.5) and −0.701 (GPT-5.1). Row 1 vs Row 2 was worth +159.7% in price for Gemini 3 Pro Preview.
- Classification: VERIFIED FACT (gemini-3-pro-preview via API, Dec 2025). EVIDENCE-BASED INFERENCE: newer Gemini models can carry larger position effects than older ones. Position effects are model-version properties.
- Surface/system tested: gemini-3-pro-preview API, ACES VLM agent.
- Source: Allouah et al. (as GE-01) — https://arxiv.org/html/2508.02630v3 (Table 3, Table 11)
- Published/updated: v3 2025-12-17
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: 22,960 observations for Gemini 3.0 Pro Preview in the conditional logit (Table 3).
- Excerpt: > "For every upgrade the position bias changed."
- Establishes: Gemini 3 Pro Preview column coefficients were positive for columns 1 and 3 (0.452, 0.445). Claude Opus 4.5 and GPT-5.1 had negative column coefficients. Position preference reversed direction between providers and between generations.
- Limitations: Preview model. Low reasoning setting. Table-only values (no narrative discussion of Gemini 3 position in the text).

### GE-03 A Gemini preview-to-GA model change inverted position bias and reshuffled product shares
- Claim: When Gemini 2.5 Flash Preview was replaced by Gemini 2.5 Flash (GA), the top-row bias flipped from negative to positive. Modal products changed in several categories.
- Classification: VERIFIED FACT (gemini-2.5-flash-preview-05-20 vs gemini-2.5-flash, API). EVIDENCE-BASED INFERENCE: a silent model update behind a Google AI surface can move product visibility without any merchant change. AURA baselines must record model version and date.
- Surface/system tested: Gemini 2.5 Flash Preview and GA via API.
- Source: Allouah et al. (as GE-01) — https://arxiv.org/html/2508.02630v3 (Appendix D)
- Published/updated: v3 2025-12-17
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: Natural experiment. A subset of experiments re-run on the GA model with the same catalog.
- Excerpt: > "inverted the model’s position bias from the bottom row to the top row"
- Establishes: Office lamp mode shifted from TORCHSTAR to SUNMORY. Toilet paper mode shifted from Cottonelle to Angel Soft. Fitbit Versa lost 25.1 p.p. and Kenmore lost 25.6 p.p.
- Limitations: Subset re-run. API models only.

### GE-04 Gemini agents penalize a "Sponsored" tag and reward a platform "Overall Pick" badge more than other models do
- Claim: Holding position fixed, a "Sponsored" tag cut a 10%-baseline product to 7.9% for Gemini 2.5 Flash. An "Overall Pick" badge raised it to 42.6%, the largest lift of the three Aug-2025 models. Gemini 3 Pro Preview had the largest sponsored penalty of the Dec-2025 models.
- Classification: VERIFIED FACT (API models in ACES). EVIDENCE-BASED INFERENCE: if a Gemini-based shopping surface shows ad labels or platform badges in the model context, they can change selection. Whether AI Mode passes such labels to the model is not established.
- Surface/system tested: Gemini 2.5 Flash and Gemini 3 Pro Preview API.
- Source: Allouah et al. (as GE-01) — https://arxiv.org/html/2508.02630v3
- Published/updated: v3 2025-12-17
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: Badges randomized per scenario. Conditional logit.
- Excerpt: > "falls to 8.9% under Claude Sonnet 4, 8.0% under GPT-4.1, and 7.9% under Gemini 2.5 Flash"
- Establishes: Headless list: Sponsored 10% → 8.9% and Overall Pick 10% → 72.7% for Gemini 2.5 Flash. Gemini 3 Pro Preview: Sponsored coefficient −0.623 (Claude Opus 4.5 −0.340, GPT-5.1 −0.371). A seller would need a 24.2% price cut to offset the sponsored tag for Gemini 3 Pro Preview (Table 11). Overall Pick was worth +138% price headroom for Gemini 2.5 Flash and +159.3% for Gemini 3 Pro Preview. The scarcity tag was weakly positive for Gemini 3 Pro Preview (0.219, p<0.05) and negative for Claude Opus 4.5.
- Limitations: Badge wording and design are ACES-specific. Tag effects are conditional on position.

### GE-05 Gemini agents are price- and rating-rational, but Gemini 3 Pro weights ratings least
- Claim: Gemini 2.5 Flash and Gemini 3 Pro Preview almost never missed a cheaper or better-rated dominant option. In the conditional logit, Gemini 3 Pro Preview's rating coefficient (4.224) was less than half of Claude Opus 4.5's (11.148) and GPT-5.1's (9.247).
- Classification: VERIFIED FACT (API). EVIDENCE-BASED INFERENCE: Gemini models respond to price and rating in the expected direction. The relative weight of rating vs price differs by model version and cannot be transferred to AI Mode.
- Surface/system tested: Gemini 2.0 Flash, 2.5 Flash, 3 Pro Preview APIs.
- Source: Allouah et al. (as GE-01) — https://arxiv.org/html/2508.02630v3 (Section 5, Tables 3, 8, 9, 11)
- Published/updated: v3 2025-12-17
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: Rationality tests with one correct option. Randomized price and rating perturbations in the main experiment.
- Excerpt: > "An increment of +0.1 in ratings, allows a seller to increase their price by a quarter with Gemini 2.5 Flash"
- Establishes: A +0.1 rating lift took a 10% product to 16.0% (Gemini 2.5 Flash, VLM). For Gemini 3 Pro Preview, +0.1 rating was worth +20.7% in price (Claude Opus 4.5 +80.6%, GPT-5.1 +39.2%). Doubling reviews was worth +17% (Gemini 2.5 Flash) and +22.9% (Gemini 3 Pro Preview). Under an "ignore position & prioritize price" prompt, a 10% price cut raised Gemini 2.5 Flash's choice odds by about 101%. Fail rates for Gemini 2.5 Flash on price and rating dominance tests were 0.0–1.0%.
- Limitations: Small perturbations. Single persona. Selection rates, not purchases.

### GE-06 One listing-text rewrite moved Gemini 2.5 Flash a lot and Gemini 3 Pro Preview not at all
- Claim: An AI-rewritten product description raised the focal product's share by +14.79 p.p. on average for Gemini 2.5 Flash, the largest of the Aug-2025 models. For Gemini 3 Pro Preview the effect was +0.32 p.p. and not significant.
- Classification: VERIFIED FACT (API). EVIDENCE-BASED INFERENCE: text sensitivity of Gemini models is version-specific. A gain measured on one Gemini version may vanish on the next.
- Surface/system tested: Gemini 2.5 Flash (seller agent GPT-4.1) and Gemini 3 Pro Preview (seller agent GPT-5.1).
- Source: Allouah et al. (as GE-01) — https://arxiv.org/html/2508.02630v3 (Section 6, Table 4)
- Published/updated: v3 2025-12-17
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: 200 shuffled trials before and after one description edit, per category.
- Excerpt: > "for Gemini 2.5 Flash, +6.5 p.p. in mousepad, and +52.0 p.p. in office lamp, +29.1 p.p. in toothpaste and +12.0 p.p. in washing machine"
- Establishes: The largest gains came from putting the query term early in the title ("SUNMORY Office Floor Lamp…"). For Gemini 3 Pro Preview, SUNMORY rose only from 0.0% to 7.1%. The mousepad edit reduced share for Gemini 3 Pro Preview.
- Limitations: Mock UI truncates descriptions, which may inflate early-token effects. One seller optimizes.

### GE-07 In an agent marketplace, Gemini 2.5 Flash showed no list-position bias, explored all options, and was vulnerable to strong prompt injection
- Claim: Gemini-2.5-Flash selected three identical businesses at near-uniform rates across list positions. It contacted every business offered. It showed some vulnerability to strong prompt injection (mean payment 1.6 of 3.0 in one scenario).
- Classification: VERIFIED FACT (gemini-2.5-flash API in a synthetic market). EVIDENCE-BASED INFERENCE: weak for AI Mode. The framing (three identical items, agent-to-agent offers) differs from consumer product ranking.
- Surface/system tested: Gemini-2.5-Flash as a customer agent in Magentic Marketplace.
- Source: Magentic Marketplace: An Open-Source Environment for Studying Agentic Markets — Bansal et al. (Microsoft Research) — https://arxiv.org/html/2510.25779v1
- Published/updated: v1 2025-10-27. arXiv preprint.
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: Synthetic restaurant and contractor markets. Position test with three identical businesses.
- Excerpt: > "Gemini-2.5-Flash consistently sent messages to all businesses provided for consideration."
- Establishes: Like all models tested, Gemini-2.5-Flash showed first-proposal bias (60–100% first-proposal selection across models). This contrasts with the strong grid position effects in GE-01..GE-03.
- Limitations: Synthetic services. Microsoft-authored environment. Not a Google surface.

### GE-08 Gemini API with Google grounding cites about 10 pages per answer, mostly third-party, with Reddit at 13%
- Claim: For US home-internet questions, Gemini 3.1 Flash Lite with Google Search grounding cited 10.1 pages per answer. 83% were on third-party websites. Reddit alone took 13%. ChatGPT (API) cited 2.0 pages, 64% on provider sites.
- Classification: VERIFIED FACT (gemini-3.1-flash-lite + Google Search grounding, API, Jun–Sep 2026). EVIDENCE-BASED INFERENCE: Gemini-family grounded answers cite broadly and lean on third-party and forum pages for commercial service questions. Not shown for the Gemini app, AIO or AI Mode, or for physical products.
- Surface/system tested: Gemini API with Google Search grounding, no system prompt, default sampling.
- Source: What Drives AI Citations? Content, Retrieval and Model Knowledge in Generative Engine Optimization (GEO) — Mahe Chen, Nick Koudas (University of Toronto) — https://arxiv.org/html/2610.15033v1
- Published/updated: v1 2026-10-10. arXiv preprint.
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: 651 queries for a US fiber ISP, daily 2026-06-24 to 2026-09-21. Cross-engine comparisons use 26,069 query-days that all three engines answered (Gemini answered only part of the queries until 25 July). Gemini: 26,069 answers, 263,300 citations.
- Excerpt: > "Gemini cites 10.1 pages, 83% of them on third-party websites (Reddit alone 13%)"
- Establishes: Gemini links part of its sources through a redirect service (1.8% of citation rows). In the niche B2B market (55 queries), "Gemini accounts for 84% of the citations".
- Limitations: API, not the app. Services, not physical retail. Queries written for a client.

### GE-09 Pages cited by grounded Gemini rarely appear in Google's own top 10 for Gemini's own sub-queries
- Claim: Only 5.6% of the pages Gemini (API, grounded) cited were in Google's top 10 for Gemini's own sub-queries. 93% were absent from Google's top 50.
- Classification: VERIFIED FACT (API). EVIDENCE-BASED INFERENCE: Google organic page rank is a poor proxy for which pages grounded Gemini cites, even though grounding uses Google Search. Whether AIO and AI Mode behave the same is a separate question (see GE-20, GE-24, GE-25).
- Surface/system tested: gemini-3.1-flash-lite with Google Search grounding; grounding metadata gives queries and sources used (not a ranked list).
- Source: Chen & Koudas (as GE-08) — https://arxiv.org/html/2610.15033v1 (Section 6.3)
- Published/updated: 2026-10-10
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: API replay 13 times on 11 days up to 2026-10-07. Public Google results fetched with a US location within 1–2 days of the replay.
- Excerpt: > "5.6% of those Gemini cites are in the top 10, although Gemini is grounded on Google"
- Establishes: "as are 93% of Gemini’s cited pages" (absent from Google's top 50). The authors state that time and place cannot account for the gap. Rank analyses used ChatGPT only, because Gemini's metadata has no ranked list.
- Limitations: Page-level, not site-level. Does not identify what retrieval Gemini grounding uses beyond the documented tool. API only.

### GE-10 Gemini's model shows no source-position effect, but brand names reorder its product rankings more than ChatGPT's
- Claim: In controlled answer-step tests, Gemini cited the same source at 57–59% in every position (no position effect). Revealing brand names on identical product profiles changed top-3 rates 3.3 times as much as repetition noise (ChatGPT 2.1x).
- Classification: VERIFIED FACT (gemini-3.1-flash-lite without search, constructed inputs). EVIDENCE-BASED INFERENCE: for Gemini-family models, brand identity likely matters more than the order of supplied sources. Magnitudes for larger production models are unverified.
- Surface/system tested: gemini-3.1-flash-lite API, no web search, instructions restricting it to supplied information.
- Source: Chen & Koudas (as GE-08) — https://arxiv.org/html/2610.15033v1 (Section 6.6, Table 4, Appendix D)
- Published/updated: 2026-10-10
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: Position: 8 sources x 100 questions x 8 orders (9,600 answers). Brand/publisher masking: 60 packets, 1,920 answers.
- Excerpt: > "Gemini cites it in 57–59% in every position"
- Establishes: First-minus-last citation difference for Gemini: −0.4 points (95% CI −2.3 to 1.6). Revealing publisher names changed rates 1.6x repetition for Gemini. Gemini declined to choose in 9% of pairwise answers in the stability experiment. In a leak test, Gemini identified well-known providers from masked facts 52–56% of the time (chance about 10%).
- Limitations: Small model (Flash Lite). Constructed inputs. ISP and B2B software markets.

### GE-11 Gemini's model "knows" more brands, and its brand ranking is largely fixed by memory before search
- Claim: The model behind Gemini named the tracked niche B2B vendors for 60–96% of questions without search (ChatGPT's model 2–16%). For large ISPs, one score per brand predicted 92% of Gemini's pairwise orders from memory alone and 89% with search.
- Classification: VERIFIED FACT (gemini-3.1-flash-lite API). EVIDENCE-BASED INFERENCE: for well-known brands, Gemini-family rankings are set mostly by the model prior; retrieved evidence changes them little. For unknown brands, evidence matters more.
- Surface/system tested: gemini-3.1-flash-lite, with and without Google Search grounding.
- Source: Chen & Koudas (as GE-08) — https://arxiv.org/html/2610.15033v1 (Sections 6.5, 7, 8)
- Published/updated: 2026-10-10
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: Prior probe without search. Controlled stability: 20 sets, six brands, 6,000 answers; search version 10,440 answers.
- Excerpt: > "one score per brand predicts 75% of the pairs for ChatGPT and 92% for Gemini"
- Establishes: A cited third-party page naming a vendor raised Gemini's odds of naming it x6.3 (consumer market) and x17.7 (niche market). The slope of answer agreement on source overlap was 0.26 for Gemini vs 1.25 for ChatGPT, so Gemini's ranking depended less on which sources it saw.
- Limitations: Two non-retail markets. Small model. Observational for the collected data.

### GE-12 Grounded Gemini rewrites queries into natural-language sub-questions, and its cited set drifts over weeks
- Claim: Gemini (API) wrote about 3 natural-language sub-questions per question and rarely added a year (2%) or a brand (5%). 47% of within-website citation variation was still shared two weeks later, and 29% ten weeks later.
- Classification: VERIFIED FACT (API). EVIDENCE-BASED INFERENCE: grounded Gemini's query fan-out stays close to the user's wording, unlike ChatGPT's keyword-style fan-out. Citation sets need longitudinal measurement.
- Surface/system tested: gemini-3.1-flash-lite + Google Search grounding.
- Source: Chen & Koudas (as GE-08) — https://arxiv.org/html/2610.15033v1 (Sections 5.3, 6.3)
- Published/updated: 2026-10-10
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: Six 14-day windows over 90 days; replay metadata.
- Excerpt: > "Gemini writes about 3 natural-language sub-questions closer to the question"
- Establishes: Cosine similarity of sub-queries to the question was 0.78 (Gemini) vs 0.66 (ChatGPT). Within a window 63–67% of variation was repeatable across engines.
- Limitations: API. One market for drift.

### GE-13 Page features and grounded Gemini citations: title match and inbound links associate with more citations; schema.org and FAQ blocks show no effect; JavaScript-only text shows fewer
- Claim: Within websites, a one-SD better title match went with +16.8% Gemini citations. More referring websites went with +33.7% per SD for Gemini. FAQ blocks and schema.org markup had no effect for any engine. Pages whose main text needs JavaScript got 10.6% fewer Gemini citations.
- Classification: VERIFIED FACT (observational, API). EVIDENCE-BASED INFERENCE: for grounded Gemini, relevance of title text and link signals matter more than markup. Causality is not established (links measured after citations).
- Surface/system tested: gemini-3.1-flash-lite + Google Search grounding.
- Source: Chen & Koudas (as GE-08) — https://arxiv.org/html/2610.15033v1 (Section 4.1, Appendix Table 8)
- Published/updated: 2026-10-10
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: Within-website models on downloaded pages; DataForSEO link counts.
- Excerpt: > "FAQ blocks and schema.org markup have no effect for any engine."
- Establishes: Best-paragraph match +7.8% per SD for Gemini. JavaScript effect: −10.6% (p=0.008). 19.9% of pages Gemini cited disallowed Googlebot in robots.txt at download time. Forum pages received 78% more citations than articles within websites (all engines).
- Limitations: Observational. Link direction not established. Services market. Schema result concerns citation of web pages, not product feeds or Merchant Center data.

### GE-14 Consumer web UI: Gemini's sources are the most repeatable of four engines; AI Mode concentrates citations most
- Claim: Scraped from Swiss consumer web interfaces, Gemini had the highest within-24h source Jaccard (0.505) of four engines. Google AI Mode had 0.318 and the highest citation concentration (Gini 0.782). Brand-set Jaccard was 0.409 (Gemini) and 0.375 (AI Mode).
- Classification: VERIFIED FACT (Gemini and Google AI Mode web interfaces, Swiss IPs, German prompts, Jan–Mar 2026). This is the closest fetched Tier 2 evidence to production Gemini and AI Mode behavior.
- Surface/system tested: Gemini web app and Google AI Mode web interface ("all data collected via web-interface scraping").
- Source: Don't Measure Once: Measuring Visibility in AI Search (GEO) — Schulte, Bleeker, Kaufmann (University of St. Gallen) — https://arxiv.org/html/2604.07585v1
- Published/updated: v1 2026-04-08. arXiv preprint.
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: 4 campaigns (incl. Consumer Electronics, Sporting Goods) x 8 German prompts. Daily 2026-01-24 to 2026-03-20. Same-day repeats up to 10 per prompt (Gemini 2026-03-22/23; AI Mode 2026-03-24/25).
- Excerpt: > "Google AI Mode exhibits the highest citation concentration (Gini = 0.782)"
- Establishes: Within-24h source RBO: Gemini 0.230, AI Mode 0.254. Brand RBO: Gemini 0.196, AI Mode 0.238. Mean engine Gini: Gemini 0.723. Gemini had data on only 22–26 of 45–46 days ("sporadic gaps"). AI Overviews were collected but excluded as "a distinct Google product".
- Limitations: Small prompt set (32). Model versions not pinned. Lexicon brand detection. Swiss locale. Logged-in state not stated.

### GE-15 Grounded Gemini 2.5 Flash cites more brand-owned and social sources than ChatGPT or Claude for consumer ranking queries
- Claim: For well-known brands, Gemini 2.5 Flash with grounding cited 63.4% earned, 25.1% brand, 11.5% social domains. For niche brands: 66.4% / 21.2% / 12.7%. ChatGPT (gpt-4o-search-preview) was 93.5–95.1% earned.
- Classification: VERIFIED FACT (gemini-2.5-flash + google_search tool, Aug 2025). EVIDENCE-BASED INFERENCE: grounded Gemini gives brand-owned pages more citation share than other engines. Not tested on AIO or AI Mode.
- Surface/system tested: Gemini API with Google Search grounding.
- Source: Generative Engine Optimization: How to Dominate AI Search — Mahe Chen, Xiaoxuan Wang, Kaiwen Chen, Nick Koudas — https://arxiv.org/html/2509.08919v1
- Published/updated: v1 2025-09-10. arXiv preprint.
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: Brand experiment across well-known and niche brands. Domains labeled Brand/Earned/Social by GPT-4o-search-preview. Data collected August 2025.
- Excerpt: > "Gemini stood between these extremes, balancing 63.4% Earned, 25.1% Brand, and 11.5% Social."
- Establishes: In banking persona prompts, "Gemini is the most brand-leaning". In local-service queries (Toronto), Gemini surfaced 98–151 distinct domains per category, the most for dentists (151) and moving companies (108); Perplexity had more for auto repair (117 vs 98). 55% (auto repair) and 54% (dentists) of Gemini's domains were unique to Gemini.
- Limitations: LLM-based domain labels. Ranking-style prompts. The paper is framed partly as practitioner guidance; only measurements are used here.

### GE-16 Grounded Gemini: language changes cited domains more than paraphrasing; brand lists stay moderately stable across paraphrases
- Claim: Gemini's cross-language domain overlap was low (peak about 0.32 for EN–DE) but modestly higher than Google's own cross-language overlap. Gemini's brand overlap across paraphrases was roughly 0.4–0.7 in most verticals.
- Classification: VERIFIED FACT (gemini-2.5-flash + grounding). EVIDENCE-BASED INFERENCE: language and locale are first-order variables for Gemini measurement; wording changes matter less for brand lists.
- Surface/system tested: Gemini API with Google Search grounding.
- Source: Chen, Wang, Chen, Koudas (as GE-15) — https://arxiv.org/html/2509.08919v1 (Sections 4.2.3–4.2.4, appendix)
- Published/updated: 2025-09-10
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: 100 English base queries across 10 consumer verticals, 5 target languages, 7 paraphrase templates.
- Excerpt: > "Gemini is more balanced, with the split fluctuating by language."
- Establishes: For German and Spanish prompts, Gemini's English-language citation share was "close to 50%". Perplexity and Gemini showed the highest domain stability across paraphrases.
- Limitations: Single run per condition implied. Run-to-run noise not separated.

### GE-17 Grounded Gemini 2.5 Flash overlaps Google's top 10 at about 11% (domain level) for consumer ranking queries
- Claim: Across 1,000 consumer ranking queries, Gemini 2.5 Flash with grounding had a mean 11.1% Jaccard domain overlap with Google's top 10. For 300 consumer-electronics queries, its sources were 46% earned and 46% brand.
- Classification: VERIFIED FACT (API). EVIDENCE-BASED INFERENCE: grounded Gemini does not reproduce Google's organic domain set even at domain level.
- Surface/system tested: Gemini 2.5 Flash API with Google Search grounding.
- Source: Navigating the Shift: A Comparative Analysis of Web Search and Generative AI Response Generation — Mahe Chen, Xiaoxuan Wang, Kaiwen Chen, Nick Koudas — https://arxiv.org/html/2601.16858v2
- Published/updated: v1 2026-01-23; v2 2026-05-16. Venue: EDBT/ICDT 2026 Workshops.
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: 100 templates x 10 topics. Paired bootstrap (10,000 iterations). Google top 10 via search API.
- Excerpt: > "followed by Gemini 2.5 Flash (11.1%, std = 10.2%)"
- Establishes: For transactional intent, "all AI systems sharply increase brand citations (52-68%)". Niche entity queries raised overlap with Google by 3–4 points for most models, including Gemini.
- Limitations: API. Google results from a programmable search API, not the live SERP.

### GE-18 Gemini 3 Flash flips from the incumbent brand on a tiny rating edge and saturates on authority-style claims
- Claim: With identical specs, every model recommended the real brand. A minimal rating advantage for a fictional competitor won 83% of trials for Gemini 3 Flash (Claude 22%). Authority-style text moved Gemini from near baseline (11.7%) to 99.3–100% at moderate or aggressive intensity.
- Classification: VERIFIED FACT (gemini-3-flash-preview API, direct prompting, no search in main experiments). EVIDENCE-BASED INFERENCE: Gemini-family models may react strongly to small visible attribute differences and to claim wording in supplied product text.
- Surface/system tested: google:gemini-3-flash-preview, temperature 0.7, English and Chinese.
- Source: Incumbent Advantage: Brand Bias and Cognitive Manipulation Dynamics in LLM Recommendation Systems — Xi Chu, Yupeng Hou — https://arxiv.org/html/2606.17443v3
- Published/updated: v1 2026-06-16; v3 2026-10-10. arXiv preprint.
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: Skincare product sets (1 real + 9 fictional brands). 20–30 repetitions per cell.
- Excerpt: > "Gemini is near baseline at subtle intensity (11.7%) but saturates near 100% from moderate intensity onward (99.3%/100%)."
- Establishes: Under universal GEO adoption the incumbent recovered only to 84.9% for Gemini (Claude 99.4%, GPT 96.2%). Gemini's Authority CI was [97.5%, 100.0%].
- Limitations: Products are given in the prompt. Fabricated claims were part of the stimulus. Not a Google surface.

### GE-19 AI Overviews trigger far less often for product-keyword queries than for questions
- Claim: AIOs appeared for 51.5% of representative real-user queries (ORCAS), 94.6% of ELI5 questions, and only 17.4% of Amazon Retail keyword queries. Question-form and longer queries triggered AIOs more.
- Classification: VERIFIED FACT (AIO via SerpApi, mobile, Newark NJ, Dec 7–8 2025). EVIDENCE-BASED INFERENCE: for short product-keyword searches, AIO is often absent, so AIO visibility is a minor channel for those queries. AI Mode trigger behavior is not measured.
- Surface/system tested: Google Search SERP and AIO via SerpApi; Gemini 2.5 Flash API with grounding (thinking off).
- Source: How Generative AI Disrupts Search: An Empirical Study of Google Search, Gemini, and AI Overviews — Riley Grossman, Songjiang Liu, Michael K. Chen, Mike Smith, Cristian Borcea, Yi Chen — https://arxiv.org/html/2604.27790v1 (abstract: https://arxiv.org/abs/2604.27790)
- Published/updated: v1 2026-04-30. Venue: ACM SIGIR 2026 (per arXiv comment).
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: 11,500-query public benchmark in 9 subsets, including Amazon Retail keywords, product comparisons (Retail-Comp) and product questions (Retail-Q). Robustness on desktop and other cities.
- Excerpt: > "94.6% of ELI5 queries, compared to just 17.4% of Amazon Retail queries, result in an AIO"
- Establishes: Interrogative queries were significantly more likely to trigger an AIO (χ²=1685.7, p<0.001). Desktop robustness sample: AIO on 67.17% of all queries (52.2% of ORCAS).
- Limitations: SerpApi proxy. Logged out. One date. Product-question subsets were generated by Gemini 2.5 Flash from Amazon keywords.

### GE-20 AIO, Gemini and Google organic results share few sources, and product queries share the fewest
- Claim: Mean URL-level Jaccard was 0.18 (AIO vs SERP), 0.16 (Gemini vs SERP) and 0.11 (AIO vs Gemini). Amazon Retail and Localized queries had the lowest similarity for every pairing.
- Classification: VERIFIED FACT (AIO via SerpApi, Gemini 2.5 Flash API). EVIDENCE-BASED INFERENCE: a page's organic rank for a product query predicts its AIO citation poorly, and grounded Gemini API results are not a proxy for AIO.
- Surface/system tested: As GE-19.
- Source: Grossman et al. (as GE-19) — https://arxiv.org/html/2604.27790v1 (Table 2)
- Published/updated: 2026-04-30
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: 7,439 queries where all three returned sources.
- Excerpt: > "In particular, the product and service queries (i.e., Amazon Retail and Localized query subsets) result in the lowest similarity for each pairing of search engines."
- Establishes: Amazon Retail Jaccard: AIO–SERP 0.08, AIO–Gemini 0.06, Gemini–SERP 0.08. "Surprisingly, despite AIO being built with a lightweight Gemini model, the source lists retrieved by AIO and Gemini are the least similar." Mean sources per answer: Gemini 9.68, AIO 9.24, SERP 8.75. Between-engine inconsistency exceeded within-engine run-to-run inconsistency.
- Limitations: URL-level. One collection date. SerpApi.

### GE-21 Generative Google surfaces cite fewer popular sites, more Google-owned pages, and skip sites that block Google-Extended
- Claim: AIOs favored google.com and youtube.com relative to organic search. Gemini (API) never cited 21 popular publishers and several review/social sites that block Google-Extended. AIOs also cited many of those sites less, although AIO has access to them.
- Classification: VERIFIED FACT (as GE-19). EVIDENCE-BASED INFERENCE: robots.txt choices (Google-Extended) are associated with lower visibility in Gemini grounding and AIO. The AIO association is observational.
- Surface/system tested: As GE-19.
- Source: Grossman et al. (as GE-19) — https://arxiv.org/html/2604.27790v1 (Section 4.3)
- Published/updated: 2026-04-30
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: Domain prevalence changes (McNemar tests). Linear probability model with query fixed effects. Tranco popularity.
- Excerpt: > "Google’s AIOs favor Google websites (i.e., google.com and youtube.com domains)."
- Establishes: Gemini cited zero times: Facebook, Instagram, TikTok, IMDb, Yelp, Tripadvisor, Consumer Reports, NYTimes and others, all of which block Google-Extended. Top-ranked source from the Tranco top 1,000: SERP 52.7% of queries, AIO 40.0%, Gemini 32.6%. Gemini had the most unique sources outside the Tranco top 10K.
- Limitations: Robots.txt status read once. Observational. Not product-feed sources.

### GE-22 AIO sources are less stable than organic results; device type changes them more than city
- Claim: Two same-config AIO runs had RBO 0.69 (organic 0.86; Gemini API 0.52). Changing device dropped AIO RBO by 0.16 (organic 0.07). Changing city (Austin vs Newark) changed metrics by only 0.01–0.02. Cosmetic query edits dropped AIO RBO to 0.49.
- Classification: VERIFIED FACT (as GE-19). EVIDENCE-BASED INFERENCE: AIO measurement must fix device and repeat runs. City-level location matters less than device within the US.
- Surface/system tested: AIO and SERP via SerpApi; Gemini 2.5 Flash API.
- Source: Grossman et al. (as GE-19) — https://arxiv.org/html/2604.27790v1 (Section 4.4, Section 5, Table 4)
- Published/updated: 2026-04-30
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: 100 stratified queries, 2 runs per device x location. 200 cosmetic edits. Manual signed-in Chrome comparison.
- Excerpt: > "the retrieved sources are more inconsistent between different devices than between different locations"
- Establishes: AIOs cited more sources on mobile (10.38) than desktop (9.42). A signed-in manual browser gave AIO RBO 0.73 between runs, close to SerpApi (0.67–0.69). Average RBO between manual and API collections was 0.67 (AIO), so SerpApi approximates a signed-in user at this level.
- Limitations: Small samples for the robustness tests. US only.

### GE-23 AIO activation on trending queries is low overall, highly question-dependent, and 14.6% in Shopping
- Claim: Across 55,393 US trending queries, AIO activation was 13.7%. Question-form queries triggered AIOs at 64.7% vs 9.5% for others. The Shopping category triggered on 23 of 158 queries (14.6%). Beauty & Fashion was lowest (3.5%).
- Classification: VERIFIED FACT (AIO from a US AWS vantage point, fresh logged-out browser profiles, Mar–Apr 2026). EVIDENCE-BASED INFERENCE: commerce-category head queries rarely get an AIO.
- Surface/system tested: Google AIO via a Puppeteer crawler (Chrome, AWS us-east-1).
- Source: Measuring Google AI Overviews: Activation, Source Quality, Claim Fidelity, and Publisher Impact — Haofei Xu, Umar Iqbal, Jacob M. Montgomery — https://arxiv.org/html/2605.14021v2
- Published/updated: v1 2026-05-13; v2 2026-10-01. Venue: ACM IMC 2026 (Proceedings pp. 529–546).
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: Google Trends queries in 19 categories, daily, 2026-03-13 to 2026-04-21. No CAPTCHA bypass (re-queue up to 20 times).
- Excerpt: > "question-form queries trigger AIOs at 64.7% versus 9.5% for non-question queries"
- Establishes: Shopping AIOs cited a median of 10 references. Real-time product queries (e.g., "costco finds") lowered Shopping claim fidelity; excluding them gave 85.90%.
- Limitations: Trending queries skew to news and sports. Shopping n=23 AIOs is small. Single vantage point.

### GE-24 About 30% of AIO-cited domains are absent from the same query's first results page
- Claim: Only 31.5% of AIO reference domains overlapped the top-5 first-page results, 48.0% the top 10, and 70.2% the whole first page. 29.8% did not appear on the first page. AIOs cited user-generated content far less than organic results.
- Classification: VERIFIED FACT (as GE-23). EVIDENCE-BASED INFERENCE: AIO source selection is not a re-ranking of the visible SERP. Organic page-1 presence is neither necessary nor sufficient for AIO citation.
- Surface/system tested: As GE-23.
- Source: Xu et al. (as GE-23) — https://arxiv.org/html/2605.14021v2 (Section 4.2)
- Published/updated: 2026-10-01 (v2)
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: 7,562 AIOs. Domain-level overlap.
- Excerpt: > "only 31.5% of AIO reference domains overlap with the top-5 first-page results, rising to 48.0% at top-10 and 70.2% across the full first page."
- Establishes: Overall UGC share: AIO refs 14.20% vs first-page 49.93%. Shopping: AIO 25.86% UGC vs first-page 54.41%. Within AIO citations, YouTube 5.49%, Facebook 3.67%, Instagram 3.66%, Reddit 0.87%. Off-page AIO references had higher domain-quality scores than on-page ones.
- Limitations: Domain-level. Trending queries. Contradicts the health-query result in GE-26 on source quality.

### GE-25 Most AIO-cited domains sit outside Google's organic top 10, and AIO sources change a lot over two months
- Claim: On average 53% of the domains AIO consulted were not in the organic top 10, and 27% were not in the top 100. Between runs about two months apart, AIO retrieved-link overlap was 18% (Jaccard), against 45% for organic results. Results from a German location differed only slightly from US results.
- Classification: VERIFIED FACT (AIO via SerpApi, logged out; Gemini-2.5-Flash API with optional search, temperature 0; Jul/Aug and Sep 2025). EVIDENCE-BASED INFERENCE: AIO citation sets are not stable enough to be read from one run, and organic top-10 rank is a weak proxy.
- Surface/system tested: Google organic, AIO (both via the same SerpApi requests), Gemini-2.5-Flash with Google Search (API), GPT-4o Search, GPT-4o with search tool, Perplexity Sonar.
- Source: Characterizing Web Search in The Age of Generative AI — Elisabeth Kirsten, Jost Grosse Perdekamp, Qinyuan Wu, Mihir Upadhyay, Krishna P. Gummadi, Muhammad Bilal Zafar — https://arxiv.org/html/2510.11560v2 (abstract: https://arxiv.org/abs/2510.11560)
- Published/updated: v1 2025-10-13; v2 2026-05-31. Venue: Findings of ACL 2026 (per the bibliography of https://arxiv.org/html/2607.14035v1; the ACL Anthology page was not fetched).
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: Over 4,600 queries in six datasets, including a "Products" set built from the 100 most-searched Amazon products of 2023 (review and "worth it" templates). Fixed IP regions via VMs in the US and Germany. One output per query.
- Excerpt: > "Overlap is substantially lower for Gemini and GPT-Search, and close to zero for GPT-Tool."
- Establishes: The 53%/27% and 18%/45% figures appear in the HTML as LaTeX-rendered values (`53\%`, `27\%`, `18\%`, `45\%`). Gemini produced the longest answers, longest for Products (mean 3,636 characters). Collection: "All queries were executed independently and in parallel in logged-out sessions using clean virtual environments." On location: "We observe only minor differences."
- Limitations: Internal inconsistency on Gemini (see Contradictions): the appendix says "GPT models show the lowest overlap with organic search results overall, while Gemini had the highest overlap." One output per query. API for Gemini.

### GE-26 For health questions, AIOs cited fewer than half of the top-5 organic results and favored commercial publishers
- Claim: AIOs appeared for 96.4% of 3,611 health questions. Only 44.4% of the top-5 organic results were cited by the matching AIO. AIOs over-represented commercial health publishers (e.g., WebMD, Healthline) relative to academic and government sources.
- Classification: VERIFIED FACT (AIO via SerpApi, US English, Sep 16–18 2026). EVIDENCE-BASED INFERENCE: AIO source selection departs from Google's organic ranking even in YMYL topics. Not product-specific; it bears on the source-quality contradiction with GE-24.
- Surface/system tested: Google AIO and top-5 organic results via SerpApi.
- Source: Does the Citation Matter? Quality, Grounding, and Physician-Rubric Accuracy of Google's AI Overviews for Medical Information — Sam Agnoli, Brigid Reilly, Lily Barna, Emőke-Ágnes Horvát — https://arxiv.org/html/2610.39339v1
- Published/updated: v1 2026-10-29. arXiv preprint.
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: HealthBench questions submitted verbatim. JAMA and HONcode credibility criteria. HallOumi grounding classifier.
- Excerpt: > "only 44.4% of the top five results were cited by the corresponding AIO"
- Establishes: AIOs averaged 8.5 cited sources. AIO-cited pages scored lower on four of six credibility criteria. The paper states that "commercial health publishers were cited more by AIOs".
- Limitations: Health only. Comparison capped at organic top 5. One collection window.

### GE-27 The Gemini consumer app and the Gemini API show different sources for the same product question
- Claim: For 117 real product-recommendation queries, the logged-out Gemini web interface and the Gemini API (gemini-3.5-flash-lite with Google Search grounding) shared on average 14.8% of displayed domains and 11.9% of pages. 43.4% of pairs shared no domain. YouTube and Reddit were 44.4 and 29.1 points more likely in the API.
- Classification: VERIFIED FACT (Gemini web interface and API, Netherlands, Sep 2026). EVIDENCE-BASED INFERENCE: Gemini API results cannot stand in for the Gemini app's product-advice sources. This constrains every API-based finding in this file (GE-08..GE-13, GE-15..GE-17).
- Surface/system tested: Gemini consumer web interface (logged out, fresh profile, rotating Dutch residential proxies, en-NL locale) and Gemini API, requests paired a median 0.17 s apart. The interface "identified gemini-3.5-flash-lite as its default model".
- Source: "If I Had to Buy Just ONE: Galaxy S26 Ultra": Auditing AI-Generated Product Recommendations — Lucas G. Uberti-Bona Marin, Thales Bertaglia, Giovanni Astante, Bram Rijsbosch, Gijs van Dijck, Anikó Hannák, Gerasimos Spanakis, Konrad Kollnig — https://arxiv.org/html/2609.18729v1
- Published/updated: v1 2026-09-16. arXiv preprint.
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: ConsumerQ subset of 117 queries x 3 repetitions x 5 conditions (ChatGPT UI/API, Gemini UI/API, AIO) = 1,755 observations; 1,536 produced a response.
- Excerpt: > "for Gemini, the corresponding overlaps were 14.8% and 11.9%."
- Establishes: Gemini's API displayed 661 distinct domains vs 376 in the interface. Domain overlap across repeats was 43.0% (API) vs 29.8% (interface). The Gemini API exposes grounding sources used in the answer, "but no separate set of sources returned by search". In the interface, Gemini's most frequent domains were pcmag.com (12.4%), reddit.com (8.0%) and youtube.com (6.9%). Gemini used first-person product preference in 7% of product-recommending answers (ChatGPT 79%).
- Limitations: One country, logged out, one week. Source types classified by an LLM (exploratory). Product names not normalized, so product overlaps are lower bounds.

### GE-28 For product questions, AIO recommends more consistent products than the Gemini app and mixes retailers, brands and UGC
- Claim: Across repeats, AIO recommended-product Jaccard was 0.421, Gemini app 0.287, ChatGPT 0.178. AIO displayed reddit.com in 35.0% and youtube.com in 30.0% of product answers with sources. AIO source types: editorial/review 25.4%, UGC/social 22.2%, retailers and marketplaces 17.8%, manufacturers and brands 16.1%.
- Classification: VERIFIED FACT (AIO and Gemini UI, Netherlands, 2026-09-04/05). EVIDENCE-BASED INFERENCE: for product questions, AIO mixes retailer, brand and community pages more than the Gemini app does. AIO appeared on only 38.2% of these product queries.
- Surface/system tested: Google Search AIO via Selenium (persistent profile, Dutch residential proxies); Gemini web interface.
- Source: Uberti-Bona Marin et al. (as GE-27) — https://arxiv.org/html/2609.18729v1
- Published/updated: 2026-09-16
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: 351 AIO searches; 134 (38.2%) had recoverable AIO content; 120 displayed a source.
- Excerpt: > "AI Overviews displayed reddit.com (35.0%) and youtube.com (30.0%) most often."
- Establishes: Mean domain overlap between repeats: Gemini 29.8%, AIO 45.9%. AIO displayed a median of five domains; Gemini and ChatGPT three. 61.7% of AIOs combined three or more source types (Gemini 19.0%). AIO and Gemini labeled a product "best" in 48% and 43% of answers (ChatGPT 73%).
- Limitations: Small AIO sample. LLM-labeled source types. Netherlands only. AI Mode not tested.

### GE-29 Real-user browsing data: AI summaries appeared on 18% of Google searches, more often for long and question queries
- Claim: In March 2025, 18% of 68,879 Google searches by 900 US adults produced an AI summary. 8% of one- or two-word searches did, against 53% of searches with 10+ words. Wikipedia, YouTube and Reddit made up 15% of AI-summary sources. .gov sites were 6% of AI-summary links vs 2% of standard results.
- Classification: VERIFIED FACT (real users' Google sessions, US, March 2025). EVIDENCE-BASED INFERENCE: short product-keyword searches rarely show an AIO. This agrees with GE-19 and GE-23.
- Surface/system tested: Google AI summaries (AIO) observed in opt-in browsing data (KnowledgePanel Digital).
- Source: Google users are less likely to click on links when an AI summary appears in the results — Pew Research Center (short read) — https://www.pewresearch.org/short-reads/2025/07/22/google-users-are-less-likely-to-click-on-links-when-an-ai-summary-appears-in-the-results/ (fetched as the `.md` twin of this URL with curl)
- Published/updated: 2025-07-22 (data March 1–31, 2025)
- Accessed: 2026-10-30
- Tier: 2 (reproducible panel measurement by a research organization; not peer-reviewed)
- Method / sample: Tracked browsing of 900 US adults; 12,593 searches with an AI summary. Click attribution counted only the first three links cited in a summary.
- Excerpt: > "Some 18% of all the Google searches in our study generated an AI summary as part of the search results."
- Establishes: 60% of queries beginning with question words produced an AI summary. 88% of summaries cited three or more sources. Users clicked a link inside a summary in 1% of visits.
- Limitations: March 2025, before later AIO model changes. Pew did not classify product queries. Clicks are outside AURA's ranking question; used here only for trigger rates and source mix.

### GE-30 On real NQ queries, AIO and organic Google share most top domains in aggregate; AIO cites social platforms less
- Claim: AIO triggered on 57.8% of 11,000 Natural Questions queries, with 7.0 references on average. AIO and organic Google shared 68% of their top-100 cited domains. Social media and forums were 8.5% of AIO citations vs 13.4% for organic.
- Classification: VERIFIED FACT (AIO via SerpApi). EVIDENCE-BASED INFERENCE: at the aggregate domain level, AIO draws from much the same ecosystem as organic Google even when per-query overlap is low (GE-20, GE-24).
- Surface/system tested: Google AIO and organic via SerpApi; also Search GPT and vanilla GPT.
- Source: Answer Bubbles: Information Exposure in AI-Mediated Search — Michelle Huang, Agam Goyal, Koustuv Saha, Eshwar Chandrasekharan — https://arxiv.org/html/2603.16138v2
- Published/updated: v1 2026-03-17; v2 2026-08-28. Venue: EMNLP 2026 (per arXiv comment).
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: 11,000 NQ queries across 11 topics.
- Excerpt: > "with only 57.8% of queries triggering a generative overview with a mean of 7.0 references"
- Establishes: AIO coverage varied by topic (business 84%, technology 32%). "While Google AIO and Organic share 68% of their top-100 domains", Search GPT shared only 24–25%. Reddit appeared in 7% of AIO queries vs 42% of organic queries.
- Limitations: Informational queries; no product subset. Aggregate top-100 domain overlap is a different unit from per-query overlap.

### GE-31 Logged in, from Italy, Google showed an AI overview for 97% of MS MARCO queries
- Claim: With a logged-in Google account and English interface, from Milan, Google generated overviews for 97.0% of English and 97.6% of Chinese MS MARCO queries. Host-domain overlap across platform-language settings was very low (maximum Jaccard 0.034).
- Classification: VERIFIED FACT (Google AI overviews in a logged-in Chrome session, Milan, Jun 20–Jul 10 2026). EVIDENCE-BASED INFERENCE: account state, location and language can move AIO trigger rates far from US logged-out measurements (GE-19, GE-23, GE-30). The cause is not isolated.
- Surface/system tested: Google Search AI overview in Chrome via Playwright; also Baidu.
- Source: Auditing Source Exposure in Baidu and Google AI Search — Yibo Li, Enci Guan, Yuedan Cai, Geng Liu, Francesco Pierri — https://arxiv.org/html/2609.24407v1
- Published/updated: v1 2026-09-21. Venue: WAC @ EMNLP 2026 (per arXiv comment).
- Accessed: 2026-10-30
- Tier: 2
- Method / sample: 500 MS MARCO queries and Chinese translations. No incognito, VPN or proxy.
- Excerpt: > "Google generated overviews for 97.6 % of Chinese queries and 97.0 % of English queries."
- Establishes: The authors state that "Google searches were conducted while logged in to a Google account". Google's topic-level appearance rates ranged 90.2%–100.0%.
- Limitations: Small sample. Single account and location. Machine translation. The 97% rate is not comparable with US logged-out studies without controlling for those factors.

### GE-32 Tier 3: Ahrefs reports AIO citations from the organic top 10 fell from 76% (Jul 2025) to 38% (Mar 2026)
- Claim: Ahrefs reported 76.10% of AIO-cited pages ranked in the top 10 in July 2025. In March 2026, on 863K keyword SERPs and 4M AIO URLs, 37.9% came from the top 10, 31.2% from positions 11–100 and 31.0% from beyond 100. YouTube was 5.6% of all AIO URLs cited.
- Classification: VERIFIED FACT as reported by the vendor. EVIDENCE-BASED INFERENCE: the link between organic rank and AIO citation weakened, or the measurement changed. Ahrefs changed its parser and states that AIOs are "now powered by Gemini 3" (not verified here). The two numbers are not a clean time series.
- Surface/system tested: Google AIO from Ahrefs Brand Radar data.
- Source A: Update: 38% of AI Overview Citations Pull From The Top 10 — Louise Linehan (contributor Xibeijia Guan), Ahrefs — https://ahrefs.com/blog/ai-overview-citations-top-10/
- Source B: 76% of AI Overview Citations Pull From the Top 10 — Louise Linehan, Ahrefs — https://ahrefs.com/blog/search-rankings-ai-citations/ (this URL served the July 2025 post)
- Published/updated: A 2026-03-02. B 2025-07-21.
- Accessed: 2026-10-30
- Tier: 3 (vendor research; Ahrefs sells Brand Radar, the data source)
- Method / sample: A: URL match between AIO citations and the same query's SERP; Test 1 all SERP blocks, Test 2 blue links only (37.10% top 10). B: 1.9M citations from 1M AIOs; top 3 citations per AIO only.
- Excerpt (A): > "Google is selecting far fewer pages straight from the original SERP."
- Establishes: Among AIO-cited pages outside the top 100, 18.2% were YouTube URLs (A). Neither post states country, device or login state.
- Limitations: Vendor data. Method changes between A and B. No shopping-query breakdown.

### GE-33 Tier 3 quasi-experiment: adding JSON-LD schema did not raise AI Mode citations; AIO citations fell slightly
- Claim: Ahrefs tracked 1,885 pages that added JSON-LD (Aug 2025–Mar 2026), each matched with three control pages. In a difference-in-differences over 30-day windows, AIO citations changed −4.6% (significant), AI Mode +2.4% (not significant), ChatGPT +2.2% (not significant).
- Classification: VERIFIED FACT as reported by the vendor. EVIDENCE-BASED INFERENCE: for already-cited web pages, adding JSON-LD is not a measurable lever for AIO or AI Mode citation. It says nothing about Merchant Center feeds or the product data that powers Google Shopping.
- Surface/system tested: Google AIO, Google AI Mode and ChatGPT citations from Ahrefs Brand Radar.
- Source: We Tracked 1,885 Pages Adding Schema. AI Citations Barely Moved. — Louise Linehan (contributor Xibeijia Guan), Ahrefs — https://ahrefs.com/blog/schema-ai-citations/ (secondary: Matt G. Southern, Search Engine Journal, 2026-05-11, https://www.searchenginejournal.com/schema-markup-didnt-move-ai-citations-in-ahrefs-test/)
- Published/updated: 2026-05-11
- Accessed: 2026-10-30
- Tier: 3 (vendor quasi-experiment; data not public)
- Method / sample: Schema addition dated from crawl history. Eligible pages had 100+ AIO citations before treatment. Schema types pooled (Article, FAQ, Product, HowTo, Organization).
- Excerpt (SEJ summary of the result): > "No platform showed a meaningful citation increase after schema was added."
- Establishes: AI Mode raw citations rose +43%, but controls rose almost as much. Treated and control pages were both declining before treatment. This agrees with the observational null for schema.org in GE-13.
- Limitations: Pages often changed other things at the same time. 30-day window. Only heavily cited pages. The stated control count (4,000) does not reconcile with three controls per treated page.

### GE-34 Tier 3: AI Mode sources change across same-day runs and overlap little with AIO or the organic top 10
- Claim: For 10,000 US keywords run three times on one day (2025-06-20), AI Mode's exact-URL overlap across all three runs averaged 9.2% (domain 14.7%). AI Mode vs AIO URL overlap was 10.7%. AI Mode vs organic top-10 URL overlap was 14%. google.com was the most cited domain (5.7%), mostly Google Maps business profiles.
- Classification: VERIFIED FACT as reported by the vendor. EVIDENCE-BASED INFERENCE: AI Mode, AIO and organic results are distinct source selections, and AI Mode needs repeated sampling. Consistent with GE-14 (AI Mode within-24h source Jaccard 0.318).
- Surface/system tested: Google AI Mode and AIO, non-logged-in, US.
- Source: AI Mode research: Volatility, source patterns, and differences from AIO and organic results — Yevheniia Khromova, SE Ranking — https://seranking.com/blog/ai-mode-research/
- Published/updated: 2025-08-29 (data 2025-06-20)
- Accessed: 2026-10-30
- Tier: 3 (vendor; sells the AI Results Tracker used)
- Method / sample: AI Mode answered 9,734 of 10,000 keywords. AIO triggered on 4,368.
- Excerpt: > "Volatility is high. Even the same query run multiple times on the same day often yields different sources."
- Establishes: Pairwise same-day URL overlap 18.5–19%. Among in-text citations, amazon.com led with 96 links (2.4%). No product-query breakdown.
- Limitations: Old (June 2025, early AI Mode). Device not stated. Vendor tool.

### GE-35 Tier 3: AI Mode shows few products, and almost none of those in the regular Google Shopping carousel
- Claim: Productrise reports that AI Mode showed at least one product on about 23% of shopping queries vs about 88% for standard search (July 2026). When products appeared, AI Mode showed 4.3 listings vs 22.5. In August 2026, only 1.28% of products in the "Popular products" carousel also appeared in AI Mode for the same query and day.
- Classification: VERIFIED FACT as reported by the vendor. EVIDENCE-BASED INFERENCE: AI Mode product selection is not a re-ranking of the organic Shopping carousel, although Google says both use the Shopping Graph (GE-36). Classic Shopping rank is a poor proxy for AI Mode product inclusion.
- Surface/system tested: Google AI Mode product cards and standard Google Search shopping results, US and UK.
- Source A: AI Mode cuts Google Shopping listings 95%, Productrise finds — Luís Rijo, PPC Land — https://ppc.land/ai-mode-cuts-google-shopping-listings-95-productrise-finds/
- Source B: AI Mode shows the same products 21.6% more expensive, Productrise finds — Luís Rijo, PPC Land — https://ppc.land/ai-mode-shows-the-same-products-21-6-more-expensive-productrise-finds/
- Published/updated: A 2026-07-29 (data 21 days in July 2026). B 2026-09-03 (data 2026-08-09 to 08-31).
- Accessed: 2026-10-30
- Tier: 3 (vendor study reported by trade press; Productrise sells Google Shopping visibility tracking; method not public)
- Method / sample: A: "more than 100,000 identical shopping searches", "clean, non-personalized sessions". B: more than 2 million listings; products matched by Google's product identifier "where present".
- Excerpt (B): > "only 1.28% of products ranking in traditional search also appeared in AI Mode for the same search on the same day."
- Establishes: A reports 0.8% overlap with a different dataset and denominator. AI Mode was 12.3% of all products tracked in B.
- Limitations: Queries focus on products Productrise monitors (not a random sample). B does not state session state or location settings. No merchant or marketplace share data.

### GE-36 Tier 3: AI Mode often leads with a different seller and a higher price than the carousel; Google says both use the Shopping Graph
- Claim: For products in both AI Mode and the carousel, the first-listed seller differed 49.6% of the time. Prices differed on 38.1% of matched products, and AI Mode showed the higher price in 68.4% of those. The lead AI Mode price averaged 21.6% higher. Google said it had not verified the claims and that all shopping results, including AI Mode, are powered by the Shopping Graph.
- Classification: VERIFIED FACT as reported (vendor figures; Google statement as quoted by SEJ). EVIDENCE-BASED INFERENCE: lowest price is not the dominant rule for which offer AI Mode shows first. UNVERIFIED HYPOTHESIS: AI Mode chooses offers on other signals (seller, relevance, data completeness). No fetched source tests this.
- Surface/system tested: As GE-35.
- Source: Google AI Mode prices differ from product carousel for same items — Matt G. Southern, Search Engine Journal — https://www.searchenginejournal.com/google-ai-mode-prices-differ-from-product-carousel-for-same-items/588227/ (plus GE-35 Source B)
- Published/updated: 2026-09-03 (Google statement given to Futurism on 2026-09-02, per SEJ)
- Accessed: 2026-10-30
- Tier: 3
- Method / sample: As GE-35 B.
- Excerpt (Google, as quoted by SEJ): > "all shopping results on Google Search, including AI Mode and the search results page, are powered by the same data source"
- Establishes: Where AI Mode was pricier, the median gap was 22.2%; where cheaper, 7.8%. Outliers (e.g., used vs new) inflate the average. The founder's view that "the cheapest price is less of a factor in AI Mode" is his interpretation (SEJ).
- Limitations: On-screen only; no clicks or purchases. Lead offer, not cheapest offer. PPC Land notes an unexplained arithmetic inconsistency in the vendor's figures.

### GE-37 Tier 3: AIOs appeared on 14% of keywords that show a Google shopping box
- Claim: Visibility Labs found AIOs on 2,919,229 of 20,900,323 shopping keywords (14.0%) in Ahrefs' keyword database. A shopping keyword was one whose results showed a shopping box.
- Classification: VERIFIED FACT as reported by the vendor. EVIDENCE-BASED INFERENCE: commerce-intent searches mostly lack an AIO, consistent with GE-19 (17.4% Amazon Retail) and GE-23 (14.6% Shopping).
- Surface/system tested: Google AIO presence in a third-party keyword database.
- Source: Google AI Overviews on shopping queries — Jeff Oxford, Visibility Labs — https://visibilitylabsofficial.pages.dev/blog/ai-overviews-shopping-queries/
- Published/updated: 2026-03-16
- Accessed: 2026-10-30
- Tier: 3 (agency selling AI SEO services; no collection date or country stated)
- Method / sample: Ahrefs keyword database filter.
- Excerpt: > "Google is now showing AI Overviews for 14% of shopping queries."
- Establishes: The post's 2.1% comparison point covers "transactional queries", a different set, so its 5.6x growth claim is not like-for-like.
- Limitations: Not a random sample. No date, country or category breakdown.

### GE-38 Amazon blocks Google's AI and shopping-agent crawlers; Tier 3 data shows Amazon absent from Gemini's top cited retailers
- Claim: amazon.com/robots.txt disallows Google-Extended, GoogleAgent-Mariner, GoogleAgent-Shopping, Gemini-Deep-Research, Google-NotebookLM, Google-CloudVertexBot and GoogleOther. LLM Pulse's Gemini retailer table (US non-branded shopping questions) lists walmart.com first at 0.92% of citations and does not list Amazon.
- Classification: robots.txt content: VERIFIED FACT (as of 2026-10-30). LLM Pulse figures: VERIFIED FACT as reported by the vendor. EVIDENCE-BASED INFERENCE: combined with GE-21 (Gemini never cited sites that block Google-Extended), Amazon's absence from Gemini grounding citations follows from its own crawler policy, not necessarily from a ranking judgment. Neither source shows whether Amazon offers appear in AI Mode product cards (Shopping Graph).
- Surface/system tested: A: Amazon's crawler policy. B: Gemini citations on US shopping questions (access path not stated).
- Source A: robots.txt — Amazon — https://www.amazon.com/robots.txt
- Source B: Gemini · Top US Retailers cited by AI — LLM Pulse — https://llmpulse.ai/data-studies/top-us-retailers/gemini
- Published/updated: A undated (live file). B "Updated October 29, 2026"; based on a July 2026 study of 391,000 citations.
- Accessed: 2026-10-30
- Tier: A Tier 1 for Amazon's own crawler policy (not Google documentation). B Tier 3 (vendor; method incomplete).
- Method / sample: A: file downloaded with curl. B: 7-day rolling window; "A retailer counts once per answer".
- Excerpt (A): > "User-agent: GoogleAgent-Shopping / Disallow: /" (two consecutive lines; the slash between them marks the line break)
- Establishes: Googlebot is not named in the file; it falls under `User-agent: *`. walmart.com/robots.txt, fetched the same day, names none of these Google AI agents. B, across engines: "Two thirds of citations go to brand-owned and manufacturer sites"; Gemini's retailer share is "under 1%".
- Limitations: B has internal inconsistencies (ranking basis; "last 90 days" vs 7-day window). B does not say whether it measured the Gemini app, API or AI Mode. A robots.txt rule shows intent to block, not what Google retrieves.

---

## Reusable methodology notes for Google surfaces

- Treat each surface as its own system. Grounded Gemini API, the Gemini app, AIO and AI Mode select different sources for the same query: AIO vs Gemini API URL Jaccard 0.11 (GE-20); Gemini app vs API domain overlap 14.8% (GE-27); AI Mode vs AIO URL overlap 10.7% (GE-34). Never report an API result as a Gemini app, AIO or AI Mode result.
- Record the trigger rate before any source analysis. AIO appears on a subset of queries. The rate depends on query form, length, topic, account state and location: 13.7% (US trending, GE-23), 14% (shopping-box keywords, GE-37), 17.4% (Amazon keywords, GE-19), 18% (real US users, GE-29), 38.2% (product questions, Netherlands, GE-28), 51.5% (ORCAS, GE-19), 57.8% (NQ, GE-30), 97% (logged in, Milan, GE-31). Condition source analyses on triggered queries and report the denominator.
- Build product query sets by form. Keyword-style product queries rarely trigger AIO; question-form and longer queries do (GE-19, GE-23, GE-29). Include keyword, question, comparison and "where to buy" forms. Grossman et al. publish Amazon-derived product subsets (Amazon Retail, Retail-Comp, Retail-Q) in a public benchmark (GE-19).
- Fix and log device. Device changes AIO sources more than city: AIO RBO −0.16 on a device change vs −0.01 to −0.02 on a city change (GE-22). AIO cites more sources on mobile.
- Log account state. Studies differ: logged out with fresh profiles (GE-23, GE-25, GE-27), a persistent profile (GE-28 AIO arm), logged in (GE-31). A signed-in browser gave AIO run-to-run RBO 0.73 vs 0.67–0.69 via SerpApi (GE-22). No study isolates personalization effects on product results.
- Log country and language. Gemini's cited domains shift by prompt language (GE-16). US vs Germany differed only slightly for AIO (GE-25). The Gemini API has no user-location parameter, so location comes only from the request IP (GE-27).
- Repeat runs. Same-config AIO source RBO is about 0.69 (GE-22). Gemini app domain overlap across repeats is 29.8% (GE-27). AI Mode three-run URL overlap is 9.2% (GE-34). Schulte et al. (GE-14 source) report that the per-brand detection-rate SE "drops below 0.10 at n=7 runs"; source coverage needs n=8. Their rolling-window SE falls below 0.10 at 10 days. Track over weeks: for the Gemini API, 47% of within-website citation variance was still shared after two weeks and 29% after ten (GE-12).
- Expect wording sensitivity. Cosmetic edits ("what is" vs "what's") dropped AIO source RBO to 0.49 (GE-22). Use paraphrase sets.
- Separate source layers. AIO shows three sources by default and more behind "Show all" (GE-21 source paper). Gemini API grounding metadata lists sources used, not a ranked retrieved list (GE-09, GE-27). Gemini links some sources through a redirect service; resolve redirects (GE-08). State which layer is the outcome.
- Log the model version. The Gemini interface self-identified its default model (GE-27). A preview-to-GA change reversed position effects (GE-03). Ahrefs attributes AIO changes to a Gemini 3 switch (GE-32, unverified).
- Record each cited and candidate domain's robots.txt rules for Google-Extended and Google agents at collection time. Blocking Google-Extended associates with zero Gemini grounding citations and fewer AIO citations (GE-21). Amazon blocks Google-Extended and GoogleAgent-Shopping (GE-38).
- Normalize product identity. Product names vary ("Apple iPhone 14" vs "iPhone 14"), so unnormalized overlaps are lower bounds (GE-28). For AI Mode product cards, match by Google's product identifier where present (GE-35, vendor method).
- Do not bypass bot checks. Xu et al. re-queued CAPTCHA pages instead of solving them (GE-23). Grossman et al. validated SerpApi against a signed-in browser at the RBO level (GE-22).
- Controlled answer-step designs that have been run on Gemini models: all-orders source rotation (GE-10), brand and publisher masking against a repetition baseline (GE-10), randomized grid positions and badges with a conditional logit (GE-01..GE-05).

## Contradictions

1. AIO overlap with organic results: URL-level Jaccard 0.18 (GE-20) vs 48.0% of AIO domains in the top 10 (GE-24) vs 53% of AIO domains not in the top 10 (GE-25) vs 44.4% of top-5 results cited (GE-26, health) vs 68% shared top-100 domains in aggregate (GE-30) vs Ahrefs 76% → 38% of cited URLs in the top 10 (GE-32). Units (URL vs domain; per query vs aggregate), denominators (AIO citations vs organic results), query sets and dates differ. All agree that a large share of AIO citations is outside the organic top 10.
2. AIO source quality: AIO-cited domains more credible than first-page results (GE-24, trending queries) vs AIO-cited pages less credible and more commercial (GE-26, health) vs generative engines less likely to retrieve gov/edu and popular sites (GE-21) vs more .gov links in AI summaries, 6% vs 2% (GE-29). Query domains and quality measures differ.
3. UGC and Reddit in Google AI surfaces: AIO cites UGC far less than organic (14.20% vs 49.93%; Reddit 0.87% of AIO citations) (GE-24) vs AIO displayed reddit.com in 35.0% of product answers with sources (GE-28) vs Reddit 13% of grounded Gemini API citations (GE-08) vs Reddit in 7% of AIO queries vs 42% of organic queries (GE-30). Metrics (share of citations vs share of answers), query intent (trending vs product advice) and surface differ.
4. Gemini overlap with organic results inside one paper: Kirsten et al. say in the main text that overlap "is substantially lower for Gemini" than for AIO; their appendix says "Gemini had the highest overlap" (GE-25). Across papers: Gemini API domain overlap with Google's top 10 is 11.1% (GE-17) vs 5.6% at page level (GE-09). Unit and query set differ.
5. Run-to-run stability of Gemini: the Gemini app had the most repeatable sources of four engines (Jaccard 0.505, GE-14) vs the Gemini app less repeatable than AIO (29.8% vs 45.9% domain overlap, GE-27) vs the Gemini API least consistent of three Google systems (Jaccard 0.46 vs AIO 0.66, GE-22). Locale, prompt type and surface differ.
6. Position effects for Gemini models: strong, version-specific grid effects (GE-01..GE-03) vs no source-order effect for Gemini 3.1 Flash Lite (GE-10) vs near-uniform list positions for Gemini 2.5 Flash (GE-07). Task framing (visual grid vs supplied sources vs three identical items) and model differ.
7. Rating sensitivity: Gemini 3 Pro Preview weights rating least of the Dec-2025 models (GE-05) vs Gemini 3 Flash switches to a competitor on a tiny rating edge in 83% of trials (GE-18). Models, designs and categories differ.
8. Brand-owned share in Gemini citations: 25.1% brand (well-known brands, GE-15) vs 46% brand (consumer electronics, GE-17) vs 83% third party (ISP services, GE-08) vs Tier 3 "two thirds" brand-owned across engines (GE-38 B). Market, intent and date drive the mix.
9. Schema markup: no observational effect for grounded Gemini (GE-13) and no positive DiD effect for AI Mode, with a small significant AIO decline (GE-33). Consistent on "no positive effect"; the AIO decline is unexplained.
10. AIO trigger rates range from 13.7% to 97% (methodology notes). The spread reflects query set, account state and location rather than a measurement conflict.
11. AI Mode vs carousel product overlap: 0.8% (July) vs 1.28% (August) from the same vendor with different datasets and denominators (GE-35).
12. Grossman et al. report AIOs cite fewer popular-domain sources than organic (GE-21); Answer Bubbles reports AIO and organic share 68% of their top-100 domains (GE-30). The first is per query and rank-weighted; the second is an aggregate set overlap.

## Knowledge gaps

- No Tier 2 study measures AI Mode product cards (which products, merchants and offers appear) under controlled conditions. All AI Mode shopping evidence is Tier 3 from one vendor (Productrise, GE-35, GE-36).
- No study at any tier tests whether Merchant Center feed quality, attribute completeness, reviews, ratings or price competitiveness change inclusion in AI Mode, AIO product units or Gemini app product results. Rating and price effects exist only for Gemini API models on constructed inputs (GE-04, GE-05, GE-18).
- No study measures the Gemini app's shopping units (product cards, merchant offers), as opposed to its text answers and cited sources (GE-14, GE-27, GE-28).
- No study isolates personalization (signed-in history, location history, purchase signals) on Gemini or AI Mode product results. Only a small signed-in check exists for AIO sources (GE-22).
- Amazon vs Walmart vs brand-DTC share in AI Mode product cards is not measured. Amazon's robots.txt blocks Google's AI and shopping agents (GE-38), so any share measurement must control for crawler policy.
- The relationship between the retrieval pipelines of Gemini API grounding, the Gemini app, AIO and AI Mode is unknown. Measured overlaps are low (GE-20, GE-27, GE-34).
- The effect of Google-Extended blocking on AIO citation is observational (GE-21). No controlled test exists.
- No study tests whether ads (Shopping ads, sponsored units) shown in AI Mode or AIO change which organic products the model selects. Badge evidence exists only for API agents in ACES (GE-04).
- No study tests whether agentic-checkout eligibility or UCP support changes product selection in Google AI surfaces.
- Production model versions behind the Gemini app, AIO and AI Mode are not pinned in any Tier 2 study, except the self-reported default model in GE-27.

## Unfetched sources

- https://searchengineland.com/google-ai-mode-product-links-google-shopping-study-499887 — HTTP 403 to WebFetch. A web-search summary attributed "Findrix" figures to it (46.5% of US AI Mode product answers linking only to Google pages; 57% of links to Google Shopping; 55,198 answers). A second search found no other source for these figures. Unverified; not used.
- https://www.emarketer.com/content/gemini-ignores-most-stores-rewards-readable-product-data — HTTP 403. Reports a Recomaze study (58,320 Gemini tests across 9,720 stores; Recomaze sells product-content tools). Not used.
- https://www.webpronews.com/ai-agents-are-picking-winners-in-online-retail-and-most-stores-lose/ — HTTP 403 (same Recomaze study). Not used.
- BrightEdge AIO shopping and citation figures (e.g., 16.7% top-10 overlap; "best [product]" queries at 83% AI presence) — seen only in search summaries and secondary blogs. BrightEdge primary pages not fetched. Not used.
- Azoma analysis of Gemini shopping-agent citations (41% retailer, 37% earned, 15% brand.com, 7% UGC) — seen only in a search summary. Not fetched; not used.
- ACM DL health-query AIO audit (https://dl.acm.org/doi/full/10.1145/3795513.3807429) — not fetched.
- Kirsten et al., ACL Anthology version (https://aclanthology.org/2026.findings-acl.526/) — not fetched; arXiv v2 was read.
- Pew data-labs full report (2025-05-23) and its methodology page — not fetched; the short read was fetched.
- Wang et al., AI in Search Reduces Publisher Referrals Without Improving User Experience (https://arxiv.org/abs/2608.18352) — abstract read via the arXiv API only. It studies clicks, not selection. Not used.
- Jellyfish study of ChatGPT, AI Mode and Alexa shopping recommendations — the WARC page (https://www.warc.com/article/ai-shopping-assistants-create-radically-different-shelves-for-the-same-product-ba34dbcb0a1b4a168de98c8ad109ef53, 2026-10-19) was fetched but gives no method and no AI Mode retailer shares. Not used.
- PYMNTS, Amazon Updates Code to Keep Out Google AI Shopping Tools (https://www.pymnts.com/?p=2878285, 2025-07-30) — fetched. It summarizes paywalled reporting by The Information and names no user agents. Superseded by the robots.txt file itself (GE-38).
- Zhang, He, Yao, From Citation Selection to Citation Absorption (https://arxiv.org/abs/2604.25707) — full text fetched. It pools "Google AI Overview/Gemini" as one platform, so it was not used for surface-specific claims.

## Source list

Tier 1
- Amazon, robots.txt (accessed 2026-10-30) — https://www.amazon.com/robots.txt (Amazon's crawler policy; not Google documentation)

Tier 2
- Allouah, Besbes, Figueroa, Kanoria, Kumar, What Is Your AI Agent Buying? (v3 2025-12-17) — https://arxiv.org/abs/2508.02630
- Bansal et al., Magentic Marketplace (2025-10-27) — https://arxiv.org/abs/2510.25779
- Chen & Koudas, What Drives AI Citations? (2026-10-10) — https://arxiv.org/abs/2610.15033
- Schulte, Bleeker, Kaufmann, Don't Measure Once (2026-04-08) — https://arxiv.org/abs/2604.07585
- Chen, Wang, Chen, Koudas, Generative Engine Optimization: How to Dominate AI Search (2025-09-10) — https://arxiv.org/abs/2509.08919
- Chen, Wang, Chen, Koudas, Navigating the Shift (EDBT/ICDT 2026 Workshops) — https://arxiv.org/abs/2601.16858
- Chu & Hou, Incumbent Advantage (v3 2026-10-10) — https://arxiv.org/abs/2606.17443
- Grossman, Liu, Chen, Smith, Borcea, Chen, How Generative AI Disrupts Search (SIGIR 2026) — https://arxiv.org/abs/2604.27790
- Xu, Iqbal, Montgomery, Measuring Google AI Overviews (IMC 2026) — https://arxiv.org/abs/2605.14021
- Kirsten et al., Characterizing Web Search in The Age of Generative AI (Findings of ACL 2026) — https://arxiv.org/abs/2510.11560
- Agnoli, Reilly, Barna, Horvát, Does the Citation Matter? (2026-10-29) — https://arxiv.org/abs/2610.39339
- Uberti-Bona Marin et al., "If I Had to Buy Just ONE: Galaxy S26 Ultra" (2026-09-16) — https://arxiv.org/abs/2609.18729
- Huang, Goyal, Saha, Chandrasekharan, Answer Bubbles (EMNLP 2026) — https://arxiv.org/abs/2603.16138
- Li, Guan, Cai, Liu, Pierri, Auditing Source Exposure in Baidu and Google AI Search (WAC @ EMNLP 2026) — https://arxiv.org/abs/2609.24407
- Pew Research Center, Google users are less likely to click on links when an AI summary appears in the results (2025-07-22) — https://www.pewresearch.org/short-reads/2025/07/22/google-users-are-less-likely-to-click-on-links-when-an-ai-summary-appears-in-the-results/
- Martinez, Optimizing Visibility in Generative Engines: A Critical Survey (2026-07-15) — https://arxiv.org/abs/2607.14035 (used only to locate Kirsten et al. and its venue)

Tier 3
- Ahrefs (Louise Linehan), Update: 38% of AI Overview Citations Pull From The Top 10 (2026-03-02) — https://ahrefs.com/blog/ai-overview-citations-top-10/
- Ahrefs (Louise Linehan), 76% of AI Overview Citations Pull From the Top 10 (2025-07-21) — https://ahrefs.com/blog/search-rankings-ai-citations/
- Ahrefs (Louise Linehan), We Tracked 1,885 Pages Adding Schema (2026-05-11) — https://ahrefs.com/blog/schema-ai-citations/
- Search Engine Journal (Matt G. Southern), Schema markup didn't move AI citations in Ahrefs test (2026-05-11) — https://www.searchenginejournal.com/schema-markup-didnt-move-ai-citations-in-ahrefs-test/
- SE Ranking (Yevheniia Khromova), AI Mode research (2025-08-29) — https://seranking.com/blog/ai-mode-research/
- PPC Land (Luís Rijo), AI Mode cuts Google Shopping listings 95%, Productrise finds (2026-07-29) — https://ppc.land/ai-mode-cuts-google-shopping-listings-95-productrise-finds/
- PPC Land (Luís Rijo), AI Mode shows the same products 21.6% more expensive, Productrise finds (2026-09-03) — https://ppc.land/ai-mode-shows-the-same-products-21-6-more-expensive-productrise-finds/
- Search Engine Journal (Matt G. Southern), Google AI Mode prices differ from product carousel for same items (2026-09-03) — https://www.searchenginejournal.com/google-ai-mode-prices-differ-from-product-carousel-for-same-items/588227/
- Visibility Labs (Jeff Oxford), AI Overviews on shopping queries (2026-03-16) — https://visibilitylabsofficial.pages.dev/blog/ai-overviews-shopping-queries/
- LLM Pulse, Gemini · Top US Retailers cited by AI (updated 2026-10-29) — https://llmpulse.ai/data-studies/top-us-retailers/gemini

