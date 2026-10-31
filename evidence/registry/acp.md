# Registry — ACP (Agentic Commerce Protocol)

Schema: `evidence/README.md`. All entries accessed 2026-10-30. OpenAI's own feed spec (developers.openai.com/commerce) is in `cgpt.md` (CGPT-027 to CGPT-032). This file covers the protocol repo and its governance.

ACP (Agentic Commerce Protocol): open spec for agent checkout, delegated payment and product feeds, founded by OpenAI and Stripe.

---

### ACP-001 — ACP is maintained by OpenAI and Stripe, with Meta on the TSC; Apache 2.0; beta
- **Claim:** OpenAI and Stripe are Founding Maintainers with a limited veto. Meta holds a TSC (Technical Steering Committee) seat since 2026-04-24. License is Apache 2.0. Status is beta.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ACP / governance
- **Source:** README.md, MAINTAINERS.md, docs/governance.md — agentic-commerce-protocol (GitHub) — https://github.com/agentic-commerce-protocol/agentic-commerce-protocol
- **Published:** Meta TSC commit 2026-04-24 · **Accessed:** 2026-10-30
- **Excerpt:** > "The specification is [maintained](MAINTAINERS.md) by **OpenAI** and **Stripe** and is currently in `beta`." / > "the Founding Maintainers (OpenAI and Stripe) reserve a limited veto authority over TSC decisions."
- **Establishes:** Who controls the protocol ChatGPT uses for merchant data.
- **Limitations:** README still names only OpenAI and Stripe; MAINTAINERS.md adds Meta.
- **Related:** ACP-002, ACP-006
- **Origin:** notes/b-…#B-07 · **Checked:** pending

