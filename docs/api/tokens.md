# API Endpoints:<br>Tokens (URLs & Email Addresses)

A **token** is a container for incoming requests and emails, and corresponds to a Webhook.site URL or Email. A **token ID** is a 36 character UUID consisting of hexadecimal characters and dashes.

Simply, the token ID is the part after `https://webhook.site/` in the URL, or before `@email.webhook.site` in the email address.


## Create token

* Can require authentication.
* Rate limit: 10 per minute (free); 60 per minute (Pro and Enterprise)

**POST** `/token`

After creating a token, the following addresses become active. `alias` can be used in place of `uuid`. Both HTTP and HTTPS can be used.

* `https://webhook.site/{uuid}`
* `https://webhook.site/{uuid}/{anything}`
* `https://{uuid}.webhook.site` 
* `https://{uuid}.webhook.site/{anything}` 
* `{uuid}@emailhook.site` (Email)
* `{uuid}.dnshook.site` (DNS)
* `{anything}.{uuid}.dnshook.site` (DNS)

#### Request

##### JSON parameters

* `default_status` (int, 200-599, default 200) sets the default response status of the URL
* `default_content` (string) sets the default response content of the URL
* `default_content_type` (string, default `text/html`) sets the default response content type of the URL (to set other headers, take a look at the [Modify Response](/custom-actions/action-types.html#modify-response) action.)
* `timeout` (int) amount of seconds to sleep before returning the response, max 30. Intended for testing timeouts, requests to tokens with timeouts are rate limited; a high timeout value will incur a lower rate limit.
* `listen` (int) amount of seconds to listen for a response from the Set Response endpoint. `0` to disable, max `10`. Default `0`.
* `expiry` (int) amount of seconds until token auto-expiration. Max value (and default for non-upgraded URLs) is 604800 (one week). Intended for e.g. automated testing pipelines. Leave out or set to `null` to disable.
* `request_limit` (int) - limits the request history of the Token, from 0 (no data stored on Webhook.site servers) to 10000 (default)
* `cors` (bool) set to true will add CORS headers to the request so browsers will send cross-domain requests to the URL
* `alias` (string) allows setting the alias of the token.
* `actions` (bool) specifies if Custom Actions are enabled and executed on every request/email (true), or disabled (false.)
* `clone_from` (uuid string) specifies a token UUID (or alias) that will act as a template for the new token. When specified, settingssuch as default content, timeout, password as well as Custom Actions are copied to the new token.
* `group_id` (int) specifies which group ID the token should be added to.

##### Example 1: JSON

```json
{
  "default_status": 200,
  "default_content": "Hello world!",
  "default_content_type": "text/html",
  "timeout": 0,
  "cors": false,
  "expiry": 604800,
  "alias": "my-webhook",
  "actions": true
}
```

##### Example 2: Creating with Python 3

Requires the `requests` module, which can be installed using `pip install requests`. You'll also need to replace the API key. [Create an API key here](https://webhook.site/api-keys).

```python
import requests

json = {
  "default_status": 200,
  "default_content": "Hello world!",
  "default_content_type": "text/html",
}

headers = {
    "api-key": "00000000-0000-0000-0000-000000000000"
}

r = requests.post('https://webhook.site/token', json=json, headers=headers)

print('URL Created: https://webhook.site/' + r.json()['uuid'])
```

#### Response

`200 OK`

```json
{
  "uuid": "9981f9f4-657a-4ebf-be7c-1915bedd4775",
  "redirect": false,
  "alias": null,
  "timeout": 0,
  "premium": true,
  "ip": "127.0.0.1",
  "user_agent": "Paw\/3.1.8 (Macintosh; OS X\/10.14.6) GCDHTTPRequest",
  "default_content": "Hello world!",
  "default_status": 200,
  "default_content_type": "text\/plain",
  "premium_expires_at": "2019-10-22 10:52:20",
  "created_at": "2019-09-22 10:52:20",
  "updated_at": "2019-09-22 10:52:20",
  "expires_at": "2019-09-29 10:52:20"
}
```

## Get token list

* Requires authentication.

#### Request

**GET** `/token`

Returns a list of all Tokens associated with an account.

##### Query string parameters

* `per_page` - amount of requests returned, defaults to 50 (max 100)
* `page` -  page number to retrieve (default 1)
* `order_by` - which field to order tokens by (`created_at` (default) or `token_id`)
* `order_direction` - order direction (`asc` (default) or `desc`)

#### Response

```json
{
  "current_page": 1,
  "data": [
    {
      "uuid": "44fb1548-cd1f-4928-880c-cce094e5e179",
      "redirect": false,
      "alias": null,
      "actions": true,
      "cors": false,
      "expiry": false,
      "timeout": 0,
      "premium": true,
      "user_id": null,
      "password": true,
      "ip": "127.0.0.1",
      "user_agent": "Mozilla\/5.0 (Macintosh; Intel Mac OS X 10_15_6) AppleWebKit\/605.1.15 (KHTML, like Gecko) Version\/14.0.3 Safari\/605.1.15",
      "default_content": "",
      "default_status": 200,
      "default_content_type": "text\/plain",
      "premium_expires_at": null,
      "created_at": "2021-08-11 18:34:44",
      "updated_at": "2021-08-11 18:34:44",
      "latest_request_id": "ea5f5920-0398-465c-8f9c-8074f0d805a4",
      "latest_request_at": "2021-08-12 19:56:50",
      "group_id": null,
      "requests": 1
    },
    ...
  ],
  "first_page_url": "https:\/\/webhook.site\/token?page=1",
  "from": 1,
  "last_page": 1,
  "last_page_url": "https:\/\/webhook.site\/token?page=1",
  "next_page_url": null,
  "path": "https:\/\/webhook.site\/token",
  "per_page": 50,
  "prev_page_url": null,
  "to": 2,
  "total": 2
}
```

## Get token

* Can require authentication.

**GET** `/token/:token_id`

#### Response

[*See **POST** `/token`*](#11-create-token)

## Update token

* Can require authentication.

**PUT** `/token/:token_id`

#### Request

[*See **POST** `/token`*](#11-create-token)

#### Response

[*See **POST** `/token`*](#11-create-token)

## Set password

* ⚠️ This endpoint is deprecated and may be removed.
* Can require authentication.
* Requires user with active subscription.

**PUT** `/token/:token_id/password`

Sets a password to view the requests of a token.

#### Request

```json
{"password": "hunter2", "old_password": "hunter1"}
```

#### Response

[*See **POST** `/token`*](#11-create-token)

## Delete token 

* Can require authentication.

**DELETE** `/token/:token_id`

#### Response

`204 No Content`

