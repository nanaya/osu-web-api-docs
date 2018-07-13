# Chat

## Get Channel List

```shell
curl "https://osu.ppy.sh/api/v2/chat/channels"
  -H "Authorization: Bearer {{token}}"
```

> The above command returns JSON structured like this:

```json
[
  {
    "channel_id": 5,
    "name": "#osu",
    "description": "The official osu! channel (english only).",
    "type": "public"
  },
  ...
]
```

This endpoint returns a list of all joinable public channels.

### HTTP Request

`GET /chat/channels`

### Response Format

Returns an array of [ChatChannel](#chatchannel)

## Join Channel

```shell
curl "https://osu.ppy.sh/api/v2/chat/channels/5/users/102"
  -X PUT
  -H "Authorization: Bearer {{token}}"
```

> The above command returns JSON structured like this:

```json
[
  {
    "channel_id": 5,
    "name": "#osu",
    "description": "The official osu! channel (english only).",
    "type": "public"
  },
  ...
]
```

This endpoint allows you to join a public channel.

### HTTP Request

`POST /chat/channels/[channel_id]/users/[user_id]`

### Response Format

Returns the joined [ChatChannel](#chatchannel)

<aside class="notice">
This endpoint will only allow the joining of public channels initially.
</aside>

<aside class="warning">Not yet implemented.</aside>

## Leave Channel

```shell
curl "https://osu.ppy.sh/api/v2/chat/channels/5/users/102"
  -X DELETE
  -H "Authorization: Bearer {{token}}"
```

> The above command will return an empty response with status code `204 No Content`

This endpoint allows you to leave a public channel.

### HTTP Request

`DELETE /chat/channels/[channel_id]/users/[user_id]`

### Response Format

_empty response_

<aside class="notice">
This endpoint will only allow the leaving of public channels initially.
</aside>

<aside class="warning">Not yet implemented.</aside>


## Create Channel

```shell
curl "https://osu.ppy.sh/api/v2/chat/new"
  -X POST
  -H "Authorization: Bearer {{token}}"
```

> The above command returns JSON structured like this:

```json
[
  "new_channel_id": 1234,
  "presence": [
    {
      "channel_id": 5,
      "name": "#osu",
      "description": "The official osu! channel (english only).",
      "type": "public",
      "last_read_id": 9150005005,
      "last_message_id": 9150005005
    },
    {
      "channel_id": 1234,
      "type": "PM",
      "name": "peppy",
      "icon": "https://a.ppy.sh/2?1519081077.png",
      "users": [
        2,
        102
      ],
      "last_read_id": 9150001235,
      "last_message_id": 9150001234
    },
    ...
  ]
  "message": {
    "message_id": 9150005005,
    "sender_id": 102,
    "channel_id": 1234,
    "timestamp": "2018-07-06T06:33:42+00:00",
    "content": "i can haz featured artist plz?",
    "is_action": 0,
    "sender": {
      "id": 102,
      "username": "nekodex",
      "profile_colour": "#333333",
      "avatar_url": "https://a.ppy.sh/102?1500537068",
      "country_code": "AU",
      "is_active": true,
      "is_bot": false,
      "is_online": true,
      "is_supporter": true
    }
  }
]
```

This endpoint allows you to create a new PM channel.

### HTTP Request

`POST /chat/new`

### POST Parameters

Parameter  | Description
---------- | -----------
target_id  | **(required)** `user_id` of user to start PM with
message    | **(required)** message to send


### Response Format

Field            | Type
---------------- | -----------------
new_channel_id   | `channel_id` of newly created [ChatChannel](#chatchannel)
presence         | array of [ChatChannel](#chatchannel)
message          | the sent [ChatMessage](#chatmessage)

<aside class="notice">
This endpoint will only allow the creation of PMs initially, group chat support will come later.
</aside>


## Get Channel Messages

```shell
curl "https://osu.ppy.sh/api/v2/chat/channels/5?limit=20"
  -H "Authorization: Bearer {{token}}"
```

> The above command returns JSON structured like this:

```json
[
  {
    "message_id": 9150005004,
    "sender_id": 2,
    "channel_id": 5,
    "timestamp": "2018-07-06T06:33:34+00:00",
    "content": "i am a lazerface",
    "is_action": 0,
    "sender": {
      "id": 2,
      "username": "peppy",
      "profile_colour": "#3366FF",
      "avatar_url": "https://a.ppy.sh/2?1519081077.png",
      "country_code": "AU",
      "is_active": true,
      "is_bot": false,
      "is_online": true,
      "is_supporter": true
    }
  },
  {
    "message_id": 9150005005,
    "sender_id": 102,
    "channel_id": 5,
    "timestamp": "2018-07-06T06:33:42+00:00",
    "content": "uh ok then",
    "is_action": 0,
    "sender": {
      "id": 102,
      "username": "nekodex",
      "profile_colour": "#333333",
      "avatar_url": "https://a.ppy.sh/102?1500537068",
      "country_code": "AU",
      "is_active": true,
      "is_bot": false,
      "is_online": true,
      "is_supporter": true
    }
  },
  ...
]
```

This endpoint returns the chat messages for a specific channel.

### HTTP Request

`GET /chat/channels/[channel_id]`

### URL Parameters

Parameter  | Description
---------- | -----------
channel_id | **(required)** The ID of the channel to retrieve messages for
limit      | number of messages to return (max of 50) [not yet implemented]

### Response Format

Returns an array of [ChatMessage](#chatmessage)

## Send Message to Channel

```shell
curl "https://osu.ppy.sh/api/v2/chat/channels/5"
  -X POST
  -d "message=i+am+a+lazerface"
  -H "Authorization: Bearer {{token}}"
```

> The above command returns JSON structured like this:

```json
{
  "message_id": 9150005004,
  "sender_id": 2,
  "channel_id": 5,
  "timestamp": "2018-07-06T06:33:34+00:00",
  "content": "i am a lazerface",
  "is_action": 0,
  "sender": {
    "id": 2,
    "username": "peppy",
    "profile_colour": "#3366FF",
    "avatar_url": "https://a.ppy.sh/2?1519081077.png",
    "country_code": "AU",
    "is_active": true,
    "is_bot": false,
    "is_online": true,
    "is_supporter": true
  }
}
```

### HTTP Request

`POST /chat/channels/[channel_id]`

### URL Parameters

Parameter  | Description
---------- | -----------
channel_id | **(required)** The `channel_id` of the channel to mark as read

### POST Parameters

Parameter  | Description
---------- | -----------
message    | **(required)** The message content (url encoded)

### Response Format

The sent [ChatMessage](#chatmessage)

<aside class="notice">
When sending a message, the <code>last_read_id</code> for the <a href='#chatchannel'>ChatChannel</a> is also updated to mark the new message as read.
</aside>


## Mark Channel as Read

```shell
curl "https://osu.ppy.sh/api/v2/chat/channels/5/mark-as-read"
  -X POST
  -d "message_id=9150005005"
  -H "Authorization: Bearer {{token}}"
```

> The above command will return an empty response with status code `204 No Content`

This endpoint marks the channel as having being read up to the given `message_id`.

### HTTP Request

`POST /chat/channels/[channel_id]/mark-as-read`

### URL Parameters

Parameter  | Description
---------- | -----------
channel_id | **(required)** The `channel_id` of the channel to mark as read

### POST Parameters

Parameter  | Description
---------- | -----------
message_id | **(required)** The `message_id` of the message to mark as read up to

### Response Format

_empty response_

<aside class="notice">
Note that the read marker cannot be moved backwards - i.e. if a channel has been marked as read up to <code>message_id = 12</code>, you cannot then set it backwards to <code>message_id = 10</code>. It will be rejected.
</aside>


## Get Updates

```shell
curl "https://osu.ppy.sh/api/v2/chat/updates?since=9150005005"
  -H "Authorization: Bearer {{token}}"
```

> The above command returns JSON structured like this:

```json
[
  "presence": [
    {
      "channel_id": 5,
      "name": "#osu",
      "description": "The official osu! channel (english only).",
      "type": "public",
      "last_read_id": 9150005005,
      "last_message_id": 9150005005
    },
    {
      "channel_id": 12345,
      "type": "PM",
      "name": "peppy",
      "icon": "https://a.ppy.sh/2?1519081077.png",
      "users": [
        2,
        102
      ],
      "last_read_id": 9150001235,
      "last_message_id": 9150001234
    },
    ...
  ],
  "messages": [
    {
      "message_id": 9150005004,
      "sender_id": 2,
      "channel_id": 5,
      "timestamp": "2018-07-06T06:33:34+00:00",
      "content": "i am a lazerface",
      "is_action": 0,
      "sender": {
        "id": 2,
        "username": "peppy",
        "profile_colour": "#3366FF",
        "avatar_url": "https://a.ppy.sh/2?1519081077.png",
        "country_code": "AU",
        "is_active": true,
        "is_bot": false,
        "is_online": true,
        "is_supporter": true
      }
    },
    {
      "message_id": 9150005005,
      "sender_id": 102,
      "channel_id": 5,
      "timestamp": "2018-07-06T06:33:42+00:00",
      "content": "uh ok then",
      "is_action": 0,
      "sender": {
        "id": 102,
        "username": "nekodex",
        "profile_colour": "#333333",
        "avatar_url": "https://a.ppy.sh/102?1500537068",
        "country_code": "AU",
        "is_active": true,
        "is_bot": false,
        "is_online": true,
        "is_supporter": true
      }
    },
    ...
  ]
]
```

This endpoint returns new messages since the given `message_id` along with updated channel 'presence' data.

### HTTP Request

`GET /chat/updates?since=[message_id]`

### URL Parameters

Parameter  | Description
---------- | -----------
message_id | **(required)** The `message_id` of the last message to retrieve messages since

### Response Format

Field            | Type
---------------- | -----------------
presence         | array of [ChatChannel](#chatchannel)
messages         | array of [ChatMessage](#chatmessage)

<aside class="notice">
Note that this returns messages for all channels the user has joined.
</aside>
