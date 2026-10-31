Title: Shopify Catalog and product discovery for agentic storefronts

URL Source: https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/products

Published Time: Wed, 21 Oct 2026 08:48:00 GMT

Markdown Content:
Your [eligible products](https://help.shopify.com/en/manual/shopify-catalog/requirements) are automatically discoverable by AI channels through [Shopify Catalog](https://help.shopify.com/en/manual/shopify-catalog), as well as other methods such as web crawling and indexing, or through product feeds that you own and share with companies for other purposes, for example, for advertising with Google.

Products are made available to Google AI Mode and Gemini through the [Google & YouTube sales channel](https://help.shopify.com/en/manual/online-sales-channels/marketplaces/google), and to Meta surfaces through the [Facebook and Instagram by Meta sales channel](https://help.shopify.com/en/manual/online-sales-channels/social-commerce/facebook-instagram-by-meta).

You can choose to remove Shopify Catalog access to your products for [ChatGPT](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/chatgpt#opt-out) or [Microsoft Copilot](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/microsoft#opt-in-out), however your products might still be displayed through other external discovery and listing methods. To hide products completely from AI channels, refer to [_Hiding products from being discoverable by AI channels_](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/products#hiding-product-discoverability).

Agentic storefronts that find products through Shopify Catalog, such as ChatGPT and Microsoft Copilot, can access and display your products only when your store is [eligible for Shopify Catalog](https://help.shopify.com/en/manual/shopify-catalog/requirements). Depending on your store status, either of the following scenarios can be displayed alongside **Sources**>**Shopify Catalog** in the **Sales channels**>[**Agentic**](https://admin.shopify.com/apps/agentic) section of your Shopify admin:

*   If your store's eligible, then the number of products that you have in Shopify Catalog is displayed. You can click the number, and then optionally click a link to [**Review product data mapping**](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/products#data-mapping).
*   If your store isn't eligible, then an **Ineligible** warning is displayed. Your store doesn't have any products in Shopify Catalog, but you can still customize your product data for Shopify Catalog on the **Channel mapping** page.

You can click **Ineligible** to view the reason that your store isn't eligible for Shopify Catalog. For a list of ineligibility messages, what each reason means, and what action you can take, refer to [_Shopify Catalog store ineligibility reasons_](https://help.shopify.com/en/manual/shopify-catalog/requirements#store-ineligibility-reasons).

If the message **Catalog eligibility details are temporarily unavailable** is displayed, then check back later or [contact Shopify Support](https://help.shopify.com/en/manual/your-account/contact-shopify-support) if the message persists.

When your products are syndicated to AI channels by [Shopify Catalog](https://help.shopify.com/en/manual/shopify-catalog), the products are listed by default with their title, description, options, images, price, availability, and other key attributes, all structured in a way that AI agents can parse and understand. Shopify Catalog continuously updates your product data, so AI channels receive your latest inventory and prices.

If your product data, such as title and description, is stored in custom fields, then you can [customize your product data for Shopify Catalog](https://help.shopify.com/en/manual/shopify-catalog/mapping) on the **Channel mapping** page to make sure that the product data is correctly sourced for agentic storefronts. Customizing your product data is most helpful for stores with custom data and grouping logic for their products, such as [metafields](https://help.shopify.com/en/manual/custom-data/metafields), [metaobjects](https://help.shopify.com/en/manual/custom-data/metaobjects), tag prefixes, or separators or delimiters in product titles. You can also group separate products that are variants of the same product, so that they're displayed as a single listing.

If you set compare-at prices on your products, then you can [choose whether Shopify Catalog uses the price or the compare-at price as the list price](https://help.shopify.com/en/manual/shopify-catalog/mapping#compare-at-prices). AI agents might use the list price to advertise strikethrough pricing for products that are on sale. If you choose **Price**, then Shopify Catalog uses each product's current price as the list price.

Shopify Catalog is the primary method for agentic storefronts to receive your product data. AI crawlers might also access your store directly through the open web. Crawler access is controlled in the following two layers:

*   **Network layer**: Bot management is handled directly for stores on Shopify, and you don't need to take any action. Shopify doesn't recommend a proxy configuration in front of Shopify, and can't provide support for this either.
*   **`/robots.txt` layer**: You can allow or block specific user-agent crawlers by [customizing your store's `robots.txt.liquid` template](https://help.shopify.com/en/manual/promoting-marketing/seo/editing-robots-txt). The rules that you set in your `/robots.txt` file are directional and advisory, and not all crawlers are guaranteed to follow them.

Every Shopify store automatically serves the following discovery URLs that AI agents can read to learn how your store works:

*   `/agents.md` — this is your canonical agent discovery URL, which is the source of truth and the primary location for agent discovery information.
*   `/llms.txt` and `/llms-full.txt` — these URLs are compatible with older AI crawlers that search for the specific URL conventions, and they can serve the same information as `/agents.md`.

By default, all three URLs return the same content, which includes context such as your store name, store URL, sitemap link, store policies, and discovery endpoints for other types of store information. You don't need a third-party app to generate these files. Shopify Catalog is the authoritative product data feed to your agentic channels. The agent discovery files are separate from Shopify Catalog, and they don't replace any Shopify Catalog capabilities.

If you want to customize what appears in your store's agent discovery files, then you can add any of the following Liquid templates to your theme:

*   `agents.md.liquid` changes the content that's served from all three URLs.
*   `llms.txt.liquid` changes content only for the `/llms.txt` URL.
*   `llms-full.txt.liquid` changes content only for the `/llms-full.txt` URL.

If you have both `agents.md.liquid` and a URL-specific template, such as `llms.txt.liquid`, then it's the URL-specific template that defines the content for that specific URL.

For more information, refer to the developer documentation about [agents.md.liquid](https://shopify.dev/docs/storefronts/themes/architecture/templates/agents-md-liquid), [llms.txt.liquid](https://shopify.dev/docs/storefronts/themes/architecture/templates/llms-txt-liquid), and [llms-full.txt.liquid](https://shopify.dev/docs/storefronts/themes/architecture/templates/llms-full-txt-liquid).

### Customize your agent discovery files

1.   From your Shopify admin, go to [**Online Store**](https://admin.shopify.com/themes).

2.   For the theme that you want to edit, click ![Image 1: Horizontal menu](https://cdn.shopify.com/shopifycloud/help-center/manual/admin-icons/MenuHorizontalIcon.svg)>**Edit code**.

3.   Click **Add a new template**, and then select `agents.md`, `llms.txt`, or `llms-full.txt`, depending on which URLs you want to override.

4.   Click **Create template**.

5.   Make your edits, and then click **Save**.

For product data accuracy and product discoverability with AI agents, you should focus on having [complete and well-structured product information in Shopify Catalog](https://help.shopify.com/en/manual/shopify-catalog/optimizing-products), and on following [SEO best practices](https://help.shopify.com/en/manual/promoting-marketing/seo). For deeper Shopify Catalog data optimization, such as metafields, conversational attributes, and mapping configurations, refer to [_Customizing your product data for Shopify Catalog_](https://help.shopify.com/en/manual/shopify-catalog/mapping).

Even when you opt out of Shopify Catalog access with Shopify's agentic storefronts, your products can still be found in AI channels in the same way that they're listed in traditional search engines such as Google. For example, if one of your products can be discovered in a Google web search, then the same product could also be found by a customer using Google Gemini. Shopify can't control any other ways in which your products might be listed by AI channels.

If you need to completely hide your products from being discoverable by AI channels, then you can [set the product status to be **Unlisted**](https://help.shopify.com/en/manual/promoting-marketing/seo/hide-a-page-from-search-engines#unlisted).

Shopify's agentic storefronts support only direct-to-consumer (D2C) sales. Products that are sold exclusively to business or wholesale customers are automatically excluded from AI channels when Shopify can identify them.

### How Shopify identifies B2B-only products

Shopify uses the following methods to detect and exclude B2B-only products:

*   [**B2B catalogs**](https://help.shopify.com/en/manual/b2b/catalogs): Products that you publish only to B2B markets, or in product catalogs that are assigned to specific [companies and locations](https://help.shopify.com/en/manual/b2b/catalogs/creating-catalogs#assign-catalog).
*   [**Customer account requirements**](https://help.shopify.com/en/manual/customers/customer-accounts/manage#b2b-customer-accounts): Products that require your customers to authenticate themselves on your store before viewing them.
*   [**Storefronts in private mode**](https://help.shopify.com/en/manual/online-store/themes/password-page): Products that require your customers to enter a password on your store before accessing them.

### Considerations for custom B2B store setups

If you use third-party apps or custom theme modifications to manage B2B pricing or product access controls on your store, such as hiding prices until customers log in, then Shopify might not be able to detect that these products are intended only for B2B customers, and they might display on your agentic storefronts.

To prevent B2B-only products from displaying on your agentic storefronts, consider any of the following options:

*   Use [Shopify B2B](https://help.shopify.com/en/manual/b2b), including [catalogs](https://help.shopify.com/en/manual/b2b/catalogs) and [companies](https://help.shopify.com/en/manual/b2b/companies-and-customers), for your wholesale business.
*   [Hide specific products from AI channels](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/products#hiding-product-discoverability) when they shouldn't be discoverable by D2C customers.
*   If you're on the Shopify Plus plan, then use a separate expansion store for B2B. Learn more about [choosing a store type for your B2B business](https://help.shopify.com/en/manual/b2b/getting-started/store-type).
