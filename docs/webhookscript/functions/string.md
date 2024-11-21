## General string functions

### string_contains(***string*** subject, ***number/string/regex*** value) : bool

Returns boolean if ***subject*** contains ***value***

### string_find_first(***string*** subject, ***number/string*** value) : number

Returns position of ***value*** in ***subject***, or false if not found

### string_find_last(***string*** subject, ***number/string*** value) : number

Returns position of ***value*** in ***subject***, or false if not found

### string_format(***string*** formatString, ...***any*** items) : string

Sprintf-like formatting of formatString with ***items***, see PHP sprintf docs.

### string_length(***string*** string) : number

Returns length of string (multibyte-aware)

### string_lower(***string*** string) : string

Converts `string` to lowercase (multibyte-aware)

### string_number_of(***string*** string) : number

Returns number value of ***string***

### string_random(***number*** length) : string

Returns a random string of *length* using the  `A–Z,a–z,0–9` alphabet.

### string_replace(***string*** subject, ***string/regex/array*** search, ***string*** replace) : string

Replaces string ***search*** with ***replace*** found in ***subject***.

```javascript
string_replace('this is a sentence', 'sentence', 'string') // -> this is a string

string_replace('this is great', r'(.*) is (.*)', '$1 was $2') // -> this was great
```

### string_replace(***string*** subject, ***array*** replace_pairs) : string

Replaces items found in ***subject*** using the ***replace_pairs*** array:

```javascript
string_replace("hello, it's good", [
    'hello': 'hi',
    'good': 'great'
]) // -> hi, it's great
```

### string_reverse(***string*** subject) : string

Reverses string ***subject*** 

### string_slice(***string*** subject, ***number*** from, ***number*** to = null) : string

Extracts a segment of a string. Multibyte-aware.

`string_slice('hello world', 0, 5)` returns `hello`.

`string_slice('hello world', 6)` returns `world`.

### string_shuffle(***string*** string) : string

Returns string where the individual characters has been shuffled.

### string_split(***string*** subject, ***string/regex*** delimiter) : array

Returns array of split string ***subject*** with ***delimiter*** 

### string_title(***string*** string) : string

Returns `string` converted to *title case*.

`string_title('hello world')` returns `Hello World`.

### string_upper(***string*** string) : string

Converts `string` to UPPERCASE (multibyte-aware).

### to_regex(***string*** regex) : regex

Converts a regex string to a regex type

### to_string(***string/number/bool*** value) : string

Returns ***value*** as string 

### trim(***string*** string): string

Returns `string` with space, tab and newline characters removed from the beginning and end of the string.

### uuid() : string

Returns a random v4 UUID.

## CSV

### csv_to_array(***string*** content, ***string*** delimiter, ***?int*** header_offset, ***string*** enclosure, ***string*** escape) : array

Takes a CSV string and outputs to an array, with each row being an item in the array.

* `content` should be a string containing the CSV document.
* `delimiter` will explicitly set the CSV delimiter the parser will attempt to use (e.g. `;`). Must be a single character. Defaults to `,` (comma.)
* `header_offset`, when specified, causes the output array item's keys to be set to the header values. Setting to `0` will mark the first row as the header row. 
* `enclosure` sets the field enclosure character. Must be a single character. Defaults to `"` (double quote.)
* `escape` sets the field escape character. Must be a single character. Defaults to `\` (backslash.)

```javascript
csv_content = 'firstname,lastname,title
"M. J.",Plumley,"Sr. Developer"
Emily,"Jenna Platt","Chief Information Officer"'

array = csv_to_array(csv_content, ',', 0)

echo(json_encode(array))

