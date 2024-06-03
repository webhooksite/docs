# API Endpoints: Requests

The Requests API is used to retrieve, manipulate and delete data sent to a given Webhook.site token (URL, E-mail Address or DNSHook.)

## Capture request

***any method*** `/:tokenId` <br>
***any method*** `/:tokenId/:statusCode` <br>
***any method*** `/:tokenId/(anything)`

If `statusCode` is valid, that HTTP status will be used in the response (instead of the default.)

Instead of `tokenId`, an the alias of the token can also be supplied. Multiple subpaths, e.g. `/:tokenId/api/v1/users`, will also be captured.

If the Token has a `timeout` value, there is a dynamic rate limit of `100 ÷ timeout` requests per minute, e.g. a timeout of 30 allows for 3 requests per minute, and 1 second allows for 100 requests per minute.

#### Response

The default response (or a response set with e.g. the Modify Response Custom Action) of the Token will be returned.

## Get requests

* Can require authentication.
* Rate limit: 120 requests per minute.

**GET** `/token/:token_id/requests`

Lists all request sent to a token. 

#### Query string parameters

* `sorting` (string) - either `newest` or `oldest` (default)
* `per_page` (int) - amount of requests returned, defaults to 50 (max 100)
* `page` (int) -  page number to retrieve (default 1)
* `date_from`, `date_to` (date string) - filter requests by date, format `yyyy-MM-dd HH:mm:ss`
* `query` (string) - filter requests by a query string search (see below for examples)

#### Search query examples

The following fields can be used to filter via the `query` parameter:

* `uuid`
* `token_id`
* `team_id`
* `type`
* `hostname`
* `size`
* `content`
* `time`
* `created_at`
* `updated_at`
* `custom_action_output`
* `files.[id]`
* `headers.[header]`
* `method` - type `web` only
* `user_agent` - type `web` only
* `url` - type `web` only
* `ip` - type `web` only
* `query.[field]` - type `web` only
* `request.[field]` - type `web`only (form fields)
* `sender` - type `email` only
* `text_content` - type `email` only
* `message_id` - type `email` only
* `checks.[type]` - type `email` only
* `destinations]` - type `email` only

You can filter requests by the following syntax:

* `foobar` - returns requests or emails with body contents containing the word `foobar`
* `content:foobar` - returns requests or emails with body contents containing the word `foobar`
* `method:GET` - returns all requests with method GET
* `headers.user-agent:"Paw/3.3.5 (Macintosh; OS X/11.6.2) GCDHTTPRequest"` - search value of user-agent header
* `query.action:create` - returns requests that have the query string `action` set to `create`.
* `_exists_:query.action` - returns requests where the action query parameter exists
* `type:web` / `type:email` - returns either Web requests or emails
* `type:web AND method:POST` - AND query
* `method:PUT OR method:POST` - OR query
* `(method:PUT) AND (content:example OR content:test) AND NOT (content:foobar)`
* `created_at:["2022-01-01 00:00:00" TO "2022-12-31 00:00:00"]` - date range query
* `created_at:["2022-01-01 00:00:00" TO *]` - date range query (from date until now)
* `created_at:[now-10m TO now]` - date range query (10 minutes ago until now; [reference for date expressions](/api/date-expressions.html))

#### Full URL Example

If you're in doubt about where these parameters go in an API request, take a look below. This URL combines a search query via the `query` parameter (searching requests containing the word `foobar`), as well as the `sorting` and `per_page` parameters.

`https://webhook.site/token/a94a7294-c4aa-4074-ab77-c4cf86fd53b1/requests?query=content:foobar&sorting=newest&per_page=10`

#### Response

