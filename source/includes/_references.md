# References
<aside class="notice">TODO: Remove?</aside>

## Routes
Method   | Route                                      | Action
-------- | ------------------------------------------ | -------
POST     | messages/new                               | MessagesController@newConversation
GET      | messages/updates                           | MessagesController@updates
GET      | messages/channel/{channel_id}              | MessagesController@channel
POST     | messages/channel/{channel_id}/mark-as-read | MessagesController@postMarkAsRead
POST     | messages/{channel_id}                      | API\ChatController@postMessage
GET      | messages/presence                          | MessagesController@presence
RESOURCE | messages                                   | MessagesController
