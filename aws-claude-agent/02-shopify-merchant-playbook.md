# Shopify merchant playbook: being selected by ChatGPT

Ordered by leverage, highest first. Each action states what to implement, why, what it affects,
evidence IDs, status, and how to test impact — per `/CLAUDE.md` §"Shopify actions".

Status vocabulary: **mandatory** (you are invisible or non-compliant without it), **recommended**
(documented by the platform as considered), **experimental** (mechanism-plausible, unproven),
**unverified** (do not spend money on this yet).

> Before anything else: the instinct is to reach for robots.txt. For a Shopify store that is close
> to the *least* effective lever available, because ChatGPT receives your products through Shopify
> Catalog, not through your HTML. "Blocking AI crawlers at the `/robots.txt` or network layer
> affects only open-web discoverability. It doesn't stop your product data from being sent by
> Shopify Catalog" <sup>`[ACA-SHOP-004]`</sup>. robots.txt is action 8 below, and its job is to avoid
> *self-harm*, not to gain anything.

---

## 1. Confirm you are actually in Shopify Catalog — mandatory

**Implement.** Shopify admin → **Sales channels** → **Agentic** → **Sources** → **Shopify
Catalog**. You see either a product count (eligible) or an **Ineligible** warning. Click
**Ineligible** to get the reason <sup>`[ACA-SHOP-003]`</sup>.

**Why.** Everything else in this document is downstream of this one switch. ChatGPT and Microsoft
Copilot "can access and display your products only when your store is eligible for Shopify Catalog"
<sup>`[ACA-SHOP-003]`</sup>. The channel is "active by default for eligible stores" <sup>`[ACA-SHOP-002]`</sup> — so most
merchants are already in and don't know it, and a minority are silently out.

**Store and product gates**, verbatim <sup>`[ACA-SHOP-007]`</sup>:

- Comply with Shopify's Terms of Service and Acceptable Use Policy.
- "Your store must be on the Starter plan or higher, and your store can't be in private mode."
- "Your products must have a title and at least 1 product image."
- "Your products must have a price greater than 0. Free products aren't included."
- Published to online store, Hydrogen, or Headless. Headless must "use the correct format for
  routes".
- "Your products must be published with an identifiable product URL."
- Not **Unlisted** and not hidden from search engines.
- No sensitive/mature content; not in an excluded category.

**The non-obvious gate.** Eligibility also depends on *account standing*, "based on a number of
factors, and is reviewed over time" <sup>`[ACA-SHOP-007]`</sup>. The listed inputs are: verified email,
two-step authentication, a passkey, completed identity/business verification, "a track record of
genuine sales to real customers", prompt and accurate fulfillment, a low chargeback rate, paid
Shopify invoices, Shopify Payments in good standing, and no open policy issues <sup>`[ACA-SHOP-007]`</sup>.
**VF.**

Operationally: your chargeback rate is now an AI-discoverability input. No amount of description
tuning compensates for falling out of Catalog.

**Affects.** Everything. **Evidence.** <sup>`[ACA-SHOP-003]`</sup>, <sup>`[ACA-SHOP-002]`</sup>, <sup>`[ACA-SHOP-007]`</sup>.
**Status.** mandatory.

**Test.** Record the product count on the Agentic page weekly. A drop with no catalog change means
an eligibility event. Excluded categories are absolute — alcohol, tobacco/vaping, drug
paraphernalia, prescription/medical devices, weapons and imitation weapons, explosives, lab
chemicals, adult content, sexual health, bullion/coins/virtual currency, prop money, warranties and
service add-ons, event tickets, live animals, and **"Uncategorized products"** <sup>`[ACA-SHOP-007]`</sup>.
That last one is self-inflicted and fixable: set the product category.

---

## 2. Fill the exact fields Shopify says AI platforms read — mandatory

**Implement.** Shopify names the fields, so there is nothing to guess. "Product details that are
considered by the AI platforms or shopping sites include the following fields" <sup>`[ACA-SHOP-008]`</sup>:

