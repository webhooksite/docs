# Webhook.site API

The Webhook.site API is public, free to use, doesn't require authentication and is relatively easy to use. 

## General Usage

Base URL: `https://webhook.site`.

You must set the `Accept` and `Content-Type` headers to `application/json`.

## Things to Note

* In all examples in this API documentation, URL parameters are prefixed with `:` (colon) to show which parameters must be changed by the user. You must not include this character in the URL.
* A *Token ID* refers to the ID of the Webhook.site URL/e-mail address, i.e., when your Webhook.site URL is `https://webhook.site/00000000-0000-0000-0000-000000000000`, the Token ID is then `00000000-0000-0000-0000-000000000000`.
* In API URLs, you *cannot* use Token Aliases in place of the Token ID.
* Webhook.site API Keys *must* be specified using the `Api-Key` HTTP header.
* Fair use guidelines, rate limits, and other limitations apply as described by the [Terms of Service](https://webhook.site/terms).

## Authentication

While many endpoints of the Webhook.site API are public and work without any authentication, some endpoints do require authentication, or will return a `401 Unauthorized` status code.

### API Key

An API Key can be generated in the Control Panel, and provides access to Tokens that are either a) password protected or b) require login.

API Keys *must* be specified in the `Api-Key` HTTP header.

<div class="center">
<a href="https://webhook.site/api-keys" class="md-button md-button--default no-underline">Create API Key</a>
</div>

### Password

!!! warning
    Password authentication is deprecated and will be removed in 2025. We recommend using API Keys.

If you have set a password on a Webhook.site URL/token, to access the API resources for that token, you can use either of the following methods:

1. Specify the password using the `password` query string: `?password=[your password]` 
2. Set the password using HTTP Basic Auth, using the Authorization header. [More info](https://en.wikipedia.org/wiki/Basic_access_authentication#Client_side)

## Common Usages

### Get data sent to URL

To retrieve the data that's sent to a Webhook.site URL or Email, you'll want to use the [Get Requests](/api/tokens.html#get-requests) endpoint.

### Create new URL/email address

To create a new *token* programmatically, you can use the API like this:

```sh
$ curl -X POST https://webhook.site/token
```

This will return information about the *token* in JSON format, including its UUID. Your URL will be available at the endpoint `https://webhook.site/[token uuid]`.

If you are a Webhook.site Pro or Enterprise customer, you should provide an API key in order to associate the created token with your account automatically:

```sh
$ curl -X POST -H 'Api-Key: 00000000-0000-0000-0000-000000000000' https://webhook.site/token
```

[More info here](/api/tokens.html#create-token).