### ACP-002 — Five dated versions; latest stable 2026-04-17; last commit 2026-07-18
- **Claim:** ACP uses date versions 2025-09-29, 2025-12-12, 2026-01-16, 2026-01-30, 2026-04-17. The repo has no tags or releases. The last commit to main is 2026-07-18.
- **Classification:** VERIFIED FACT (versions, commit date). Reduced activity since July is only an observation. · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ACP / versions
- **Source:** README.md, changelog/*.md, GitHub API — https://github.com/agentic-commerce-protocol/agentic-commerce-protocol
- **Published:** 2026-04-17 release commit; 2026-07-18 latest commit · **Accessed:** 2026-10-30
- **Excerpt:** > "ACP uses **date-based versioning** in `YYYY-MM-DD` format. Each version represents a complete snapshot of the specification at that point in time."
- **Establishes:** Version to cite: 2026-04-17.
- **Limitations:** Whether OpenAI implements 2026-04-17 in production is not stated.
- **Related:** ACP-003, ACP-005
- **Origin:** notes/b-…#B-08 · **Checked:** pending

### ACP-003 — ACP 2026-04-17 adds a push Feed API, carts, orders, `/.well-known/acp.json` and an MCP binding
- **Claim:** The 2026-04-17 release adds an agent-hosted Feed API (merchants push catalogs to agents), carts, native orders, delegate authentication, a discovery document and an MCP transport binding for checkout.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ACP / components
- **Source:** changelog/2026-04-17.md — agentic-commerce-protocol (GitHub) — https://github.com/agentic-commerce-protocol/agentic-commerce-protocol
- **Published:** 2026-04-17 · **Accessed:** 2026-10-30
- **Excerpt:** > "These endpoints are hosted by Agents and called by merchants. The Feed API is a push model: merchants push product catalog metadata and product records to Agents, rather than Agents pulling catalog data from merchant-hosted endpoints."
- **Establishes:** ACP's discovery mechanism is merchant push, not agent crawl.
- **Limitations:** ACP paths (`/feeds/...`) differ from OpenAI's documented API (`/product_feeds/...`).
- **Related:** CGPT-018, CGPT-027
- **Origin:** notes/b-…#B-09 · **Checked:** pending

### ACP-004 — The ACP product-feed RFC puts ranking explicitly out of scope
- **Claim:** The feed RFC defines the data surface only. Agents build their own retrieval and ranking.
- **Classification:** VERIFIED FACT · **Confidence:** High (RFC status "Proposal") · **Tier:** 1
- **Subject / topic:** ACP / ranking
- **Source:** rfcs/rfc.product_feeds.md — agentic-commerce-protocol (GitHub) — https://raw.githubusercontent.com/agentic-commerce-protocol/agentic-commerce-protocol/main/rfcs/rfc.product_feeds.md
- **Published:** "Status: Proposal", "Version: unreleased" · **Accessed:** 2026-10-30
- **Excerpt:** > "- **Search or ranking algorithms**: This RFC defines the data surface, not how agents rank products or personalize recommendations."
- **Establishes:** Adopting ACP gives data delivery, not a ranking guarantee.
- **Limitations:** RFC is a proposal.
- **Related:** CGPT-029, CGPT-030
- **Origin:** notes/b-…#B-10 · **Checked:** pending

### ACP-005 — OpenAI's checkout spec page lags the ACP repo
- **Claim:** OpenAI's Agentic Checkout Spec still uses `fulfillment_address` and 2025-09 API versions. ACP renamed the field and deprecated 2025-09-29 in the 2025-12-12 release.
- **Classification:** VERIFIED FACT (text comparison). "Not maintained since the pivot" is an EVIDENCE-BASED INFERENCE. · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** ACP / documentation currency
- **Source:** https://developers.openai.com/commerce/llms-full.txt ; changelog/2025-12-12.md — https://github.com/agentic-commerce-protocol/agentic-commerce-protocol
- **Published:** not stated; 2025-12-12 · **Accessed:** 2026-10-30
- **Excerpt:** > "#### 1. Renamed `fulfillment_address` to `fulfillment_details`" … "- Previous version `2025-09-29` is deprecated"
- **Establishes:** OpenAI commerce docs contain stale sections. Verify every developer-doc claim against the current help center and repo.
- **Limitations:** OpenAI may accept several versions.
- **Related:** CGPT-032
- **Origin:** notes/b-…#B-12 · **Checked:** pending

### ACP-006 — No OpenAI or ACP statement on UCP; Stripe and Meta sit on both governance bodies
- **Claim:** No fetched OpenAI page or ACP repo file mentions UCP. Stripe is on UCP's Governing and Tech Councils. Meta joined both ACP's TSC and UCP's Tech Council in April 2026.
- **Classification:** VERIFIED FACT (absence in fetched corpus; memberships) · **Confidence:** Medium (absence of evidence) · **Tier:** 1
- **Subject / topic:** ACP / UCP relationship
- **Source:** ACP repo (grep `UCP|universal commerce`: 0 hits); UCP announcements — https://github.com/Universal-Commerce-Protocol/ucp ; "Universal Commerce Protocol" — Stripe Docs — https://docs.stripe.com/agentic-commerce/protocols/ucp.md
- **Published:** UCP announcements 2026-04-24, 2026-04-28 · **Accessed:** 2026-10-30
- **Excerpt:** > "Stripe has joined the UCP Governing Council as a new member, joining existing permanent members Google and Shopify."
- **Establishes:** ChatGPT's documented protocol is ACP. UCP support by ChatGPT is undocumented.
- **Limitations:** Absence of evidence only.
- **Related:** SHOP-014
- **Origin:** notes/b-…#B-34; notes/c-…#C-16 · **Checked:** pending

### ACP-007 — Stripe's catalog feed (not OpenAI's) has `popularity_score` and says agents "rank" products
- **Claim:** Stripe's Agentic Commerce Suite catalog feed recommends fields that "improve discovery, ranking and personalisation", including `popularity_score`. OpenAI's spec has no such field.
- **Classification:** VERIFIED FACT (Stripe doc). Any effect on ChatGPT ranking: UNVERIFIED HYPOTHESIS. · **Confidence:** Medium · **Tier:** 1 (Stripe, not OpenAI)
- **Subject / topic:** ACP / feeds, ranking
- **Source:** "Catalogue feed" — Stripe Docs — https://docs.stripe.com/agentic-commerce/concepts/catalog-feed.md
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "These fields are optional but recommended. They improve discovery, ranking and personalisation across agentic interfaces."
- **Establishes:** Feed providers convert data per agent. A field accepted by Stripe may not reach ChatGPT.
- **Limitations:** Stripe states it converts feeds "to the format each agent requires".
- **Related:** CGPT-018, CGPT-030
- **Origin:** notes/b-…#B-35 · **Checked:** pending

### ACP-008 — Stripe's Shared Payment Token is the first delegated-payment implementation
- **Claim:** Stripe's Shared Payment Token is the first Delegated Payment Spec implementation. OpenAI's checkout docs list `stripe`, `adyen`, `braintree` as processors.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** ACP / payments
- **Source:** OpenAI commerce docs — https://developers.openai.com/commerce/llms-full.txt ; https://www.agenticcommerce.dev
- **Published:** not stated · **Accessed:** 2026-10-30
- **Excerpt:** > "Stripe is the first compatible PSP with its Shared Payment Token."
- **Establishes:** Payment rails for in-chat checkout (now limited to a beta, CGPT-023).
- **Limitations:** Not relevant to discovery today.
- **Related:** CGPT-023
- **Origin:** notes/b-…#B-11 · **Checked:** pending
