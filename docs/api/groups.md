# API Endpoints: Groups

Webhook.site Groups allows you to organize your Tokens. Each Group is a container for multiple Tokens.

## Create Group

* Requires authentication.

#### Request

**POST** `/groups`

* `name` (string) The name of the group.

```json
{
  "name": "My Group"
}
```

#### Response

```json
{
  "id": 3498,
  "team_id": 12098,
  "name": "My Group",
  "updated_at": "2023-04-26 18:43:46",
  "created_at": "2023-04-26 18:43:46"
}
```

## Get all Groups

* Requires authentication.

#### Request

**GET** `/groups`

#### Response

```json
{
   "current_page": 1,
   "data": [
      {
         "id": 3498,
         "team_id": 12098,
         "name": "My Group",
         "created_at": "2022-10-26 14:25:11",
         "updated_at": "2022-10-26 14:25:11"
      },
      {
         "id": 3499,
         "team_id": 12098,
         "name": "My nice group",
         "created_at": "2023-04-26 09:57:40",
         "updated_at": "2023-04-26 09:57:40"
      }
   ],
   "first_page_url": "https:\/\/webhook.site\/groups?page=1",
   "from": 1,
   "last_page": 1,
   "last_page_url": "https:\/\/webhook.site\/groups?page=1",
   "next_page_url": null,
   "path": "https:\/\/webhook.site\/groups",
   "per_page": "2",
   "prev_page_url": null,
   "to": 2,
   "total": 2
}
```

## Update Group

#### Request

**PUT** `/groups/:groupId`

(See *Create Group* above for request.)

#### Response

(See *Create Group* above for response.)

## Delete Group

#### Request

**DELETE** `/groups/:groupId`

#### Response

`204 No content`
