---
title: DNSHook
nav_order: 395
---

# DNSHook by Webhook.site

## What is DNSHook?

Webhook.site DNSHook is a type of *hook*, like webhooks and emailhooks, that on Webhook.site will automatically show all [DNS](https://da.wikipedia.org/wiki/Domain_Name_System) requests to a unique DNS name and all its subdomains. 

DNSHooks can be used to send data solely via DNS. DNSHooks can also be used as a canary token as DNS can be useful in cases where it can bypass firewalls, for example.

## Create DNS workflows with Custom Actions

You can even create workflows from DNSHook requests with [Custom Actions](/custom-actions.html). 

For example, you can send a notification to your phone whenever a specific subdomain has had its DNS looked up via the [*Ntfy* action](https://docs.webhook.site/custom-actions/action-types.html#ntfysh).

## Receive data via DNS

As all subdomains are also logged and shown on Webhook.site, you can send data in DNSHooks by e.g. base64-encoding a subdomain. For example, the string `hello world` can be encoded in a DNS lookup as the following.

```
aGVsbG8gd29ybGQ.47bb8761-e40b-42c2-8c98-a448f492df70.dnshook.site
```

(In this case, `aGVsbG8gd29ybGQ` base64-decodes to `hello world` and `47bb8761-e40b-42c2-8c98-a448f492df70` is the ID of the Webhook.site token/URL.)

Indeed, you can even use different record types, like CNAME and MX, as flags to transfer information to Webhook.site.

## Send DNS Response

You can also set the DNS response dynamically by using the URL response in the following format. You can return one or more responses.

``` json
[
    {
        "type": "a",
        "value": "127.0.0.1"
    },
    {
        "type": "cname",
        "value": "example.com."
    },
    {
        "type": "txt",
        "value": "hello world"
    }
]
```

To set the response, either enter the JSON in *Edit* &rarr; *Content*, or use the *Modify Response* Custom Action and setting the Response Body field.

![](https://sf.gl/share/1710929466.png)

`type` can be one of the following:

* `a`
* `cname`
* `txt`

Note: If the response isn't valid (e.g. invalid JSON, using a domain name in an A record), no response is returned. It is currently not possible to be notified of DNS parsing errors, so make sure to test this well.

For `txt` responses, multiple lines can be sent by separating with `\n` (newline).


