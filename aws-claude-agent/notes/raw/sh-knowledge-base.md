Title: Answering customer questions with your knowledge base

URL Source: https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/knowledge-base

Published Time: Wed, 21 Oct 2026 08:48:00 GMT

Markdown Content:
You can publish facts about your store for AI retrieval with the **Knowledge base** page in your Shopify admin.

You can review and confirm store details such as your return process, shipping timelines, or brand values. These facts are the source of truth for AI agents for all non-product information about your store.

When a customer asks a question about your store in an AI chat, the agent can query your knowledge base through the [Storefront MCP](https://shopify.dev/docs/apps/build/storefront-mcp) to find answers. A reliable and up-to-date knowledge base gives AI agents a trustworthy data source to generate accurate answers from.

You can review knowledge base references and sources, edit information, manually add information to existing facts, and add your own facts.

Before you make any changes to your knowledge base, review the following considerations:

*   Your store's published knowledge base is publicly available through the Storefront MCP and can be used by AI channels including [Shop](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/agentic-home#shop) and third-party platforms.
*   The facts that Shopify generates from a scan of your storefront are unpublished until you publish them.
*   The facts that are linked to your Shopify admin, such as your store policies and your contact details, are published when Shopify creates them.
*   You can [publish or unpublish](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/knowledge-base#publish-unpublish) all referenced information, only specific categories of information, or just individual fields of category information.
*   Your knowledge base can hold a total of 1,000 facts, which includes both the facts that are generated for you and any additional facts.
*   [Custom storefronts](https://help.shopify.com/en/manual/custom-storefronts) and stores on the [Agentic plan](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/agentic-plan-setup) can add only [additional facts](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/knowledge-base#additional-facts) to their knowledge base.
*   If your Shopify store is [password-protected](https://help.shopify.com/en/manual/online-store/themes/password-page), then knowledge base can't access your online store, and your knowledge base displays data and information only from your Shopify admin.

Your knowledge base content is automatically generated from information that's publicly available on your storefront, and from any applicable Shopify admin data.

Your store is regularly scanned, and when a scan finds new information, it can be offered as a suggested update that you can [accept or reject](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/knowledge-base#accept-reject). Shopify never changes knowledge base content on your behalf. You continue to receive suggested updates for content that you edit manually.

Information is standardized and grouped into the following available categories, with sources and reference links for individual fields, based on what AI agents are likely to query about your store:

*   **About the Store**: Includes a store description and your target audience, plus the core facts about your business, including details about ownership, history, size, business model, and social mission.
*   **Brand and Identity**: Details about your own product brands and any third-party brands that you sell, plus your brand values and brand aesthetic that represent your business and store.
*   **Company policies**: Details and links for your available store policies, including **Terms of service**, **Privacy policy**, **Shipping policy**, and **Returns policy**. You're also notified about any **Missing** policies in the **Policies** section of the knowledge base page.
*   **Contact**: Address, email, phone number, and social media profiles for your store.
*   **Gift services**: Whether you offer gift cards, gift receipts, gift registry, or gift wrapping.
*   **Payment**: Information about the accepted payment methods that customers can use on your store's checkout.
*   **Returns & warranty**: Details about your return policy and window, refund information, and warranty services, plus a link for [customer self-serve returns](https://help.shopify.com/en/manual/fulfillment/managing-orders/returns/self-serve-returns) if you offer that service on your store.
*   **Second hand**: Whether you sell second-hand products.
*   **Fulfillment**: The types of shipping and delivery that your store offers, such as international shipping, express delivery, or pickup in store.
*   **Additional facts**: Add store information that's not already answered by your knowledge base, and that you want AI agents to know about.

### Understanding your knowledge base sources

Each knowledge base category contains individual fields for specific pieces of information. The icon that's displayed with a field depends on the source that the information has come from. Review the following icons that might be displayed:

You can review your knowledge base to understand what AI agents know about your store, including viewing the sources and references in each category of information, changing a source, adding new references, or removing references.

Each individual field of category information in your knowledge base has one source, and can have multiple reference links.

The source is where the information in a field comes from. A field can be sourced from a scan of your storefront, from a specific location in your Shopify admin, or from information that you enter manually. The [icon](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/knowledge-base#source-icons) that's displayed with a field tells you which source it uses. You can [change a storefront source or an admin source to a manual source](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/knowledge-base#change-source) at any time. If you set a field to **Manual**, then the ![Image 1: Compose](https://cdn.shopify.com/shopifycloud/help-center/manual/admin-icons/ComposeIcon.svg) icon is displayed with the field, because the information doesn't come directly from your storefront or your Shopify admin.

References are URLs that act as supporting links for a field. They're available to AI agents along with the information in that field, so that an agent can refer to where an answer came from. A field can have references that come from its source, and references that you add yourself.

You can make changes to knowledge base content directly. Ensure that the content on your storefront matches what you add to your knowledge base, and provide a customer-facing and publicly available reference.

### Accept or reject a suggested change

Shopify regularly scans your online store for new information. If a scan finds new information, then a **Suggested update** for the related category information might be displayed in your knowledge base. You can approve or reject each suggested update. Knowledge base content is never changed without your approval.

#### Steps:

1.   From your Shopify admin, go to **Sales channels**>[**Agentic**](https://admin.shopify.com/apps/agentic).

2.   In the **Sources** section, click **Knowledge Base**.

3.   Find a category that has **Suggested update** displayed.

4.   Review the suggested change, and then do either of the following:

    *   To accept the suggested change, click **Approve & publish**.
    *   To reject the suggested change:
        1.   Click the ![Image 2: Reject](https://cdn.shopify.com/shopifycloud/help-center/manual/admin-icons/ThumbsDownIcon.svg) icon.
        2.   In the **What is wrong with this?** dialog, select the relevant option.
        3.   Click **Submit**.

5.   Click **Save**.

### View knowledge base references and sources

1.   From your Shopify admin, go to **Sales channels**>[**Agentic**](https://admin.shopify.com/apps/agentic).

2.   In the **Sources** section, click **Knowledge Base**.

3.   Find the category that you want to review.

4.   For the specific category information field that you want to review, click the number of **references** or click the [existing source icon](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/knowledge-base#source-icons).

5.   Optional: To update any store information that's being referenced, go to the relevant page or section in your Shopify admin and make any changes to the information.

### Change an information source

When you change the source for a field, any references that the previous source provided are removed from the field. Any references that you add yourself are kept with the field.

#### Steps:

1.   From your Shopify admin, go to **Sales channels**>[**Agentic**](https://admin.shopify.com/apps/agentic).

2.   In the **Sources** section, click **Knowledge Base**.

3.   Find the category that you want to change an information source for.

4.   For the specific category information field that you want to change the source for, click the [existing source icon](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/knowledge-base#source-icons).

5.   Do either of the following:

    *   To use the source that Shopify detected, click **Scanned from your store**, or the name of the Shopify admin location, depending on which option is displayed.
    *   To enter information manually, click **Manual**, and then enter your information in the text field.

6.   Click **Save**.

### Add a knowledge base reference

You can add a reference URL to your knowledge base only when the category field's source has been changed to **Manual**. Changing the source to **Manual** removes any references that the previous source provided, and you then maintain the information in the field yourself.

#### Steps:

1.   From your Shopify admin, go to **Sales channels**>[**Agentic**](https://admin.shopify.com/apps/agentic).

2.   In the **Sources** section, click **Knowledge Base**.

3.   Find the category that you want to add a reference to.

4.   For the specific category information field that you want to add a reference to, [change the source](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/knowledge-base#change-source) to **Manual**.

5.   Click the number of **references**.

6.   In the **References** dialog, enter a URL for a page from your online store that you want to reference information from, or an external URL containing relevant business information that you want to reference, and then click **Add**.

7.   Click **Save**.

### Remove a knowledge base reference

You can remove a reference URL from your knowledge base only when the category field's source has been changed to **Manual**. Changing the source to **Manual** removes any references that the previous source provided, and you then maintain the information in the field yourself.

#### Steps:

1.   From your Shopify admin, go to **Sales channels**>[**Agentic**](https://admin.shopify.com/apps/agentic).

2.   In the **Sources** section, click **Knowledge Base**.

3.   Find the category that you want to remove a reference from.

4.   For the specific category information field that you want to remove a reference from, [change the source](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/knowledge-base#change-source) to **Manual**.

5.   Click the number of **references**.

6.   In the **References** dialog, click the ![Image 3: delete](https://cdn.shopify.com/shopifycloud/help-center/manual/admin-icons/DeleteIcon.svg) icon for the reference that you want to remove.

7.   Click **Save**.

### Delete a category field in your knowledge base

You can delete a category field if you don't want it to be used or displayed in your knowledge base.

#### Steps:

1.   From your Shopify admin, go to **Sales channels**>[**Agentic**](https://admin.shopify.com/apps/agentic).

2.   In the **Sources** section, click **Knowledge Base**.

3.   Find the category that you want to delete a standard information field from.

4.   For the specific category information field that you want to delete, click the [existing source icon](https://help.shopify.com/en/manual/online-sales-channels/agentic-storefronts/knowledge-base#source-icons).

5.   Click **Delete fact**.

6.   Click **Save**.

### Restore a deleted category field in your knowledge base

You can restore a deleted category field if you decide that you want to use it in your knowledge base. The field is restored without its previous information, so you need to enter the information again, or choose a source for it.

#### Steps:

1.   From your Shopify admin, go to **Sales channels**>[**Agentic**](https://admin.shopify.com/apps/agentic).

2.   In the **Sources** section, click **Knowledge Base**.

3.   Find the category where you want to restore and use a standard information field.

4.   In the **Hidden fields** drop-down menu at the end of the category, click the category field that you want to restore.

5.   Enter the required information, or choose your data source and click **Confirm**.

6.   Hover over the **Unpublished** button, and then click **Publish**.

7.   Click **Save**.

### Add additional facts to your knowledge base

You can add extra store information to your knowledge base that you want AI agents to know about. Each additional fact has a title that describes what the information is, and a type that sets the format of the answer.

Choose from the following additional fact types to match the kind of questions that a customer might ask:

*   **Paragraph**: For information that needs an explanation, such as how your loyalty program works, or what your products are made from. An agent uses your text as the source for its answer but with its own words and phrasing.
*   **Yes/No**: For a question that has only two answers, such as whether you offer gift wrapping. The answer that you select is the whole fact, so you don't need to add any extra text.
*   **Tags**: For a set of short, related values, such as the materials that you use, or the certifications that your business holds. The whole list is available to an agent, so it can refer to whichever tags are relevant to a customer's question.

An additional fact can have only one type. If you want to provide both an explanation and a list of values for a piece of information, then add a separate fact for each.

#### Steps:

1.   From your Shopify admin, go to **Sales channels**>[**Agentic**](https://admin.shopify.com/apps/agentic).

2.   In the **Sources** section, click **Knowledge Base**.

3.   In the **Additional facts** section, click **Add fact**.

4.   In the **Untitled fact** field, enter a descriptive title that AI agents can refer to.

5.   Click the drop-down menu, select the fact type that you want, and then do one of the following:

    *   For **Paragraph**, enter your text in the **Add information** field.
    *   For **Yes/No**, select **Yes** or **No**.
    *   For **Tags**, click the ![Image 4: Add](https://cdn.shopify.com/shopifycloud/help-center/manual/admin-icons/PlusIcon.svg) icon, and then enter one or more tag names.

6.   Optional: To add other relevant information that AI agents can use when answering questions related to your additional fact:

    1.   Click the number of **references**.
    2.   In the **References** dialog, enter a URL for a page from your online store that you want to reference information from, or an external URL containing relevant business information that you want to reference.
    3.   Click **Add**.

7.   Hover over the **Unpublished** button, and then click **Publish**.

8.   Optional: To add another fact, repeat steps 3 to 7.

9.   Click **Save**.

### Publish or unpublish your knowledge base information

You can manage which categories and fields of information are published for discovery by AI agents through your knowledge base.

#### Steps:

1.   From your Shopify admin, go to **Sales channels**>[**Agentic**](https://admin.shopify.com/apps/agentic).

2.   In the **Sources** section, click **Knowledge Base**, and then do any of the following:

    *   To manage all fields in all categories:
        1.   In the **Status** section, click **Published facts**.
        2.   Click either **Publish all** or **Unpublish all**.

    *   To manage a specific information category and all its fields, click **Publish all** or **Unpublish all** for the category name.
    *   To manage only a specific field within an information category:
        *   To publish an individual field, hover over the **Unpublished** button, and then click **Publish**.
        *   To unpublish an individual field, hover over the **Published** button, and then click **Unpublish**.

3.   Click **Save**.

You can request a rescan of your store from the **Knowledge base** page in your Shopify admin. A rescan can take up to 48 hours to be completed.

#### Steps:

1.   From your Shopify admin, go to **Sales channels**>[**Agentic**](https://admin.shopify.com/apps/agentic).

2.   In the **Sources** section, click **Knowledge Base**.

3.   Click **Request rescan**.

4.   In the dialog, optionally enter a reason for requesting a rescan, and then click **Submit**.
