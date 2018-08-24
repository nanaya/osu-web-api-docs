# Object Structures

## ChatChannel
```json
{
  "channel_id": 1337,
  "name": "test channel",
  "description": "wheeeee",
  "icon": "/images/layout/avatar-guest@2x.png",
  "type": "GROUP",
  "last_read_id": 9150005005,
  "last_message_id": 9150005005,
  "users": [
    2,
    3,
    102
  ]
}
```

Represents an individual chat "channel" in the game.

Field            | Type                 | Description
---------------- | -------------------- | ------------------
channel_id       | int                  |
name             | string               |
description      | ?string              |
icon?            | string               | display icon for the channel
type             | string               | see channel types below
last_read_id?    | ?int                 | `message_id` of last message read (only returned in presence responses)
last_message_id? | ?int                 | `message_id` of last known message (only returned in presence responses)
users?           | ?int[]               | array of `user_id` listing those in the channel (only for `GROUP` channels)

### Channel Types

Type        | Permission Check for Joining/Messaging
----------- | -----------------------------------------------------
PUBLIC      |
PRIVATE     | is player in the allowed groups? (channel.allowed_groups)
MULTIPLAYER | is player currently in the mp game?
SPECTATOR   |
TEMPORARY   | _deprecated_
PM          | see below (user_channels)
GROUP       | is player in channel? (user_channels)

For PMs, two factors are taken into account:

- Is either user blocking the other? If so, deny.
- Does the target only accept PMs from friends? Is the current user a friend? If not, deny.

<aside class="notice">
Public channels, group chats and private DMs are all considered "channels".
</aside>


## ChatMessage
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

Represents an individual Message within a [ChatChannel](#chatchannel).

Field      | Type                         | Description
---------- | ---------------------------- | ------------------------------------------------------------
message_id | int                          | unique identifier for message
sender_id  | int                          | `user_id` of the sender
channel_id | int                          | `channel_id` of where the message was sent
timestamp  | string                       | when the message was sent, ISO-8601
content    | string                       | message content
is_action  | boolean                      | was this an action? i.e. `/me dances`
sender     | [UserCompact](#usercompact)  | embeded UserCompact object to save additional api lookups


## User
```json
{
  "💃": true,
}
```

Represents a User.

<aside class="notice">TODO: This &gt;.&gt;</aside>


## UserCompact
```json
{
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
```
This is a subset of the above [User](#user), mainly used for embedding in certain responses to save additional api lookups.

Field          | Type        | Description
-------------- | ------------| ----------------------------------------------------------------------
id             | int         | unique identifier for user
username       | string      | user's display name
profile_colour | string      | colour of username/profile highlight, hex code (e.g. `#333333`)
avatar_url     | string      | url of user's avatar
country_code   | string      | two-letter code representing user's country
is_active      | boolean     | has this account been active in the last x months?
is_bot         | boolean     | is this a bot account?
is_online      | boolean     | is the user currently online? (either on lazer or the new website)
is_supporter   | boolean     | does this user have supporter?
