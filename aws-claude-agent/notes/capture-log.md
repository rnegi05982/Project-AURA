# Capture log

Raw captures only. No interpretation. All fetched **2026-10-30** from a Windows host via
`curl`/`WebFetch`.

## Method notes

- `openai.com`, `help.openai.com`, `help.shopify.com`, `shopify.dev` and `www.shopify.com` return
  403 to plain `curl`, or render content client-side. Where a file below is a `.md` with a
  `Title:` / `URL Source:` / `Published Time:` header, it was obtained through the
  `r.jina.ai` text-extraction proxy. That is one remove from origin bytes — recorded in the
  registry's fidelity column.
- `developers.openai.com` serves genuine markdown at `<page>.md`; those captures are origin bytes.
- Search engines were unusable for discovery (see `ACA-OBS-006`). Sources were found by enumerating
  `https://help.shopify.com/sitemap-en.xml`, `https://openai.com/sitemap.xml` children, and
  `https://developers.openai.com/commerce/llms.txt`, then following links.

## Files

### OpenAI — origin bytes
| File | Source |
|---|---|
| `oai-key-concepts.md` | developers.openai.com/commerce/guides/key-concepts.md |
| `oai-feed-products.md` | developers.openai.com/commerce/specs/file-upload/products.md |
| `oai-get-started.md` | developers.openai.com/commerce/guides/get-started.md |
| `oai-best-practices.md` | developers.openai.com/commerce/guides/best-practices.md |
| `oai-production.md` | developers.openai.com/commerce/guides/production.md |
| `oai-bots.md` | developers.openai.com/api/docs/bots.md |
| `oai-ip-searchbot.json` | openai.com/searchbot.json — `creationTime` 2026-01-02 |
| `oai-ip-gptbot.json` | openai.com/gptbot.json — `creationTime` 2026-09-22 |
| `oai-ip-chatgpt-user.json` | openai.com/chatgpt-user.json — `creationTime` 2026-10-27 |
| `oai-ip-adsbot.json` | openai.com/adsbot.json — `creationTime` 2026-05-12 |

### OpenAI — via reader proxy
| File | Source | Date in capture |
|---|---|---|
| `oai-buy-it-in-chatgpt.md` | openai.com/index/buy-it-in-chatgpt/ | none |
| `oai-shopping-research.md` | openai.com/index/chatgpt-shopping-research/ | none |
| `oai-commerce-policies.md` | openai.com/policies/commerce-policies/ | none |
| `oai-merchant-feed-tos.md` | openai.com/policies/merchant-feed-terms-of-service/ | none |
| `oai-allowlisting.md` | requested `.../11845367-chatgpt-agent-allowlisting`; **final URL** `.../11845367-chatgpt-works-cloud-browser-allowlisting` | none |

### Shopify — via reader proxy
| File | Source | Date in capture |
|---|---|---|
| `sh-agentic-overview.md` | help.shopify.com/.../agentic-storefronts | 2026-10-21 |
| `sh-agentic-chatgpt.md` | help.shopify.com/.../agentic-storefronts/chatgpt | 2026-10-21 |
| `sh-agentic-products.md` | help.shopify.com/.../agentic-storefronts/products | 2026-10-21 |
| `sh-data-privacy.md` | help.shopify.com/.../agentic-storefronts/data-privacy | none |
| `sh-knowledge-base.md` | help.shopify.com/.../agentic-storefronts/knowledge-base | — |
| `sh-catalog.md` | help.shopify.com/en/manual/shopify-catalog | none |
| `sh-catalog-requirements.md` | help.shopify.com/en/manual/shopify-catalog/requirements | 2026-10-21 |
| `sh-catalog-optimizing.md` | help.shopify.com/en/manual/shopify-catalog/optimizing-products | 2026-10-21 |
| `sh-robots.md` | help.shopify.com/.../seo/editing-robots-txt | — |
| `sh-robots-liquid.md` | shopify.dev/.../templates/robots-txt-liquid | — |
| `sh-liquid-robots-object.md` | shopify.dev/docs/api/liquid/objects/robots | — |
| `sh-liquid-rule-object.md` | shopify.dev/docs/api/liquid/objects/rule | — |
| `sh-global-catalog.md` | shopify.dev/docs/agents/catalog/global-catalog | — |
| `sh-agentic-readiness.md` | www.shopify.com/agentic-readiness | — |

### Live-store observations (origin bytes)
| File | Source | Note |
|---|---|---|
| `ab_agents.md` | allbirds.com/agents.md | 5,750 bytes |
| `ab_llms.txt` | allbirds.com/llms.txt | 5,793 bytes — **not** byte-identical to `agents.md` |
| `ab_robots.txt` | allbirds.com/robots.txt | only `*` and `adsbot-google` groups |
| `ab_well-known-ucp.json` | allbirds.com/.well-known/ucp | UCP `2026-08-25` |
| `allbirds-pdp.html` | allbirds.com/products/mens-tree-runners | fetched with UA `OAI-SearchBot/1.4; +https://openai.com/searchbot` → HTTP 200, 804,715 bytes |

## Not captured, and why

- `openai.com/index/introducing-chatgpt-search/` — read through a rendering tool only; quotes from
  it are marked `[paraphrase]` and it is flagged stale (2024-10-31).
- `openai.com/index/expanding-access-to-ai-with-chatgpt-ads/` — rendering tool only.
- `agenticcommerce.dev`, `agenticcommerce.dev/docs`, `ucp.dev`, `shopify.dev/docs/agents` —
  rendering tool only; used for provenance, not for load-bearing claims.
- Exact code samples on `shopify.dev` pages and the full Global Catalog host
  (`catalog.shopify.com/...`) are injected client-side and absent from the text captures.

## Downloaded-content handling

Captures live only in this directory. The one HTML file was parsed with `python3 -I` and an explicit
path argument, from a different working directory, so nothing in this folder was importable or
executable by the parser.
