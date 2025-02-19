---
title: Webhook.site CLI
nav_order: 400
---

# Webhook.site CLI

The Webhook.site Command Line Interface (`whcli`) listens for requests to a Webhook.site URL and forwards/redirects them to your local computer or server.

For example, when a Webhook.site URL is hit, `whcli` will automatically forward the request to the specified URL, which can be on localhost, the local network or any other URL that can be connected to, and can automatically forward the response back to the Webhook.site URL, acting as a proxy.

Under the hood, to listen for requests, `whcli` uses an automatically reconnecting WebSocket that can stay active indefinitely.

Webhook.site CLI is licensed under MIT and [source code is available on Github](https://github.com/webhooksite/cli).

<!-- Place this tag in your head or just before your close body tag. -->
<script async defer src="https://buttons.github.io/buttons.js"></script>
<!-- Place this tag where you want the button to render. -->
<a class="github-button" href="https://github.com/webhooksite/cli" data-color-scheme="no-preference: light; light: light; dark: dark;" data-icon="octicon-star" data-size="large" data-show-count="true" aria-label="Star webhooksite/cli on GitHub">Star</a>

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/KHVPI3-RZgI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

## Installation

### Docker

After installing [Docker](https://docs.docker.com/get-docker/), you can run Webhook.site CLI via `docker run`:

`docker run -ti webhooksite/cli -- whcli help`

### Node.js

[Node](https://nodejs.org/en/download) version 14 or greater required.

To install: `npm install -g @webhooksite/cli`

Then you can run e.g. `whcli help`

## Environment variables

`WH_LOG_LEVEL`: Sets log level (silent, trace, debug, info, warn, error, fatal.) Defaults to info.

`NODE_TLS_REJECT_UNAUTHORIZED`: Set to `"0"` to disable SSL certificate validation (for e.g. self-signed development certificates) when using the `forward` command.

## Variable replacement

For some commands and arguments, runtime variables can be replaced with the standard Webhook.site Custom Actions syntax (e.g. $variable$). Global Variables are not replaced.

The variables that are available are the [default base variables](/custom-actions/variables.html#base-variables) and any variables defined in a Custom Action that was run during the request.

## Commands

### `help`: List commands

Lists commands available to the CLI.

### `forward`: Forward requests

The `forward` commands acts as a bidirectional proxy, listening to incoming traffic to your Webhook.site URL, forwarding it to the `target` URL, and returning the response back to Webhook.site.

| Parameter            | Environment Variable | Description                                                                                                                                                       |
|----------------------|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `--token=`           | `WH_TOKEN`           | Required. The Webhook.site URL ID (also called [token ID](/api/tokens.html#api-endpointstokens-urls-email-addresses))                                                       |
| `--api-key=`         | `WH_API_KEY`         | An [API key](/api/about.html#api-key), required when using a Token that belongs to a Webhook.site account                                                                    |
| `--target=`          | `WH_TARGET`          | Specifies URL where traffic should be forwarded.<br>Default: `https://localhost`                                                                                  |
| `--listen-timeout=` |                      | Amount of seconds to wait for a response from the Target URL to send back as a response for the Webhook.site URL.<br>Set to `0` to disable bidirectional forwarding.<br>Default `5`. Max `10`. |
| `--keep-url`         |                      | When specified, disables URL merging (see below.)                                                                                                                 |

#### Example

```shell
whcli forward \
  --token=1e25c1cb-e4d4-4399-a267-cd2cf1a6c864 \
  --api-key=ef6ef2f8-3e48-4f77-a54c-3891dc11c05c \ 
  --target=https://localhost:8080
```

#### Bidirectional forwarding

Per default, Webhook.site CLI waits for 5 seconds for a response from the target and forwards it to the Webhook.site URL as a response. 

If you have a Web application that uses absolute paths, you should use your Webhook.site URL as a subdomain rather than a path, e.g. `https://1e25c1cb-e4d4-4399-a267-cd2cf1a6c864.webhook.site` rather than `https://webhook.site/1e25c1cb-e4d4-4399-a267-cd2cf1a6c864`.

To disable bidirectional forwarding, add parameter `--listen-timeout=0`.

#### URL merging

The request method, headers and any additional path or query string parameters added to the Webhook.site URL is forwarded on to the target. For example, if the target URL is `https://example.com`, sending a POST request to `https://webhook.site/c33f3c3e-6018-4634-b406-65338edee460/example?query=value`, the target URL will also receive a POST request on `https://example.com/example?query=value`.

To disable this, use the `--keep-url` parameter.

#### Docker and Localhost

When running Webhook.site CLI in Docker, to access the host machine, you can't use `localhost` or `127.0.0.1`. Instead, you must use the special hostname `host.docker.internal`. [More info here](https://stackoverflow.com/a/67781603).

#### Self-signed certificates

If the target uses a self-signed certificate, you could get an error message about this. To allow self-signed certs, run `whcli` with the following environment variable: `NODE_TLS_REJECT_UNAUTHORIZED="0"`

### `exec`: Execute commands

Allows executing terminal commands for new incoming requests sent to your Webhook.site URL. Custom Action variables are replaced in the `--command` argument.

| Parameter            | Environment Variable | Description                                                                                                                                                       |
|----------------------|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `--token=`           | `WH_TOKEN`           | The Webhook.site URL ID (also called [token ID](/api/tokens.html#api-endpointstokens-urls-email-addresses))                                                       |
| `--api-key=`         | `WH_API_KEY`         | An [API key](/api/about.html#api-key), if using a Token that belongs to a Webhook.site account                                                                    |
| `--command=`         | `WH_COMMAND`         | Specifies which command should be run                                                                                    |

#### Example

```shell
whcli exec \
  --token=1e25c1cb-e4d4-4399-a267-cd2cf1a6c864 \
  --api-key=ef6ef2f8-3e48-4f77-a54c-3891dc11c05c \ 
  --command='ping $request.ip$'
```