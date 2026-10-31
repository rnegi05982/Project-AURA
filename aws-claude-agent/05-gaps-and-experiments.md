# Knowledge gaps, contradictions, and experiment designs

A gap stays a gap. Nothing here is softened into an inference.

---

## Part 1 — What no source establishes

### G-1. How ChatGPT ranks product results
OpenAI names five factors for choosing *between merchants selling the same product* — availability,
price, quality, primary-seller status, Instant Checkout enablement `[ACA-CGPT-001]`. No source
describes:
- how the candidate set is built in the first place (feed index vs web index vs live reads, and how
  they merge);
- any weight, ordering, or threshold among the five;
- what "quality" means — the word is never defined in any OpenAI document I fetched;
- what "primary seller" is determined from (brand ownership? `brand` field? `seller_name`?
  authorised-retailer data? none is stated).

Anything you read online that specifies these is Tier 4 speculation.

### G-2. Whether optional feed attributes actually change ranking
`[ACA-CGPT-003]` says recommended attributes "improve ranking, relevance, and user trust". That is
a vendor assertion with no magnitude, no field-level breakdown, and no way to audit. The playbook
treats it as directionally sound because the cost of compliance is near zero — not because it is
measured.

### G-3. How a Universal Product ID (UPID) is derived
Shopify clusters cross-merchant results by UPID `[ACA-SHOP-006]` but does not document how a UPID is
computed. Whether GTIN/barcode, title similarity, image embedding, or category+brand heuristics
feed it is unknown. This gap sits directly under playbook action 3 (fill the Barcode field), which
is why that action is marked **recommended / mechanism experimental** rather than mandatory.

### G-4. Whether ChatGPT reads schema.org markup at all
OpenAI's feed spec never mentions schema.org or Google Merchant Center `[ACA-CGPT-007]`. Shopify
markets structured data as "the structured data that AI agents read" `[ACA-SHOP-012]`. No OpenAI
source confirms or denies consuming JSON-LD. Both statements can hold if Shopify means Google and
other agents. **Unresolved.** Playbook action 11 is therefore "recommended; ranking effect
unverified."

### G-5. What retrieval stack ChatGPT search uses in 2026
The only statement is from 2024-10-31 — "third-party search providers, as well as content provided
directly by our partners" `[ACA-CGPT-005]`. Two years stale. `OAI-SearchBot` implies a first-party
index `[ACA-CGPT-008]`, and its IPs are Azure `[ACA-OBS-001]`, but no current source describes the
stack. Do not assert Bing.

### G-6. Shopify Catalog's update latency
Shopify says the catalog "continuously updates your product data" `[ACA-SHOP-003]` — no interval,
no SLA, no propagation figure. The only numbers anywhere nearby are 7 days for an opt-out to
propagate to ChatGPT `[ACA-SHOP-002]` and 48 hours for a knowledge-base rescan `[ACA-SHOP-010]`.
So a merchant cannot currently answer "if I fix my title today, when does ChatGPT see it?"

### G-7. What Shopify actually sends OpenAI, field by field
Shopify lists the fields AI platforms consider `[ACA-SHOP-008]` and the attributes shipped by
default `[ACA-SHOP-003]`. OpenAI publishes a feed schema `[ACA-CGPT-007]`. **Nobody publishes the
mapping between them.** Whether Shopify populates `gtin`, `review_count`/`star_rating`,
`shipping_price`, `accepts_returns`, `age_group`, `size_system` on a merchant's behalf is unknown.
This is the highest-value gap in the whole report: it decides whether playbook actions 3 and 4
reach ChatGPT or stop at Shopify's own surfaces.

### G-8. Whether an independent Shopify merchant can reach Instant Checkout
OpenAI's feed/checkout onboarding is "available to approved partners" `[ACA-CGPT-006]`. Shopify
says there is no ChatGPT direct-checkout setting `[ACA-SHOP-002]`. Whether a single merchant can
apply at `chatgpt.com/merchants` *independently of Shopify*, and what happens to a store already in
Shopify Catalog if they do, is undocumented.

### G-9. The shopping-research allowlisting path
`[ACA-CGPT-002]` tells merchants to "follow the allowlisting process", linking to an article whose
final URL is **ChatGPT Work's Cloud browser allowlisting** `[ACA-CGPT-009]`. The article ID is
stable; the slug and subject have drifted to an enterprise-browser topic. So there is no clear
merchant-facing allowlisting procedure for shopping research. Treat the CDN/WAF steps in playbook
action 9 as the best available reading, not as the documented process.

