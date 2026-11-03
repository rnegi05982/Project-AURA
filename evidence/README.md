# Evidence registry — schema

`registry/` is the single source of truth for every claim AURA makes. One file per ID prefix. Reports cite registry IDs. Raw captures in `research/**/notes/` are inputs, not citations.

The brief proposed one `evidence-registry.md` plus separate `verified-facts.md`, `inferences.md` and `hypotheses.md`. AURA splits by subject instead, and keeps classification as a field:
- One claim lives in one file, so it never drifts between copies.
- Per-subject files stay small enough to load whole.
- Filter by classification with grep, e.g. `rg "Classification:\*\* EVIDENCE-BASED" evidence/registry`.

## Files

| File | Prefix | Subject | Entries (2026-10-31) |
|---|---|---|---|
| `registry/cgpt.md` | CGPT | ChatGPT / OpenAI product behavior and documentation | 54 |
| `registry/acp.md` | ACP | Agentic Commerce Protocol specification and governance | 8 |
| `registry/gem.md` | GEM | Google consumer AI surfaces: Gemini app, AI Mode, AI Overviews | 17 |
| `registry/goog.md` | GOOG | Google merchant and search infrastructure: Merchant Center, Shopping Graph, UCP on Google, crawlers, structured data | 35 |
| `registry/ucp.md` | UCP | Universal Commerce Protocol and AP2 specification and governance | 5 |
| `registry/shop.md` | SHOP | Shopify platform, Shopify Catalog, Google & YouTube channel, themes | 38 |
| `registry/mkt.md` | MKT | Marketplaces and other commerce platforms | 29 |
| `registry/res.md` | RES | Independent research: papers, studies, experiments by others | 48 |
| `registry/exp.md` | EXP | AURA's own experiments | not started |

Add a file and prefix when a new subject starts (e.g. CLA, PPLX, COP). IDs are permanent. A retracted claim keeps its ID and gets `Classification: RETRACTED` with the reason.

## Entry template

```markdown
### CGPT-001 — Short claim title
- **Claim:** One or two sentences. What is true, for which system, as of when.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ChatGPT / ranking
- **Source:** "Page title" — Publisher — https://exact.url/
- **Published:** 2025-09-29 (or "not stated"; "≈YYYY-MM-DD" when converted from "Updated: N days ago") · **Accessed:** 2026-10-30
- **Excerpt:** > "Verbatim text from the source."
- **Establishes:** What the excerpt proves, and nothing more.
- **Limitations:** What it does not prove. Scope, region, date, wording ambiguity.
- **Related:** CGPT-004 (supports), RES-002 (contradicts)
- **Origin:** notes/a-openai-search-and-shopping.md#A-07 · **Checked:** 2026-10-30
```

Optional field for Tier 2 entries: `**Method:**` (system tested, sample, design).

`Checked` records whether the lead researcher re-read the excerpt on the live source before promotion: a date, or `pending`. Re-check `pending` entries before a report relies on them for a new conclusion.

## Classification

| Value | Meaning |
|---|---|
| VERIFIED FACT | The source directly states it. For Tier 2 sources: the study reports this result for the system it tested. |
| EVIDENCE-BASED INFERENCE | Follows from documented facts. The platform has not stated it. |
| UNVERIFIED HYPOTHESIS | Plausible. Needs a source or an experiment. |
| EXPERIMENTALLY OBSERVED | Reproduced by an AURA experiment. Cite the `experiments/` record. |

## Source tiers

| Tier | Sources |
|---|---|
| 1 | Official platform docs, help centers, engineering blogs, API docs, protocol specs and repos, robots.txt files, court filings |
| 2 | Peer-reviewed papers, arXiv preprints, university research, reproducible independent experiments |
| 3 | Industry analysis, technical SEO research, reputable press, vendor studies |
| 4 | Forums, Reddit, merchant anecdotes. Raise questions only. |

## Confidence

| Value | Meaning |
|---|---|
| High | Tier 1, explicit wording, current page. |
| Medium | Tier 1 with ambiguous wording, marketing copy or an old date; or Tier 2. |
| Low | Tier 3, absence-of-evidence claims, or an inference across several indirect facts. |
