# Node-RED_Twitch_EventSub
Node-RED flow to subscribe, receive and respond to Twitch webhook
<img src="https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/pictures/Dashboard.png" >
<img src="https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/pictures/EventSubFlow.PNG" >
## Note 
- My [Twitch channel](https://www.twitch.tv/ioodyme)
- To [support me](https://paypal.me/ioodyme)
- It is **HIGHLY** recommended to [secure](https://nodered.org/docs/user-guide/runtime/securing-node-red#editor--admin-api-security) your Node-RED flow (your server will be exposed to the internet) !!
- [EventSub doc](https://dev.twitch.tv/docs/eventsub)
- This Flow is compatible with the [Twitch API](https://dev.twitch.tv/docs/api/reference)

## Prerequisites 
- [Node-RED](https://nodered.org/) running on port 443 with [HTTPS](https://nodered.org/docs/user-guide/runtime/securing-node-red#enabling-https-access) enabled OR a [ngrok auth token](https://dashboard.ngrok.com/get-started/your-authtoken)

- Twitch [APP](https://dev.twitch.tv/console/apps/) Client ID
- Twitch [APP](https://dev.twitch.tv/console/apps/) Client Secret

## Dependencies 
- node-red-dashboard
- node-red-contrib-crypto-js-dynamic
- Optional : node-red-contrib-ngrok

## For ngrok users
- Create a free account on [ngrok](https://ngrok.com/) 
- Save your AuthToken
- Install the [ngrok](https://flows.nodered.org/node/node-red-contrib-ngrok) node on Node-RED
- Drag and drop a ngrok node on your flow
- Setup the node using your AuthToken
- Open a tunnel and save the URL

<img src="https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/pictures/NgrockURL.png" width="50%">

## Twitch Setup
- Create an [APP](https://dev.twitch.tv/console/apps/) and save your APP ID and Secret
- Add the following URL using your domain name or ngrok tunnel URL
<img src="https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/pictures/Redirect.png" width="80%">

*Note : As your Node-RED should be secured with http basic auth the URI are **https://admin:password@xxxxxxxxx.eu.ngrok.io** or **https://admin:password@your.domain.name** with "admin" and "password" corresponding to you Node-RED auth.*

## Node-RED Setup

### API

<img src="https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/pictures/Settings1.png" width="75%">

- [Import](https://nodered.org/docs/user-guide/editor/workspace/import-export) the [flow](https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/EventSub-Twitch-Flow.json)
- Edit the API Settings node with your
   - Twitch client ID
   - Twitch client secret
   - Sub secret : a password (defined by the user) to validate the Twitch event signature 
   - Twitch channel 
   - Sub URI : your Node-RED server name or ngrok tunnel URL **WITHOUT**  "HTTPS://" (Ex : your.domain.name or xxxxxxxxxxx.ngrok.io and admin:password@your.domain.name or admin:password@xxxxxxxxxxx.ngrok.io for a properly secured server)
   - [Scopes](https://dev.twitch.tv/docs/authentication#scopes) (space-separated) 
   
*Scopes*
> bits:read channel:manage:broadcast channel:manage:polls channel:manage:predictions channel:manage:redemptions channel:read:polls channel:read:predictions channel:read:redemptions channel:read:subscriptions moderation:read user:read:follows user:read:subscriptions channel:moderate channel:read:hype_train

### Tokens

<img src="https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/pictures/Auth.png" width="30%">

- Go to the Node-RED dashboard (https://your.domain.name/ui or https://xxxxxxxxxx.ngrok.io/ui)
- Generate an APP token and USER token by clicking on Auhtorize APP and Authorize USER (will requires to loggin with your Twitch account and accept the scopes)
- Optional : you can test the validity and expiration of the Token using "Validate" nodes on the Node-RED editor 

*Note : The Authorize App and Authorize User buttons will appear when the API options are submitted*

## Subscribe
- Type the channel username
- Subscribe to an event by selecting the desired Event on the Node-RED GUI
- Clic on "Subscribe"

<img src="https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/pictures/Sub.png" width="50%">

## Unsubscribe
- Refresh the subscriptions
- Select the channel 
- Select the event you want to unsubscribe
- Clic on "Unsubscribe"

<img src="https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/pictures/Unsub.png" width="30%">

## Events

If you subscribed to multiple channels you can separte the event by the broadcaster channel ID.

<img src="https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/pictures/Subfilter.png" width="25%">

- When an event is posted to /webhook the JSON will be validated using the "Sub secret" code and sent to the second flow "Reponse"
- The "Inject" node and "Fake event" function can be removes as they are only used for Testing/Debug purposes
- Retrieve and use the events informations by connectig your node/function to the annotated functions

<img src="https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/pictures/Responses.png" width="40%">

<img src="https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/pictures/Annotation.png" width="40%">

**HAVE FUN**