// [
//     {
//         "firstname": "John",
//         "lastname": "Doe",
//         "title": "Sr. Developer"
//     },
//     {
//         "firstname": "Emily",
//         "lastname": "Jenna Platt",
//         "title": "Chief Information Officer"
//     }
// ]
```

## Base64

### base64_decode(***string*** string) : string

Returns a base64-decoded string.

### base64_urldecode(***string*** string) : string

Returns a base64url-decoded string.

If the base64 string was encoded using URL-friendly `base64url` format, this function should be used rather the regular `base64_decode` function.

### base64_encode(***string*** string) : string

Returns base64-encoded string.

### base64_urlencode(***string*** string) : string

Returns a URL-friendly base64url-encoded string, where characters `+`, `/` have been replaced by `-` and `_`, and any `=` padding characters have been removed.

## Hashing

### hash(***string/number*** value, ***string*** algo) : string

Returns a hashed version of `value` using the `algo` algorithm.

```javscript
'hello world'.hash('md5')  // 5eb63bbbe01eeed093cb22bb8f5acdc3
```
<br>

The following built-in algorithms are available: `md2`, `md4`, `md5`, `sha1`, `sha224`, `sha256`, `sha384`, `sha512/224`, `sha512/256`, `sha512`, `sha3-224`, `sha3-256`, `sha3-384`, `sha3-512`, `ripemd128`, `ripemd160`, `ripemd256`, `ripemd320`, `whirlpool`, `tiger128,3`, `tiger160,3`, `tiger192,3`, `tiger128,4`, `tiger160,4`, `tiger192,4`, `snefru`, `snefru256`, `gost`, `gost-crypto`, `adler32`, `crc32`, `crc32b`, `fnv132`, `fnv1a32`, `fnv164`, `fnv1a64`, `joaat`, `haval128,3`, `haval160,3`, `haval192,3`, `haval224,3`, `haval256,3`, `haval128,4`, `haval160,4`, `haval192,4`, `haval224,4`, `haval256,4`, `haval128,5`, `haval160,5`, `haval192,5`, `haval224,5`, `haval256,5`.

### hmac(***string*** value, ***string*** algo, ***string*** secret) : string

Returns the calculated message digest/hash in a hexadecimal formatted as a string.

For a list of possible values for `algo`, see `hash()` above.

See also [binary and hexadecimal conversion functions](/webhookscript/functions/math.html#hexadecimal-binary).

In the following example, the hash needs to be converted to binary, and then to base64, to match the signature.

```javascript

hmac = hmac(var('request.content'), 'sha256', 'insert_secret_here');
signature = var('request.header.x-signature', '');
hash = base64_encode(hex2bin(hmac))

if (hash != signature) {
    respond('Unauthorized', 401);
}
```

## Cryptography

List of available algorithms for functions in the Cryptography section:

* `blake2b512`
* `blake2s256`
* `md4`
* `md5`
* `md5-sha1`
* `ripemd160`
* `sha1`
* `sha224`
* `sha256`
* `sha3-224`
* `sha3-256`
* `sha3-384`
* `sha3-512`
* `sha384`
* `sha512`
* `sha512-224`
* `sha512-256`
* `shake128`
* `shake256`
* `sm3`
* `whirlpool`

### sign(***string*** value, ***string*** private_key, ***string*** algo) : false/string

Signs `value` using `private_key` and `algo`. Returns signature on success, `false` on failure.

For an example using sign() for JWT authorization, [see here](/webhookscript/examples.html#jwt).


### digest(***string*** value, ***string*** algo) : false/string

Returns a cryptographic digest of `value` using `algo`. Returns `false` on failure.

### verify(***string*** value, ***string*** signature, ***string*** public_key, ***string*** algo) : true/false

Verifies `value` using `signature`, `public_key` and `algo`

## HTML and Markdown

### html_strip_tags(***string*** string) : string

Returns a string with all HTML tags removed.

`html_strip_tags('<b>test</b>')` returns `test`.

### html_to_text(***string*** string) : string

Converts HTML to plaintext. A more aggressive version of `html_strip_tags`.

`html_to_text('<b>test</b>')` returns `test`.

### html_decode(***string*** string) : string

Decodes all HTML entities (for example, `&nbsp;`) to normal characters.

### html_encode(***string*** string) : string

Replaces characters in a string with HTML encoded versions.

### markdown_to_html(***string*** string, ***bool*** safe_mode = false) : string

Converts a Markdown string to HTML.

`markdown_to_html('# Hello world')` returns `<h1>Hello world</h1>`.

If `safe_mode` is set to true, characters like `<`, `>` are HTML-entity encoded.

## JSON

### json_decode(***string*** json) : array

Decodes `json` and returns an array.

```javascript
array = json_decode(var('request.content'))
```

### json_encode(***array*** array, ***bool*** format = true) : string

Takes an array and encodes it as a JSON string.

Per default, the JSON array is formatted with whitespace. To turn it off, set `format` to false.

### json_path(***string*** json, ***string*** jsonpath, ***bool*** return_first = true) : string

Returns the result of a `json` string parsed using the [JSONPath](/custom-actions/action-types.html#extract-jsonpath) functionality.

Per default, if there's just one match (e.g. if matching on a property value that's a string), this value is returned. To always return an array, set `return_first` to false. 

```javascript
dump(json_path('{"v": []}', 'v[*]', false))
dump(json_path('{"v": []}', 'v[*]'))
// []
// ""
 
