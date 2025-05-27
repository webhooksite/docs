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

* In this API documentation, URL parameters are prefixed with `:` (colon) to show which parameters must be changed by the user. You must *not* include this character in the URL.
* A *Token ID* refers to the ID of the Webhook.site URL/e-mail address, i.e., when your Webhook.site URL is `https://webhook.site/00000000-0000-0000-0000-000000000000`, the Token ID is then `00000000-0000-0000-0000-000000000000`.
* In API URLs, you *cannot* use Token Aliases in place of the Token ID.
* Webhook.site API Keys *must* be specified using the `Api-Key` HTTP header.
* Fair use guidelines, rate limits, and other limitations apply as described by the [Terms of Service](https://webhook.site/terms).

## Authentication

While many endpoints of the Webhook.site API are public and work without any authentication, some endpoints do require authentication, or will return a `401 Unauthorized` status code.

### API Key

An API Key can be generated in the Control Panel, and provides access to Tokens that are either a) password protected or b) require login.

API Keys have the same privileges as the user who created them.

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

## WebSocket

You can connect to Webhook.site's WebSocket server (`wss://ws.webhook.site`) and listen for incoming requests, emails and DNSHooks in your own application. If you listen to a token associated with a Webhook.site account, you must specify and API key. Alternatively, you can use [Webhook.site CLI](/cli.html).

### JavaScript

```javascript
import Echo from "laravel-echo";
import client from "socket.io-client";

let apiKey = '000-000...';
let tokenId = '111-111...';

const headers = apiKey ? {'Api-Key': apiKey} : {};
const echo = new Echo.default({
    host: 'wss://ws.webhook.site',
    broadcaster: 'socket.io',
    client,
    auth: {headers}
})

let channel = echo.private(`token.${tokenId}`);

channel.listen('.request.created', (data) => {
    // console.log(data)
})
```

### Python

```python
import socketio
import pprint

api_key = '000-000...'
token_id = '111-111...'

# Create a Socket.IO client
sio = socketio.Client()

@sio.event
def disconnect():
    print("Disconnected from server")

@sio.event
def connect():
    sio.emit("subscribe", {
        "channel": f'private-token.{token_id}',
        "auth": {
            "headers": {
                "Api-Key": api_key
            }
        }
    })
    print(f"Subscribed to channel")

@sio.on("request.created")
def on_message(channel, data):
    print(f"Received event on channel {channel}")
    pprint.pprint(data)

# Connect with headers for authentication
sio.connect(
    'https://ws.webhook.site',
    transports=['websocket']
)

# Keep the script running
sio.wait()

```