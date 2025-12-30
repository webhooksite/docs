# Webhook.site API

The Webhook.site API is public, free and easy to use. If you have a Webhook.site Account, you should authorize via an [Api-Key](#api-key).

<div style="height:32px">
View, fork and modify in Postman: &nbsp;<a href="https://god.gw.postman.com/run-collection/45321203-694a428b-d10f-4dbb-885c-79ed4441ba2e?action=collection%2Ffork&source=rip_markdown&collection-url=entityId%3D45321203-694a428b-d10f-4dbb-885c-79ed4441ba2e%26entityType%3Dcollection%26workspaceId%3D0793a22a-b783-4ee3-ba4d-139c851deef2"><img src="https://run.pstmn.io/button.svg" alt="Run In Postman" style="vertical-align:middle; width: 128px; height: 32px;"></a>
</div>

## General Usage

Base URL: `https://webhook.site`.

You must set the `Accept` and `Content-Type` headers to `application/json`.

You must set the [`Api-Key`](#api-key) header if you have a Webhook.site account.

## Common Uses

* [Create a Webhook.site URL](/api/tokens.html#create-token)
* [Fetch or search data sent to a Webhook.site URL](/api/requests.html#get-requests)

## Things to Note

* In this documentation, replaceable URL parameters are highlighted.<br> For example, <code><span class="url-param">tokenId</span></code> indicates a parameter that *must* be replaced with a token ID.
* A *Token ID* refers to the ID of the Webhook.site URL/e-mail address, i.e., when your Webhook.site URL is `https://webhook.site/00000000-0000-0000-0000-000000000000`, the Token ID is then `00000000-0000-0000-0000-000000000000`.
* In API URLs, you *cannot* use Token Aliases in place of the Token ID.
* Webhook.site API Keys *must* be specified using the `Api-Key` HTTP header.
* Fair use guidelines, rate limits, and other limitations apply as described by the [Terms of Service](https://webhook.site/terms).
* If you're interacting with Tokens or Requests, make sure you keep the `/token/` part! (Otherwise Webhook.site won't recognize it as an API URL.)

## API Key

While many endpoints of the Webhook.site API are public and work without any authentication, some endpoints do require authentication, or will return a `401 Unauthorized` status code. Resources that are associated with a Webhook.site account always require an API Key.

API Keys have the same privileges as the user who created them.

API Keys *must* be specified in the `Api-Key` HTTP header.

<div class="center">
<a href="https://webhook.site/api-keys" class="md-button md-button--default no-underline">Create API Key</a>
</div>

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
