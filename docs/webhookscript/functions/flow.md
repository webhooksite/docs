## Script Execution

### action(***string*** action_type, ***array*** parameters) : ***array***

Runs Custom Actions in WebhookScript. Can be used to loop over items in a way that not possible using the visual Custom Actions editor.

The function returns an array of runtime variables which can be used to fetch the result of an action that sets a variable, like `google_sheets_get_values`.

The `action_type`s and their parameters [can be seen here](/api/action-types.html).

The following action extracts a list of files from an array of objects in a JSON array and uploads each file to Dropbox using the `dropbox_upload_file` action.

**Example**

In this example, we assume that the request content sent to the Webhook.site URL contains the following:

```json
{
  "files": [
    {
      "url": "https://example.com/path/980e683e-9bd7-4512-bc0e-acfd6e022a81",
      "name": "example_1.png"
    },
    {
      "url": "https://example.com/path/c8e1282f-46a7-45ab-9699-0472ff9ab96c",
      "name": "example_2.png"
    }
  ]
}
```

In the script, the request contents are JSON decoded and looped over. For each item, the file's URL is downloaded and a Dropbox Upload File action is executed.

```javascript
files = json_path(var('request.content'), '.files.*')

for (file_info in files) {
  
  // Download file from URL
  file_download = request(file_info['url'])
  
  // Generate a destination path for the Dropbox file
  destination_path = '/Example Files/%s'.format(file_info['name'])

  // Execute Dropbox Upload File action
  action(
    'dropbox_upload_file',
    [
      'path': destination_path,
      'body': file_download['content'],
      'mode': 'update',
      'provider_id': providerId
    ]
  )
    
}
```

### delay(***int*** seconds, ***string*** code) *[deprecated]*


!!! warning
    This function has been deprecated and should no longer be used. As an alternative, it's recommended that you mark a WebhookScript Custom Action as *Queued*. [More info here](/custom-actions.html#queued-actions).

Executes code in the future. Any output will be stored on the request and will show with a "Was delayed" label. 

The code will not inherit the execution scope.

In this example, the `format` function is used to prepare the code string with a URL, causing `{}` to be replaced with with `https://example.com`.

```javascript
code = '
  request(
      "{}",
      \'{"message": "Hello World!"}\',
      "POST"
  )
'

url = 'https://example.com'

delay(5, code.format(url));
```

The maximum amount of seconds allowed is 604800 (7 days).


### dont_save()

Marks the request so it is not saved in Webhook.site, which is useful when receiving a large amount of requests. The request can still be seen when it comes in, but will not be available through through the app later, or through the API. The action is useful in cases where e.g. a URL receive a large amount of requests.

### exec(***string*** code) : ***any***

Executes code in `code` and returns the result. The code will inherit the execution scope.

### import(***string*** url) : ***any***

Downloads code located at `url` and returns the result. The code will inherit the execution scope. 

As an example, this can be used if you want to re-use code. Just upload it to a server or e.g. Github and use it in different WebhookScript actions.

```javascript
result = import('https://raw.githubusercontent.com/webhooksite/scripts/ec22946a83ea85f607fcc6bff83f9d81ed2fe4ed/hello_world.ws')
echo(result) // value
```

### stop()

Stops Custom Action execution.

## Responses

### respond(***string*** content, ***int*** status, ***array*** headers)

Stops Custom Action execution and return a response immediately.

### set_content(***string*** content)

Sets or overwrites the response content of the URL. Script execution continues.

### set_header(***string*** header_name, ***string*** header_value)

Sets or overwrites a response header of the URL. Script execution continues.

### set_response(***string*** content, ***int*** status, ***array*** headers)

Sets or overwrites response content, status and headers in single function.  Script execution continues.

`headers` should be an array of strings e.g. `["X-Example: Value", "X-Foo: Bar"]`.

### set_status(***number*** status)

Sets or overwrites the HTTP response status of the current URL.  Script execution continues.
