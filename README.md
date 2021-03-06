# xauthbot for Telegram

Use my bot to connect your webapp or software to Telegram and let users log in with their Telegram accounts.

### How to use it
 * Register your app first ([here](https://xauth.ldkf.de/registerapp.php))
 * To connect a user, forward them to https://xauth.ldkf.de/connect.php?appid=YOURAPPID&ret=RET
 * After successfully authenticating, your user will be forwarded to https://yourdomain.tld/RET?id= (or http if you didn't select https at registration) where id is the user's id.
 * You'll need this id when you want to make requests to the API

### The API

 * URL: https://xauth.ldkf.de/api.php
 * For a successful request you need the following POST or GET (you can even combine them) parameters:
    * appid - you get it after the registration of your app together with the secret
    * id - the user id, you get when the user returns after connecting
    * action - what you want to do with the API (see below)
    * hash - the sha256 hash of the following data without separation between: secret (from app registration), appid, id, action[, mesg] - a string to hash could look like this: 6O4BZl1yj9btgqyjRFBH43username
    * [msg - only needed if you want to send a message]

#### Actions

* username - to get the user's username on Telegram (keep in mind that not everyone has one - this could return an empty string)
* first_name - to get the user's first name on Telegram
* last_name - to get the user's username on Telegram (keep in mind that not everyone has one - this could return an empty string)
* all - to get username, first_name and last_name
* logout - to log a user out
* message - Send a message to a user - you need to send the message in the msg parameter - make sure to include msg in the hash

#### Response

* The API will return data json encoded
* A response will always have a statuscode and status
* Statuscodes used at the moment are
    * 200 - Success
    * 400 - Syntax Error (this could be a wrong hash, missing parameters or non-existing users)
    * 402 - Not logged out (Error logging out, most likely the user is already logged out)
    * 403 - Syntax Error, no message provided (You didn't send a message with the message parameter)
    * 405 - User rejects messages (The user disabled messaging for your site)
* In case of 200, the requested data will be in the corresponding field (ie the username in the username field)

### How it works

* When visiting the connect page, the user will get an entry with an authentication code
* If they click on the link to the bot, the authentication code will be sent to the bot via deep linking - the user never sees it


### To-do
* you tell me
