---
title: Webhook.site CLI
nav_order: 400
---

# Webhook.site CLI

The Webhook.site Command Line Interface listens for requests to a Webhook.site URL and forwards/redirects them to your local computer or server.

<!-- Place this tag in your head or just before your close body tag. -->
<script async defer src="https://buttons.github.io/buttons.js"></script>
<!-- Place this tag where you want the button to render. -->
<a class="github-button" href="https://github.com/webhooksite/cli" data-color-scheme="no-preference: light; light: light; dark: dark;" data-icon="octicon-star" data-size="large" data-show-count="true" aria-label="Star webhooksite/cli on GitHub">Star</a>

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/XL_QdBFKt7w" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

## Installation

### Docker

After installing [Docker](https://docs.docker.com/get-docker/), you can run Webhook.site CLI via `docker run`:

`docker run -ti webhooksite/cli -- whcli help`

### Node.js

[Node](https://nodejs.org/en/download) version 14 or greater required.

To install: `npm install -g @webhooksite/cli`

Then you can run e.g. `whcli help`

## Environment variables

Some command arguments can be specified via environment variables:

        --token         WH_TOKEN
        --api-key       WH_API_KEY
        --target        WH_TARGET
        --command       WH_COMMAND

General environment variables:

`WH_LOG_LEVEL` Sets log level (silent, trace, debug, info, warn, error, fatal.) Defaults to info.

## Variable replacement

For some commands and arguments, runtime variables can be replaced with the standard Webhook.site Custom Actions syntax (e.g. $variable$). Global Variables are not replaced.

The variables that are available are the [default base variables](/custom-actions/variables.html#base-variables) and any variables defined in a Custom Action that was run during the request.

## Commands

### `help`: List commands

Lists commands available to the CLI.

### `forward`: Forward requests

The `forward` command listens for new incoming requests sent to your Webhook.site URL and immediately relays them to any URL you specify, or simply `localhost` (so it can be used as an ngrok alternative). This URL can be any URL that the machine running Webhook.site CLI can access.

* The token ID (`--token`) parameter must specify the Webhook.site URL ID (also called token ID). The token ID is the long 36-character ID at the end of your Webhook.site URL.
* An API key (`--api-key`) must also be specified when the token belongs to a Webhook.site account, and can be generated from the Webhook.site [Control Panel](https://webhook.site/control-panel).
* Finally, the target (`--target`) specifies where traffic should be redirected (defaults to `https://localhost`)

#### Example

```shell
whcli forward \
  --token=1e25c1cb-e4d4-4399-a267-cd2cf1a6c864 \
  --api-key=ef6ef2f8-3e48-4f77-a54c-3891dc11c05c \ 
  --target=https://example.com
```

Custom Action variables are replaced in the `--target` argument.

The request method, headers and any additional path or query string parameters added to the Webhook.site URL is forwarded on to the target. For example, if the target URL is `https://example.com`, sending a POST request to `https://webhook.site/c33f3c3e-6018-4634-b406-65338edee460/example?query=value`, the target URL will also receive a POST request on `https://example.com/example?query=value`.

#### Docker and Localhost

When running Webhook.site CLI in Docker, to access the host machine, you can't use `localhost` or 127.0.0.1. Instead, use the special hostname `host.docker.internal`. [More info here](https://stackoverflow.com/a/67781603).

#### Self-signed certificates

If the target uses a self-signed certificate, you could get an error message about this. To allow self-signed certs, run `whcli` with the following environment variable and value:

```bash
NODE_TLS_REJECT_UNAUTHORIZED="0"
```

### `exec`: Execute commands

Allows executing terminal commands for new incoming requests sent to your Webhook.site URL. Custom Action variables are replaced in the `--command` argument.

#### Example

```shell
whcli exec \
  --token=1e25c1cb-e4d4-4399-a267-cd2cf1a6c864 \
  --api-key=ef6ef2f8-3e48-4f77-a54c-3891dc11c05c \ 
  --command='ping $request.ip$'
```