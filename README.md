# Node-RED_Twitch_EventSub
Node-RED flow to subscribe, receive and respond to Twitch webhook
<img src="https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/pictures/EventSubFlow.PNG" >

## Note 
- My [Twitch channel](https://www.twitch.tv/ioodyme)
- It is **HIGHLY** recommended to [secure](https://nodered.org/docs/user-guide/runtime/securing-node-red#editor--admin-api-security) your Node-RED flow (your server will be exposed to the internet) !!
- [EventSub doc](https://dev.twitch.tv/docs/eventsub)
- This Flow is compatible with the "regular" [Twitch API](https://dev.twitch.tv/docs/api/reference) and the following [flow](https://github.com/n3odym3/Twitch-API_Node-RED) 

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

## Node-RED Setup
- [Import](https://nodered.org/docs/user-guide/editor/workspace/import-export) the [flow](https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/EventSub-Twitch-Flow.json)
- Edit the API Settings node with your
   - Twitch client ID
   - Twitch client secret
   - Sub secret : a password (defined by the user) to validate the Twitch event signature 
   - Twitch channel 
   - Sub URI : your Node-RED server name or ngrok tunnel URL **WITHOUT**  "HTTPS://" (Ex : your.domain.name or xxxxxxxxxxx.ngrok.io)
   - [Scopes](https://dev.twitch.tv/docs/authentication#scopes) (space-separated)
<img src="https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/pictures/Settings.png" width="50%">
- Go to the Node-RED dashboard (https://your.domain.name/ui or https://xxxxxxxxxx.ngrok.io/ui)
- Generate an APP token and USER token by clicking on Auhtorize APP and Authorize USER (will requires to loggin with your Twitch account and accept the scopes)
- Optional : you can test the validity and expiration of the Token using "Validate" nodes on the Node-RED editor
- Clic on the "Get channel ID" inject node
<img src="https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/pictures/Authorizations.png" width="25%">

## Subscribe
- Subscribe to an event by selecting the desired Event on the Node-RED GUI
- Clic on "Subscribe"
<img src="https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/pictures/Sub1.png" width="30%">

## Unsubscribe
- Refresh the subscriptions
- Select the event you want to unsubscribe
- Clic on "Unsubscribe"
<img src="https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/pictures/UnSubOK.png" width="30%">

## Events
<img src="https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/pictures/Responses.png" width="50%">

- When an event is posted to /webhook the JSON will be validated using the "Sub secret" code and sent to the second flow "Reponse"

- The "Inject" node and "Fake event" function can be removes as they are only used for Testing/Debug purposes

- Retrieve and use the events informations by connectig your node/function to the annotated functions
<img src="https://github.com/n3odym3/Node-RED_Twitch_EventSub/blob/main/pictures/Annotation.png" width="50%">

**HAVE FUN**