```json
{
  "data": [
    {
      "uuid": "a2a6a4ae-4130-4063-953a-84fa29d81d43",
      "token_id": "a94a7294-c4aa-4074-ab77-c4cf86fd53b1",
      "ip": "127.0.0.1",
      "hostname": "webhook.site",
      "method": "POST",
      "user_agent": "Paw\/3.1.8 (Macintosh; OS X\/10.14.6) GCDHTTPRequest",
      "content": "{\"first_name\":\"Arch\",\"last_name\":\"Weber\"}",
      "query": {
        "action": "create"
      },
      "request": {
        "status": "example"
      },
      "files": {
        "file": {
           "id": "98bf4c25-58ab-4c5d-ba91-fb6f709ea78d",
           "filename": "example.png",
           "size": 420915,
           "content_type": "image/png"
        }
      },
      "headers": {
        "content-length": [
          "271"
        ],
        "user-agent": [
          "Paw\/3.1.8 (Macintosh; OS X\/10.14.6) GCDHTTPRequest"
        ],
        "request-id": [
          "37856131"
        ]
      },
      "url": "https:\/\/webhook.site\/a94a7294-c4aa-4074-ab77-c4cf86fd53b1\/201?",
      "created_at": "2019-10-03 19:06:35",
      "updated_at": "2019-10-03 19:06:35",
      "custom_action_output": []
    }
  ],
  "total": 1,
  "per_page": 50,
  "current_page": 1,
  "is_last_page": true,
  "from": 1,
  "to": 1
}
```

## Export requests to CSV

* Can require authentication.
* Rate limit: 3 requests per minute.

**GET** `/token/:token_id/requests/export`

Returns a CSV file with all requests (maximum 10000.) The amount of columns of the CSV vary depending on the request data headers, query strings, form fields, files, etc.

#### Query string parameters

* `sorting` (string) - either `newest` or `oldest` (default)
* `per_page` (int) - amount of requests returned, defaults to 10000 (max 10000)
* `page` (int) -  page number to retrieve (default 1)
* `date_from`, `date_to` (date string) - filter requests by date, format `yyyy-MM-dd HH:mm:ss`
* `query` (string) - filter requests by a query string search (see [here](#search-query-examples) for examples)

#### Response

`200 OK`

## Get single/latest request

* Can require authentication.

**GET** `/token/:token_id/request/:request_id`

**GET** `/token/:token_id/request/latest` - retrieves the latest request sent to the URL

#### Response

```json
{
  "uuid": "a2a6a4ae-4130-4063-953a-84fa29d81d43",
  "token_id": "a94a7294-c4aa-4074-ab77-c4cf86fd53b1",
  "ip": "127.0.0.1",
  "hostname": "webhook.site",
  "method": "POST",
  "user_agent": "Paw\/3.1.8 (Macintosh; OS X\/10.14.6) GCDHTTPRequest",
  "content": "{\"first_name\":\"Arch\",\"last_name\":\"Weber\"}",
  "query": {
    "action": "create"
  },
  "headers": {
    "content-length": [
      "271"
    ],
    "user-agent": [
      "Paw\/3.1.8 (Macintosh; OS X\/10.14.6) GCDHTTPRequest"
    ]
  },
  "files": {
    "foo": {
      "id": "65d6e0ce-a840-47bc-b6b6-ff1ff38c34ca",
      "filename": "example.json",
      "size": 5132873,
      "content_type": "text/plain"
    }
  },
  "url": "https:\/\/webhook.site\/a94a7294-c4aa-4074-ab77-c4cf86fd53b1\/201?",
  "created_at": "2019-10-03 19:06:35",
  "updated_at": "2019-10-03 19:06:35"
}
```

## Get raw request content

* Can require authentication.

**GET** `/token/:token_id/request/:request_id/raw`

**GET** `/token/:token_id/request/latest/raw` - retrieves the latest request sent to the URL

Returns the request as a response (body, content-type.)

#### Response

`200 OK`

## Download request file

* Can require authentication.

**GET** `/token/:tokenId/request/:requestId/download/:fileId`

Files that are included in a request or as email attachments are available to download using this endpoint.

#### Response

`304 Redirect`

## Delete request

* Can require authentication.

**DELETE** `/token/:token_id/request/:request_id`

Deletes a request. 

#### Response

`200 OK`

## Delete multiple requests

* Can require authentication.
* Rate limit: 10 requests per minute.

**DELETE** `/token/:token_id/request`

Deletes all requests associated with the token, or if `query`, `date_from` and/or `date_to` is specified, only that subset of requests is deleted.

### Query string parameters

* `date_from`, `date_to` - filter requests by date, format `yyyy-MM-dd HH:mm:ss`
* `query` - filter requests by a query string search. [See here for examples](#search-query-examples).

### Response

`200 OK`