# API Examples

If you have a Webhook.site account, before using the API, please first [create an API key here](https://webhook.site/api-keys). The examples below can also be used without an account, but in that case you should remove the API key header.

Don't have an account yet? [Sign up here](https://webhook.site/register).

## cURL

### Send JSON data to URL

```bash
curl -X POST 'https://webhook.site/00000000-0000-0000-0000-000000000000' \
  -H 'content-type: application/json' \
  -d $'{"id": 7, "name": "Jack Daniels", "position": "Assistant"}'
```

### Get data of last request sent to URL

```bash
curl 'https://webhook.site/token/00000000-0000-0000-0000-000000000000/request/latest/raw' \
  -H 'accept: application/json' \
  -H 'api-key: 00000000-0000-0000-0000-000000000000'
```

Output:

```json
{"id": 7, "name": "Jack Daniels", "position": "Assistant"}
```

### Send file to URL

Uploads the file `example.png` from the current directory.

```bash
curl -F 'file=@example.png' https://webhook.site/00000000-0000-0000-0000-000000000000
```

To download the file, click the Download link in the Webhook.site interface, or via the API, use the [download endpoint](/api/tokens.html#download-request-file).

## Python

### Fetch latest data

Requires the `requests` module, which can be installed using `pip install requests`. 

Prints the 50 latest requests sent to a given URL to console.

```python
import requests

token_id = "00000000-0000-0000-0000-000000000000"
headers = {"api-key": "00000000-0000-0000-0000-000000000000"}

r = requests.get('https://webhook.site/token/'+ token_id +'/requests?sorting=newest', headers=headers)

for request in r.json()['data']:
	print(request)
```


### Create URL/Email address

Requires the `requests` module, which can be installed using `pip install requests`. 

You'll also need to replace the API key. 

```python
import requests

json = {
  "default_status": 200,
  "default_content": "Hello world!",
  "default_content_type": "text/html",
}

headers = {
    "api-key": "00000000-0000-0000-0000-000000000000"
}

r = requests.post('https://webhook.site/token', json=json, headers=headers)

print('URL Created: https://webhook.site/' + r.json()['uuid'])
```

## PHP

### Create Token (URL/Email address)

Creates a Webhook.site Token and outputs its Web URL. You'll need to replace the API key.

```php
<?php
$apiKey = '00000000-0000-0000-0000-000000000000';

// Create a stream context
$context = stream_context_create(['http' => [
	'method' => 'POST',
	'header' => "Api-Key: $apiKey\r\n"
]]);

// Send API request
$response = json_decode(file_get_contents('https://webhook.site/token', false, $context), true);

echo "URL Created: https://webhook.site/{$response['uuid']}";
```

### Fetch latest data

Simple example of how to loop through the latest requests or emails sent to a Webhook.site URL or email and display in a friendly manner. 

You'll need to replace the API key (if you have a Webhook.site account, otherwise leave it out) and token ID. 

```php
<?php
$apiKey = '00000000-0000-0000-0000-000000000000';
$tokenId = '00000000-0000-0000-0000-000000000000';

$url = "https://webhook.site/token/$tokenId/requests?sorting=newest";

$context = stream_context_create(['http' => ['header' => "Api-Key: $apiKey\r\n"]]);

$response = json_decode(file_get_contents($url, false, $context), true);

foreach ($response['data'] as $req) {
	echo "\n";
	echo json_encode([
		'method' => $req['method'],
		'body' => $req['content'],
		'date' => $req['created_at'],
	], \JSON_PRETTY_PRINT);
}
```

Example output when running the script after running e.g. `curl -X POST https://webhook.site/00000000-0000-0000-0000-000000000000 -d "Hello world"`:

```text
{
    "method": "POST",
    "body": "Hello world",
    "date": "2023-06-08 13:04:33"
}
{
    "method": "POST",
    "body": "just testing",
    "date": "2023-06-08 13:03:57"
}
```

### Download all request data as files

Per default, this script saves the body content of all requests or emails sent to a URL as .json files in the `/requests` directory relative to the script file location.

```php
<?php
$directory = __DIR__ . '/requests';
//$apiKey = '00000000-0000-0000-0000-000000000000';
$tokenId = '00000000-0000-0000-0000-000000000000';

if (!is_dir($directory) || !is_writable($directory)) {
    throw new Exception(sprintf('%s not writable, directory missing or rights issue.', $directory));
}

$context = stream_context_create(['http' =>
    isset($apiKey) ? ['header' => "Api-Key: $apiKey\r\n"] : [],
]);

$page = 1;

do {
    $url = sprintf('https://webhook.site/token/%s/requests?sorting=newest&page=%d', $tokenId, $page);
    $response = json_decode(file_get_contents($url, false, $context), true);

    foreach ($response['data'] as $req) {
        file_put_contents(
            sprintf('/%s/%s.json', $directory, $req['uuid']),
            $req['content']
        );
        echo(sprintf(
            "[Page %3d] Downloaded request %s sent at %s (%d bytes)\n",
            $page, $req['uuid'], $req['created_at'], $req['size']
        ));
    }

    $page++;
    sleep(1);
} while (!$response['is_last_page'] && isset($response['data']));
```

## Node.js

### Fetch latest data

This script outputs the data sent to a Webhook.site URL in the last 2 hours. 

To do this, the script uses the `query` parameter (more info [here](/api/tokens.html#get-requests)) in conjunction with a `created_at` filter.

Before running the script, you should install dependencies by running `npm install axios moment`.

```javascript
import axios from 'axios';
import moment from 'moment';

// Change these!
const apiKey = '00000000-0000-0000-0000-000000000000';
const tokenId = '00000000-0000-0000-0000-000000000000';

async function getData(apiKey, tokenId) {
  let date = moment.utc().subtract(2, 'hours').format('YYYY-MM-DD hh:mm:ss');  
  let dateQuery = `created_at:["${date}" TO "*"]`
  
  try {
    const response = await axios.get(`https://webhook.site/token/${tokenId}/requests`, {
      params: {
        query: dateQuery,
      },
      headers: {
        'Api-Key': apiKey,
        'Accept': 'application/json',
      }
    });
    
    return response.data;
  } catch (error) {
    console.error(error);
  }
}

const requests = await getData(apiKey, tokenId);

console.log(`${requests.total} requests found:`);

for (const request of requests.data) {
  console.log({
    method: request.method, 
    body: request.content,
    date: request.created_at,
  });
}
```
