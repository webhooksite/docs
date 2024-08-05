---
title: FAQ
nav_order: 50
---

# Webhook.site Frequently Asked Questions

## What's a webhook?

The term '[webhook](https://en.wikipedia.org/wiki/Webhook)' refers to the general technology of Web-based systems communication. 

In short, many systems (e.g. a payment platform and a customer management system) communicate with each other by sending Web requests back and forth, e.g. from https://paymentsys.example to https://customersys.example/register-payment.

We don't offer support or help with general questions or issues with webhooks. [More about webhooks](https://simonfredsted.com/1583).

## What's Webhook.site?

Webhook.site is a tool for building software that use webhooks, either by allowing developers to inspect the data that's being sent via a webhook, but also helps users create workflows that respond to and interact with webhooks from various systems.

With [Webhook.site](https://webhook.site), users instantly get a unique, random URL and e-mail address. Everything that's sent to these addresses are shown instantly. With this, users can test and debug Webhooks and HTTP requests, as well as create workflows using the [Custom Actions](/custom-actions.html) graphical builder or [WebhookScript](/webhookscript.html), a simple scripting language, to transform, validate and process HTTP requests in a variety of ways – without setting up and maintaining your own infrastructure.

Webhook.site company stats as of March 2024:

- [Registered corporation](https://datacvr.virk.dk/enhed/virksomhed/41561718) since August 2020
- 280.000+ monthly unique users 
- 1900+ subscribed customers
- Handles more than 250 million requests per day

## Why should I pay for a Webhook.site subscription?

* URLs never expire (free URLs expire after 7 days)
* No limit on the amount requests, emails, DNSHooks a URL can receive (free URLs accept a max of 100)
* The data sent to your URLs is protected in your account
* Custom aliases for your URLs (https://webhook.site/my-alias)
* You can manage your URLs with our Control Panel
* Unlimited e-mail support
* Features like Custom Actions, CSV Export and Schedules
* Higher rate limits on API endpoints

[Click here to create a Webhook.site subscription](https://webhook.site/register).

## Is my data private?

Yes. Per default, all URLs associated with a paid Webhook.site subscription are protected with login. Additionally, users can decide exactly how much (or little) data Webhook.site stores, either by amount of requests/emails, how long a URL stays active or other criteria, like the content of a request or email.

For users of the free version of Webhook.site, as the free version operates without a login, data is accessible to anyone who knows the ID of the URL.

## Can I use Webhook.site for production workloads?

Yes. Thousands of our customers use Webhook.site to build workflows that help their business, without needing to hire a programmer or pay for and setup servers. We take care of the infrastructure so you can build what you need.

## How much data does Webhook.site store?

For each URL associated with a Webhook.site Pro account, Webhook.site makes the latest 10.000 requests or emails available. Old requests are automatically rotated/purged periodically. 

In other words, A URL associated with an upgraded account will keep accepting an unlimited amount of requests and emails, but only the latest 10.000 will be available. (If you want to store data permanently, you can use Custom Actions to transfer data to a storage provider like AWS S3 or Dropbox.)

For free users of Webhook.site (URLs not associated with an upgraded account), the URL stops accepting new requests and emails after a limit of 100 requests or emails. However, the limit is automatically removed once the URL is upgraded and associated with a Webhook.site account.

## How long is data stored on Webhook.site?

For Free users, the URL – and its data – is automatically removed after 7 days with no activity.

For Pro and Enterprise URLs, URLs never automatically expire, but data is removed after 365 days.

## How can I automatically remove data from Webhook.site?

**By amount**

You can lower the request history amount of Webhook.site stores on your URL. 

The default request limit is 10.000. Any value lower than that can be used. 

If the value is set to 0, no request history is stored in the Webhook.site Cloud, but Custom Actions will execute, requests are streamed to the Webhook.site interface and Webhook.site CLI forwarding will function. 

To change it, click *Edit* in the upper-right corner, or use the API via the [`request_limit`](/api/tokens.html#create-token) parameter.

**By date**

Using the Webhook.site API (specifically, the [Delete Multiple Requests endpoint](/api/requests.html#delete-multiple-requests)) and [Schedules](/schedules.html), you can easily auto-dete data from Webhook.site URLs with very flexible settings.

To set it up, first, [create an API Key](https://webhook.site/api-keys). 

Then create a Schedule like the following screenshot. 

In this example, Webhook.site will remove data older than 7 days every 24 hours. Remember to click the URL Encode button before saving.

* Schedule Name: Can be anything you want.
* URL: `https://webhook.site/token/00000000-0000-0000-000000000/request?query=created_at:[* TO now-7d]` - replace `00000000-0000-0000-000000000` with the URL/Token ID.
* Method: `DELETE`
* Headers: `Api-Key: 00000000-0000-0000-000000000` - replace `00000000-0000-0000-000000000` with your API key.

<figure markdown="span">
  ![Auto JSON in action](/images/schedule-autodelete.png){ width="300" }
  <figcaption>Automatically removing requests using Webhook.site API and Schedules</figcaption>
</figure>

## What's a Webhook.site "Token"?

A *token* is how a Webhook.site URL is referred to in our API, essentially the technical name for it. A *token* has a unique UUID, which is also the Web address, email address and DNSHook address. It acts as a container for requests, emails and DNS queries. [More about Tokens](/api/tokens.html)

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

## I want to whitelist Webhook.site in our firewall, which IPs do you use?

You'll need to whitelist the IPs `46.4.105.116`, `178.63.67.106`, `178.63.67.153`. 

Both inbound and outbound originate and destinate at these IP addresses.

Note that this may change in the future, so sign up for the [newsletter](news.markdown) to be notified of changes.

## How do I add authentication to my URL?

The easiest way to add authentication is by using the Basic Auth action type. [More about the Basic Auth action](/custom-actions/action-types.html#basic-auth).

You can also use the Conditions [Custom Action](/custom-actions.html) to add a quick header based authentication mechanism to your URL. You can also add the Don't Save action as a condition if you don't wish to save the unauthenticated request.

![Quick Conditions Based Authentication](/images/auth.png)

We also have an example [WebhookScript](/webhookscript/index.html) for adding basic auth:

```javascript
username = 'john'
password = '1234'

if (var('request.header.php-auth-user', '') != username and var('request.header.php-auth-pw', '') != password) {
    respond('', 401, ['WWW-Authenticate: Basic realm="Authentication required"']);
    dont_save()
}

respond('Login OK!');
```

## Can I get a push notification on my phone when my URL receives a request?

Via [Custom Actions](/custom-actions.html), Webhook.site [supports](/custom-actions/action-types.html#ntfy) servies like Pushed and Ntfy, which both has free tiers.

Alternatively, at least on iPhones, you can use the [Send Email](/custom-actions/action-types.html#send-email) custom action and mark the sender address as VIP. This will trigger a push notification when the email is received. 

## Can I pay via invoice?

After you've paid for and [created a subscription](https://webhook.site/register), you will receive an invoice via email.

If you are an enterprise customer that wishes to buy a subscription via bank transfer, please contact [Support](https://support.webhook.site).

## How do I add my company name to my invoice?

Go to [Control Panel -> Billing](https://webhook.site/control-panel), then click View next to an invoice and finally click [the "Add Address & VAT Number" link](https://sf.gl/share/1708090417.png).

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

With [Webhook.site Pro](pro.markdown), there's a variety of different ways to export data sent to your URL or email address.

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

*For Webhook.site Pro or Enterprise users:* If you're getting this error with a Webhook.site URL, the URL may have been automatically blocked due to an extraordinarly large amount of requests, as per the Fair Use guidelines in our Terms of Service. This is done to prevent a decrease in service level for our other customers. For more info, or to request a whitelisting, please contact [Support](https://support.webhook.site). If you're getting this error with a Webhook.site API endpoint, you have exceeded the API endpoint quota, and should implement e.g. a backoff strategy.

## I'm getting a 413 Payload Too Large, what's wrong? / What's the request size limit?

The HTTP body data (e.g. files or JSON data) submitted to Webhook.site must be below 10 megabytes. More than that will cause a HTTP 413 response.

## I'm getting an "Access Control Check error"

If you're requesting the Webhook.site endpoint from another domain via JavaScript, you'll need to enable CORS so the browser allows the request.

To do this, click *Edit* in the upper-right corner, check the *Add CORS headers* checkbox, and click *Save*.

## I'm getting a "Certificate Expired" error

Our SSL certificate is fully working; the issue lies with your system. In september 2021, our SSL provider, LetsEncrypt, [updated their root certificate](https://letsencrypt.org/docs/dst-root-ca-x3-expiration-september-2021/). This can mean that if your locally installed trusted root certificates are of an old version, you'll be seeing a certificate error as Webhook.site now runs a certificate that is based on the new root certificate chain.

To remediate this problem, you'll need to update your local certificate trust store:

* Debian-based systems: Use `update-ca-certificates`; [more info here](https://manpages.debian.org/buster/ca-certificates/update-ca-certificates.8.en.html).
* Red Hat based systems: `yum update ca-certificates`; [more info here](https://access.redhat.com/solutions/1549003)

Some systems and packages, like [Python certifi/urllib3](https://github.com/certifi/python-certifi/pull/162), also come with static certificates. We cannot support updating these.

## What is a DNSHook?

For more information about DNSHook, please [see here](/dnshook.html).
