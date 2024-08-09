# API Endpoints: Global Variables

With Global Variables, you can store data permanently that can be shared between your URLs. Global Variables can be used when creating Custom Actions and in Schedules. [More about Global Variables](/custom-actions/variables.html#global-variables)

## Create Global Variable

* Requires authentication.

After creating, the variable `$name$` will be available in Custom Actions.

#### Request

**POST** `/global-variables`

* `name` (string) The name of the variable.
* `value` (string) The value of the variable.

```json
{
  "name": "content_type",
  "value": "application/json"
}
```

#### Response

```json
{
  "id": 598297,
  "name": "content_type",
  "team_id": 1,
  "value": "application\/json",
  "updated_at": "2024-04-15T11:20:02.000000Z",
  "created_at": "2024-04-15T11:20:02.000000Z"
}
```

## Get all Global Variables

* Requires authentication.

#### Request

**GET** `/global-variables`

#### Query string parameters

* `per_page` (int) - amount of requests returned, defaults to 50 (max 100)
* `page` (int) -  page number to retrieve (default 1)
* `search` (string) - filter variables by name

#### Response

```json
{
  "current_page": 1,
  "data": [
    {
      "id": 598297,
      "user_id": 0,
      "team_id": 1,
      "name": "content_type",
      "value": "application\/json",
      "created_at": "2024-04-15T11:20:02.000000Z",
      "updated_at": "2024-04-15T11:20:02.000000Z"
    },
    {
      "id": 598294,
      "user_id": 0,
      "team_id": 1,
      "name": "test",
      "value": "\ud83e\udd72",
      "created_at": "2024-04-14T13:21:24.000000Z",
      "updated_at": "2024-04-14T13:21:24.000000Z"
    }
  ],
  "first_page_url": "https:\/\/webhook.test\/global-variables?page=1",
  "from": 1,
  "last_page": 21992,
  "last_page_url": "https:\/\/webhook.test\/global-variables?page=21992",
  "links": [
    {
      "url": null,
      "label": "&laquo; Previous",
      "active": false
    },
    {
      "url": "https:\/\/webhook.test\/global-variables?page=1",
      "label": "1",
      "active": true
    },
    {
      "url": null,
      "label": "...",
      "active": false
    },
    {
      "url": "https:\/\/webhook.test\/global-variables?page=21991",
      "label": "21991",
      "active": false
    },
    {
      "url": "https:\/\/webhook.test\/global-variables?page=2",
      "label": "Next &raquo;",
      "active": false
    }
  ],
  "next_page_url": "https:\/\/webhook.test\/global-variables?page=2",
  "path": "https:\/\/webhook.test\/global-variables",
  "per_page": 15,
  "prev_page_url": null,
  "to": 15,
  "total": 329870
}
```

## Update Global Variable

#### Request

**PUT** `/global-variables/:globalVariableId`

(See *Create Global Variable* above for request.)

#### Response

(See *Create Global Variable* above for response.)

## Delete Global Variable

#### Request

**DELETE** `/global-variables/:globalVariableId`

#### Response

`204 No content`
