Title: Editing robots.txt.liquid

URL Source: https://help.shopify.com/en/manual/promoting-marketing/seo/editing-robots-txt

Markdown Content:
Search engines, such as Google, constantly crawl the internet in search of new data as a source for their search results. The **robots.txt** file tells search engine bots, known as crawlers, which pages to request to view from your online store. All Shopify stores have a default **robots.txt** file that's optimal for Search Engine Optimization (SEO).

Your sitemap is used by search engines to place your online store in the search engine results. Learn how to [find and submit your sitemap](https://help.shopify.com/en/manual/promoting-marketing/seo/find-site-map).

When working with robots.txt, it's important to understand the difference between **crawling** and **indexing**:

*   **Crawling**: When search engine bots (such as Googlebot) examine all the content and code on your pages and analyze it
*   **Indexing**: When pages become eligible to appear in search engine results

These processes aren't mutually exclusive - search engines can index a page without crawling it if they discover it through other means.

The default **robots.txt** file works for most stores. If you want to customize the **robots.txt** file, then you must first add a **robots.txt.liquid** file to the **templates** folder of your theme in [the code editor](https://help.shopify.com/en/manual/online-store/themes/customizing-themes/edit-code/edit-theme-code), and then customize the content of the file. You can make the following edits:

*   Allow or disallow certain URLs from being crawled.
*   Add crawl-delay rules for certain crawlers.
*   Add extra sitemap URLs.
*   Block certain crawlers.

The **robots.txt** file is located at the root directory of your Shopify store's [primary domain name](https://help.shopify.com/en/manual/domains/managing-domains). Such as: `example.com/robots.txt`.

If you want to edit the**robots.txt.liquid**file, then you should work with a Shopify Partner or have expertise in code edits and SEO.

You can use Liquid to add or remove directives from the **robots.txt.liquid** template. This method preserves Shopify’s ability to keep the file updated automatically in the future, and is recommended. For a full guide on editing this file, refer to Shopify's Developer page [Customize robots.txt.liquid](https://shopify.dev/themes/seo/robots-txt).

Remove any previous customizations or workarounds, such as using a third-party service such as Cloudflare, before you edit the**robots.txt.liquid**file.

#### Steps:

1.   From your Shopify admin, go to [**Online Store**](https://admin.shopify.com/themes).

2.   For the relevant theme, click ![Image 1: Horizontal menu](https://cdn.shopify.com/shopifycloud/help-center/manual/admin-icons/MenuHorizontalIcon.svg)>**Edit code**.

3.   Click **Add a new template**, and then select **robots**.

4.   Click **Create template**.

5.   Make the changes that you want to make to the default template. For more information on liquid variables and common use cases, refer to Shopify's Developer page [Customize robots.txt.liquid](https://shopify.dev/themes/seo/robots-txt).

6.   Save changes to the robots.txt.liquid file in your published theme.

Changes are instant, but crawlers don't always react immediately. You can test changes using [Google's robots.txt Tester](https://support.google.com/webmasters/answer/6062598?hl=en).

You can also delete the contents of the template and replace it with plain text rules. This method is strongly not recommended, as rules may become out of date. If you choose this method, then Shopify can’t ensure that SEO best practices are applied to your robots.txt over time, or make changes to the file with future updates.

In Google Search Console, URLs might display as "indexed, though blocked by robots.txt". This is normal behavior and usually not a cause for concern.

### Why this happens

Many pages are intentionally blocked by robots.txt for SEO optimization. This message is Google's way of letting you know they've discovered blocked content, in case the blocking was unintentional. Everything in Shopify's default robots.txt file is there for a reason to help your SEO.

If a normal page on your site (such as your homepage) displays as "Indexed, though blocked," then it usually means Google's data about your store is outdated. Google can take days, weeks, or months to update their database with the latest changes to any website.

### What to do

In most cases, no action is needed. This is expected behavior for pages that should be blocked from crawling but might still be indexed through other discovery methods.

If you sell through [agentic storefronts](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts) such as ChatGPT or Microsoft Copilot, then your product data is syndicated to those channels through [Shopify Catalog](https://help.shopify.com/en/manual/shopify-catalog), independently of `/robots.txt`. AI crawlers might also access your store directly through the open web. Crawler access has the following two layers of control:

*   **Network layer**: Bot management is handled directly for stores on Shopify, and you don't need to take any action. Shopify doesn't recommend a proxy configuration in front of Shopify, and can't provide support for this either.
*   **`/robots.txt` layer**: You can allow or block specific user-agent crawlers by [customizing your store's `robots.txt.liquid` template](https://help.shopify.com/en/manual/promoting-marketing/seo/editing-robots-txt#edit-robots-txt-liquid). The rules that you set in your `/robots.txt` file are directional and advisory, and not all crawlers are guaranteed to follow them.

Blocking AI crawlers at the `/robots.txt` or network layer affects only open-web discoverability. It doesn't stop your product data from being sent by Shopify Catalog to the agentic storefronts that you've activated. To control what Shopify Catalog shares with agentic storefronts, refer to [_Understanding your agentic storefronts settings_](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/agentic-home#manage-for-me).

Shopify's default **robots.txt** file includes rules that optimize your store's SEO. The following are some of the key entries:

*   The `Allow: /` rule lets crawlers request your public content, such as your product, collection, page, blog, and policy pages.
*   The `Disallow: /admin` rule keeps admin pages from being crawled, because crawlers can't access them anyway.
*   The `Disallow: /cart/` rule keeps cart links from being crawled, because they're unique to each customer.
*   The `Disallow: /checkout` and `Disallow: /checkouts/` rules keep checkout pages from being crawled.
*   The `Disallow: /account` and `Disallow: /orders` rules keep account and order pages from being crawled, because they're specific to a single customer.
*   The `Disallow: /collections/*+*` rule keeps filtered collection pages from being crawled, because they duplicate content that's already on the collection page.
*   The `Disallow: /collections/*sort_by*` rule keeps sorted collection pages from being crawled, because they return the same products in a different order.

These rules help search engines focus on your unique content rather than on administrative or duplicate pages.

If you want to use the default **robots.txt** file again, then you can delete your custom **robots.txt.liquid** file.

#### Steps:

1.   From your Shopify admin, go to [**Online Store**](https://admin.shopify.com/themes).

2.   Click ![Image 2: Horizontal menu](https://cdn.shopify.com/shopifycloud/help-center/manual/admin-icons/MenuHorizontalIcon.svg)>**Edit code**.

3.   Right-click the **robots.txt.liquid**, and select **Delete permanently** from the drop-down menu.

4.   Click **Delete**.

You can always edit the `robots.txt.liquid` file in the future, or if you saved your past customizations, then you can redo your changes by copying over your saved previous customizations.
