# API Endpoints: Custom Actions

The Custom Actions API allows you to manage the Custom Actions associated with a given Token. [More info about Custom Actions](/custom-actions.html).

[List of the API names and parameters for Action Types](action-types.md).

## Actions

### Create Custom Action

* Can require authentication.

**POST** `/token/:token_id/actions`

* `type` (string) is the name of an [Action Type](action-types.md).
* `order` (int) specified which order the action is executed in.
* `parameters` (object) can vary depending on the [Action Type](action-types.md). 
* `disabled` (bool) if set to true, the action is skipped upon execution.
* `queue` (bool) If set to true, the action is run asynchronously. [More info here](/custom-actions.html#queued-actions)
* `delay` (int, max 86400) If set (along with `queue` to true), Webhook.site waits the specified amount of seconds to run the action.
* `condition` (uuid) If set to an ID of a Conditions action, the action will only run if the condition passes, and is otherwise skipped.

#### Request


##### Example 1: Condition action

```json
{
  "type": "condition",
  "order": 3,
  "disabled": false,
  "parameters": {
    "input": "$request.content$",
    "operator": "eq",
    "value": "",
    "action": "stop"
  }
}
```

##### Example 2: WebhookScript action

```json
{
    "type": "script",
    "order": 1,
    "parameters": {
        "script": "expiry = '2021-08-01T00:00:00.000000Z'\nnow = to_date('now')\n\nif (date_interval(now, expiry) < 0) {\n    // Respond with 410 Gone\n    respond('This content is no longer available.', 410)\n}\n"
    }
}
```

##### Example 3: Creating WebhookScript action with Python 3

Same script as Example 2. Requires the `requests` module, which can be installed using `pip install requests`.

```python
import requests

script = """
expiry = '2021-08-01T00:00:00.000000Z'
now = to_date('now')

if (date_interval(now, expiry) < 0) {
    // Respond with 410 Gone
    respond('This content is no longer available.', 410)
}
"""

data = {
    "type": "script",
    "order": 1,
    "parameters": {
        "script": script
    }
}

r = requests.post('https://webhook.site/token/7d63959e-4fec-49bd-90dc-a4615722825e/actions', json=data)
```

#### Response

```json
{
    "uuid": "7ae324d6-c65b-416b-8f83-18fb89e0c740",
    "token_id": "fe18d303-631d-4620-acb3-5c0b1b0b876d",
    "type": "condition",
    "order": 3,
    "disabled": null,
    "parameters": {
        "input": "$request.content$",
        "operator": "eq",
        "value": "",
        "action": "stop"
    }
}
```

### Get Custom Actions

* Can require authentication.

**GET** `/token/:token_id/actions`

#### Response

`200 OK`

```json
{
  "data": [
    {
      "uuid": "52055928-099a-44dc-ba31-e8d808b98ea1",
      "token_id": "fe18d303-631d-4620-acb3-5c0b1b0b876d",
      "type": "condition",
      "order": 1,
      "disabled": false,
      "parameters": {
        "input": "$request.header.content-type$",
        "operator": "nct",
        "value": "application/json",
        "action": "stop"
      }
    },
    {
      "uuid": "27b07ca7-ea83-48f5-b376-2372cf25d3a1",
      "token_id": "fe18d303-631d-4620-acb3-5c0b1b0b876d",
      "type": "condition",
      "order": 2,
      "disabled": null,
      "parameters": {
        "input": "$request.content$",
        "operator": "eq",
        "value": "",
        "action": "stop"
      }
    }
  ]
}
```

### Update Custom Action

* Can require authentication.

**PUT** `/token/:token_id/actions/:action_id`

#### Request

*See [Create Custom Action](#create-custom-action) endpoint.*

#### Response

*See [Create Custom Action](#create-custom-action) endpoint.*

### Test Custom Action

* Can require authentication.

#### Request

**POST** `/token/:token_id/test-action`

##### Query string parameters

* `request_id`: A request ID to base the test run on. If not set, uses default request variables.
* `action_id`: When set, overwrites the parameters of an existing action. If not, tests a temporary new, empty action with ID `00000000-0000-4000-0000-000000000000`.

```json
{
  "type": "script",
  "order": 2,
  "parameters": {
    "script": "echo('hello world')"
  }
}
```

#### Response

`200 OK`

```json
{
  "success": true,
  "result": {
    "output": {
      "08529a4f-ad84-450b-977a-1d126d6ca6b7": [
        "Set runtime variable $aaa$ to \"example\""
      ],
      "00000000-0000-4000-0000-000000000000": [
        "hello world"
      ]
    },
    "response": {
      "content": null,
      "status": null,
      "headers": null
    },
    "variables": {
      "request.header.content-length": "57362",
      "request.header.user-agent": "Paw/3.3.5 (Macintosh; OS X/11.6.2) GCDHTTPRequest",
      "request.header.connection": "close",
      "request.header.host": "webhook.site",
      "request.header.content-type": "application/json",
      "request.uuid": "87240a26-1426-45dd-9b4c-961a323652a9",
      "request.token_id": "7fc77812-9efe-41b6-9365-e2c1fb5feb62",
      "request.content": "",
      "request.date": "2022-03-20 10:18:58",
      "request.timestamp": 1647771538,
      "request.hostname": "webhook.site",
      "request.size": 0,
      "request.type": "web",
      "request.ip": "127.0.0.1",
      "request.user_agent": "Paw/3.3.5 (Macintosh; OS X/11.6.2) GCDHTTPRequest",
      "request.url": "https://webhook.site/7fc77812-9efe-41b6-9365-e2c1fb5feb62",
      "request.method": "POST",
      "aaa": "example"
    }
  }
}
```

### Execute Custom Actions

* Can require authentication.

**POST** `/token/:token_id/request/:request_id/execute`

Runs all Custom Actions for a specific token and request and returns the output. 

#### Response

`200 OK`

*See [Test Custom Action](#test-custom-action) endpoint.*

### Delete Custom Action

* Can require authentication.

**DELETE** `/token/:token_id/actions/:action_id`