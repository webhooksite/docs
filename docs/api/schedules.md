# API Endpoints: Schedules

[More info about Schedules](/schedules.html).

## Create schedule

* Requires authentication.

#### Request

**POST** `/schedules`

* `name` The name of the schedule.
* `interval` One of the following interval strings: `monthly`, `weekly`, `daily`, `hourly`, `10-minute`, `5-minute`, `1-minute`, `cron`
* `cron` When `interval` is `cron`, specify a cron-style interval, e.g. `*/5 * * * *` for every 5 minutes. Otherwise can be left out.
* `request_url` The request URL that the schedule should act on.
* `request_method` HTTP Method (POST, GET, etc.)
* `request_body` 
* `request_headers` HTTP headers, separated by `\n`
* `timeout` Timeout in seconds (min 1, max 30)
* `require_body` If specified, Webhook.site sends an error notification if response body doesn't contain this string.
* `require_status_min` If specified, Webhook.site sends an error notification if response status doesn't fit within range.
* `require_status_max` If specified, Webhook.site sends an error notification if response status doesn't fit within range.

Variables will be replaced in the fields `request_url`, `request_method`, `request_headers` and `request_body`. [More info here](/custom-actions.html#variables).

```json
{
  "name": "My schedule",
  "interval": "5-minute",
  "request_url": "https://example.com",
  "request_method": "POST",
  "request_body": "{\"json\": \"message\"}",
  "request_headers": "Authorization: Bearer mytoken\nContent-Type: application/json"
}
```

#### Response

```json
{
  "name": "My schedule",
  "interval": "5-minute",
  "request_url": "https:\/\/example.com",
  "request_method": "POST",
  "request_body": "{\"json\": \"message\"}",
  "request_headers": "Authorization: Bearer mytoken\nContent-Type: application\/json",
  "require_body": null,
  "require_status_min": null,
  "require_status_max": null,
  "user_id": 21,
  "updated_at": "2021-05-01 13:27:25",
  "created_at": "2021-05-01 13:27:25",
  "id": 58
}
```

## Get all schedules

**GET** `/schedules?page=1&per_page=15`

#### Response

```json
{
  "current_page": 1,
  "data": [
    {
      "id": 58,
      "name": "My schedule",
      "interval": "5-minute",
      "cron": null,
      "user_id": 21,
      "request_method": "POST",
      "request_url": "https:\/\/example.com",
      "request_headers": "Authorization: Bearer mytoken\nContent-Type: application\/json",
      "request_body": "{\"json\": \"message\"}",
      "timeout": 5,
      "require_body": null,
      "require_status_min": null,
      "require_status_max": null,
      "last_run_at": null,
      "last_status": null,
      "created_at": "2021-05-01 13:27:25",
      "updated_at": "2021-05-01 13:27:25"
    }
  ],
  "first_page_url": "https:\/\/webhook.site\/schedules?page=1",
  "from": 1,
  "last_page": 1,
  "last_page_url": "https:\/\/webhook.site\/schedules?page=1",
  "next_page_url": null,
  "path": "https:\/\/webhook.site\/schedules",
  "per_page": 15,
  "prev_page_url": null,
  "to": 6,
  "total": 6
}
```

## Get single schedule

#### Request

**GET** `/schedules/:scheduleId`

#### Response

```json
{
  "id": 58,
  "name": "My schedule",
  "interval": "5-minute",
  "cron": null,
  "user_id": 21,
  "request_method": "POST",
  "request_url": "https:\/\/example.com",
  "request_headers": "Authorization: Bearer mytoken\nContent-Type: application\/json",
  "request_body": "{\"json\": \"message\"}",
  "timeout": 5,
  "require_body": null,
  "require_status_min": null,
  "require_status_max": null,
  "last_run_at": null,
  "last_status": null,
  "created_at": "2021-05-01 13:27:25",
  "updated_at": "2021-05-01 13:27:25"
}
```

## Update schedule

#### Request

**PUT** `/schedules/:scheduleId`

(See *Create schedule* above for request.)

#### Response

(See *Get single schedule* for response.)

## Delete schedule

#### Request

**DELETE** `/schedules/:scheduleId`

#### Response

`204 No content`

## Run Schedule Now

#### Request

**POST** `/schedules/:scheduleId/run-now`

## Get Schedule Logs

**GET** `/schedules/:scheduleId/logs`

Set `Accept` header to `application/json`.

Rate limit: 60 requests per minute.

#### Query string parameters

* `sorting` (string) - either `newest` or `oldest` (default)

#### Response

```json
{
  "data": [
    {
      "id": 2,
      "schedule_id": 1,
      "response_status": 200,
      "response_headers": {
        "Age": [
          "447707"
        ],
        "Cache-Control": [
          "max-age=604800"
        ],
        "Content-Type": [
          "text\/html; charset=UTF-8"
        ]
      },
      "response_body": "<!doctype html>\n<html>\n<head>...",
      "time": 0.23,
      "error": null,
      "created_at": "2022-11-06 19:27:09",
      "updated_at": "2022-11-06 19:27:09"
    },
    {
      "id": 3,
      "schedule_id": 1,
      "response_status": 200,
      "response_headers": {
        "Age": [
          "404973"
        ],
        "Cache-Control": [
          "max-age=604800"
        ],
        "Content-Type": [
          "text\/html; charset=UTF-8"
        ]
      },
      "response_body": "<!doctype html>\n<html>\n<head>...",
      "time": 1.23,
      "error": null,
      "created_at": "2022-11-06 19:30:02",
      "updated_at": "2022-11-06 19:30:02"
    }
  ],
  "current_page": 1,
  "first_page_url": "https:\/\/webhook.site\/control-panel\/schedules\/1\/logs?page=1",
  "from": 1,
  "last_page": 1,
  "last_page_url": "https:\/\/webhook.site\/control-panel\/schedules\/1\/logs?page=1",
  "next_page_url": null,
  "path": "https:\/\/webhook.site\/control-panel\/schedules\/1\/logs",
  "per_page": 15,
  "prev_page_url": null,
  "to": 2,
  "total": 2
}
```