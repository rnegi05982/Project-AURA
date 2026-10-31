# AURA

Global AI Commerce Discovery & Product Recommendation Research.

AURA studies how AI applications discover, retrieve, rank and recommend products from marketplaces, Shopify stores and independent websites. It turns cited evidence into actions for Shopify merchants. Full scope: [docs/project-brief.md](docs/project-brief.md). Working rules: [CLAUDE.md](CLAUDE.md).

## Start here

- ChatGPT vs Google comparison: [reports/platform-comparisons.md](reports/platform-comparisons.md)
- ChatGPT report: [research/ai-platforms/chatgpt/report.md](research/ai-platforms/chatgpt/report.md)
- Gemini / AI Mode / AI Overviews report: [research/ai-platforms/gemini/report.md](research/ai-platforms/gemini/report.md)
- Shopify actions: [shopify/chatgpt.md](shopify/chatgpt.md), [shopify/gemini.md](shopify/gemini.md)
- Evidence registry: [evidence/README.md](evidence/README.md)
- Experiment designs: [experiments/test-cases/](experiments/test-cases/)

## Status (2026-10-31)

| Phase | Item | Status |
|---|---|---|
| 2 | ChatGPT / OpenAI | Report done. No experiments run yet. |
| 2 | Google: Gemini app, AI Mode, AI Overviews | Report done. No experiments run yet. |
| 2 | Claude, Perplexity, Copilot | Not started |
| 3 | Marketplaces, Shopify, other platforms | ChatGPT and Google angles (registry MKT, SHOP) |
| 4 | Technologies | ACP and UCP/AP2 covered; Schema.org via Google docs; MCP partial |
| 5 | Shopify implementation guide | Per-platform files for ChatGPT and Google |
| 6 | Experiments | Methodology + two test cases designed (CGPT-T01, GEM-T01) |

Registry: 222 entries across 8 subject files (see `evidence/README.md`).

## Layout

| Path | Contents |
|---|---|
| `docs/` | Project brief |
| `research/ai-platforms/<platform>/report.md` | Platform report. Claims cite registry IDs. |
| `research/ai-platforms/<platform>/notes/` | Raw source captures (excerpts + metadata, no interpretation) |
| `evidence/registry/<prefix>.md` | Every claim, its source, excerpt, classification and limitations |
| `evidence/README.md` | Registry schema, ID prefixes, tiers, classifications |
| `shopify/<platform>.md` | Merchant actions derived from the evidence, per platform |
| `experiments/` | Methodology, fixed query sets, raw observations, findings |
| `reports/` | Cross-platform comparisons and final recommendations (later phases) |

Folders from the brief's suggested structure are created when their research starts.

## Deviations from the suggested structure

- Evidence registry split by subject prefix, not by classification. Reason: one claim, one place; files stay loadable.
- Each platform folder has a `notes/` subfolder for raw captures. Reason: the brief requires raw material to stay separate from interpretation.
- Shopify actions are per platform (`shopify/chatgpt.md`) until enough platforms exist to merge into `implementation-guide.md`.
