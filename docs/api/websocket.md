# WebSocket

You can connect to Webhook.site's WebSocket server (`https://ws.webhook.site`) and listen for incoming requests, emails and DNSHooks in your own application. 

If you listen to a token associated with a Webhook.site account, you must specify and API key. Alternatively, you can use [Webhook.site CLI](/cli.html).

## Examples

### JavaScript

First, install dependencies: `npm install socket.io-client@2` (version 2.x is required)

```javascript
const io = require("socket.io-client");

// Replace these with your actual API key and token ID
let apiKey = "000-000...";
let tokenId = "111-111...";

const socket = io("https://ws.webhook.site");

socket.on("connect_error", (e) => console.log('Connection error', e));
socket.on("error", (e) => console.log('Connection error', e));

socket.on("connect", () => {
    socket.emit("subscribe", {
        channel: `private-token.${tokenId}`,
        auth: {headers: apiKey ? {"Api-Key": apiKey} : {}}
    });
    console.log("Subscribed to channel");
});

socket.on("request.created", (channel, data) => {
    console.log(`Received event on channel ${channel}`);
    console.dir(data, {depth: null});
});
```

### Python

First, install dependencies: `pip install "python-socketio[client]"`

```python
import socketio
import pprint

api_key = '000-000...'
token_id = '111-111...'

# Create a Socket.IO client
sio = socketio.Client()

@sio.event
def disconnect():
    print("Disconnected from server")

@sio.event
def connect():
    sio.emit("subscribe", {
        "channel": f'private-token.{token_id}',
        "auth": {
            "headers": {
                "Api-Key": api_key
            }
        }
    })
    print(f"Subscribed to channel")

@sio.on("request.created")
def on_message(channel, data):
    print(f"Received event on channel {channel}")
    pprint.pprint(data)

# Connect with headers for authentication
sio.connect(
    'https://ws.webhook.site',
    transports=['websocket']
)

# Keep the script running
sio.wait()

```