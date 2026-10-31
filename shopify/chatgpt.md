# Shopify merchant actions — ChatGPT

Derived from `research/ai-platforms/chatgpt/report.md`. Evidence as of 2026-10-30. Each action names its evidence, status and test.

Status values (from the brief):
- **Mandatory** — a documented platform requirement. Without it, the product cannot enter that path.
- **Recommended** — evidence-backed improvement. A documented factor or input supports it.
- **Experimental** — plausible, evidence is indirect or Tier 3. Test before relying on it.
- **Unverified** — no evidence it affects ChatGPT.

Two separate paths reach ChatGPT for a Shopify store. Actions below say which path they touch:
- **Catalog path:** Shopify Catalog → ChatGPT product results. US buyers only. Default-on [SHOP-001, CGPT-017].
- **Web path:** OAI-SearchBot crawl and partner search → ChatGPT search answers and citations [CGPT-004, CGPT-006, SHOP-011].

---

## Mandatory (Catalog path)

| # | Action | Why | Evidence | How to verify |
|---|---|---|---|---|
| M1 | Keep the store on the Starter plan or higher and not password-protected. | Catalog eligibility gate. | SHOP-005 | Settings > Plan; Online Store > Preferences. |
| M2 | Give every product a title, at least one image, a price above 0, and a published URL. Do not set Unlisted or `seo.hidden`. | Products missing any of these never enter Catalog. | SHOP-005, SHOP-010 | Bulk-export products; filter for missing image, price 0, Unlisted. |
| M3 | Avoid Catalog-excluded and OpenAI-prohibited categories, or accept that those products will not show. | Policy gates before ranking. | SHOP-005, SHOP-003, CGPT-026 | Compare product types against Shopify's exclusion list. |
| M4 | Sell to customers in the United States (Markets settings). | The ChatGPT channel requires US selling; ChatGPT shopping is documented as US-only. | SHOP-003, CGPT-022 | Settings > Markets includes US. |
| M5 | Complete Terms of service, Privacy policy and Return/refund policy. | ChatGPT channel requirement. | SHOP-003 | Settings > Policies. |
| M6 | Leave ChatGPT's Shopify Catalog access on (it is on by default). If it was turned off, turning it back on is the only fix on this path. | Opt-out removes the store from the Catalog path within ~7 days. | SHOP-001, SHOP-010 | Sales channels > Agentic > ChatGPT. |

## Mandatory (web path)

| # | Action | Why | Evidence | How to verify |
|---|---|---|---|---|
| W1 | Allow `OAI-SearchBot` in robots.txt and at any CDN or firewall in front of the store. | OpenAI's stated eligibility condition for search inclusion. Opted-out sites appear only as navigational links. | CGPT-004, CGPT-006 | Fetch `/robots.txt`; search for `OAI-SearchBot` and any `User-agent: *` `Disallow: /`. Shopify's default allows it. |
| W2 | If the theme has a custom `robots.txt.liquid`, re-check it. Custom templates do not inherit Shopify's default changes. | Large stores' custom files diverge from the default. | SHOP-017 | Compare live `/robots.txt` with a default Dawn store. |

Note: blocking `GPTBot` (training) does not affect search [CGPT-007]. Blocking `ChatGPT-User` is not a documented visibility control [CGPT-008]. Both are merchant choices, not visibility actions.

---

## Recommended

