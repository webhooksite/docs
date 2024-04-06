# API Endpoints: Templates

Webhook.site Templates allows you to create templates of actions, and re-use these templates with the Include Template Custom Action.

## Create Template

* Requires authentication.

#### Request

**POST** `/template`

* `name` The name of the template.
* `actions` An array of objects containing Custom Actions. All parameters of actions except `disabled` can be used. [More info here](/api/custom-actions.html)
* `variables` An array of name-value objects containing predefined variables. These variables are defined before the action runs, and are available to any subsequent actions after the template is included.

```json
{
    "actions": [
        {
            "name": null,
            "type": "conditions",
            "queue": false,
            "delay": 0,
            "condition": null,
            "parameters": {
                "conditions": [
                    {
                        "input": "$date$",
                        "operator": "eq",
                        "value": "$post-news-last-date$"
                    }
                ],
                "mode": "all",
                "action": "stop"
            },
            "order": 2
        },
        {
            "name": null,
            "type": "twitter_tweet",
            "queue": false,
            "delay": 0,
            "condition": null,
            "parameters": {
                "provider_id": "501133",
                "tweet": "$tweet$"
            },
            "order": 3
        },
        {
            "name": null,
            "type": "store_global_variable",
            "queue": false,
            "delay": 0,
            "condition": null,
            "parameters": {
                "name": "post-news-last-date",
                "value": "$date$"
            },
            "order": 4
        }
    ],
    "name": "My Template",
    "variables": [
        {
            "name": "example",
            "value": "hello world"
        }
    ],
}
```

#### Response

```json
{
  "name": "My Template",
  "variables": [
    {
      "name": "example",
      "value": "hello world"
    }
  ],
  "team_id": 1,
  "updated_at": "2024-02-20T10:01:29.000000Z",
  "created_at": "2024-02-20T10:01:29.000000Z",
  "id": 21,
  "actions": [
    {
      "condition": null,
      "delay": 0,
      "parameters": {
        "mode": "all",
        "conditions": [
          {
            "input": "$date$",
            "operator": "eq",
            "value": "$post-news-last-date$"
          }
        ],
        "action": "stop"
      },
      "token_id": "f1bd342e-c98b-4ac4-bf3f-c35f1f338161",
      "type": "conditions",
      "order": 2,
      "name": null,
      "template_id": 21,
      "uuid": "9b615454-3c64-4da2-a2f7-d524797a8925",
      "updated_at": "2024-02-20T10:01:29.000000Z",
      "created_at": "2024-02-20T10:01:29.000000Z"
    },
    {
      "condition": null,
      "delay": 0,
      "parameters": {
        "tweet": "$tweet$",
        "provider_id": "501133"
      },
      "token_id": "f1bd342e-c98b-4ac4-bf3f-c35f1f338161",
      "type": "twitter_tweet",
      "order": 3,
      "name": null,
      "template_id": 21,
      "uuid": "9b615454-3ce7-4c63-bc8b-3412694ae633",
      "updated_at": "2024-02-20T10:01:29.000000Z",
      "created_at": "2024-02-20T10:01:29.000000Z"
    },
    {
      "condition": null,
      "delay": 0,
      "parameters": {
        "name": "post-news-last-date",
        "value": "$date$"
      },
      "token_id": "f1bd342e-c98b-4ac4-bf3f-c35f1f338161",
      "type": "store_global_variable",
      "order": 4,
      "name": null,
      "template_id": 21,
      "uuid": "9b615454-3d5f-4cd6-bd4b-94b55e6f6f2f",
      "updated_at": "2024-02-20T10:01:29.000000Z",
      "created_at": "2024-02-20T10:01:29.000000Z"
    }
  ]
}
```

## Get all Templates

* Requires authentication.

#### Request

**GET** `/templates`

#### Response

```json
{
  "current_page": 1,
  "data": [
    {
      "name": "My Template",
      "variables": [
        {
          "name": "example",
          "value": "hello world"
        }
      ],
      "team_id": 1,
      "updated_at": "2024-02-20T10:01:29.000000Z",
      "created_at": "2024-02-20T10:01:29.000000Z",
      "id": 21,
      "actions": [
        {
          "condition": null,
          "delay": 0,
          "parameters": {
            "mode": "all",
            "conditions": [
              {
                "input": "$date$",
                "operator": "eq",
                "value": "$post-news-last-date$"
              }
            ],
            "action": "stop"
          },
          "token_id": "f1bd342e-c98b-4ac4-bf3f-c35f1f338161",
          "type": "conditions",
          "order": 2,
          "name": null,
          "template_id": 21,
          "uuid": "9b615454-3c64-4da2-a2f7-d524797a8925",
          "updated_at": "2024-02-20T10:01:29.000000Z",
          "created_at": "2024-02-20T10:01:29.000000Z"
        },
        {
          "condition": null,
          "delay": 0,
          "parameters": {
            "tweet": "$tweet$",
            "provider_id": "501133"
          },
          "token_id": "f1bd342e-c98b-4ac4-bf3f-c35f1f338161",
          "type": "twitter_tweet",
          "order": 3,
          "name": null,
          "template_id": 21,
          "uuid": "9b615454-3ce7-4c63-bc8b-3412694ae633",
          "updated_at": "2024-02-20T10:01:29.000000Z",
          "created_at": "2024-02-20T10:01:29.000000Z"
        },
        {
          "condition": null,
          "delay": 0,
          "parameters": {
            "name": "post-news-last-date",
            "value": "$date$"
          },
          "token_id": "f1bd342e-c98b-4ac4-bf3f-c35f1f338161",
          "type": "store_global_variable",
          "order": 4,
          "name": null,
          "template_id": 21,
          "uuid": "9b615454-3d5f-4cd6-bd4b-94b55e6f6f2f",
          "updated_at": "2024-02-20T10:01:29.000000Z",
          "created_at": "2024-02-20T10:01:29.000000Z"
        }
      ]
    }
  ],
  "first_page_url": "https:\/\/webhook.site\/templates?page=1",
  "from": 1,
  "last_page": 1,
  "last_page_url": "https:\/\/webhook.site\/templates?page=1",
  "links": [
    {
      "url": null,
      "label": "&laquo; Previous",
      "active": false
    },
    {
      "url": "https:\/\/webhook.site\/templates?page=1",
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
  "path": "https:\/\/webhook.site\/templates",
  "per_page": 15,
  "prev_page_url": null,
  "to": 1,
  "total": 1
}
```

## Update Template

#### Request

**PUT** `/templates/:templateId`

(See *Create Template* above for request.)

#### Response

(See *Create Template* above for response.)

## Delete Template

#### Request

**DELETE** `/templates/:templateId`

#### Response

`204 No content`