| Field | Shopify admin location | Do this |
|---|---|---|
| **Title** | Product → Title | Product name + the variant-distinguishing attribute. Keep ≤150 chars (OpenAI's feed limit) <sup>`[ACA-CGPT-007]`</sup> |
| **Description** | Product → Description | Factual. State specs as text, not only in an image or a tab |
| **Images** | Product → Media | At least 1; direct image URLs; per-variant images where the variant looks different |
| **Type** | Product organization | Fill it. Blank → "Uncategorized" risk (action 1) |
| **Vendor** | Product organization | Real brand name. Maps to `brand` / primary-seller signals |
| **Collections** | Product organization | Category context |
| **Tags** | Product organization | Attribute vocabulary |
| **Barcode (ISBN, UPC, GTIN, etc.)** | Variant → Inventory → Barcode | See action 3 — highest-value underfilled field |
| **Variants, including Option name** | Variants | Option names must be real dimensions: Color, Size, not "Option 1" |
| **External product URL** | Agentic plan only | Required if no published Shopify storefront <sup>`[ACA-SHOP-007]`</sup> |

**Why.** "Make sure to provide accurate, detailed, and descriptive product information… You can
improve the way your products rank in search results by following these best practices"
<sup>`[ACA-SHOP-008]`</sup>. **VF (as stated by Shopify).** On the OpenAI side, recommended attributes
"improve ranking, relevance, and user trust" <sup>`[ACA-CGPT-003]`</sup>. **VF (as stated).**

**Affects.** Shopify Catalog payload → every AI channel, plus your own storefront search.
**Evidence.** <sup>`[ACA-SHOP-008]`</sup>, <sup>`[ACA-CGPT-003]`</sup>, <sup>`[ACA-CGPT-007]`</sup>. **Status.** mandatory.

**Test.** Export products to CSV and count blanks per field. Track "percent of SKUs with
non-empty Type / Vendor / Barcode / Option name" as a single readiness number over time.

---

## 3. Fill `Barcode` with a real GTIN on every variant — recommended, underrated

**Implement.** Variant → Inventory → Barcode. Use the manufacturer's UPC/EAN/GTIN. OpenAI's feed
spec requires a GTIN to be "exactly 8, 12, 13, or 14 digits, including a valid check digit"
<sup>`[ACA-CGPT-007]`</sup>.

**Why.** The one published ranking paragraph is about *the same product sold by several merchants*:
"When ranking multiple merchants that sell the same product, ChatGPT considers factors like
availability, price, quality, whether a merchant is the primary seller" <sup>`[ACA-CGPT-001]`</sup>. **VF.**

And the retrieval layer on Shopify's side works by exactly that grouping: "Results are clustered by
Universal Product ID (UPID) and include offers from multiple merchants" <sup>`[ACA-SHOP-006]`</sup>. **VF.**

**EBI:** both systems need to decide that two listings are the same product before price and
availability can be compared. GTIN is the standard identifier for that, and Shopify lists Barcode
among the fields AI platforms consider <sup>`[ACA-SHOP-008]`</sup>. Without it you are likelier to sit outside
the cluster — which removes you from the one comparison where your levers (price, stock) are
decisive. **Caveat, stated plainly:** how a UPID is derived is not documented, and no source says
GTIN feeds it. This is an inference with a clear test (E-3 in `05`), not a documented rule.

**Affects.** Cross-seller dedupe, comparison placement, Google Merchant Center feeds in parallel.
**Evidence.** <sup>`[ACA-CGPT-001]`</sup>, <sup>`[ACA-SHOP-008]`</sup>, <sup>`[ACA-CGPT-007]`</sup>. **Status.** recommended
(mechanism is **experimental**).

**Test.** Percent of variants with a valid-check-digit barcode. For a sample of 20 SKUs, query
ChatGPT for the exact product name + a competing retailer and record whether your store appears in
the comparison set. Log in `notes/` as raw observations before interpreting.

---

## 4. Make products *filterable*, not just describable — recommended

**Implement.** Shopify's cross-merchant Global Catalog accepts a closed set of filters agents can
use: `available`, `ships_to`, `ships_from`, `price`, `condition` (`new`/`secondhand`), `rating`
(with `min` and `min_count`), `price_tier`, `media` type, `categories` by taxonomy ID, and
`attributes`: "Filter by Shopify taxonomy attributes. Supported names are `Color`, `Size`, and
`Target gender`. Entries combine with AND logic. Values within one entry combine with OR logic.
Unsupported attribute names are ignored" <sup>`[ACA-SHOP-006]`</sup>. **VF.**

So, concretely:

- Variant options named exactly **Color** and **Size** (not "Colour", not "Shade", not "Fit").
- **Target gender** populated via product category metafields.
- Product category set so `categories` filtering can reach you.
- Reviews live, because `rating` filtering has a `min_count` — a product with 2 reviews fails
  `min_count: 10` no matter how good it is.
- Shipping countries configured, because `ships_to` is a filter.
- `available` "defaults to only sale-ready items" <sup>`[ACA-SHOP-006]`</sup> — out-of-stock is not a ranking
  penalty, it is a filter exclusion.

**Why.** **EBI:** a filter is a hard gate, not a weight. A missing attribute does not lower your
rank; it removes you from the candidate set for any query an agent translates into that filter.
This is the cheapest and most deterministic win available, and it is the one place where a published
field list tells you exactly what an agent can exclude you on.

Reinforcing signal on the ChatGPT side: shopping research is evaluated on "the percentage of
products in each response that meet the user requirements" <sup>`[ACA-CGPT-002]`</sup>. **VF.** A model scored
on constraint satisfaction has no reason to surface an item whose constraints it cannot verify.
**EBI.**

**Affects.** Global Catalog retrieval, Storefront Catalog, every UCP-based agent.
**Evidence.** <sup>`[ACA-SHOP-006]`</sup>, <sup>`[ACA-CGPT-002]`</sup>. **Status.** recommended.

**Test.** Call the public endpoint yourself and look for your own SKUs. It requires an agent
profile <sup>`[ACA-SHOP-006]`</sup>; set one up with `@shopify/ucp-cli` <sup>`[ACA-SHOP-009]`</sup>, then run
`search_catalog` with and without each filter and record which filters drop your products. That is
a direct, repeatable measurement of your own filterability, not a proxy metric.

---

## 5. Let Shopify's inference work for you — recommended

**Implement.** Write descriptions that state specifications in plain sentences: material, weight,
drop, width fit, use case, care. Put legal disclosures in **the first 6,000 characters** of the
description <sup>`[ACA-SHOP-002]`</sup>. **VF.**

**Why.** Shopify generates and ships extra structured fields derived from your content, flagged
`Inferred`: `description`, `options`, `metadata.attributes`, `tech_specs`, `top_features`,
`unique_selling_points`, `variants[].condition` — to be treated as "discovery and merchandising
signals, not as merchant-authored source text" <sup>`[ACA-SHOP-006]`</sup>. **VF.**

**EBI:** you do not control those fields directly, but they are extracted from text you do control.
Prose that names the spec ("8 mm heel-to-toe drop, 238 g, knit upper") yields usable `tech_specs`;
prose that says "engineered for effortless miles" yields nothing extractable.

**Affects.** Inferred catalog attributes → filterability (action 4) → retrieval.
**Evidence.** <sup>`[ACA-SHOP-006]`</sup>, <sup>`[ACA-SHOP-002]`</sup>. **Status.** recommended.

**Test.** `get_product` via Storefront Catalog MCP on your own store and read back the `tech_specs`
and `top_features` Shopify generated. Rewrite one product's copy, wait for the next catalog update,
re-read. Keep both payloads in `notes/raw/`.

---

## 6. Complete store policies and the agentic knowledge base — mandatory / recommended

**Implement.**
1. Settings → Policies: refund/return, privacy, terms, shipping. "Make sure that your store
   policies are complete and up-to-date… so that when a customer asks about your return policy in
   an AI interaction, the AI agent can reference the correct information that you've stored in
   Shopify" <sup>`[ACA-SHOP-008]`</sup>. **VF.**
2. **Sales channels** → **Agentic** → **Sources** → **Knowledge Base**. Publish non-product facts —
   returns process, shipping timelines, brand values. It is "the source of truth for AI agents for
   all non-product information about your store", queried "through the Storefront MCP"
   <sup>`[ACA-SHOP-010]`</sup>. **VF.** Cap: 1,000 facts. Content is auto-generated from your public storefront
   and admin data but stays unpublished until you publish it; Shopify "never changes knowledge base
   content on your behalf" <sup>`[ACA-SHOP-010]`</sup>. **VF.** Rescans take up to 48 hours.

**Why.** An agent that cannot resolve "what's the return window?" has a reason to recommend a
competitor who answers cleanly. **EBI** — no source quantifies this. On the ACP side, policy URLs
are structurally required for checkout eligibility (`seller_privacy_policy`, `seller_tos`), and
OpenAI's production checklist requires ToS and Privacy links "present and functional"
<sup>`[ACA-CGPT-007]`</sup>, <sup>`[ACA-CGPT-013]`</sup>. **VF.**

**Affects.** Agent answer quality, Copilot/Gemini direct checkout eligibility, ACP readiness.
**Evidence.** <sup>`[ACA-SHOP-008]`</sup>, <sup>`[ACA-SHOP-010]`</sup>, <sup>`[ACA-CGPT-007]`</sup>, <sup>`[ACA-CGPT-013]`</sup>.
**Status.** policies mandatory; knowledge base recommended.

**Test.** Ask ChatGPT and Gemini five store questions (returns, shipping time, sizing, materials,
warranty). Record the answer and whether it matches your published policy. Re-run after publishing
knowledge-base facts. Raw transcripts to `notes/raw/`, interpretation separate.

---

## 7. Map custom data and fix variant grouping — recommended

**Implement.** **Sales channels** → **Agentic** → **Shopify Catalog** → **Review product data
mapping** (Channel mapping). Needed if your real titles/descriptions live in metafields,
metaobjects, tag prefixes, or behind delimiters in titles <sup>`[ACA-SHOP-003]`</sup>. **VF.** You can also
"group separate products that are variants of the same product, so that they're displayed as a
single listing" <sup>`[ACA-SHOP-003]`</sup>. **VF.**

Also decide the compare-at behaviour: "you can choose whether Shopify Catalog uses the price or the
compare-at price as the list price. AI agents might use the list price to advertise strikethrough
pricing" <sup>`[ACA-SHOP-003]`</sup>. **VF.** In the Global Catalog, `list_price` appears only if the merchant
"shares compare-at prices with Shopify Catalog" and it exceeds the selling price <sup>`[ACA-SHOP-006]`</sup>.

**Why.** If a theme assembles the real product copy from metafields, the Catalog payload may be
sending something thinner than what shoppers see. Separately, one product split across five
"products" competes with itself and dilutes review counts — which then fails `rating.min_count`
filtering (action 4). **EBI.**

**Affects.** Catalog payload fidelity; variant consolidation; sale display.
**Evidence.** <sup>`[ACA-SHOP-003]`</sup>, <sup>`[ACA-SHOP-006]`</sup>. **Status.** recommended.

**Test.** Compare your PDP against the `get_product` payload field by field. Any field a shopper
sees but the payload lacks is a mapping gap.

---

## 8. robots.txt: do no harm, and don't block the wrong bot — mandatory (as a check)

**Implement.** Fetch `https://yourstore.com/robots.txt` and confirm nothing disallows OpenAI's
agents. Shopify's default is already permissive — `Allow: /` with admin/cart/checkout/account
disallowed <sup>`[ACA-SHOP-004]`</sup>. Observed on a live Shopify store: only `User-agent: *` and
`adsbot-google` groups, no AI-bot blocks <sup>`[ACA-OBS-003]`</sup>. **EO.**

The four agents and what blocking each costs you <sup>`[ACA-CGPT-008]`</sup>:

| Agent | Block it and you lose |
|---|---|
| `OAI-SearchBot` | ChatGPT search visibility — opted-out sites "will not be shown in ChatGPT search answers" |
| `ChatGPT-User` | Live user-triggered page reads (and "robots.txt rules may not apply" anyway) |
| `OAI-AdsBot` | Ad landing-page eligibility only |
| `GPTBot` | Training-corpus inclusion only — **no search effect** |

**GPTBot is the only genuine policy choice here.** It is about training, not visibility. Blocking
`OAI-SearchBot` to "protect content" is the common, costly mistake.

If you participate in OpenAI's feed programme, blocking is also a terms breach: merchants commit
not to block OpenAI crawlers "including via robots.txt" and to allowlist "OpenAI's and its
Affiliates' signed Web Bot Auth traffic" <sup>`[ACA-CGPT-011]`</sup>. **VF.**

**Only if you must customise**, add `templates/robots.txt.liquid`. Shopify: adding the template
"replaces Shopify's generated `robots.txt` output"; use the Liquid `robots` object so Shopify can
keep updating the defaults <sup>`[ACA-SHOP-011]`</sup>, <sup>`[ACA-SHOP-004]`</sup>. The `robots` object exposes
`default_groups`; a `group` has a `user_agent`, `rules` and an optional `sitemap`; a `rule` has a
`directive` (`Allow`/`Disallow`) and a `value` <sup>`[ACA-SHOP-011]`</sup>. **VF.**

```liquid
{%- comment -%}
  templates/robots.txt.liquid
  Renders Shopify's default groups unchanged, then appends explicit AI-agent groups.
  Explicit allows are belt-and-braces: `Allow: /` in the `*` group already permits these.
  Verify the rendered output against a saved copy of your previous /robots.txt before publishing.
{%- endcomment -%}
{%- for group in robots.default_groups -%}
  {{- group.user_agent }}
  {%- for rule in group.rules %}
  {{ rule }}
  {%- endfor %}
  {%- if group.sitemap %}
  {{ group.sitemap }}
  {%- endif %}

{% endfor -%}

User-agent: OAI-SearchBot
Allow: /
Disallow: /cart
Disallow: /checkout
Disallow: /account

User-agent: ChatGPT-User
Allow: /

User-agent: OAI-AdsBot
Allow: /

{%- comment -%} Training corpus. Flip to `Disallow: /` if that is your policy. {%- endcomment -%}
User-agent: GPTBot
Allow: /
```

**Warnings, verbatim.** Shopify calls this an unsupported customization, says support "can't help
with edits", and that "Incorrect use of the feature can result in loss of all traffic"
<sup>`[ACA-SHOP-004]`</sup>. Theme uploads through the admin "won't import robots.txt.liquid"
<sup>`[ACA-SHOP-004]`</sup>. Changes are instant "but crawlers don't always react immediately"
<sup>`[ACA-SHOP-004]`</sup>; OpenAI says search-related robots changes take "roughly a day" <sup>`[ACA-CGPT-008]`</sup>.
Remove any pre-existing Cloudflare-style workaround first <sup>`[ACA-SHOP-004]`</sup>.

**Affects.** Open-web discoverability only — not Shopify Catalog <sup>`[ACA-SHOP-004]`</sup>.
**Evidence.** <sup>`[ACA-SHOP-004]`</sup>, <sup>`[ACA-CGPT-008]`</sup>, <sup>`[ACA-CGPT-011]`</sup>, <sup>`[ACA-SHOP-011]`</sup>,
<sup>`[ACA-OBS-003]`</sup>. **Status.** mandatory as an audit; the template itself is **recommended** only if
you have a reason.

**Test.** `curl -s https://yourstore.com/robots.txt | grep -iA3 'OAI-\|GPTBot\|ChatGPT'`. Then
confirm real crawl traffic by checking server/CDN logs against OpenAI's published ranges —
`openai.com/searchbot.json`, `gptbot.json`, `chatgpt-user.json`, `adsbot.json` <sup>`[ACA-OBS-001]`</sup>.
User-agent strings alone are forgeable; the IP files are the check that means something.

---

## 9. Don't break agent access at the edge — mandatory if you run a proxy

**Implement.** Shopify: "Bot management is handled directly for stores on Shopify, and you don't
need to take any action. Shopify doesn't recommend a proxy configuration in front of Shopify, and
can't provide support for this either." <sup>`[ACA-SHOP-003]`</sup> **VF.** So the correct action for most
merchants is *remove* the extra layer.

If you keep one, allowlist ChatGPT's signed agent traffic. It signs requests per RFC 9421 with
`Signature`, `Signature-Input` and `Signature-Agent: "https://chatgpt.com"`, verifiable against
`https://chatgpt.com/.well-known/http-message-signatures-directory` <sup>`[ACA-CGPT-009]`</sup>. **VF.**

- **Cloudflare**: Security → WAF → custom rule → *Bot Detection ID equals* → `129220581`
  ("ChatGPT Operator") → Allow/Skip. "No additional signature verification is required."
- **Akamai**: Bot management → Custom Bot Categories → add Akamai-Defined bot "ChatGPT Agent" →
  Allow.
- **HUMAN Sightline**: Policies → Traffic Policy Settings → Known bots & Crawlers → "ChatGPT Agent"
  → ON / Allow.
- **Vercel**: nothing to configure; recognised as `chatgpt-operator`.
- **Other CDNs**: match `Signature-Agent` exactly against `"https://chatgpt.com"` (quotes
  included), fetch the key, validate per RFC 9421, "Allow requests only after successfully
  verifying their signatures."

All <sup>`[ACA-CGPT-009]`</sup>. **VF.**

**Why.** Shopping research reads product pages live <sup>`[ACA-CGPT-002]`</sup>. A WAF challenge returns a
challenge page instead of your product, and OpenAI explicitly ties merchant availability in
shopping research to following the allowlisting process <sup>`[ACA-CGPT-002]`</sup>. **VF.**

**Affects.** Path C (agentic page reading), ChatGPT agent/cloud-browser sessions.
**Evidence.** <sup>`[ACA-CGPT-009]`</sup>, <sup>`[ACA-CGPT-002]`</sup>, <sup>`[ACA-SHOP-003]`</sup>. **Status.** mandatory if a
proxy/WAF sits in front of your store; otherwise N/A.

**Test.** From outside your network:
`curl -s -o /dev/null -w '%{http_code}\n' -A 'OAI-SearchBot/1.4; +https://openai.com/searchbot' https://yourstore.com/products/<handle>`
Expect 200. A 403/503 means your edge blocks declared crawlers. Observed on a live Shopify store:
HTTP 200, 804,715 bytes with that user agent <sup>`[ACA-OBS-004]`</sup>. **EO.** This tests user-agent
handling only, not IP reputation — a pass here is necessary, not sufficient.

---

## 10. Agent discovery files: already done for you — recommended to review

**Implement.** Every Shopify store "automatically serves" `/agents.md` (the "canonical agent
discovery URL"), plus `/llms.txt` and `/llms-full.txt` for "older AI crawlers". All three return
the same content by default — store name, URL, sitemap link, policies, discovery endpoints — and
"You don't need a third-party app to generate these files." <sup>`[ACA-SHOP-003]`</sup> **VF.**

**Observed on a live Shopify store** <sup>`[ACA-OBS-002]`</sup> **EO**: `/agents.md` returns agent
instructions naming the Shop skill (`https://shop.com/SKILL.md`), UCP at `https://ucp.dev`,
`GET /.well-known/ucp` for the store profile, and the MCP endpoint `/api/ucp/mcp`. The
`/.well-known/ucp` document advertises UCP `2026-08-25` with cart, checkout, fulfillment, discount,
buyer-consent and order capabilities.

**Observed caveat** <sup>`[ACA-OBS-005]`</sup> **EO**: a headless (Next.js) Shopify store returned its SPA
HTML shell at `/agents.md`, not agent instructions. If you run Hydrogen/headless, verify this
yourself — the automatic behaviour is tied to the Shopify-served storefront.

To customise, add `agents.md.liquid` (changes all three URLs), or `llms.txt.liquid` /
`llms-full.txt.liquid` for one URL; the URL-specific template wins <sup>`[ACA-SHOP-003]`</sup>. **VF.**
Shopify's own framing: "Shopify Catalog is the authoritative product data feed to your agentic
channels. The agent discovery files are separate from Shopify Catalog, and they don't replace any
Shopify Catalog capabilities." <sup>`[ACA-SHOP-003]`</sup> **VF.**

**So: do not let an app sell you an `llms.txt` generator.** The file exists, and it is not the
product-data path.

**Affects.** Agent orientation and protocol discovery, not product ranking.
**Evidence.** <sup>`[ACA-SHOP-003]`</sup>, <sup>`[ACA-OBS-002]`</sup>, <sup>`[ACA-OBS-005]`</sup>. **Status.** recommended
(review); customisation **experimental**.

**Test.**
```bash
curl -s https://yourstore.com/agents.md | head -30
curl -s https://yourstore.com/.well-known/ucp | python3 -I -m json.tool | head -40
curl -s -o /dev/null -w '%{http_code}\n' https://yourstore.com/llms.txt
```

---

## 11. Product-page structured data — recommended

**Implement.** Keep `Product`/`ProductGroup` JSON-LD on PDPs with price, availability, brand,
GTIN and ratings. Shopify's own position is that this is what agents read: its agentic-readiness
scanner "check[s] your product page for the structured data that AI agents read to answer shoppers'
questions" <sup>`[ACA-SHOP-012]`</sup>. **VF (as stated by Shopify).** Run it:
`https://www.shopify.com/agentic-readiness`.

**Observed baseline** on a live Shopify store's PDP <sup>`[ACA-OBS-004]`</sup> **EO**: two `ld+json` blocks —
a `ProductGroup` with `@id`, `productGroupID`, `name`, `brand`, `description`, `image`, `sku`,
`offers` (`priceCurrency`, `price`, `itemCondition`, `availability`), `variesBy` and `hasVariant`;
and a *separate* block containing only `aggregateRating` (`ratingValue` 4.6, `reviewCount` 9951)
with no `@type` on the wrapper.

**EBI:** a review block detached from the Product node is weaker than one nested in it, because a
consumer has to join them. If your theme does this, nesting the rating inside the product node is a
low-risk improvement. **UH** that it changes ChatGPT ranking — OpenAI's docs never mention
schema.org. Note the asymmetry honestly: OpenAI's feed spec does not reference schema.org at all
<sup>`[ACA-CGPT-007]`</sup>, while Shopify markets structured data as what agents read <sup>`[ACA-SHOP-012]`</sup>. Both
can be true — different paths.

```html
<!-- Minimal addition if your theme emits aggregateRating detached from the product node -->
<script type="application/ld+json">
{
  "@context": "https://schema.org/",
  "@type": "Product",
  "name": "Trail Runner GTX",
  "brand": { "@type": "Brand", "name": "Your Brand" },
  "gtin13": "0123456789012",
  "sku": "TRGTX-BLK-9",
  "image": ["https://cdn.shopify.com/.../trgtx-black.jpg"],
  "aggregateRating": { "@type": "AggregateRating", "ratingValue": "4.6", "reviewCount": "9951" },
  "offers": {
    "@type": "Offer",
    "url": "https://yourstore.com/products/trail-runner-gtx?variant=123",
    "priceCurrency": "USD",
    "price": "95.00",
    "itemCondition": "https://schema.org/NewCondition",
    "availability": "https://schema.org/InStock"
  }
}
</script>
```

**Affects.** Path B/C only. Not the Shopify Catalog payload.
**Evidence.** <sup>`[ACA-SHOP-012]`</sup>, <sup>`[ACA-OBS-004]`</sup>, <sup>`[ACA-CGPT-007]`</sup>. **Status.** recommended;
specific ranking effect **unverified**.

**Test.** Shopify's scanner before/after, plus Google's Rich Results Test. Treat the scanner output
as what it says it is: "informational signals… that AI agents may use", with no guarantee
<sup>`[ACA-SHOP-012]`</sup>.

---

## 12. Keep B2B out, deliberately — mandatory if you sell B2B

Agentic storefronts "support only direct-to-consumer (D2C) sales" and Shopify auto-excludes B2B-only
products detected via B2B catalogs, customer-account requirements, or password-protected
storefronts <sup>`[ACA-SHOP-003]`</sup>. **VF.** But: "If you use third-party apps or custom theme
modifications to manage B2B pricing or product access controls… then Shopify might not be able to
detect that these products are intended only for B2B customers, and they might display on your
agentic storefronts." <sup>`[ACA-SHOP-003]`</sup> **VF.** Products sold to both audiences show your D2C price;
"B2B pricing doesn't display on agentic storefronts" <sup>`[ACA-SHOP-003]`</sup>. **VF.**

Fixes: native Shopify B2B catalogs/companies, product status **Unlisted**, or (Plus) a separate B2B
expansion store <sup>`[ACA-SHOP-003]`</sup>. **Status.** mandatory if applicable.

---

## 13. What you cannot control — read before promising anything

- Inclusion ≠ display. Shopify: inclusion "doesn't guarantee that a product will appear in a
  specific AI answer, be ranked in a specific position" <sup>`[ACA-SHOP-001]`</sup>. **VF.**
- "each channel controls the final ranking, wording, and shopping experience" <sup>`[ACA-SHOP-001]`</sup>.
  **VF.**
- OpenAI's feed terms: "Nothing in these Terms requires OpenAI to use or surface any Merchant
  Content" <sup>`[ACA-CGPT-011]`</sup>. **VF.**
- Feed eligibility flags: "Eligibility does not guarantee display" <sup>`[ACA-CGPT-007]`</sup>. **VF.**
- Opting a channel out does not remove you from the open web <sup>`[ACA-SHOP-002]`</sup>. **VF.**
- Accuracy is imperfect by OpenAI's own account: shopping research "might make mistakes about
  product details like price and availability" <sup>`[ACA-CGPT-002]`</sup>. **VF.** Expect wrong prices to be
  shown about your products, and keep availability current to reduce it.

---

## One-page checklist

```
[ ] Sales channels > Agentic > Shopify Catalog shows a product count, not "Ineligible"
[ ] Account standing clean: email verified, 2FA on, chargebacks low, invoices paid
[ ] Every product: category/Type set (never "Uncategorized"), Vendor = real brand
[ ] Every variant: valid GTIN in Barcode
[ ] Variant options named exactly Color / Size; Target gender populated
[ ] Reviews collected and live (rating filters have a min_count)
[ ] Shipping countries configured (ships_to is a filter)
[ ] Specs stated as plain text in the description; legal disclosures in first 6,000 chars
[ ] Settings > Policies complete (refund, privacy, terms, shipping)
[ ] Sales channels > Agentic > Knowledge Base reviewed and published
[ ] Channel mapping checked if product data lives in metafields/metaobjects
[ ] Duplicate "products" that are really variants grouped into one listing
[ ] robots.txt does not block OAI-SearchBot / ChatGPT-User / OAI-AdsBot
[ ] GPTBot decision made deliberately (training only — no search cost)
[ ] No unsupported proxy in front of Shopify; if one exists, ChatGPT signed agent allowlisted
[ ] /agents.md and /.well-known/ucp return real content (check twice if headless)
[ ] PDP JSON-LD: aggregateRating nested in the Product node; gtin13 present
[ ] shopify.com/agentic-readiness scan run and recorded
[ ] B2B-only products excluded by a method Shopify can detect
```
