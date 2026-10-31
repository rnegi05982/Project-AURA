Title: Global Catalog MCP

URL Source: https://shopify.dev/docs/agents/catalog/global-catalog

Markdown Content:
Use Global Catalog MCP when your agent needs to discover products across multiple Shopify merchants — for example, comparison shopping, cross-merchant discovery, or recommendations not tied to a specific store. For single-store agents, use [Storefront Catalog MCP](https://shopify.dev/docs/agents/catalog/storefront-catalog).

Product discovery follows a two-step flow:

1.   **Discover**: Your agent finds matching products using `search_catalog` or `lookup_catalog`. `search_catalog` supports a text query, an image, or a set of product IDs to find similar items. `lookup_catalog` resolves known identifiers to their current catalog data. Results are clustered by Universal Product ID (UPID) and include offers from multiple merchants.
2.   **Evaluate**: Your agent calls `get_product` with a product or variant ID to explore available options and refine selection — for example, which colors are available in size medium — then retrieve pricing and seller checkout links for the buyer's chosen variant.

The [Shopify AI Toolkit](https://shopify.dev/docs/apps/build/ai-toolkit)[installs](https://shopify.dev/docs/agents#get-started) the `ucp` skill, which lets agents in Cursor, Claude Code, and other compatible IDEs reach the Global Catalog by name. Ask your assistant in natural language (`"find me crewneck sweaters under $50"`) and the skill picks the right [UCP CLI](https://github.com/Shopify/ucp-cli) command, or run `ucp catalog` directly in a terminal. The skill also knows when to search the global catalog and when to scope to a single merchant.

Omit `--business` to query the global catalog; pass `--business <url>` to scope a search to a single merchant's storefront.

Pass a buyer-linked token to return personalized `search_catalog` results for a signed-in Shop customer. Request the `dev.ucp.shopping.catalog.search:read` scope when you [create the buyer-linked token](https://shopify.dev/docs/agents/profiles/buyer-linked-tokens).

Each variant includes `price`, the price the buyer pays, when a price is available. A variant can also include `list_price`, the merchant's compare-at price for the buyer's market. Use `list_price` to show a strikethrough price next to `price`.

`list_price` is returned only when both of the following are true:

*   The merchant shares compare-at prices with Shopify Catalog.
*   The variant's compare-at price is higher than its price.

Like `price`, `list_price` is in minor currency units and uses the same currency as `price`.

The `/api/ucp/mcp` endpoint requires an [agent profile](https://shopify.dev/docs/agents/get-started/profile). Every request must include a `meta.ucp-agent.profile` URL pointing to your agent's UCP profile. The returned tools depend on the capabilities your agent advertises.

If you host your own profile, declare both the base UCP capabilities and Shopify's extensions: the base capabilities unlock the tools, the extensions unlock Shopify's enriched fields, and an extension without its base capability is pruned in negotiation. For the Catalog, that means `dev.ucp.shopping.catalog.search` and `dev.ucp.shopping.catalog.lookup` plus `dev.shopify.catalog.global` (or `dev.shopify.catalog` on a merchant storefront). The [hosted profile](https://shopify.dev/ucp/agent-profiles/examples/2026-08-25/valid-with-capabilities.json) used in the examples below declares all of them.

*   [`search_catalog`](https://shopify.dev/docs/agents/catalog/global-catalog#search_catalog): Search for products across all Shopify merchants.
*   [`lookup_catalog`](https://shopify.dev/docs/agents/catalog/global-catalog#lookup_catalog): Look up products or variants by identifier.
*   [`get_product`](https://shopify.dev/docs/agents/catalog/global-catalog#get_product): Get full product details with variant selection.

For Shopify-specific extension fields, such as additional filters, variant fields, and inferred metadata, see [Global Catalog extension](https://shopify.dev/docs/agents/catalog/global-catalog-extension).

Some Global Catalog response fields are generated or enriched by Shopify, and are marked `Inferred` in the reference. These fields might not always be present or might vary in accuracy depending on available product data. Treat them as discovery and merchandising signals, not as merchant-authored source text.

| Field | Tag | Notes |
| --- | --- | --- |
| `description` | `Inferred` | Product description generated or enriched by Shopify. |
| `options` | `Inferred` | Product options normalized for catalog discovery and variant selection. |
| `metadata.attributes` | `Inferred` | Product attributes such as material, style, and occasion. |
| `metadata.tech_specs` | `Inferred` | Technical specifications. |
| `metadata.top_features` | `Inferred` | Top product features. |
| `metadata.unique_selling_points` | `Inferred` | Unique selling propositions. |
| `variants[].condition` | `Inferred` | Product condition labels, such as `"new"` or `"secondhand"`. |

Searches for products across all Shopify merchants.

The response conforms to the [UCP catalog search response](https://ucp.dev/latest/specification/shopping/catalog/search/), including a UCP metadata envelope; products with title, description, price range (minor units), media, and variants with `price` and, when available, `list_price`.

When to use:

*   A customer asks "I'm looking for trail running shoes under $150."
*   You need to find products matching criteria from any merchant.
*   A customer wants to compare products across multiple stores.

All parameters are wrapped in a `catalog` object. Refer to the [UCP catalog search spec](https://ucp.dev/latest/specification/shopping/catalog/search/) for the complete schema.

* * *

catalog.query•string

Free-text search query. For example, "trail running shoes", "organic coffee beans".

* * *

catalog.catalog_id•string

ID of a catalog configuration saved in the Dev Dashboard. Its filters set the request boundaries: values within them narrow the results, while values outside them fall back to the saved filters. The saved query prefix is prepended to catalog.query, combining both queries.

You can enable promoted placement for a saved catalog. Refer to [Earn with promoted placements](https://shopify.dev/docs/agents/catalog/promoted-placement) for setup, payouts, and disclosure details.

* * *

catalog.saved_catalog_slug•string

Deprecated compatibility alias for `catalog.catalog_id`. Use `catalog.catalog_id` for new integrations. If you pass both fields, then `catalog.catalog_id` takes precedence.

* * *

catalog.like•array

Similar item to search by. Use either an [item reference or image content](https://shopify.dev/docs/agents/catalog/global-catalog-extension#similarity-search).

Pass both `catalog.query` and an image in `catalog.like` for multimodal search. Multimodal search uses the text query to describe what the agent is looking for and the image to provide visual context, such as style, shape, or pattern. Pass only an image for visual similarity search, which returns items that visually resemble the image without additional text intent.

* * *

catalog.context•object

Buyer signals for relevance and localization (`address_country`, `address_region`, `postal_code`, `language`, `currency`, and `intent`).

* * *

catalog.filters.available•boolean

Filter by availability. Defaults to `true` (only sale-ready items). Set to `false` to include unavailable items.

* * *

catalog.filters.ships_to•object

Filter to products that ship to a given location. Accepts `country` (ISO 3166-1 alpha-2), `region`, and `postal_code`.

* * *

catalog.filters.ships_from•array

Filter by merchant origin country. Each entry accepts `country` (ISO 3166-1 alpha-2). Multiple entries use OR logic. Digital products that don't require shipping can still match this filter.

* * *

catalog.filters.price•object

Price range in minor currency units. Accepts `min` and `max` integers. For example, `{"min": 5000, "max": 20000}` = $50.00–$200.00 USD.

* * *

catalog.filters.condition•array

Product condition filter. Known values: `"new"`, `"secondhand"`. Multiple values use OR logic.

* * *

catalog.filters.shops•array

Filter to specific shops. Accepts an array of shop GIDs, for example `gid://shopify/Shop/987654321`. You can pass up to 1000 shop IDs per request.

* * *

catalog.filters.attributes•array

Filter by Shopify taxonomy attributes. Supported names are `Color`, `Size`, and `Target gender`. Entries combine with AND logic. Values within one entry combine with OR logic. Unsupported attribute names are ignored and returned in `messages`.

* * *

catalog.filters.rating•object

Filter by variant rating. `variant` matches products with at least one variant whose rating meets the given thresholds. Set `variant.min` for the minimum rating value (0–5 scale) and `variant.min_count` for the minimum number of reviews.

* * *

catalog.filters.price_tier•array

Filter by relative price tier within each product's category. Supported values are `low`, `medium`, and `high`. Multiple values use OR logic. Unsupported values are ignored and returned in `messages`.

* * *

catalog.filters.media•array

Filter by product media. Each entry is an object with a `type` field, and matches products that have at least one media item of that type. Supported types are `image`, `video`, `external_video`, and `model_3d`. `video` matches only Shopify-hosted videos. Use `external_video` for videos that are hosted on a third-party platform. Entries combine with AND logic. Unsupported types are ignored and returned in `messages`. For example, `[{"type": "video"}, {"type": "model_3d"}]` returns only products that have a video and a 3D model.

* * *

catalog.filters.categories•array

Filter by product category using taxonomy IDs. Each item accepts `id` (required) and `taxonomy` (optional, defaults to Shopify's standard taxonomy). Multiple values use OR logic.

* * *

catalog.pagination•object

Cursor-based pagination controls. Accepts `cursor` (string, opaque cursor from a previous response) and `limit` (integer, min `1`, default `10`, max `50`). Pass the returned `pagination.cursor` as `catalog.pagination.cursor` to request the next page. The cursor carries only the next result offset, so the request's `limit` controls page size. You can paginate up to 1,000 results. Beyond that depth, `has_next_page` is `false` regardless of how many results match.

The `total_count` field in the response is an estimate of how many results match the query, not an exact count. Don't rely on it for precise totals or to calculate an exact number of pages.

* * *

With the [Shopify AI Toolkit](https://shopify.dev/docs/apps/build/ai-toolkit)[installed](https://shopify.dev/docs/agents#get-started), ask your assistant in natural language (`"find wireless headphones under $100"`) and the `ucp` skill picks the right [UCP CLI](https://github.com/Shopify/ucp-cli) command. You can also run the command directly in a terminal:

Retrieves products or variants by identifier from across all Shopify merchants.

The response conforms to the [UCP catalog lookup response](https://ucp.dev/latest/specification/shopping/catalog/lookup/), including products with `inputs` correlation on each variant and `not_found` messages for unresolved identifiers. Variants include `list_price` when available. Refer to [Prices and list prices](https://shopify.dev/docs/agents/catalog/global-catalog#prices-and-list-prices).

When to use:

*   You have product or variant IDs from search results or deep links.
*   You need to resolve multiple identifiers in a single request.
*   You're validating cart items against current catalog data.

All parameters are wrapped in a `catalog` object. Refer to the [UCP catalog lookup spec](https://ucp.dev/latest/specification/shopping/catalog/lookup/) for the complete schema.

* * *

catalog.ids•array Required

Array of product or variant identifiers (1 to 50). Accepts `gid://shopify/p/{upid}`, `gid://shopify/ProductVariant/{id}`, and `http` or `https` Shopify product URLs. Multiple IDs that resolve to the same product are grouped into a single product in the response.

* * *

catalog.filters.ships_to•object

Filter to products that ship to a given location. Accepts `country`, `region`, and `postal_code`.

* * *

catalog.filters.ships_from•array

Filter by merchant origin country. Each entry accepts `country` (ISO 3166-1 alpha-2). Multiple entries use OR logic. Digital products that don't require shipping can still match this filter.

* * *

catalog.filters.available•boolean

Filter by availability. Defaults to `true` (only sale-ready items). Set to `false` to include unavailable items.

* * *

catalog.filters.condition•array

Product condition filter. Known values: `"new"`, `"secondhand"`. Multiple values use OR logic.

* * *

catalog.filters.shops•array

Filter to specific shops. Accepts an array of shop GIDs, for example `gid://shopify/Shop/987654321`. You can pass up to 1000 shop IDs per request.

* * *

catalog.context•object

Buyer context for localization (`address_country`, `address_region`, `postal_code`, `language`, `currency`, and `intent`).

* * *

With the [Shopify AI Toolkit](https://shopify.dev/docs/apps/build/ai-toolkit)[installed](https://shopify.dev/docs/agents#get-started), ask your assistant in natural language (`"look up this variant"`) and the `ucp` skill picks the right [UCP CLI](https://github.com/Shopify/ucp-cli) command. You can also run the command directly in a terminal:

Retrieves full details for a single product with optional variant selection.

The response conforms to the [UCP catalog `get_product`response](https://ucp.dev/latest/specification/shopping/catalog/lookup/#response_1), including `product.selected` reflecting effective option selections, option values with `available` and `exists` signals, and variants matching the selection. Variants include `list_price` when available. Refer to [Prices and list prices](https://shopify.dev/docs/agents/catalog/global-catalog#prices-and-list-prices).

When to use:

*   A customer has selected a product and needs full details.
*   You need to show variant options with availability signals.
*   A customer is making option selections (Color, Size, and so on).

All parameters are wrapped in a `catalog` object. Refer to the [UCP catalog lookup spec](https://ucp.dev/latest/specification/shopping/catalog/lookup/) for the complete schema.

* * *

catalog.id•string Required

Product or variant identifier. Accepts `gid://shopify/p/{upid}` or `gid://shopify/ProductVariant/{id}`.

* * *

catalog.selected•array

Option selections for variant narrowing. For example, `[{"name": "Color", "label": "Blue"}, {"name": "Size", "label": "10"}]`. The response reflects these selections in `product.selected` and filters the returned variants accordingly.

* * *

catalog.preferences•array

Option names in relaxation priority order. When an exact match isn't available, options are dropped from the end of this list first. For example, `["Color", "Size"]` drops Size before Color.

* * *

catalog.filters.ships_to•object

Filter to products that ship to a given location. Accepts `country`, `region`, and `postal_code`.

* * *

catalog.filters.ships_from•array

Filter by merchant origin country. Each entry accepts `country` (ISO 3166-1 alpha-2). Multiple entries use OR logic. Digital products that don't require shipping can still match this filter.

* * *

catalog.filters.available•boolean

Filter by availability. Defaults to `true` (only sale-ready items). Set to `false` to include unavailable items.

* * *

catalog.filters.condition•array

Product condition filter. Known values: `"new"`, `"secondhand"`. Multiple values use OR logic.

* * *

catalog.filters.shops•array

Filter to specific shops. Accepts an array of shop GIDs, for example `gid://shopify/Shop/987654321`. You can pass up to 1000 shop IDs per request.

* * *

catalog.context•object

Buyer context for localization (`address_country`, `address_region`, `postal_code`, `language`, `currency`, and `intent`).

* * *

With the [Shopify AI Toolkit](https://shopify.dev/docs/apps/build/ai-toolkit)[installed](https://shopify.dev/docs/agents#get-started), ask your assistant in natural language (`"show me this product in black"`) and the `ucp` skill picks the right [UCP CLI](https://github.com/Shopify/ucp-cli) command. You can also run the command directly in a terminal:
