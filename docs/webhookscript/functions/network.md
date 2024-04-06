## HTTP

### query(***array*** form_values) : string

Converts an associative array into a form-style string, used for e.g. `application/x-www-form-urlencoded` requests or HTTP query strings.

```javascript
query(['country': 'Curaçao', 'population': 158665]) 
// country=Cura%C3%A7ao&population=158665
```

### http(***string*** url, ***array*** options) : array

Sends a HTTP request and returns an array with the following keys containing response data:

* `content` (contains a cURL error message in case of an error)
* `status` (`null` in case of an error)
* `headers`
* `url`

#### Options array

The `options` array can contain the following keys; none are required.

* `mode` - string, one of: text (default), multipart, urlencoded, forward
* `content` - string, body content, used when mode is text
* `method` - string, HTTP method, e.g. POST
* `multipart` - array of arrays, used when mode is multipart, containing keys:
    * `name` - required, string, form item name
    * `filename` - string
    * `content-type` - string
    * `content` - string
* `urlencoded` - array of arrays, used when mode is urlencoded, containing keys:
    * `name` - required, string, form item name
    * `value` - string
* `headers` - array of strings, HTTP headers
* `skip_ssl_verification` - default false, skips TLS/SSL certificiate validation for HTTPS requests
* `timeout` - number, default 5, timeout in seconds

#### POST Request

To send a simple POST request containing e.g. JSON data, use the following:

```javascript
http(
    'https://example.com',
    [
        'method': 'POST', 
        'content': '{"example": "json"}', 
        'headers': ['Content-Type: application/json']
    ]
)
```

#### form/multipart request

```javascript
http(
    'https://example.com', 
    [
        'method': 'POST',
        'mode': 'multipart', 
        'multipart': [
            [
                'name': 'value1',
                'content': 'This is a value',
            ]
        ]
    ]
)
```

### request(***string*** url, ***string*** body, ***string*** method = 'GET', ***array*** headers, ***bool*** override = false, timeout = 5) : array

Sends a HTTP request and returns an array with the following keys containing response data:

* `content` (contains a cURL error message in case of an error)
* `status` (`null` in case of an error)
* `headers`
* `url`

The headers should be an array of strings, for example:

```javascript
[
  'Content-Type: application/json',
  'Accept: application/json, text/plain, */*'
]
```

To get a JSON document, validate if valid JSON, and get a property:

```javascript
response = request('https://example.com')

decoded = json_decode(response['content'])
if (decoded) {
  value = decoded['value']
}
```

If `override` is set to true, none of the content from the original request is included (e.g. query strings, headers, content.)

### multipart(***string*** url, ***array*** items, ***string*** method = 'POST', ***array*** headers, ***num*** timeout) : ***array***

Sends a HTTP Multipart request, e.g. for uploading files.

`name` (the form name value) and `content` are required in the `items` array; the rest is optional.

`timeout` specifies the request timeout in seconds.

The return value is an array with the following keys containing response data:

* `content` (contains a cURL error message in case of an error)
* `status` (`null` in case of an error)
* `headers`
* `url`

Example:

```javascript
multipart(
  'https://example.com/file-upload', [
    [
      'name': 'file[]',
      'filename': 'file1.txt',
      'content': 'hello world',
      'headers': ['Header1': 'value', 'Header2': 'othervalue']
    ],
    [
      'name': 'client_id',
      'content': 'abcd123',
    ]
  ],
  'POST',
  ['Api-Key: xxxx']
)
```

### url_decode(***string*** value) : string

Returns an URL-decoded version of *value*.

### url_encode(***string*** value) : string

Returns an URL-encoded version of *value*.

```javascript
url_encode('here\'s a value') // here%27s+a+value
```
