# Webhook.site as an ngrok alternative

With Webhook.site CLI, you can easily forward requests to your Webhook.site URL to a local endpoint, or even another endpoint that's behind a firewall.

To get started, install Webhook.site CLI (`whcli`) via NPM or Docker, and follow the examples. If you're a Webhook.site subscriber, you'll also need an API key.

1. To install via NPM: `npm install -g @webhooksite/cli`
2. Now you should be able to run `whcli`
3. To create the tunnel, use the following command: 
   ```shell
   whcli forward --token=abc-123 --api-key=def-456 --target=https://localhost:8080
   ```
   
Where `token` is your Webhook.site URL ID (e.g. if your Webhook.site URL `webhook.site/abc-123`, your token ID is `abc-123`.)

If you are a free Webhook.site user, you do not need the `--api-key` flag.

To read more about Webhook.site CLI, for example how to handle self-signed certificates, [go here](/cli.html).