### G-10. Why `/agents.md` was absent on a headless store
`[ACA-OBS-005]`: Vuori — a merchant OpenAI itself names `[ACA-CGPT-001]` — returned an SPA shell at
`/agents.md`, against the doc's "Every Shopify store automatically serves" `[ACA-SHOP-003]`. n=1,
cause unknown (headless routing, custom domain, or doc overstatement).

### G-11. Third-party verification of any of this
Search engines were inaccessible to automated fetching `[ACA-OBS-006]`. Almost every claim in this
report is the operator describing its own system. There is no independent audit of ChatGPT product
ranking in evidence here, and I should not pretend otherwise.

---

## Part 2 — Contradictions on record

### C-1. Shopify merchants and in-ChatGPT checkout
- OpenAI `[ACA-CGPT-001]`: "over a million Shopify merchants, like Glossier, SKIMS, Spanx and Vuori,
  coming soon."
- Shopify `[ACA-SHOP-002]`, published 2026-10-21: "ChatGPT is a product discovery channel… there's
  no option to activate or deactivate a ChatGPT direct checkout setting in your Shopify admin."

Both VF as statements by their owners. The OpenAI post carries **no date in the capture** (the
origin 403s non-browser clients), so I cannot order them confidently. Most likely: announced
intent vs shipped state. **Resolve by getting a date on the OpenAI post from a browser.** Until
then, tell merchants ChatGPT is referral-only on Shopify, with in-channel checkout available on
Gemini/Copilot/Meta `[ACA-SHOP-005]`.

### C-2. Instant Checkout as a ranking factor, in one paragraph
`[ACA-CGPT-001]` says "Instant Checkout items are not preferred in product results" and, two
sentences later, lists "whether Instant Checkout is enabled" among ranking factors. Not reconciled
by OpenAI. Plausible reading: a tiebreaker within relevance rather than a boost — **UH**.

### C-3. robots.txt: merchant choice vs contractual obligation
Shopify presents allowing/blocking AI crawlers as a merchant choice `[ACA-SHOP-004]`. OpenAI's feed
terms commit merchants not to block OpenAI crawlers, including via robots.txt, and to allowlist
signed traffic `[ACA-CGPT-011]`. For a Shopify merchant whose data flows via Shopify Catalog, which
terms bind them is unclear — Shopify is the feed party, the merchant is not a direct signatory.
Flag to legal rather than guessing.

### C-4. `/agents.md` ≡ `/llms.txt`
Doc: all three URLs "return the same content" by default `[ACA-SHOP-003]`. Observed: 5,750 vs 5,793
bytes `[ACA-OBS-002]`. Trivial in effect; worth noting so nobody builds a byte-equality check.

### C-5. A tool summary that the raw bytes do not support
A rendered fetch of Shopify's "Selling on ChatGPT" page reported an eligibility requirement to
complete Settings → Policies. The raw markdown capture contains no such sentence
`[ACA-SHOP-002]`. The claim was dropped. Logged because it is the clearest demonstration in this
round that summarising fetch tools invent plausible detail, and the reason the registry carries a
fidelity column at all.

---

## Part 3 — Experiment designs

Conventions: raw observations go to `notes/raw-observations/` unedited; interpretation goes to
`notes/findings/`. Every run records UTC timestamp, account tier, region, and the exact prompt. A
single ChatGPT answer is not evidence — these are designed around repetition because the systems
are non-deterministic and personalised `[ACA-CGPT-002]`.

### E-1. Does fixing catalog fields change ChatGPT visibility? (the core question)
- **Tests:** G-2, G-6, G-7.
- **Design:** split your catalogue into matched pairs by category, price band and review count.
  Treat one of each pair: fill Type, Vendor, Barcode/GTIN, option names normalised to Color/Size,
  category metafields, specs stated in description. Leave the control untouched.
- **Measure:** weekly, 25 fixed prompts per category ("best trail running shoes under $120",
  "waterproof running shoes wide fit"), 3 fresh sessions each (logged-out where possible, memory
  off, one fixed region). Record: product named y/n, position, price quoted, whether the quoted
  price matches, citation URL.
- **Also record** server-side: `OAI-SearchBot` and `ChatGPT-User` hits per URL, validated against
  the published IP files `[ACA-OBS-001]` — not user agent alone.
- **Confound to state up front:** you cannot isolate ChatGPT from Shopify Catalog's own ranking
  changes, nor from competitors' edits. This measures the whole pipeline, not one stage.
- **Duration:** 6 weeks minimum, given the unknown propagation latency (G-6).

### E-2. What does Shopify actually ship about my products?
- **Tests:** G-7 — the highest-value gap.
- **Design:** set up an agent profile (`@shopify/ucp-cli` `[ACA-SHOP-009]`), then call
  `search_catalog` / `get_product` against your own store via Storefront Catalog MCP and the global
  endpoint `[ACA-SHOP-006]`. Dump the full JSON payload to `notes/raw-observations/`.
