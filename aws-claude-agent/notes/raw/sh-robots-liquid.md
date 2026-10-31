Title: robots.txt.liquid

URL Source: https://shopify.dev/docs/storefronts/themes/architecture/templates/robots-txt-liquid

Markdown Content:
The `robots.txt.liquid` template renders the `robots.txt` file, which is hosted at the `/robots.txt` URL.

The `robots.txt` file tells search engines which pages can, or can't, be crawled on a site. It contains groups of rules for doing so, and each group has three main components:

*   The user agent, which notes which crawler the group of rules applies to. For example, `adsbot-google`.
*   The rules themselves, which note specific URLs that crawlers can, or can't, access.
*   An optional sitemap URL.

Shopify generates a `robots.txt` file by default, which works for most shops, so this template isn't included in any themes by default.

Tip

If you want to customize the `robots.txt.liquid` template, then refer to [Customize robots.txt](https://shopify.dev/docs/storefronts/themes/seo/robots-txt) for more information.

* * *

The `robots.txt.liquid` template is located in the `templates` directory of the theme:

If your theme doesn't already contain the `robots.txt.liquid` template, then you can add it with the following steps:

1.   From your Shopify admin, go to **Online Store**>**Themes**.

2.   Find the theme that you want to edit, and then click **...**>**Edit code**.

1.   In the left sidebar, locate the **Templates** folder.
2.   Right-click on the **Templates** folder.
3.   Click **New File** from the context menu.
4.   Name the file `robots.txt.liquid`.
5.   Press Enter to create the file.

* * *

This template can't be a [JSON template](https://shopify.dev/docs/storefronts/themes/architecture/templates/json-templates). It must be `robots.txt.liquid`.

Adding this template replaces Shopify's generated `robots.txt` output. The Liquid [`robots` object](https://shopify.dev/docs/api/liquid/objects/robots) provides default rule groups that you can use as a starting point for customizations, but the rendered template output doesn't always match the generated file exactly.

Before you publish a customization, save a copy of your current `/robots.txt` output and compare it with the rendered template output.

The following example outputs the rule groups from the `robots` object:

While you can replace all the template content with plain text rules, it's strongly recommended to use the provided Liquid objects whenever possible.

* * *

If you want to customize the `robots.txt.liquid` template, then you need to add it with the following steps:

1.   In the code editor for the theme you want to edit, locate the **Templates** folder.
2.   Right-click on the **Templates** folder.
3.   Click **New File** from the context menu.
4.   Name the file `robots.txt.liquid`.
5.   Press Enter to create the file.

To learn about customizing this template, refer to [Customize robots.txt](https://shopify.dev/docs/storefronts/themes/seo/robots-txt).

* * *

Was this page helpful?
