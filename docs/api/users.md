# API Endpoints: Users

## Invite User

* Requires [authentication](/api/about.html#api-key)
* Requires Administrator user type

If part of a SSO-enabled Webhook.site Team, the user is sent a login URL where they can log in immediately. Otherwise, they are sent a link to a page where they can set up their profile and password.

#### Request

**POST** `https://webhook.site/users/invite`

* `name` (string) The name of the user.
* `email` (string) The user's email, and where the invite is sent.
* `user_type_id` (int) One of: `100` (Administrator), `200` (Member),  `300` (Viewer)

```json
{
  "name": "Elijah Craig",
  "email": "ej@example.com",
  "user_type_id": 300,
  "role_id": 20001
}
```

#### Response

```json
{
  "id": 30001
  "name": "Elijah Craig",
  "email": "ej@example.com",
  "user_type_id": 300
  "team_id": 10001,
  "roles": [
    {
      "id": 20001,
      "team_id": 10001,
      "name": "Test Role",
      "created_at": "2024-10-15T10:19:07.000000Z",
      "updated_at": "2025-02-17T12:00:48.000000Z"
    }
  ]
  "updated_at": "2025-09-29T08:18:56.000000Z",
  "created_at": "2025-09-29T08:18:56.000000Z"
}
```

## Get all Users

* Requires [authentication](/api/about.html#api-key)
* Requires Administrator user type

#### Request

**GET** `https://webhook.site/users`

#### Response

```json
{
  "current_page": 1,
  "data": [
    {
      "id": 1001,
      "name": "Jim Beam",
      "email": "jb@example.com",
      "two_factor_enabled": 0,
      "created_at": "2020-01-08T21:34:25.000000Z",
      "updated_at": "2025-02-27T10:50:13.000000Z",
      "last_login_at": "2025-09-29T07:59:15.000000Z",
      "team_id": 10001,
      "user_type_id": 100
    },
    {
      "id": 30001
      "name": "Elijah Craig",
      "email": "ej@example.com",
      "two_factor_enabled": 0,
      "created_at": "2025-02-13T13:22:48.000000Z",
      "updated_at": "2025-08-01T16:05:20.000000Z",
      "last_login_at": "2025-09-23T07:52:15.000000Z",
      "team_id": 10001,
      "user_type_id": 300
    }
  ],
  "first_page_url": "https:\/\/webhook.site\/users?page=1",
  "from": 1,
  "last_page": 1,
  "last_page_url": "https:\/\/webhook.site\/users?page=1",
  "links": [
    {
      "url": null,
      "label": "&laquo; Previous",
      "active": false
    },
    {
      "url": "https:\/\/webhook.site\/users?page=1",
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
  "path": "https:\/\/webhook.site\/users",
  "per_page": 15,
  "prev_page_url": null,
  "to": 2,
  "total": 2
}
```

## Update User

#### Request

**PUT** <code>https://webhook.site/users/<span class="url-param">userId</span></code>

* `name` (string) The name of the user.
* `email` (string)
* `user_type_id` (int) One of: `100` (Administrator), `200` (Member),  `300` (Viewer)

```json
{
  "name": "Elijah Craig",
  "email": "ej@example.com",
  "user_type_id": 300,
  "role_id": 20001,
}
```

#### Response

(See *Create User* above for response.)

## Delete User

#### Request

**DELETE** <code>https://webhook.site/users/<span class="url-param">userId</span></code>

#### Response

`204 No content`