- **Measure:** diff the payload against your admin data. Specifically: is barcode/GTIN present? Is
  `rating`/review count present? `ships_to`? `condition`? What did Shopify put in the `Inferred`
  fields (`tech_specs`, `top_features`, `unique_selling_points`)?
- **Why it is first in line:** it is cheap, deterministic, needs no competitor cooperation, and it
  tells you whether actions 3 and 4 are real or theatre. Run this before E-1.

### E-3. Is GTIN what clusters offers across merchants?
- **Tests:** G-3.
- **Design:** pick 10 products you sell that other merchants also sell. Verify a correct GTIN on
  5 of them; clear it on the other 5 (or start from a sample where it is already missing). Call
  `lookup_catalog` with your product URL and inspect whether the returned cluster contains other
  merchants' offers.
- **Measure:** cluster membership and offer count per UPID, before and after.
- **Note:** this probes Shopify's clustering, which is **not** proven to be what ChatGPT uses.
  State that limit in the finding.

### E-4. Filter exclusion mapping
- **Tests:** G-2, and converts playbook action 4 from inference to measurement.
- **Design:** for each documented filter `[ACA-SHOP-006]` — `available`, `ships_to`, `price`,
  `condition`, `rating.min_count`, `price_tier`, `media`, `categories`, and `attributes` limited to
  Color/Size/Target gender — run `search_catalog` with the filter set and unset, scoped to your
  shop GID.
- **Measure:** how many of your SKUs survive each filter. Output a table: filter → percent of
  catalogue reachable. That table *is* the deliverable; it names your exclusions in priority order.
- **Cost:** low. This is the single most informative experiment per hour spent.

### E-5. Crawler and agent reachability
- **Tests:** G-9, G-10, playbook actions 8–10.
- **Design:** daily cron. For 20 PDPs: fetch with (a) a normal browser UA, (b)
  `OAI-SearchBot/1.4`, (c) `ChatGPT-User/1.0`. Record status, bytes, and whether the `ld+json`
  Product block is present in the response body. Separately, fetch `/agents.md`, `/llms.txt`,
  `/.well-known/ucp` and record status and bytes.
- **Measure:** any non-200, or any response where the structured data is missing for a bot UA but
  present for a browser.
- **Caveat to carry into the finding:** this tests UA handling only. Real crawl verification needs
  log analysis against the published IP ranges `[ACA-OBS-001]`, because UA strings are forgeable —
  the Cloudflare/Perplexity case is the cautionary precedent (see `04-reading-list.md` §6).

### E-6. Quoted-price accuracy audit
- **Tests:** the practical cost of G-6, plus OpenAI's own caveat that shopping research "might make
  mistakes about product details like price and availability" `[ACA-CGPT-002]`.
- **Design:** weekly, ask ChatGPT for the price and stock status of 20 of your SKUs by exact name.
  Record quoted price, quoted availability, and your true values at that moment.
- **Measure:** error rate and staleness in days. Then run one deliberate price change and time how
  long the stale figure persists.
- **Why it matters commercially:** a wrong low price in a product card is a support and chargeback
  problem, and it is the clearest business case for feed-freshness work.

### E-7. Knowledge-base effect on answer quality
- **Tests:** playbook action 6, which rests on inference.
- **Design:** 10 store-policy questions (returns window, exchange, shipping time, international,
  warranty) asked across ChatGPT, Gemini and Copilot, before and after publishing knowledge-base
  facts. Three sessions each, fresh context.
- **Measure:** answered-correctly / answered-incorrectly / refused-or-deflected. Score against your
  published policy text.
- **Note:** the knowledge base is queried via Storefront MCP `[ACA-SHOP-010]`, so a ChatGPT effect
  is not expected unless ChatGPT calls that endpoint — which no source confirms. A null result for
  ChatGPT alongside a positive result for an MCP-using agent would itself be the finding.

---

## Part 4 — What I would do next, in order

1. **E-2**, this week. It unblocks the interpretation of everything else and costs an afternoon.
2. **E-4**, immediately after. Produces the exclusion table that drives catalogue work.
3. Get a browser-read publication date on `openai.com/index/buy-it-in-chatgpt/` to settle **C-1**.
4. **E-5** as standing monitoring, since it is cheap and catches regressions.
5. Round 2 on Gemini — the Google & YouTube channel and Merchant Center feed path
   `[ACA-SHOP-005]`. Different mechanism, in-channel checkout, and a far better documented feed
   spec, which makes it a useful contrast for the G-7 mapping question.
6. Only then **E-1**, which is the expensive one and is only interpretable once E-2 has established
   what ChatGPT is actually being given.
