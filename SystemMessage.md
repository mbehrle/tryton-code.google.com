

# Introduction #

For various reasons, a SysAdmin may have the requirement to inform the Tryton users about an upcoming event
  * Planned downtime
  * Temporary unavailability of certain services
  * Updates being installed
  * ...

# Details #
In order to do so, a system message should be issued to inform all affected users. A user is affected, if he currently works with the system or logs on to the system

## Data Entry ##
The SysAdmin resp. the individual with SysAdmin Rights should enter the system message in a message table, together with expiry date and time of the message.
  * More than one message at a time should be possible.
  * Limitation to 255 chars per message should be sufficient.
  * Manual deletion of message should be possible.

## Message display ##
### In case a user is logged-in when the system message is created ###
The user should receive a pop-up with the system message, and the user name of the individual who created the message. The pop-up is displayed as soon as the user performs an activity that makes the client connect to the server.
The user should confirm the message ('OK'). The message is not displayed again during this session.

### In case the user is not logged in ###
When the user logs-on to the system the message is displayed as first activity. Rest of the processing as above.

## Deletion of message ##
The Tryton system should remove the system message after its expiry date automatically. Manual deletion by SysAdmin should be possible