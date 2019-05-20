# Notifications

## Get Notifications

```shell
curl "https://osu.ppy.sh/api/v2/notification"
  -H "Authorization: Bearer {{token}}"
```

> The above command returns JSON structured like this:

```json
{
  has_more: true,
  notifications: {
    id: 1,
    name: 'forum_topic_reply',
    created_at: '2019-04-24T07:12:43+00:00',
    object_type: 'forum_topic',
    object_id: 1,
    source_user_id: 1,
    is_read: false,
    details: {
        title: 'A topic',
        post_id: 2,
        username: 'User',
        cover_url: 'https://...'
    }
  },
  unread_count: 100,
  notification_endpoint: 'wss://notify.ppy.sh'
  ...
}
```

This endpoint returns a list of the user's unread notifications. Sorted descending by `id` with limit of 50.

### HTTP Request

`GET /notifications`

### URL Parameters

Parameter | Description
--------- | ------------------------------------------------------------------------------------------------------------------
`max_id`  | Maximum `id` fetched. Can be used to load earlier notifications. Defaults to no limit (fetch latest notifications)

### Response Format

Returns an object containing [Notification](#notification) and other related attributes.

Field                 | Type
--------------------- | ---------------------------------------------------
has_more              | boolean whether or not there are more notifications
notifications         | array of [Notification](#notification)
unread_count          | total unread notifications
notification_endpoint | url to connect to websocket server

## Mark Notifications as Read

```shell
curl "https://osu.ppy.sh/api/v2/notifications/mark-read"
  -X POST
  -H "Authorization: Bearer {{token}}"
```

> The above command will return an empty response with status code `204 No Content`

This endpoint allows you to mark notifications read.

### HTTP Request

`POST /notifications/mark-read`

### POST Parameters

Parameter  | Description
---------- | -----------
`ids[]`    | **(required)** `id` of notifications to be marked as read.

### Response Format

_empty response_

## Listen Notifications

```shell
wscat -c "{notification_endpoint}"
  -H "Authorization: Bearer {{token}}"
```

> The above command will wait and display new notifications as they arrive

This endpoint allows you to receive notifications without constantly polling the server. Correct notification will be a JSON string with at least `event` field:

Field | Type   | Description
----- | ------ | -----------
event | string | See below

Events:

- `logout`: user session using same authentication key has been logged out (not yet implemented for OAuth authentication)
- `new`: new notification
- `read`: notification has been read


### `logout` event

Server will disconnect session after sending this event so don't try to reconnect.

Field | Type   | Description
----- | ------ | -----------
event | string | `logout`

### `new` event

New notification. See [Notification](#notification) object for type of notifications.

Field | Type                          | Description
----- | ----------------------------- | -----------
event | string                        | `new`
data  | [Notification](#notification) |


### `read` event

Notification has been read.

Field | Type    | Description
----- | ------- | ----------------------------------
event| string   | `read`
ids  | number[] | id of Notifications which are read
