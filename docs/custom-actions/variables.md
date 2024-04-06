---
title: Variables
nav_order: 200
parent: Custom Actions
---

Variables are the most important part of Custom Actions, and are characterized by a name surrounded by two dollar signs: `$example$`. Variables can be used in any field that has a ⓥ icon in the editor. They act as placeholders that are replaced by dynamic content as the request or email is received.

Each request or email has a set of Base Variables (see below) that contain information like the request IP, method, headers, query string values, form values and the request content. To see a list of variables, click the Variables button in the editor. Clicking on a variable copies it to the clipboard.

![Variables Menu](/images/variables.png)

Many of the the available Custom Actions can register a variable during the runtime of the actions, so for example you can register the result of a JSONPath query and use it in a "Modify Response" action to make the response dynamic, or even use it to send a request to another HTTP address, and then use the response of that. Files can referred to and be used through Variables.

This works since Custom Actions are executed synchronously in a chain, sharing data as they're being executed.

The format of variables are dollar signs surrounded by a word, for example: `$example$`.

### Variable Modifiers

Adding specific suffixes to variable names will let you process the value in the following ways:

| Variable                | Example Input                          | Example Output                         | Description                                                                                                                           |
|-------------------------|----------------------------------------|----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| $example$               | `{"json": "value"}`                    | `{"json": "value"}`                    | *no modifier*                                                                                                                         |
| $example.json$          | `{"json": "value"}`                    | `{\"json\": \"value\"}`                | Escapes all special JSON characters, allowing to use any string in a JSON object. Escaped characters include \b, \f, \n, \r, \t, ", \ |
| $example.html_encode$   | `<p>some html</p>`                     | `&lt;p&gt;some html&lt;/p&gt;`         | Escapes all special HTML characters                                                                                                   |
| $example.html_decode$   | `&lt;p&gt;some html&lt;/p&gt;`         | `<p>some html</p>`                     | Replaces all escaped HTML escapes with normal characters                                                                              |
| $example.html_strip$    | `<p>some html</p>`                     | `some html`                            | Removes all HTML tags from input string                                                                                               |
| $example.base64_encode$ | `{"json": "<b>value</b>"}`             | `eyJqc29uIjogIjxiPnZhbHVlPC9iPiJ9Cg==` | Encodes the variable to base64                                                                                                        |
| $example.base64_decode$ | `eyJqc29uIjogIjxiPnZhbHVlPC9iPiJ9Cg==` | `{"json": "<b>value</b>"}`             | Decodes a base64 encoded string                                                                                                       |
| $example.url_encode$    | `{"json": "value"}`                    | `%7B%22json%22%3A+%22value%22%7D`      | Escapes all special HTTP URL characters                                                                                               |
| $example.url_decode$    | `%7B%22json%22%3A+%22value%22%7D`      | `{"json": "value"}`                    | Replaces all special HTTP URL escapes with normal characters                                                                          |

### Base Variables

These variables are automatically available for each request or email. Different variables are available depending on the type.

| Variable Name                     | Available For | Description                                                                                            |
|------------------------------- ---|---------------|--------------------------------------------------------------------------------------------------------|
| request.uuid                      | All           | The UUID of the request                                                                                |
| request.token_id                  | All           | The Token UUID (URL ID) of the request                                                                 |
| request.content                   | All           | The body content of the request                                                                        |
| request.date                      | All           | Creation date in Y-m-d H:m:s format                                                                    |
| request.date                      | All           | Creation date in UNIX timestamp format                                                                 |
| request.hostname                  | All           | Hostname of the request (usually `webhook.site`)                                                       |
| request.header.[name]             | All           | Created for each HTTP header                                                                           |
| request.size                      | All           | Request body size in bytes                                                                             |
| request.type                      | All           | Request type (`email` or `web`)                                                                        |
| request.file.[name].filename      | All           | Created for each file upload, with `name` being the input name property. Contains the client file name |
| request.file.[name].size          | All           | Contains the file size in bytes                                                                        |
| request.file.[name].content       | All           | Contains the file content                                                                              |
| request.file.[name].content_type  | All           | Contains the file content type (e.g. image/png)                                                        |
| request.file.[name].id            | All           | Contains the Webhook.site file ID                                                                      |
| request.file.[name].link          | All           | Contains the [direct download link to](/api/tokens.html#download-request-file) the file from Webhook.site's server. |
| request.query.[name]              | Web           | Created for each query string (e.g. ?name=value)                                                       |
| request.form.[name]               | Web           | Created for each form field                                                                            |
| request.ip                        | Web           | IP of the host making the request                                                                      |
| request.user_agent                | Web           | User agent header                                                                                      |
| request.url                       | Web           | Full URL of the request (e.g. https://webhook.site/xxx-xxx...)                                         |
| request.path                      | Web           | Sub-path of URL, after the token ID. Defaults to `/`                                                   |
| request.query                     | Web           | Full query string of the URL                                                                           |
| request.method                    | Web           | HTTP method (GET, POST, etc.)                                                                          |
| request.sender                    | Email         | Sender address                                                                                         |
| request.message_id                | Email         | Email message ID                                                                                       |
| request.text_content              | Email         | Parsed plaintext content                                                                               |
| request.destinations              | Email         | Comma separated list of recipients.                                                                    |
| request.checks.[name]             | Email         | True or false for email checks (DKIM, SPF, etc.)                                                       |