dump(json_path('{"v": ["item1"]}', 'v[*]', false))
dump(json_path('{"v": ["item1"]}', 'v[*]'))
// [0: "item1"]
// "item1"
 
dump(json_path('{"v": ["item1", "item2"]}', 'v[*]', false))
dump(json_path('{"v": ["item1", "item2"]}', 'v[*]'))
// [0: "item1", 1: "item2"]
// [0: "item1", 1: "item2"]
```

### json_escape(***string*** json) : string

JSON-escapes all special JSON characters like double quotes, newlines, etc.

## Regex

### preg_match(***string*** regex, ***string*** subject) : array/false

Returns the matching values as an array, or `false` if the regex did not match. Supports regex [pattern modifiers](https://www.php.net/manual/en/reference.pcre.pattern.modifiers.php).

```javascript
// Returns anything enclosed within <html> tags in a string
html = preg_match('/<html>(.*)<\\/html>/s', content)
```

### regex_extract(***regex*** regex, ***string*** subject) : array/false

Returns the matching string and all match groups as an array, and `false` on failure.

```javascript
input = "You're a good bot"

output = regex_extract(r"You're (\w) (.*)", input)

dump(output) // [0: "You're a good bot", 1: "a", 2: "good bot"]
```

### regex_extract_first(***regex*** regex, ***string*** subject, ***any*** default) : string/false

Returns the first match group of a regex, and `false` (or `default`, if set) on failure.

```javascript
input = "You're a good bot"
output = regex_extract(r"You're (.*)", input)
dump(output) // "a good bot"

input = "Hello world"
output = regex_extract(r"You're (.*)", input, 'no value')
dump(output) // "no value"
```

### regex_match(***regex*** regex, ***string*** subject) : string/false

Returns the first matching string, otherwise false.

```javascript
input = "You're a good bot"

output = regex_match(r"You're .*", input)

dump(output) // "You're a good bot"
```

### regex_to_string(***regex*** regex) : string

Returns the regex converted to a string

## XML

### xml2array(***string*** xml) : array

Converts XML to a WebhookScript array. This can be useful for parsing XML, or e.g. converting XML to JSON.

Note that this function is opinionated - there's no one way to convert XML to an array as XML has more features than WebhookScript arrays. Therefore the function attempts to carry over all the data by automatically generating properties like `@value` and `@attributes` depending on the input data.

For example, the following XML:

```xml
<orders>
  <record>
    <Name type="full">John Doe</Name>
    <Reference>49690</Reference>
  </record>
  <record>
    <Name type="username">someone@example.com</Name>
    <Reference>49690</Reference>
  </record>
</orders>
```

Converts to JSON via the following script:

```javascript
json_encode(xml2array(var('request.content')))
```

Which returns:

```json
{
  "orders": {
    "record": [
      {
        "Name": {
          "@value": "John Doe",
          "@attributes": {
            "type": "full"
          }
        },
        "Reference": 49690
      },
      {
        "Name": {
          "@value": "someone@example.com",
          "@attributes": {
            "type": "username"
          }
        },
        "Reference": 49690
      }
    ]
  }
}
```

### xpath(***string*** xpath, ***string*** input): string/null

Returns the first result of an XPath query on XML document `input`.

Given a request with the following content:

```xml
<?xml version="1.0"?>
<organization name="ExampleCo">
  <employees>
    <employee id="1">Jack</employee>
    <employee id="2">Ann</employee>
  </employees>
</organization>
```

* `xpath(var('$request.content$'), '//employee[1]') // returns "Jack"`

[More information and examples regarding XPath](/custom-actions/action-types.html#extract-xpath).

### xpath_all(***string*** xpath, ***string*** input): string/null

Returns the results of an XPath query on XML document `input` as an array.

Given a request with the following content:

```xml
<?xml version="1.0"?>
<organization name="ExampleCo">
  <employees>
    <employee id="1">Jack</employee>
    <employee id="2">Ann</employee>
  </employees>
</organization>
```

* `xpath_all(var('$request.content$'), '//employee]') // returns [0: "Jack", 1: "Ann"]`

[More information and examples regarding XPath](/custom-actions/action-types.html#extract-xpath).

## Special string functions

### convert_kana(***string***, ***mode***) : string

Performs a "han-kaku" - "zen-kaku" conversion for string string. This function is only useful for Japanese. [See here](https://www.php.net/manual/en/function.mb-convert-kana.php) for more info.
