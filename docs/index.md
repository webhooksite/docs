---
title: FAQ
nav_order: 50
---

# Webhook.site Frequently Asked Questions

## What is a "webhook"?

You've likely encountered the term '[webhook](https://en.wikipedia.org/wiki/Webhook)' when integrating different web services. At its core, a webhook is a way for web-based applications to communicate with each other in near real-time.

Think of it like this: instead of one system constantly asking another "Hey, is there any new information?", a webhook sets up a system where the second system proactively says, "Here's some new information!" whenever an event occurs.

For example, imagine an e-commerce platform and a shipping service. When a customer places an order, the e-commerce platform can instantly notify the shipping service about the new order details via a webhook. This eliminates the need for the shipping service to repeatedly check for new orders. The communication flows directly when something important happens.

Essentially, webhooks facilitate machine-to-machine communication over the web using HTTP requests. When a specific event happens in one system, it triggers an HTTP request (usually a POST request with data in formats like JSON or XML) to a pre-configured URL in another system.

You can find more in-depth information about webhooks at [More about webhooks](https://simonfredsted.com/1583).

## Introducing Webhook.site

[Webhook.site](https://webhook.site) is a powerful and versatile tool designed to help you work effectively with webhooks and other types of web communication. It goes beyond just inspecting webhook data; it empowers you to build sophisticated workflows and interactions without the burden of managing your own infrastructure.

When you visit [Webhook.site](https://webhook.site), you're immediately provided with a unique, random URL and email address. Any data sent to these endpoints is instantly displayed in your browser. This immediate feedback loop is invaluable for testing and debugging webhooks and general HTTP requests.

Furthermore, Webhook.site allows you to create automated workflows using its intuitive [Custom Actions](/custom-actions.html) graphical builder or [WebhookScript](/webhookscript.html), a straightforward scripting language. With these tools, you can transform, validate, and process incoming HTTP requests in numerous ways, all without needing to set up and maintain your own servers or applications.

Webhook.site has been a [registered corporation](https://datacvr.virk.dk/enhed/virksomhed/41561718) in Denmark since August 2020, operated by Webhook ApS (VAT ID: DK41561718), located at Skibsbyggerstræde 20 5. th, 5000 Odense, Denmark. The company director is [Simon Fredsted](https://simonfredsted.com), and you can find [Contact information](https://support.webhook.site) on their support page.

### Webhook.site in Numbers (as of February 2025):

- **Monthly Unique Users:** 300,000+
- **Subscribed Customers:** 2,300+
- **Daily HTTP Requests Processed:** 460 million

## Common Use Cases for Webhook.site

Webhook.site offers a wide range of applications for developers and engineers:

* **Effortlessly Receive Webhooks:** You can receive webhooks from any service without the complexity of setting up and maintaining a publicly accessible web server. This is incredibly useful for testing integrations.
* **Build Advanced Automations:** Create custom workflows that trigger automatically when a URL is accessed or an email is received. This allows you to connect different services and automate repetitive tasks.
* **Act as an Intermediary and Proxy:** Use Webhook.site to inspect, modify, and forward requests. This is helpful for understanding data flow and integrating systems with different requirements. You can see the complete history of requests and responses.
* **Handle Webhooks for Internal Systems:** If your server is behind a firewall or on a private network, you can use Webhook.site to receive external webhooks and then forward them to your internal system.
* **Transform and Re-route Data:** Convert webhook data into different formats (e.g., XML to JSON) and send it to various target systems. This enables seamless integration between incompatible APIs.
* **Connect Incompatible Systems:** Bridge the gap between different computer systems or APIs that don't natively communicate with each other. Webhook.site can act as a translation layer.
* **Quickly Prototype APIs:** Build simple APIs without the need for extensive infrastructure setup. You can define endpoints and observe the incoming requests and outgoing responses.
* **Build Contact Forms with Email Functionality:** Create simple contact forms that send data to Webhook.site, which can then be configured to send emails based on the received data.

The following video demonstrates how Webhook.site's Custom Actions can be used to automate posting news updates to X/Twitter:

<center><iframe width="100%" height="440" src="https://www.youtube.com/embed/wg08ny5bh9w" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

## Why Consider a Webhook.site Subscription?

While Webhook.site offers a generous free tier, a subscription unlocks several powerful features and removes limitations, making it ideal for more serious development and production use:

* **Persistent URLs:** Free URLs expire after 7 days. With a subscription, your URLs will never expire, ensuring consistent endpoints for your integrations.
* **Unlimited Request Handling:** Free URLs are limited to a maximum of 100 requests. Paid subscriptions allow for an unlimited number of requests, emails, and DNSHooks.
* **Data Privacy and Security:** The data sent to your subscribed URLs is securely stored within your account, providing better privacy and control.
* **Custom URL Aliases:** You can create memorable and branded aliases for your URLs (e.g., `https://webhook.site/your-project`).
* **Centralized URL Management:** The Control Panel provides a user-friendly interface to manage all your Webhook.site URLs in one place.
* **Priority Support:** Subscribers receive unlimited email support, ensuring you get help when you need it.
* **Advanced Features:** Access powerful features like Custom Actions, CSV Export for data analysis, and Scheduled tasks for automated workflows.
* **Higher API Rate Limits:** If you're using Webhook.site's API programmatically, paid subscriptions offer higher rate limits for more intensive usage.

[Click here to explore Webhook.site subscription options](https://webhook.site/register).

## Exploring Alternatives for Webhook Inspection

While Webhook.site offers a comprehensive solution, you might also find the following tools useful for specific webhook inspection needs:

* **Beeceptor:** [https://beeceptor.com/](https://beeceptor.com/) - Beeceptor allows you to instantly create mock endpoints to inspect and analyze HTTP requests, including webhooks. It provides a simple interface to view headers, body, and other request details, making it excellent for quick testing and debugging.
* **HTTPBin:** [https://httpbin.org/](https://httpbin.org/) - HTTPBin is a free, open-source HTTP request and response service. While primarily designed for testing HTTP clients, you can send webhooks to its endpoints (like `/post`) to inspect the received data.

These alternatives offer different features and might be more suitable depending on your specific workflow and requirements. It's always good to have options when working with webhooks!

## Is my data private?

Yes. Per default, all URLs associated with a paid Webhook.site subscription are protected with login. Additionally, users can decide exactly how much (or little) data Webhook.site stores, either by amount of requests/emails, how long a URL stays active or other criteria, like the content of a request or email.

For users of the free version of Webhook.site, as the free version operates without a login, data is accessible to anyone who knows the ID of the URL.

## Can I use Webhook.site for production workloads?

Yes. Thousands of our customers use Webhook.site to build workflows that help their business, without needing to hire a programmer or pay for and setup servers. We take care of the infrastructure so you can build what you need.

## How much data does Webhook.site store?

For each URL associated with a subscribed Webhook.site account, Webhook.site makes the latest 10.000 requests or emails available. Old requests are automatically rotated/purged periodically. 

In other words, A URL associated with an account will keep accepting an unlimited amount of requests and emails, but only the latest 10.000 will be available. (If you want to store data permanently, you can use Custom Actions to transfer data to a storage provider like AWS S3 or Dropbox.)

For free users of Webhook.site (URLs not associated with an upgraded account), the URL stops accepting new requests and emails after a limit of 100 requests or emails. However, the limit is automatically removed once the URL is upgraded and associated with a Webhook.site account.

## How long is data stored on Webhook.site?

For subscribed customers, URLs associated with an account never automatically expire, but data is automatically purged after a maximum of 365 days.

For free users, the URL – and its data – is automatically removed after 7 days.

## How can I automatically remove data from Webhook.site?

Many businesses have strict requirements on the amount of data that can be stored by third-party companies, and Webhook.site provides full flexibility to handle these data protection and security requirements by limiting the amount of data stored on the Webhook.site Cloud.

**By amount**

It is possible to lower or entirely disable the request limit of a Webhook.site URL. The default request history limit is 10.000 requests, emails or DNSHooks. 

If the value is set to 0, no request history is stored in the Webhook.site Cloud, but Custom Actions will continue to run, requests are streamed to the Webhook.site interface and Webhook.site CLI forwarding will continue to function. 

To change the request limit, click *Edit* in the upper-right corner, or use the API via the [`request_limit`](/api/tokens.html#create-token) parameter.

**By date**

Using the Webhook.site API (specifically, the [Delete Multiple Requests endpoint](/api/requests.html#delete-multiple-requests)) and [Schedules](/schedules.html), you can easily auto-dete data from Webhook.site URLs with very flexible settings.

To set it up, first, [create an API Key](https://webhook.site/api-keys). 

Then create a Schedule like the following screenshot. 

In this example, Webhook.site will remove data older than 14 days every 24 hours. `now-12h` would be 12 hours. [More date format examples](/api/date-expressions.html).

Remember to click the URL Encode button before saving.

* URL: `https://webhook.site/token/00000000-0000-0000-000000000/request?query=created_at:[* TO now-14d]` - replace `00000000-0000-0000-000000000` with the URL/Token ID.
* Method: `DELETE`
* Headers: `Api-Key: 00000000-0000-0000-000000000` - replace `00000000-0000-0000-000000000` with your API key.

<figure markdown="span">
  ![Automatically remove requests with Schedules](/images/schedule-autodelete.png){ width="300" }
  <figcaption>Automatically removing requests using Webhook.site API and Schedules</figcaption>
</figure>

## What's a Webhook.site "Token"?

A *Token* is how a Webhook.site URL is referred to in our API, it's the technical name for it. A *Token* corresponds to a unique UUID, which is also the Web address, email address and DNSHook address. A Token acts as a container for requests, emails and DNS queries. [More about Tokens](/api/tokens.html)

## How do I transfer my Webhook.site account and data?

To hand over your account to a different business or individual you essentially only need to change the email address, as it is the only piece of identification we store. However, be aware of the following:

1. If billing details need to change, make sure to [cancel the subscription](https://webhook.site/payment) first. The subscription will continue to work until the expiry date.

2. If 2-Factor Authentication is enabled, [disable 2-Factor](https://webhook.site/user/2fa).

3. For Enterprise users, make sure you [delete any extraneous users](https://webhook.site/control-panel/users).

4. [Delete any extraneous API keys](https://webhook.site/api-keys) that you should no longer have access to.

2. [Change the account email address](https://webhook.site/user) to the receiver's email address.

5. You, or the account receiver, can then [issue a Password Reset email](https://webhook.site/password/reset) so they can set their own password.

6. The account receiver can then [create a new subscription](https://webhook.site/payment) on the account.

After this, you will no longer have access to your account and it is fully handed over.

Alternatively, contact [Webhook.site Support](https://support.webhook.site) for help with transferring data to another Webhook.site account.

## I want to whitelist Webhook.site in our firewall, which IPs do you use?

You'll need to whitelist the IPs `178.63.67.106`, `178.63.67.153` and, for IPv6, `2a01:4f8:121:114d::/64` and `2a01:4f8:121:11a5::/64`.

Both inbound and outbound originate and destinate at these IP addresses.

Note that this may change in the future, so sign up for the [newsletter](news.markdown) to be notified of changes.

## How do I add authentication to my URL?

**Basic Auth**

The easiest way to add authentication is by using the Basic Auth action type. [More about the Basic Auth action](/custom-actions/action-types.html#basic-auth).

**Conditions**

You can also use the Conditions [Custom Action](/custom-actions.html) to add a quick header based authentication mechanism to your URL. You can also add the Don't Save action as a condition if you don't wish to save the unauthenticated request.

![Quick Conditions Based Authentication](/images/auth.png)

## Can I get a push notification on my phone when my URL receives a request?

Via [Custom Actions](/custom-actions.html), Webhook.site [supports](/custom-actions/action-types.html#ntfy) servies like Pushed and Ntfy, both which have free tiers.

Alternatively, at least on iPhones, you can use the [Send Email](/custom-actions/action-types.html#send-email) custom action and mark the sender address as VIP. This will trigger a push notification when the email is received. 

## Can I pay via invoice?

After you've paid for and [created a subscription](https://webhook.site/register), you will receive an invoice via email.

If you are an enterprise customer that wishes to buy a subscription via bank transfer, please contact [Support](https://support.webhook.site).

## I'm VAT exempt, how do I add my VAT number during checkout?

Click the "Add VAT Number" button:

<figure markdown="span">
  ![Adding company information to invoices](/images/checkout-vat.png){ width="300" }
  <figcaption>Adding VAT number during checkout</figcaption>
</figure>

## How do I add my company name and details to my invoice?

Go to [Control Panel -> Billing](https://webhook.site/control-panel), then click View next to an invoice and finally click [the "Add Address & VAT Number" link](https://sf.gl/share/1708090417.png). Once the data is entered, it will automatically be used for all forthcoming invoices.

<figure markdown="span">
  ![Adding company information to invoices](/images/invoice-company-details.png){ width="300" }
  <figcaption>Adding company information to invoices</figcaption>
</figure>

## How can I see the pricing in my currency?

Once you start the checkout process, you will see the amount in your local currency, including any applicable VAT.

## The JSON data is in a weird format/can't be parsed by Extract JSONPath

The JSON data might have been attached to the request as form data rather than as request body data, which is usually how JSON is sent.

The data might look like this on Webhook.site:

![JSON Form Data](/images/json-form-data.png)

To remediate this in Extract JSONPath, you'll need to set the source field to the form field variable, which is automatically set by Webhook.site. In the screenshot above, the variable name would be `$request.form.my_json_data$`, which works with Extract JSONPath:

![JSON Form Data in JSONPath](/images/json-form-data-jsonpath.png)

## JSON data is invalid when using the HTTP Request action

If you use any variables in the JSON that could contain e.g. new lines or quote characters, these characters need to be "escaped" properly so that the JSON remains valid.

Webhook.site provides an easy way to do this with the `.json` Variable Modifier, which will automatically escape any special JSON characters. [More info here](/custom-actions/variables.html#variable-modifiers).

Before:

```json
{
  "message": "$request.query.message$"
}
```

After, with the JSON Escape Variable Modifier:

```json
{
  "message": "$request.query.message.json$"
}
```

## How do I export the data stored on Webhook.site?

With a [Webhook.site subscription](pro.markdown), there's a variety of different ways to export data sent to your URL or email address.

1. Custom Actions can be used in a variety of ways to export data. Below are listed a few examples of actions that could be used. [More info here](/custom-actions/action-types.html).
     * [Database Query](/custom-actions/action-types.html#database-query)
     * [HTTP Request](/custom-actions/action-types.html#http-request)
     * [Run SSH Command](/custom-actions/action-types.html#run-ssh-command)
     * [Amazon Web Services S3](/custom-actions/action-types.html#s3)
     * [Dropbox](/custom-actions/action-types.html#dropbox)

1. Webhook.site provides a CSV Export functionality, simply click the button in the menu to download all data as a CSV file.

    ![CSV Export](/images/csv-export.png)

2. Data can be retrieved and saved using the [Webhook.site API](api/tokens.md#get-requests) using any programming language.

3. With the Webhook.site CLI (Command-Line Interface), requests can be forwarded directly from Webhook.site to a local workstation or server. [More info here](cli.md) 

## How do I send data to my computer/localhost?

There's several ways to accomplish this depending on your needs.

1. You can periodically fetch the data using the [Webhook.site API](api/tokens.md#get-requests)

2. Requests can also be streamed to a local URL using the [Webhook.site CLI](cli.md), in a similar fashion to e.g. ngrok.

3. Webhook.site also supports the XHR Redirect feature, which uses your browser in order to forward the requests. The endpoint will need to respond with CORS headers in all requests so that the browser will be able to send requests to it. The forwarding will only work as long as the browser window is open.

The following CORS headers should allow Webhook.site to forward requests to your local endpoint via XHR Redirect:

```
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: *
Access-Control-Allow-Headers: *
Access-Control-Expose-Headers: Content-Length,Content-Range
```

## How can I test an IPv6-only request?

If you access Webhook.site with the hostname [https://ipv6.webhook.site](https://ipv6.webhook.site), your URL will only work with IPv6.

To use it with a URL, simply replace the `webhook.site` hostname with `ipv6.webhook.site`.

## I'm getting a 404 Not Found, what's wrong? / When does Webhook.site URLs expire?

Using the free version of Webhook.site, URLs automatically expire in 7 days. After that, the URL is no longer available and data is deleted.

With the paid version, Webhook.site Pro, URLs never expire automatically.

## I'm getting a 405 Method Not Allowed, what's wrong?

You might be copying the URL for the Webhook.site application (by copying the link from your browsers' address bar), and not the actual URL.

Webhook.site app (⛔️ wrong):<br>`https://webhook.site/#!/view/6dbb3859-4ad5-4e85-acae-e44d6e37ea4a`

Webhook.site url (✅ correct):<br>`https://webhook.site/6dbb3859-4ad5-4e85-acae-e44d6e37ea4a`

## I'm getting a 429 Too Many Requests, what's wrong?

First, make sure that you have copied the correct URL, [see here](#im-getting-a-405-method-not-allowed-whats-wrong).

*For free users:* The URL has met the limit of the amount of requests it can receive. To unlock more requests, the URL must be associated with a Webhook.site Pro or Enterprise account. To associate a URL to your account, click Upgrade in the upper-right corner when logged in.

*For Webhook.site Pro or Enterprise users:* If you're getting this error with a Webhook.site URL, the URL may have been automatically blocked due to an extraordinarily large amount of requests, as per the Fair Use guidelines in our Terms of Service. This is done to prevent a decrease in service level for our other customers. For more info, or to request a whitelisting, please contact [Support](https://support.webhook.site). If you're getting this error with a Webhook.site API endpoint, you have exceeded the API endpoint quota, and should implement e.g. a backoff strategy.

## I'm getting a 413 Payload Too Large, what's wrong? / What's the request size limit?

The HTTP body data (e.g. files or JSON data) submitted to Webhook.site must be below 10 megabytes. More than that will cause a HTTP 413 response.

## I'm getting an "Access Control Check error"

If you're requesting the Webhook.site endpoint from another domain via JavaScript, you'll need to enable CORS so the browser allows the request.

To do this, click *Edit* in the upper-right corner, check the *Add CORS headers* checkbox, and click *Save*.

## What is a DNSHook?

For more information about DNSHook, please [see here](/dnshook.html).

## What does "This URL has no default content configured" mean?

This is not an error - when a Webhook.site URL is created, this is simply the default HTTP response it's configured with. On Webhook.site, you can change this by clicking **Edit** in the upper-right corner, or via the [API, using the `default_content` parameter](http://localhost:8001/api/tokens.html#create-token).

With a Webhook.site subscription, you can also use the [Modify Response](/custom-actions/action-types.html#modify-response) action.

![](/images/default-response.png)
