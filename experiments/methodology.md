# Experiment methodology

Experiments observe what AI applications output. They do not reveal internal algorithms. A finding from an experiment is classified EXPERIMENTALLY OBSERVED and states its conditions, sample size and limitations.

## Unit of observation

A **run** is one query, sent once, to one application, in one mode, under one account state, from one location, at one timestamp. Every product the answer shows is an **item** of that run.

## Conditions to fix and record per run

| Condition | Values to record | Why it matters |
|---|---|---|
| Application + version | e.g. ChatGPT web, app build if shown | UI and features differ by client |
| Model | model picker value, or "default" | Model choice changes answers |
| Mode | default chat / search / shopping research / agent / other | Each mode uses different retrieval paths |
| Account state | logged-out / logged-in fresh / logged-in with history | Personalization |
| Personalization | memory on/off, chat history reference on/off, custom instructions empty?, temporary chat? | Memory can change recommendations |
| Location | IP country and city, VPN yes/no, account country | Regional catalogs and currency |
| Language and currency | query language, currency in query | ₹ vs $ can change sources |
| Date-time | ISO 8601 with timezone | Indexes and prices change |
| Operator | who ran it | Audit |

Default condition for baseline runs: logged-out or temporary chat, no custom instructions, India IP without VPN, English query.

## Query sets

- Queries are fixed strings stored in `test-cases/`. Never edit a query after the first run; add a new query ID instead.
- Each query set mixes intents: price-constrained ("under ₹1,000"), attribute-constrained ("microwave-safe"), use-case ("for office use"), style ("minimalist, wooden handle"), and brand-neutral superlatives ("best").
- Keep one query per run. Follow-up turns are a separate experiment type.

## Probe products

A **probe product** is a product AURA tracks across runs, with ground truth captured on the run date from its own product page: title, price, currency, availability, material, dimensions, GTIN if shown, canonical URL. Probe panels mix Shopify stores, Amazon.in, Flipkart and other independent stores. Ground truth lets us score attribute accuracy.

## Repetition

- Minimum 5 runs per query per condition, spread over at least 3 calendar days.
- Run all conditions for a query within the same day when comparing conditions.
- Report variance, not only means. A product seen in 1 of 5 runs is a different finding from one seen in 5 of 5.

## Metrics

| Metric | Definition |
|---|---|
| Appearance rate | runs containing the product ÷ total runs |
| Mean position | average 1-based rank among items, over runs where it appears |
| Source-type share | share of items by seller type: marketplace / Shopify store / other independent store / unknown |
| Run-to-run stability | mean pairwise Jaccard similarity of item sets (by canonical product URL or GTIN) across repeated runs |
| Attribute accuracy | share of shown attributes (price, availability, material, size) that match ground truth captured the same day |
| Citation domains | domains of cited links, counted per run |
| Sponsored share | items or units labeled sponsored/ad ÷ all items |

Seller platform detection (e.g. "is this a Shopify store?") is recorded with the method used (e.g. `/cart.js` response, `cdn.shopify.com` assets) and treated as an inference.

## Recording format

One JSON object per run in `raw-observations/<platform>/<YYYY-MM-DD>/<run-id>.json`, plus a full-page screenshot with the same base name.

```json
{
  "run_id": "CGPT-Q01-20261101-01",
  "query_id": "Q01",
  "query_text": "Best ceramic coffee mug under ₹1,000",
  "platform": "ChatGPT",
  "client": "web",
  "model": "default",
  "mode": "default",
  "account_state": "logged-out",
  "personalization": {"memory": "off", "temporary_chat": true, "custom_instructions": "none"},
  "location": {"ip_country": "IN", "city": "", "vpn": false},
  "timestamp": "2026-11-01T10:15:00+05:30",
  "operator": "",
  "items": [
    {
      "position": 1,
      "product_title": "",
      "seller": "",
      "seller_type": "marketplace|shopify|independent|unknown",
      "url_shown": "",
      "price_shown": "",
      "currency": "INR",
      "attributes_shown": {},
      "image_shown": true,
      "label": "organic|sponsored|unknown",
      "ui_unit": "product carousel|inline text|merchant list|other"
    }
  ],
  "citations": [""],
  "notes": ""
}
```

Raw observation files are never edited after capture. Corrections go in `findings/` with the run ID.

## Interventions (controlled store changes)

Single-variable tests on a store AURA controls, e.g. unblock a crawler, add GTINs, submit a product feed.

1. Run a baseline: at least 2 weeks of runs before the change.
2. Change one variable. Log the exact change and timestamp.
3. Keep running the same query set for at least 4 weeks.
4. Report the change in appearance rate with the baseline variance beside it.

Known confounds: platform model updates, index refresh timing, competitor changes, seasonality. Record platform release notes published during the test window.

Shopify-hosted storefronts do not give merchants raw server access logs. Verifying crawler visits to a Shopify store needs a separate method (unverified; to be researched).

## Compliance

- OpenAI's Terms of Use list this among prohibited uses: "Automatically or programmatically extract data or Output (defined below)." (OpenAI, Terms of Use, https://openai.com/policies/row-terms-of-use/, accessed 2026-10-30). ChatGPT runs are therefore manual.
- API results (e.g. a model with a web search tool) are a different system from the ChatGPT consumer product. Label them as API runs and never mix them with ChatGPT runs.
- Check each other platform's terms before automating any run.

## Interpretation rules

- Raw observations stay separate from interpretation.
- One experiment never establishes a ranking algorithm. It establishes an observed output under stated conditions.
- Distinguish organic items from sponsored items in every metric.