| # | Action | Why | Systems affected | Evidence | How to test impact |
|---|---|---|---|---|---|
| R1 | Keep price and inventory accurate and in sync; avoid out-of-stock variants staying "available". | Merchant ranking uses availability and price. The headline price is the first-ranked merchant's. | ChatGPT merchant list | CGPT-014, CGPT-015, SHOP-006 | Probe products: compare ChatGPT's shown price/stock with the store on the same day (methodology metric "attribute accuracy"). |
| R2 | Sell and label your own brand: set `vendor` to the maker's brand for products you make. | "Maker or primary seller" is a documented merchant-ranking factor. How ChatGPT decides "maker" is unknown. | ChatGPT merchant list | CGPT-015, SHOP-022 (vendor → JSON-LD brand) | Find a product sold by you and resellers; record merchant order over repeated runs (US location). |
| R3 | Collect product reviews through a source Shopify treats as verified. | Catalog's listing quality counts only verified reviews; ChatGPT considers reviews and summarizes public reviews. | Shopify Catalog search; ChatGPT selection | SHOP-009, CGPT-011, CGPT-013, RES-003, RES-006 | Agentic admin listing-quality score before/after; appearance rate in repeated runs. |
| R4 | Fill product data completely: barcode (GTIN/UPC/EAN), product type, vendor, variant options, all images, specific descriptions. Put legal disclosures in the first 6,000 characters. | Shopify lists these as fields AI platforms consider. Catalog may infer missing fields with variable accuracy. | Shopify Catalog; ChatGPT (via Catalog) | SHOP-003, SHOP-008, SHOP-015 | Agentic admin listing-quality and search preview. |
| R5 | Set the Shopify product category explicitly. | Default JSON-LD shows `"category": ""` when unset; Catalog classifies products itself and can differ. | Shopify Catalog; JSON-LD | SHOP-005, SHOP-022 | Compare admin category with the Catalog search preview. |
| R6 | Use the Agentic admin page and ChatGPT referral attribution as the measurement baseline. | Shows queries the store ranks for and ChatGPT-referred orders. | Measurement | SHOP-012, SHOP-013 | Export weekly; keep in `experiments/raw-observations/`. |

---

## Experimental

| # | Action | Hypothesis | Evidence | How to test |
|---|---|---|---|---|
| E1 | Remap Catalog title and description to AI-specific metafields (Catalog > Channel mapping). | Clearer, attribute-rich titles may improve Catalog matching. ChatGPT may still rewrite titles. | SHOP-007, CGPT-013, RES-005 | A/B on a matched product pair; ≥5 runs per query per week for 4 weeks. |
| E2 | Earn coverage on third-party review and comparison sites for your category. | For "best X" queries, OpenAI's search model cited mostly third-party media (API study). | RES-011, RES-024 (contradicting market) | Track citation domains for category queries over time. |
| E3 | Maintain a Google Merchant Center listing. | A vendor study matched 83% of ChatGPT carousel products to Google Shopping. OpenAI names no Google provider. | RES-021, CGPT-002 | Compare carousel appearance for products in vs out of Merchant Center. |
| E4 | Keep product facts (price, rating, review count) competitive on items where you compete with known brands. | LLMs use brand as a tie-breaker; small attribute advantages override it. | RES-015, RES-017 | Lab: API replay with masked vs revealed brands. Production: repeated runs. |

---

## Unverified for ChatGPT (do not prioritize for this platform)

| Item | Status | Evidence |
|---|---|---|
| Adding AggregateRating, shipping or return-policy JSON-LD | No OpenAI source mentions structured data. One API study found no citation lift. May still matter for Google (separate research). | SHOP-022, RES-012 |
| Custom `llms.txt` / `agents.md` | Shopify serves defaults; no evidence ChatGPT reads them. | SHOP-020 |
| UCP adoption for ChatGPT | No source says ChatGPT uses UCP. | SHOP-014, ACP-006 |
| Applying for a direct OpenAI feed | Shopify stores are already integrated via Catalog. | CGPT-017, CGPT-025 |
| Building a ChatGPT plugin | OpenAI positions plugins for larger merchants; feed first; beta. | CGPT-039, CGPT-040 |
| Buying ChatGPT ads to improve organic results | Ads are separate from organic results, per OpenAI. | CGPT-010, CGPT-042 |

---

## India-only stores

A store that does not sell to the US is not eligible for the ChatGPT Catalog path [SHOP-003]. OpenAI documents no shopping results for India [CGPT-046]. For such a store only the web path applies: W1, W2, and the experimental items E2–E4. Run `experiments/test-cases/chatgpt-coffee-mug.md` from India before investing further.
