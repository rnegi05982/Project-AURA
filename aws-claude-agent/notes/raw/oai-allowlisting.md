Title: ChatGPT Work's Cloud browser allowlisting | OpenAI Help Center

URL Source: https://help.openai.com/en/articles/11845367-chatgpt-agent-allowlisting

Final URL: https://help.openai.com/en/articles/11845367-chatgpt-works-cloud-browser-allowlisting

Markdown Content:
Allow ChatGPT Work's Cloud browser to reach your site securely and reliably.

Updated: 11 days ago

## Overview

ChatGPT Work's Cloud browser uses Web Bot Auth to sign outbound HTTP requests, allowing website operators to verify that requests genuinely originate from ChatGPT.

Allowlisting Cloud browser traffic in your CDN or firewall helps prevent legitimate requests from being blocked while preserving your existing security controls.

## How message signatures work

Cloud browser uses the HTTP Message Signatures standard, [RFC 9421](https://www.rfc-editor.org/rfc/rfc9421.html), to authenticate requests.

Each request includes:

*   A `Signature` header.

*   A `Signature-Input` header.

*   A `Signature-Agent` header set to `"https://chatgpt.com"`.

Public keys for verifying these signatures are available at:

[https://chatgpt.com/.well-known/http-message-signatures-directory](https://chatgpt.com/.well-known/http-message-signatures-directory)

Your CDN, firewall, or edge service can retrieve the public key, validate the signature, and confirm that a request originated from ChatGPT.

## Allowlisting with Akamai

Akamai identifies Cloud browser traffic under the existing bot name **ChatGPT Agent** in its Artificial Intelligence bots category.

To allow this traffic:

*   In your Akamai Security Configuration, open the relevant Security Policy.

*   Select **Bot management**, then **Custom Bot Categories**.

*   Under settings, select **Manage Bot Categories**.

*   Add a new bot category and create a bot with:

    *   **Type:** Akamai-Defined

    *   **Bot name:** ChatGPT Agent

*   Return to **Custom Bot Categories** and set the new category’s action to **Allow**.

Akamai verifies request signatures automatically. No custom signature verification is required.

## Allowlisting with Cloudflare

Cloudflare recognizes Cloud browser traffic as a signed agent in its Bots and Agents directory.

The existing identifiers are:

*   **Bot tag:**`chatgpt-agent`

*   **Detection ID:**`129220581`

To allow this traffic:

*   In the Cloudflare dashboard, open **Security → WAF** and create a custom rule.

*   Set the rule expression to **Bot Detection ID equals**.

*   Search for **ChatGPT Operator** and select detection ID `129220581`.

*   Configure the rule to allow or skip requests matching this detection ID.

*   Save and deploy the rule.

Cloudflare verifies request signatures automatically. No additional signature verification is required.

## Allowlisting with HUMAN

### HUMAN Sightline

HUMAN recognizes Cloud browser traffic under the existing bot name **ChatGPT Agent** in Known Bots & Crawlers.

To allow it:

*   In your Sightline or BD console, go to **Policies → Traffic Policy Settings → Known bots & Crawlers**.

*   Search for **ChatGPT Agent**.

*   Set the rule to **ON** and select **Allow**.

### HUMAN AgenticTrust

HUMAN AgenticTrust verifies Cloud browser traffic and allows you to manage permissions associated with the existing **ChatGPT Agent** entry.

To update those permissions:

*   In your Sightline console, open **Policies → AI Agents Permissions**.

*   Search for **ChatGPT Agent**.

*   Review and update the available permissions as needed.

HUMAN verifies request signatures automatically. Its permission settings do not change Cloud browser’s supported capabilities: at launch, Cloud browser cannot sign in to websites or complete payments.

## Allowlisting with Vercel

If your site is hosted on Vercel, no additional configuration is required to allow Cloud browser traffic.

Vercel recognizes this traffic through the existing **ChatGPT Agent** entry, identified as `chatgpt-operator`, and automatically verifies its signed requests.

For more information, see [Vercel’s support for Web Bot Auth](https://vercel.com/changelog/vercels-bot-verification-now-supports-web-bot-auth).

## Allowlisting with other CDNs

If your CDN or firewall does not automatically recognize Cloud browser traffic, you can verify requests directly:

*   Confirm the `Signature-Agent` header exactly matches `"https://chatgpt.com"`, including the quotation marks.

*   Retrieve the corresponding public key from [https://chatgpt.com/.well-known/http-message-signatures-directory](https://chatgpt.com/.well-known/http-message-signatures-directory).

*   Verify the `Signature` and `Signature-Input` headers according to [RFC 9421](https://www.rfc-editor.org/rfc/rfc9421.html).

*   Allow requests only after successfully verifying their signatures.

## Troubleshooting

If legitimate Cloud browser traffic is blocked, confirm that intermediate proxies preserve the following headers:

*   `Signature`

*   `Signature-Input`

*   `Signature-Agent`

Also confirm that your allowlisting rule uses the provider-specific bot name or detection ID listed above.

## Need more help? Contact us for product questions, account support and general troubleshooting.

AI Chat

Calls may be recorded to improve OpenAI services. If you wish to report content, please use the in-app reporting or the [Report Content Form](https://openai.com/form/report-content/). [Learn more.](https://help.openai.com/articles/11391933-1-888-gpt-0090-openai-help-over-phone)

## Related articles

*   [IP allowlisting for ChatGPT Ensure only traffic from trusted IPs can reach ChatGPT](https://help.openai.com/en/articles/12111596-ip-allowlisting-for-chatgpt)
*   [Using cloud browser in ChatGPT Let ChatGPT handle supported web tasks, including on websites where you sign in.](https://help.openai.com/en/articles/20001280-using-cloud-browser-in-chatgpt)
*   [IP allowlisting for OpenAI API Restrict which IP addresses can access your OpenAI API.](https://help.openai.com/en/articles/20001201-ip-allowlisting-for-openai-api)

## Was this article helpful?
