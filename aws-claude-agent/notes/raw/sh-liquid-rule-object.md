Title: Liquid objects: rule

URL Source: https://shopify.dev/docs/api/liquid/objects/rule

Markdown Content:
[Skip to main content](https://shopify.dev/docs/api/liquid/objects/rule#main-content)

[![Image 1: Docs page](https://shopify-assets.shopifycdn.com/shopifycloud/shopify-dev/production/assets/dev-docs-logo-2-light-D4UI1jxY.svg)![Image 2: Docs page](https://shopify-assets.shopifycdn.com/shopifycloud/shopify-dev/production/assets/dev-docs-logo-2-dark-BQ-Bk9XA.svg)](https://shopify.dev/docs)

*   [Apps](https://shopify.dev/docs/apps/build)
*   [Storefronts](https://shopify.dev/docs/storefronts)
*   [Agents](https://shopify.dev/docs/agents)
*   References
*   [Changelog](https://shopify.dev/changelog)

*   Ask assistant/

*   [Help](https://shopify.dev/support)
*   •
*   [Log in](http://dev.shopify.com/dashboard)

[![Image 3: Shopify Editions](https://shopify-assets.shopifycdn.com/shopifycloud/shopify-dev/production/assets/medallion-bag-3XHvC113.png)](https://www.shopify.com/editions/fall2026?utm_source=shopify-dev&utm_medium=shopify-dev&utm_campaign=fall2026_rkerbz&utm_content=shopify-dev-medallion-v1&utm_term=medallion#dev)

Expand sidebar

[Back to all APIs Liquid](https://shopify.dev/docs/api)

*   [Overview](https://shopify.dev/docs/api/liquid)
*   [What is a template language?](https://shopify.dev/docs/api/liquid#what-is-a-template-language)
*   [Variations of Liquid](https://shopify.dev/docs/api/liquid#variations-of-liquid)
*   [Liquid basics](https://shopify.dev/docs/api/liquid#liquid-basics)
*   [Defining logic with tags](https://shopify.dev/docs/api/liquid#defining-logic-with-tags)
*   [Modifying output with filters](https://shopify.dev/docs/api/liquid#modifying-output-with-filters)
*   [Referencing objects](https://shopify.dev/docs/api/liquid#referencing-objects)
*   [Resources & tools](https://shopify.dev/docs/api/liquid#resources-and-tools)

* * *

*   [Basics](https://shopify.dev/docs/api/liquid/basics)
*   Tags  
*   Filters  
*   
Objects

    *   [additional_ checkout_ buttons](https://shopify.dev/docs/api/liquid/objects/additional_checkout_buttons)
    *   [address](https://shopify.dev/docs/api/liquid/objects/address)
    *   [all_ country_ option_ tags](https://shopify.dev/docs/api/liquid/objects/all_country_option_tags)
    *   [all_ products](https://shopify.dev/docs/api/liquid/objects/all_products)
    *   [app](https://shopify.dev/docs/api/liquid/objects/app)
    *   [article](https://shopify.dev/docs/api/liquid/objects/article)
    *   [articles](https://shopify.dev/docs/api/liquid/objects/articles)
    *   [block](https://shopify.dev/docs/api/liquid/objects/block)
    *   [blog](https://shopify.dev/docs/api/liquid/objects/blog)
    *   [blogs](https://shopify.dev/docs/api/liquid/objects/blogs)
    *   [brand](https://shopify.dev/docs/api/liquid/objects/brand)
    *   [brand_ color](https://shopify.dev/docs/api/liquid/objects/brand_color)
    *   [brand_ colors](https://shopify.dev/docs/api/liquid/objects/brand_colors)
    *   [canonical_ url](https://shopify.dev/docs/api/liquid/objects/canonical_url)
    *   [cart](https://shopify.dev/docs/api/liquid/objects/cart)
    *   [checkout](https://shopify.dev/docs/api/liquid/objects/checkout)
    *   [closest](https://shopify.dev/docs/api/liquid/objects/closest)
    *   [collection](https://shopify.dev/docs/api/liquid/objects/collection)
    *   [collections](https://shopify.dev/docs/api/liquid/objects/collections)
    *   [color](https://shopify.dev/docs/api/liquid/objects/color)
    *   [color_ scheme](https://shopify.dev/docs/api/liquid/objects/color_scheme)
    *   [color_ scheme_ group](https://shopify.dev/docs/api/liquid/objects/color_scheme_group)
    *   [comment](https://shopify.dev/docs/api/liquid/objects/comment)
    *   [company](https://shopify.dev/docs/api/liquid/objects/company)
    *   [company_ address](https://shopify.dev/docs/api/liquid/objects/company_address)
    *   [company_ location](https://shopify.dev/docs/api/liquid/objects/company_location)
    *   [content_ for_ additional_ checkout_ buttons](https://shopify.dev/docs/api/liquid/objects/content_for_additional_checkout_buttons)
    *   [content_ for_ header](https://shopify.dev/docs/api/liquid/objects/content_for_header)
    *   [content_ for_ index](https://shopify.dev/docs/api/liquid/objects/content_for_index)
    *   [content_ for_ layout](https://shopify.dev/docs/api/liquid/objects/content_for_layout)
    *   [country](https://shopify.dev/docs/api/liquid/objects/country)
    *   [country_ option_ tags](https://shopify.dev/docs/api/liquid/objects/country_option_tags)
    *   [currency](https://shopify.dev/docs/api/liquid/objects/currency)
    *   [current_ page](https://shopify.dev/docs/api/liquid/objects/current_page)
    *   [current_ tags](https://shopify.dev/docs/api/liquid/objects/current_tags)
    *   [customer](https://shopify.dev/docs/api/liquid/objects/customer)
    *   [customer_ payment_ method](https://shopify.dev/docs/api/liquid/objects/customer_payment_method)
    *   [discount](https://shopify.dev/docs/api/liquid/objects/discount)
    *   [discount_ allocation](https://shopify.dev/docs/api/liquid/objects/discount_allocation)
    *   [discount_ application](https://shopify.dev/docs/api/liquid/objects/discount_application)
    *   [external_ video](https://shopify.dev/docs/api/liquid/objects/external_video)
    *   [filter](https://shopify.dev/docs/api/liquid/objects/filter)
    *   [filter_ value](https://shopify.dev/docs/api/liquid/objects/filter_value)
    *   [filter_ value_ display](https://shopify.dev/docs/api/liquid/objects/filter_value_display)
    *   [focal_ point](https://shopify.dev/docs/api/liquid/objects/focal_point)
    *   [font](https://shopify.dev/docs/api/liquid/objects/font)
    *   [forloop](https://shopify.dev/docs/api/liquid/objects/forloop)
    *   [form](https://shopify.dev/docs/api/liquid/objects/form)
    *   [form_ errors](https://shopify.dev/docs/api/liquid/objects/form_errors)
    *   [fulfillment](https://shopify.dev/docs/api/liquid/objects/fulfillment)
    *   [generic_ file](https://shopify.dev/docs/api/liquid/objects/generic_file)
    *   [gift_ card](https://shopify.dev/docs/api/liquid/objects/gift_card)
    *   [group](https://shopify.dev/docs/api/liquid/objects/group)
    *   [handle](https://shopify.dev/docs/api/liquid/objects/handle)
    *   [image](https://shopify.dev/docs/api/liquid/objects/image)
    *   [image_ presentation](https://shopify.dev/docs/api/liquid/objects/image_presentation)
    *   [images](https://shopify.dev/docs/api/liquid/objects/images)
    *   [instructions](https://shopify.dev/docs/api/liquid/objects/instructions)
    *   [line_ item](https://shopify.dev/docs/api/liquid/objects/line_item)
    *   [link](https://shopify.dev/docs/api/liquid/objects/link)
    *   [linklist](https://shopify.dev/docs/api/liquid/objects/linklist)
    *   [linklists](https://shopify.dev/docs/api/liquid/objects/linklists)
    *   [localization](https://shopify.dev/docs/api/liquid/objects/localization)
    *   [location](https://shopify.dev/docs/api/liquid/objects/location)
    *   [market](https://shopify.dev/docs/api/liquid/objects/market)
    *   [measurement](https://shopify.dev/docs/api/liquid/objects/measurement)
    *   [media](https://shopify.dev/docs/api/liquid/objects/media)
    *   [metafield](https://shopify.dev/docs/api/liquid/objects/metafield)
    *   [metafield_ namespace](https://shopify.dev/docs/api/liquid/objects/metafield_namespace)
    *   [metafields](https://shopify.dev/docs/api/liquid/objects/metafields)
    *   [metaobject](https://shopify.dev/docs/api/liquid/objects/metaobject)
    *   [metaobject_ definition](https://shopify.dev/docs/api/liquid/objects/metaobject_definition)
    *   [metaobject_ system](https://shopify.dev/docs/api/liquid/objects/metaobject_system)
    *   [metaobjects](https://shopify.dev/docs/api/liquid/objects/metaobjects)
    *   [model](https://shopify.dev/docs/api/liquid/objects/model)
    *   [model_ source](https://shopify.dev/docs/api/liquid/objects/model_source)
    *   [money](https://shopify.dev/docs/api/liquid/objects/money)
    *   [option_ with_ value](https://shopify.dev/docs/api/liquid/objects/option_with_value)
    *   [order](https://shopify.dev/docs/api/liquid/objects/order)
    *   [page](https://shopify.dev/docs/api/liquid/objects/page)
    *   [page_ description](https://shopify.dev/docs/api/liquid/objects/page_description)
    *   [page_ image](https://shopify.dev/docs/api/liquid/objects/page_image)
    *   [page_ title](https://shopify.dev/docs/api/liquid/objects/page_title)
    *   [pages](https://shopify.dev/docs/api/liquid/objects/pages)
    *   [paginate](https://shopify.dev/docs/api/liquid/objects/paginate)
    *   [parent_ relationship](https://shopify.dev/docs/api/liquid/objects/parent_relationship)
    *   [part](https://shopify.dev/docs/api/liquid/objects/part)
    *   [pending_ payment_ instruction_ input](https://shopify.dev/docs/api/liquid/objects/pending_payment_instruction_input)
    *   [policy](https://shopify.dev/docs/api/liquid/objects/policy)
    *   [powered_ by_ link](https://shopify.dev/docs/api/liquid/objects/powered_by_link)
    *   [predictive_ search](https://shopify.dev/docs/api/liquid/objects/predictive_search)
    *   [predictive_ search_ resources](https://shopify.dev/docs/api/liquid/objects/predictive_search_resources)
    *   [product](https://shopify.dev/docs/api/liquid/objects/product)
    *   [product_ option](https://shopify.dev/docs/api/liquid/objects/product_option)
    *   [product_ option_ value](https://shopify.dev/docs/api/liquid/objects/product_option_value)
    *   [quantity_ price_ break](https://shopify.dev/docs/api/liquid/objects/quantity_price_break)
    *   [quantity_ rule](https://shopify.dev/docs/api/liquid/objects/quantity_rule)
    *   [rating](https://shopify.dev/docs/api/liquid/objects/rating)
    *   [recipient](https://shopify.dev/docs/api/liquid/objects/recipient)
    *   [recommendations](https://shopify.dev/docs/api/liquid/objects/recommendations)
    *   [remote_ details](https://shopify.dev/docs/api/liquid/objects/remote_details)
    *   [remote_ product](https://shopify.dev/docs/api/liquid/objects/remote_product)
    *   [remote_ shop](https://shopify.dev/docs/api/liquid/objects/remote_shop)
    *   [request](https://shopify.dev/docs/api/liquid/objects/request)
    *   [robots](https://shopify.dev/docs/api/liquid/objects/robots)
    *   [routes](https://shopify.dev/docs/api/liquid/objects/routes)
    *   [rule](https://shopify.dev/docs/api/liquid/objects/rule)
    *   [script](https://shopify.dev/docs/api/liquid/objects/script)
    *   [scripts](https://shopify.dev/docs/api/liquid/objects/scripts)
    *   [search](https://shopify.dev/docs/api/liquid/objects/search)
    *   [section](https://shopify.dev/docs/api/liquid/objects/section)
    *   [self](https://shopify.dev/docs/api/liquid/objects/self)
    *   [selling_ plan](https://shopify.dev/docs/api/liquid/objects/selling_plan)
    *   [selling_ plan_ allocation](https://shopify.dev/docs/api/liquid/objects/selling_plan_allocation)
    *   [selling_ plan_ allocation_ price_ adjustment](https://shopify.dev/docs/api/liquid/objects/selling_plan_allocation_price_adjustment)
    *   [selling_ plan_ checkout_ charge](https://shopify.dev/docs/api/liquid/objects/selling_plan_checkout_charge)
    *   [selling_ plan_ group](https://shopify.dev/docs/api/liquid/objects/selling_plan_group)
    *   [selling_ plan_ group_ option](https://shopify.dev/docs/api/liquid/objects/selling_plan_group_option)
    *   [selling_ plan_ option](https://shopify.dev/docs/api/liquid/objects/selling_plan_option)
    *   [selling_ plan_ price_ adjustment](https://shopify.dev/docs/api/liquid/objects/selling_plan_price_adjustment)
    *   [settings](https://shopify.dev/docs/api/liquid/objects/settings)
    *   [shipping_ method](https://shopify.dev/docs/api/liquid/objects/shipping_method)
    *   [shop](https://shopify.dev/docs/api/liquid/objects/shop)
    *   [shop_ locale](https://shopify.dev/docs/api/liquid/objects/shop_locale)
    *   [sitemap](https://shopify.dev/docs/api/liquid/objects/sitemap)
    *   [sort_ option](https://shopify.dev/docs/api/liquid/objects/sort_option)
    *   [store_ availability](https://shopify.dev/docs/api/liquid/objects/store_availability)
    *   [store_ credit_ account](https://shopify.dev/docs/api/liquid/objects/store_credit_account)
    *   [swatch](https://shopify.dev/docs/api/liquid/objects/swatch)
    *   [tablerowloop](https://shopify.dev/docs/api/liquid/objects/tablerowloop)
    *   [tax_ line](https://shopify.dev/docs/api/liquid/objects/tax_line)
    *   [taxonomy_ category](https://shopify.dev/docs/api/liquid/objects/taxonomy_category)
    *   [template](https://shopify.dev/docs/api/liquid/objects/template)
    *   [theme](https://shopify.dev/docs/api/liquid/objects/theme)
    *   [transaction](https://shopify.dev/docs/api/liquid/objects/transaction)
    *   [transaction_ payment_ details](https://shopify.dev/docs/api/liquid/objects/transaction_payment_details)
    *   [unit_ price_ measurement](https://shopify.dev/docs/api/liquid/objects/unit_price_measurement)
    *   [user](https://shopify.dev/docs/api/liquid/objects/user)
    *   [user_ agent](https://shopify.dev/docs/api/liquid/objects/user_agent)
    *   [variant](https://shopify.dev/docs/api/liquid/objects/variant)
    *   [video](https://shopify.dev/docs/api/liquid/objects/video)
    *   [video_ source](https://shopify.dev/docs/api/liquid/objects/video_source)

[Full index](https://shopify.dev/docs/api/liquid/objects/rule)

# rule

Install AI Toolkit Ask about this page Copy MD

A rule for the `robots.txt` file, which tells crawlers which pages can, or can't, be accessed.

A rule consists of a directive, which can be either `Allow` or `Disallow`, and a value of the associated URL path.

For example:

Copy

9

1

Disallow: /policies/

`Disallow: /policies/`
You can output a rule directly, instead of referencing each of its properties.

* * *

Tip

You can [customize the `robots.txt` file](https://shopify.dev/themes/seo/robots-txt) with the [`robots.txt.liquid` template](https://shopify.dev/themes/architecture/templates/robots-txt-liquid).

**Tip:**
You can [customize the `robots.txt` file](https://shopify.dev/themes/seo/robots-txt) with the [`robots.txt.liquid` template](https://shopify.dev/themes/architecture/templates/robots-txt-liquid).

**Tip:** You can <a href="/themes/seo/robots-txt">customize the <code>robots.txt</code> file</a> with the <a href="/themes/architecture/templates/robots-txt-liquid"><code>robots.txt.liquid</code> template</a>.

* * *

## Properties

[Anchor to](https://shopify.dev/docs/api/liquid/objects/rule#rule-directive)

directive**directive**

[string](https://shopify.dev/docs/api/liquid/basics#string)

The directive of the rule.

[Anchor to](https://shopify.dev/docs/api/liquid/objects/rule#rule-value)

value**value**

[string](https://shopify.dev/docs/api/liquid/basics#string)

The value of the rule.

Example Access

9

1

2

3

4

{

"directive":"Disallow",

"value":"/*/checkouts/"

}

##### Example

```json
{
  "directive": "Disallow",
  "value": "/*/checkouts/"
}
```

Was this section helpful?

Yes No

### Updates

*   [Developer changelog](https://shopify.dev/changelog)
*   [Shopify Editions](https://www.shopify.com/editions)

### Business growth

*   [Shopify Partners Program](https://www.shopify.com/partners?shpxid=222dd762-CA08-48FF-E4D4-FF926B8FFCAD)
*   [Shopify App Store](https://apps.shopify.com/?shpxid=222dd762-CA08-48FF-E4D4-FF926B8FFCAD)

### Legal

*   [Terms of service](https://www.shopify.com/legal/terms?shpxid=222dd762-CA08-48FF-E4D4-FF926B8FFCAD)
*   [API terms of use](https://www.shopify.com/legal/api-terms?shpxid=222dd762-CA08-48FF-E4D4-FF926B8FFCAD)
*   [Privacy policy](https://www.shopify.com/legal/privacy?shpxid=222dd762-CA08-48FF-E4D4-FF926B8FFCAD)
*   [Partners Program Agreement](https://www.shopify.com/partners/terms?shpxid=222dd762-CA08-48FF-E4D4-FF926B8FFCAD)

### Shopify

*   [About Shopify](https://www.shopify.com/about?shpxid=222dd762-CA08-48FF-E4D4-FF926B8FFCAD)
*   [Shopify Plus](https://www.shopify.com/plus?shpxid=222dd762-CA08-48FF-E4D4-FF926B8FFCAD)
*   [Careers](https://www.shopify.com/careers?shpxid=222dd762-CA08-48FF-E4D4-FF926B8FFCAD)
*   [Investors](https://investors.shopify.com/home/default.aspx?shpxid=222dd762-CA08-48FF-E4D4-FF926B8FFCAD)
*   [Press and media](https://shopify.com/news?shpxid=7db0d4e4-24E8-4087-58FA-7EE470CA745A)

Assistant
