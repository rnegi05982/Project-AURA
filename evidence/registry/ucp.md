# Registry — UCP (Universal Commerce Protocol, and AP2)

Schema: `evidence/README.md`. Accessed 2026-10-30. Google's own UCP implementation (feeds, checkout, onboarding) is in `goog.md`. Shopify's UCP endpoints are in `shop.md` (SHOP-007, SHOP-015, SHOP-020).

UCP (Universal Commerce Protocol): open spec, led by Google and Shopify, for agents to exchange catalog, cart, checkout, identity and order data with businesses. AP2 (Agent Payments Protocol): Google-originated spec for agent-initiated payments.

---

### UCP-001 — UCP launched 2026-01-11; co-developed with Shopify, Etsy, Wayfair, Target, Walmart; Flipkart among endorsers
- **Claim:** Google launched UCP at NRF 2026, co-developed with Shopify, Etsy, Wayfair, Target and Walmart and endorsed by 20+ others, including Flipkart, Best Buy, Visa, Mastercard and Stripe. The first use case is checkout in AI Mode and Gemini.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** UCP / governance
- **Source:** "New tech and tools for retailers to succeed in an agentic shopping era" — The Keyword — https://blog.google/products/ads-commerce/agentic-commerce-ai-tools-protocol-retailers-platforms/
- **Published:** 2026-01-11 · **Accessed:** 2026-10-30
- **Excerpt:** > "UCP was co-developed with industry leaders including Shopify, Etsy, Wayfair, Target and Walmart, and endorsed by more than 20 others across the ecosystem like Adyen, American Express, Best Buy, Flipkart, Macy’s Inc., Mastercard, Stripe, The Home Depot, Visa and Zalando."
- **Establishes:** Flipkart is a UCP endorser (relevant to India, GEM-016).
- **Limitations:** Endorsement ≠ integration.
- **Related:** UCP-003, SHOP-014, ACP-006
- **Origin:** notes/gb-…#GB-18; notes/ga-…#GA-06 · **Checked:** pending

### UCP-002 — UCP spec: Apache 2.0, date versions v2026-01-11 → v2026-08-25, REST/MCP/A2A transports
- **Claim:** UCP is at github.com/Universal-Commerce-Protocol/ucp under Apache 2.0. Releases: v2026-01-11, v2026-01-23, v2026-04-08, v2026-08-25. Capabilities: checkout, cart, catalog (from v2026-04-08), identity linking, order, loyalty. Transports: REST, MCP, A2A, Embedded.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** UCP / spec
- **Source:** Universal-Commerce-Protocol/ucp — GitHub — https://github.com/Universal-Commerce-Protocol/ucp ; https://ucp.dev/latest/specification/overview/
- **Published:** latest release v2026-08-25; last commit 2026-10-29 · **Accessed:** 2026-10-30
- **Excerpt:** > "**Transport Agnostic:** The protocol is designed to work across various transports. Businesses can offer Capabilities via REST APIs, MCP (Model Context Protocol), or A2A, depending on their infrastructure."
- **Establishes:** Version to cite: v2026-08-25. Google surfaces implement 2026-01-23 and 2026-04-08 (GOOG-006).
- **Limitations:** README "autonomous discovery" means capability discovery via `/.well-known/ucp`, not product ranking.
- **Related:** UCP-004, GOOG-006
- **Origin:** notes/gb-…#GB-40 · **Checked:** pending

### UCP-003 — Governance: Google and Shopify hold permanent seats; Google holds proxy votes for open seats until Dec 2028
- **Claim:** The UCP Governing Council has 5 seats: one permanent each for Google and Shopify, three elected (one filled by Stripe). Google holds the proxy vote for open seats until December 2028 and is custodian of ucp.dev.
- **Classification:** VERIFIED FACT. "Google holds 3 of 5 votes today" is an EVIDENCE-BASED INFERENCE from the proxy rule and current membership. · **Confidence:** High · **Tier:** 1
- **Subject / topic:** UCP / governance
- **Source:** GOVERNANCE.md, MAINTAINERS.md — Universal-Commerce-Protocol/.github — https://github.com/Universal-Commerce-Protocol/.github
- **Published:** last commit 2026-10-29 · **Accessed:** 2026-10-30
- **Excerpt:** > "Google holds proxy vote for all open seats until Dec 2028 to facilitate rapid early stage growth & adoption of the protocol."
- **Establishes:** UCP is Google-controlled in practice for now; OpenAI is absent (ACP-006).
- **Limitations:** Membership lists conflict slightly between files.
- **Related:** ACP-001, ACP-006
- **Origin:** notes/gb-…#GB-41 · **Checked:** pending

### UCP-004 — UCP has a Catalog capability, but Google documents discovery on its surfaces as Shopping Graph-based
- **Claim:** UCP defines catalog search and lookup so platforms can query a business's catalog; the business ranks its own results. Google's AI Mode/Gemini docs require Merchant Center feeds and attribute discovery to the Shopping Graph. No Google shopping guide shows AI Mode calling a merchant catalog endpoint for discovery.
- **Classification:** VERIFIED FACT (spec and doc text). "UCP does not feed AI Mode/Gemini discovery or ranking today" is an EVIDENCE-BASED INFERENCE. · **Confidence:** Medium · **Tier:** 1
- **Subject / topic:** UCP / discovery
- **Source:** Catalog capability — UCP spec `docs/specification/shopping/catalog/` — https://github.com/Universal-Commerce-Protocol/ucp ; "Frequently asked questions" — Google for Developers — https://developers.google.com/merchant/ucp/faq
- **Published:** repo 2026-10-29; FAQ 2026-10-16 · **Accessed:** 2026-10-30
- **Excerpt:** > "The Catalog capability allows platforms to search and browse business product catalogs. This enables product discovery before checkout"
- **Establishes:** For Google discovery, Merchant Center is the documented input; UCP is the documented checkout path.
- **Limitations:** Google's March 2026 post says Catalog lets agents fetch real-time variants, inventory and pricing "where necessary" (notes/ga-…#GA-07).
- **Related:** GOOG-003, GOOG-004, SHOP-015
- **Origin:** notes/gb-…#GB-42 · **Checked:** pending

### UCP-005 — AP2 is the payment layer within UCP; v0.2 (2026-04-28) adds "Human Not Present" and moves to the FIDO Alliance
- **Claim:** AP2 was announced 2025-09-16. Google calls it a specialized payment layer within UCP. AP2 v0.2 (2026-04-28) adds "Human Not Present" payments, and Google donated AP2 to the FIDO Alliance.
- **Classification:** VERIFIED FACT · **Confidence:** High · **Tier:** 1
- **Subject / topic:** AP2 / payments
- **Source:** "We're donating Agent Payments Protocol to the FIDO Alliance" — The Keyword — https://blog.google/products-and-platforms/platforms/google-pay/agent-payments-protocol-fido-alliance/ ; AP2 FAQ — https://github.com/google-agentic-commerce/AP2
- **Published:** 2026-04-28 · **Accessed:** 2026-10-30
- **Excerpt:** > "While the Universal Commerce Protocol orchestrates the broader purchase lifecycle, AP2 is the specialized payment layer responsible for authorizing and signing transactions."
- **Establishes:** AP2 targets autonomous purchases; it is not needed for discovery.
- **Limitations:** No source confirms AP2 in production on AI Mode or Gemini.
- **Related:** UCP-002, ACP-008
- **Origin:** notes/gb-…#GB-43, #GB-44 · **Checked:** pending
