# API Endpoints: Databases

[More info about Databases](/databases.html).

## Run Query

#### Request

**POST** <code>https://webhook.site/database/<span class="url-param">databaseId</span>/query</code>

* `query`: The SQL query to execute.

```json
{
  "query": "select * from mytable;"
}
```

#### Response

* `result`: (array) The returned data.
* `error`: (string) If the query results in an error, the error is represented here.
* `time`: (float) Query execution time in milliseconds.

```json
{
  "result": [
    {
      "id": 1,
      "value": "hello world"
    },
    {
      "id": 2,
      "value": "it's a great day to be a query"
    }
  ],
  "error": null,
  "time": 0
}
```

Or, for an error:

```json
{
  "result": null,
  "error": "Undefined table: 7 ERROR:  relation \"nonexisting_table\" does not exist",
  "time": 0
}
```

## Create database

* Requires [authentication](/api/about.html#api-key)
* Will return `401 Unauthorized` when no databases purchased in subscription

#### Request

**POST** `https://webhook.site/databases`

* `name` (required) The name of the database.
* `group_id` Enter a group ID to attach database to a group.
* `plan` (required) Either `db-s`, `db-m`, `db-l`.

```json
{
  "name": "My Database",
  "group_id": null,
  "plan": "db-s"
}
```

#### Response

```json
{
  "id": "23984",
  "name": "My Database",
  "plan": "db-s",
  "group_id": null,
  "max_bytes": 104857600,
  "max_tables": 1,
  "team_id": 181,
  "updated_at": "2025-09-24T08:52:50.000000Z",
  "created_at": "2025-09-24T08:52:50.000000Z"
}
```

## Get all databases

**GET** `https://webhook.site/database?page=1&per_page=15`

#### Response

```json
{
  "current_page": 1,
  "data": [
    {
      "id": "23984",
      "name": "My Database",
      "plan": "db-s",
      "team_id": 345987,
      "group_id": null,
      "max_bytes": 104857600,
      "max_tables": 1,
      "bytes_used": 0,
      "tables_used": 1,
      "created_at": "2025-09-23T10:26:51.000000Z",
      "updated_at": "2025-09-23T10:26:55.000000Z",
      "group": null
    }
  ],
  "first_page_url": "https:\/\/webhook.test\/databases?page=1",
  "from": 1,
  "last_page": 1,
  "last_page_url": "https:\/\/webhook.test\/databases?page=1",
  "links": [
    {
      "url": null,
      "label": "&laquo; Previous",
      "active": false
    },
    {
      "url": "https:\/\/webhook.test\/databases?page=1",
      "label": "1",
      "active": true
    },
    {
      "url": null,
      "label": "Next &raquo;",
      "active": false
    }
  ],
  "next_page_url": null,
  "path": "https:\/\/webhook.test\/databases",
  "per_page": 15,
  "prev_page_url": null,
  "to": 1,
  "total": 1
}
```

## Update database

#### Request

**PUT** `https://webhook.site/databases`

* `name` (required) The name of the database.
* `group_id` Enter a group ID to attach database to a group.

```json
{
  "name": "My Updated Database",
  "group_id": null
}
```

#### Response

```json
{
  "id": "100014",
  "name": "My Updated Database",
  "plan": "db-s",
  "team_id": 181,
  "group_id": null,
  "max_bytes": 104857600,
  "max_tables": 1,
  "bytes_used": 0,
  "tables_used": 0,
  "created_at": "2025-09-24T08:52:50.000000Z",
  "updated_at": "2025-09-24T08:56:29.000000Z"
}
```

## Delete database

#### Request

**DELETE** <code>https://webhook.site/database/<span class="url-param">databaseId</span></code>

#### Response

`204 No content`

