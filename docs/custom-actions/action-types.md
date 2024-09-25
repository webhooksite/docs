## Text

### Extract JSONPath

This action runs a JSONPath query on the contents of a request. With it, you can extract any data from a JSON document and store it in a variable, which can then be used in a downstream action.

JSONPath is very similar to the `jq` commandline utility.

##### JSONPath Examples

Example data:

```json
{
  "store": {
    "name": "Cool Books Ltd",
    "books": [
      {
        "title": "12 Rules for Life",
        "author": "Jordan B. Peterson",
        "author.age": 60,
        "price": 10,
        "isbn": "13123123123"
      },
      {
        "title": "How to Win Friends and Influence People",
        "author": "Dale Carnegie",
        "price": 9,
        "isbn": "23482394"
      }
    ]
  }
}
```

JSONPath                   | Result
---------------------------|-------------------------------------
`.store.name`              | `name` property of `store` object
`.store.books[0]["author.age"]` | author age of first book (bracket syntax can be useful for e.g. keys containing periods)
`$.store.books[*].author`  | the authors of all books in the store
`$..author`                | all authors
`$.store..price`           | the price of everything in the store.
`$..books[2]`              | the third book
`$..books[(@.length-1)]`   | the last book in order.
`$..books[-1:]`            | the last book in order.
`$..books[0,1]`            | the first two books
`$..books[:2]`             | the first two books
`$..books[::2]`            | every second book starting from first one
`$..books[1:6:3]`          | every third book starting from 1 till 6
`$..books[?(@.isbn)]`      | filter all books with isbn number property
`$..books[?(@.isbn != '')]` | filter all books with isbn that isn't null or `""` (empty string.) (Bracket syntax can also be used here, e.g. `.values[?(@['my value'] != '')]`)
`$..books[?(@.price<10)]`  | filter all books cheaper than 10
`$..*`                     | all elements in the data (recursively extracted)


##### JSONPath Syntax

Symbol                | Description
----------------------|-------------------------
`$`                   | The root object/element (not strictly necessary)
`@`                   | The current object/element
`.` or `[]`           | Child operator
`..`                  | Recursive descent
`*`                   | Wildcard. All child elements regardless their index.
`[,]`                 | Array indices as a set
`[start:end:step]`    | Array slice operator borrowed from ES4/Python.
`?()`                 | Filters a result set by a script expression
`()`                  | Uses the result of a "script" expression as the index


For more details on what's possible with JSONPath, [take a look at the docs](https://github.com/FlowCommunications/JSONPath#jsonpath-examples).

As you start entering a JSONPath, the results are validated and shown next to the input field.

### Auto JSON

This action automatically converts JSON data to Webhook.site Variables, and can be used as an alternative for Extract JSONPath when there's a large amount of variables that need to be extracted.

<figure markdown="span">
  ![Auto JSON in action](/images/custom-actions.png){ width="300" }
  <figcaption>Auto JSON in action</figcaption>
</figure>

Per default, the action works on the JSON found in the `$request.content$` variable, e.g. the request body data. 

If the JSONPath parameter is specified, this can be used to limit the variable creation to only the subset of data specified by the JSONPath query.

##### Auto JSON Example

If the following data is specified in the Source parameter:

```json
{
  "Actors": [
    {
      "name": "Tom Cruise",
      "age": 56,
      "Born At": "Syracuse, NY",
      "Birthdate": "July 3, 1962",
      "photo": "https://jsonformatter.org/img/tom-cruise.jpg"
    },
    {
      "name": "Robert Downey Jr.",
      "age": 53,
      "Born At": "New York City, NY",
      "Birthdate": "April 4, 1965",
      "photo": "https://jsonformatter.org/img/Robert-Downey-Jr.jpg"
    }
  ]
}
```

If the JSONPath parameter is empty, the following 10 variables will be created:

| Variable Name               | Value                                              |
|-----------------------------|----------------------------------------------------|
| `$json.Actors.0.name$ `     | Tom Cruise                                         |
| `$json.Actors.0.age$ `      | 56                                                 |
| `$json.Actors.0.Born At$ `  | Syracuse, NY                                       |
| `$json.Actors.0.Birthdate$` | July 3, 1962                                       |
| `$json.Actors.0.photo$ `    | https://example.com/tom-cruise.jpg                 |
| `$json.Actors.1.name$ `     | Robert Downey Jr.                                  |
| `$json.Actors.1.age$ `      | 53                                                 |
| `$json.Actors.1.Born At$ `  | New York City, NY                                  |
| `$json.Actors.1.Birthdate$` | April 4, 1965                                      |
| `$json.Actors.1.photo$ `    | https://example.com/Robert-Downey-Jr.jpg           |

If the JSONPath parameter is set to `.Actors.0`, only the following 5 variables are created:

| Variable Name               | Value                                              |
|-----------------------------|----------------------------------------------------|
| `$json.0.name$ `            | Tom Cruise                                         |
| `$json.0.age$ `             | 56                                                 |
| `$json.0.Born At$ `         | Syracuse, NY                                       |
| `$json.0.Birthdate$`        | July 3, 1962                                       |
| `$json.0.photo$ `           | https://example.com/tom-cruise.jpg                 |

### Extract Regex

This action runs a Regex (regular expression) query on the contents of a request. With it, you can extract any data from a text document and store it in a variable, which can then be used in a downstream action.

As you start entering a Regex, the results are validated and shown next to the input field.

### Extract XPath

Similar to the Extract JSONPath Custom Action, Extract XPath lets you extract values from an XML or HTML document and save the result as a variable.

##### XPath Examples

The following examples are based on this XML document:

```xml
<?xml version="1.0"?>
<organization name="ExampleCo">
  <employees>
    <employee id="1">Jack</employee>
    <employee id="2">Ann</employee>
  </employees>
</organization>
```

Example XPath                                     | Notes                                                       | Result
--------------------------------------------------|-------------------------------------------------------------|----------------
`/organization`                                   | Finds all content within the organization element           | Jack<br>Ann
`//employee[@id != 1]`                            | `//` traverses all `<employee>` elements in document, the @id query selects all except those with `id`=1 | Jack
`/organization/@name`                             | `@name` to get the "name" property of the element           | ExampleCo
`/organization/employees/employee[2]`             | `[2]` specifies 2nd element                                 | Ann
`/organization/employees/employee[2]/@id`         | Get the "id" property of second employee element            | 2
`/organization/employees/employee[@id=1]`         | Employee element with id property equal to "1"              | Jack
`/organization/employees/employee[last()]`        | Last employee element                                       | Ann
`//employee[contains(@id, "2")]`                  | Employee within any parent element where id contains "2"    | Ann

For more examples, see [W3CSchools](https://www.w3schools.com/xml/xml_xpath.asp) or [XPath Cheatsheet](https://devhints.io/xpath)

### Replace Text

An action that allows replacing multiple inputs to a string with specified replacements. Additionally, Webhook.site will replace all variables in the source text as well as the text being replaced, and the replacement.

### Split Text

Split text into multiple variables. Using `hello,world` as Source, and `,` as Delimiter, 2 variables will be created: `$variable.1$` is "hello" and `$variable.2$` is "world".

Entering `\n` as Delimiter will split text by each line.

The maximum amount of variables created is 1024.

### Map Text

Sets a variable depending on what maps to the source value and operator.

If we set Source to `John`, Operator to `ends with`, Variable Name to `$user_id$`, Default to `unknown`, and add a mapping of From: `John` -> To: `123`, then the variable name `$user_id$` would be set to `123`. 

If the Source had been `Jack`, `$user_id$` would have been set to `unknown.`

## Network

### HTTP Request

This will send a HTTP/HTTPS request from the Webhook.site cloud. 

The HTTP Request action has several modes:

* **Text**: In the default text mode, this allows sending plain-text content, but also data like JSON and XML.
* **JSON**: Similar to the Text mode, but also sets the Content-Type header to application/json and allows JSON formatting.
* **Multipart**: With Multipart selected, it is possble to build a form/multipart request and send form data and files. Note that the Filename and Content-Type fields are not required.
* **URL Encoded**: In URL Encoded mode, the keys and values are sent using URL Encoding.
* **Forward**: In forward mode, all data sent to the Webhook.site URL is forwarded here, including the HTTP method, query strings, headers and body data. It is possible to overwrite the method and append headers. To forward the HTTP method, set the Method dropdown to the blank option.

The response of the request is stored in a series of variable names prefixed with a value of your choosing. The following variables are set after the request has been fired:

* `$your_prefix.content$` - response body content
* `$your_prefix.status$` - response status code
* `$your_prefix.headers$` - response headers
* `$your_prefix.url$` - the URL the request was sent to
* `$your_prefix.error$` - if the request resulted in an error, it's stored in this variable.

#### Retry

When checked, this option will cause the HTTP to be retried in case of a network error, timeout, or related issue.

<figure markdown="span">
  ![Retry configuration screenshot](/images/http-retry.png){ width="300" }
  <figcaption>Retry configuration screenshot</figcaption>
</figure>

Per default, there are 3 retries (4 requests total) with 1 second delay between each retry.

!!! note
    As Webhook.site URLs have a maximum of 30 seconds to respond, it's best to use a low delay and retry number that stays under 30 seconds total. Otherwise there's a risk the actions won't complete. Alternatively, you can mark the HTTP Request action as [Queued](/custom-actions.html#queued-actions), which has a timeout of 120 seconds.

If a status code is specified, the request will also be retried when the response status doesn't match the specified status code. The character `*` can be used as wildcard, e.g. `20*` will match any status code in the range 200-209.

Each retry attempt will add an extra line of output.

### Send Email

This will send a email with variable contents from the Webhook.site cloud. Variables extracted previously can be used.

### Send Email (SMTP)

This will send a email with variable contents from your own email provider. Variables extracted previously can be used.

#### Gmail and Google Workspace

For Gmail, the following specific setup is required:

* Hostname: `smtp.gmail.com`
* Port:`587`
* Username: youraccount@gmail.com or youraccount@example.com (replace with your Gmail address)
* Password: You must [create a Mail App Password](https://myaccount.google.com/u/1/apppasswords)
* Encryption: `TLS`

### Run SSH Command

Allows you to run one or more SSH command on a server. Webhook.site captures the output (stdout), stderr and the command exit code as Variables that can be used in downstream actions:

* `$ssh.stdout$`
* `$ssh.stderr$`
* `$ssh.exit$`

We recommend authenticating using a pre-generated keypair, which can be created under Control Panel -> Providers.

### SFTP Upload

Allows uploading a file to a SFTP (SSH) server, specifying a hostname, port, username, password, relative path to the file. The file content can be specified, in which Variables are replaced.

We recommend authenticating using a pre-generated keypair, which can be created under Control Panel -> Providers.

### SFTP Download

Allows downloading a file to a SFTP (SSH) server, specifying a hostname, port, username, password and the path to the file. The file content is downloaded to a Variable.

We recommend authenticating using a pre-generated keypair, which can be created under Control Panel -> Providers.

### FTP(S) Upload

Allows uploading a file to a FTP or FTPS (FTP with TLS/SSL) server, specifying a hostname, port, username, password, relative path to the file, whether to use SSL and whether to use passive mode. Finally, the file content can be specified, in which Variables are replaced.

We recommend storing the password as a Global Variable.

### FTP(S) Download

Allows downloading a file to a FTP or FTPS (FTP with TLS/SSL) server, specifying a hostname, port, username, password, path, whether to use SSL and whether to use passive mode. The file content is downloaded to a Variable.

We recommend storing the password as a Global Variable.

### Database Query

Allows running a database query, with support for fetching out data in a series of variables. We recommend storing the password as a Global Variable. The query timeout is 10 seconds.

#### Supported Database Servers

Currently supported are:

* PostgreSQL
* MySQL/MariaDB
* Microsoft SQL Server

If your database server is not on the list, please [contact support](https://support.webhook.site).

#### Using Parameters

When using e.g. INSERT or UPDATE statements, you should use *parameters* for each column value. Doing this, you avoid SQL injection attacks and other issues when using user-submitted data (e.g. via Variables), or even just data containing special characters like quotes, that could otherwise break a query.

Each parameter name should start with a colon (:) and be a single word. You can then reference these parameters inside the query, like in the following example:

![](/images/database.png)

#### Fetching data

When fetching data using e.g. SELECT statements, Webhook.site automatically inserts data in a series of Custom Action Variables, which are then available to downstream actions.

For example, when fetching rows from the following table:

![](/images/database-example-table.png)

Using the following statement:

```SQL
select * from employees
```

If the variable name prefix would be set to `output`, the following variables would be created containing specific values:

| Variable Name       | Value                          |
|---------------------|--------------------------------|
| $output.0.id$       | 1                              |
| $output.0.fname$    | Simon                          |
| $output.0.lname$    | Fredsted                       |
| $output.0.title$    | Founder                        |
| $output.1.id$       | 2                              |
| $output.1.fname$    | Jack                           |
| $output.1.lname$    | Daniels                        |
| $output.1.title$    | Assistant                      |

A variable would be created with the name `$output.json$` containing the data in JSON format:

```json
[                              
  {
    "id": 1,
    "fname": "Simon",
    "lname": "Fredsted",
    "title": "Founder"
  },
  {
    "id": 2,
    "fname": "Jack",
    "lname": "Daniels",
    "title": "Assistant"
  }
]
```

A variable named `$output.rows$` - containing the number of affected rows - would be set to `2`.

If the action encounters an error, the `$output.error$` variable is set to the error message. You can use this to check that the action was successful in conjunction with the Conditions action, specifically the *variable exists* operator.

#### Postgres Endpoint ID

If your database host requires an endpoint ID to be specified, you can do so via the Password field, for example: `endpoint=my_endpoint;password`. Replace `my_endpoint` with the endpoint ID, and `password` with the actual password.

## Behavior

### Don't Save

Marks the request so it is not saved in Webhook.site, which is useful (especially in combination with Conditions) when receiving a large amount of requests.

### Log

Adds a custom log entry to the Request's action output.

### Modify Response

This action can be used to modify the response of the Webhook.site URL based on the input.

### Rate Limit

This action can be used to allow a specific amount of requests in a specific amount of time per a given IP.

If the IP is rate limited, the URL will respond with a `HTTP 429`, action execution is stopped, and the request is not saved in Webhook.site.

### Stop

Immediately stops Custom Action execution and returns the default response.

### Basic Auth

With this action, the URL is protected with Basic Authentication. If the username and password combination is wrong, the request is automatically marked as *Don't Save*, action execution is stopped, and the response status is HTTP 401. The action has no effect for emails or DNSHooks.

Basic Auth works with the Authorization HTTP header, where the username and password is encoded in base64, separated by a colon (`:`). For example, a successfull request when the username is `user` and password is `pass123` would have the following header:

```
Authorization: Basic dXNlcjpwYXNzMTIz
```

<figure markdown="span">
  ![Basic Auth in browsers](/images/basic-auth.png){ width="300" }
  <figcaption>Basic Auth in browsers</figcaption>
</figure>

When the URL is visited with a Web browser, a username and password form will be shown.

## Logic

### Conditions

!["Condition" Custom Action screenshot](/images/condition-action.png)

Useful if you need to validate that the request does or does not conform to certain criteria, the Condition action will either stop or continue based on a condition.

In both the *input* and the *value* fields, variables will be replaced (including Global Variables from the Control Panel), so you can compare e.g. JSONPath or Regex values - or even values from a previous HTTP request that was sent. 

Currently, three *actions* are provided: use result, stop and continue. *Use Result* allows using the Condition result in further actions. *Stop* will stop further action execution of the condition is a match. *Continue* will *only* continue further execution if the condition is a match, and otherwise stop.

To make an *is equal to* condition on a boolean value from a JSON structure, you can enter `0` for `false` or `1` for `true`. 

#### Operators with value argument

* is equal to
* is not equal to
* starts with
* ends with
* contains
* does not contain
* is greater than
* is greater than or equal to
* is less than
* is less than or equal to

#### Operators without value argument

* variable exists - whether a Webhook.site variable is defined
* is numeric - whether input is numeric; examples include `42`, `123.45`, `0x539`, `02471`,
    `0b10100111001`
* is integer - whether input is an integer; `42` is; `123.45` is not. 
* is float - whether input is a valid float/double (e.g. both `42` and `123.45` are valid)
* is json - whether input is valid JSON
* is email
* is domain - e.g. `webhook.site`
* is URL - e.g. `https://webhook.site?value=xxx`

The "result" of the condition will be logged below the request details, so you can see what happened.

To use the result of the Condition, select it in the "only run when condition passes" checkbox:

![](/images/EQeP6s783LK1y5hnj6u7ObvO.png)

Tip: To check if a Variable is set (or exists), you must enter the variable name in both input and value fields and use the "is not equal to" operator, since non-existing variables are not replaced.

### JavaScript

With the JavaScript action, you can execute JavaScript code using a Node.js sandbox that runs on the Webhook.site cloud.

![](/images/javascript.png)

#### General Functions

<code>console.log(*line*)</code> / <code>echo(*line*)</code> - log a string to Action output

<code>set(*variable_name*, *value*)</code> - sets a Webhook.site variable for use in downstream actions

The following code would set the variable $myvar$ to `value`:

``` javascript
set('myvar', 'value')
```

<code>get(*variable_name*)</code> - gets a Webhook.site variable (except Global Variables; use the `global()` function for that)

<code>variables</code> - global array variable containing Webhook.site variables

<code>global(*variable_name*)</code> - retrieves the value of a Webhook.site Global Variable. Must be used async. Returns `null` if variable doesn't exist.

```javascript
echo(await global('my-variable'))
```

<code>store(*variable_name*, *value*)</code> - stores the value of a Webhook.site Global Variable. Must be used async.

<code>stop()</code> - stops action execution and return response

<code>dont_save()</code> - marks current requests as [*Don't Save*](#dont-save), so it won't be stored or shown in the Webhook.site requests list

<code>respond(*content*, *status*, *headers*)</code> - stops action execution and return response

``` javascript
respond('OK', 200, ['Content-Type: text/plain'])
```

<code>set_response(*content*, *status*, *headers*)</code> - sets response, but doesn't stop action execution

#### Utility Modules

Code executed with the Webhook.site JavaScript action runs in a sandbox where the following utility libraries are available by using the `require()` function:

* [`axios`](https://www.npmjs.com/package/axios) - HTTP Client
   ``` javascript
   axios = require('axios')
   await axios.get('https://webhook.site')
      .then(response => {
        console.log(response.status)
      });
   // 200
   ```
* [`lodash`](https://www.npmjs.com/package/lodash) - General utility library
  ``` javascript
  _ = require('lodash')
  console.log(_.last([1, 2, 3]))
  // 3
  ```
* [`dayjs`](https://www.npmjs.com/package/dayjs) - Date and time manipulation
   ``` javascript
   dayjs = require('dayjs')
   console.log(dayjs(1318781876406))
   // "2011-10-16T16:17:56.406Z"
   ```
* [`cheerio`](https://www.npmjs.com/package/cheerio) - JQuery-like HTML selector library
   ``` javascript
   cheerio = require('cheerio')
   const $ = cheerio.load('<ul id="fruits">banana</ul>');
   console.log($('#fruits').text());
   // banana
   ```
* [`jsonpath`](https://www.npmjs.com/package/jsonpath) - JSONPath query library
   ``` javascript
   jsonpath = require('jsonpath')
   var cities = [
     { name: "London", "population": 8615246 },
     { name: "Berlin", "population": 3517424 },
   ];

   var names = jsonpath.query(cities, '$..name');

   console.log(names)
   // ["London","Berlin"]
   ```
* `crypto` – Node.js built-in crypto library
   ```javascript
   crypto = require('crypto');

   const secret = 'abcdefg';
   const hash = crypto.createHmac('sha256', secret)
                  .update('I love Webhook.site')
                  .digest('hex');
               
   console.log(hash);
   // 1745c764246c2782ebf97e25b89547a92571f19d41846b42880d3815480f098e
   ```
* [`faker`](https://www.npmjs.com/package/@faker-js/faker) - Seed data generator
   ```javascript
   faker = require('faker')

   console.log(faker.internet.email())
   // Ila_Gutkowski9@yahoo.com
   ```
* [`nats`](https://www.npmjs.com/package/nats) - NATS Client
   ```javascript
   const nats = require('nats')
   const nc =  nats.connect({ servers: ["demo.nats.io:4442", "demo.nats.io:4222"] });
   ```
* [`supabase`](https://www.npmjs.com/package/@supabase/supabase-js) - Supabase Client
   ```javascript
   const createClient = require('supabase')
   const supabase = createClient('https://xyzcompany.supabase.co', 'public-anon-key')
   ```
* [`moment`](https://momentjs.com/docs) - Date and Time library
   ```javascript
   const moment = require('moment')
   const startOfLastWeek = moment().subtract(1, 'weeks').startOf('isoWeek').startOf('day').format();
   console.log(startOfLastWeek)
   // 2024-09-16T00:00:00+02:00
   ```
   
Do you need a library that isn't listed here? Please <a href="https://support.webhook.site">contact support</a>!

### WebhookScript

!["WebhookScript" Custom Action screenshot](/images/webhookscript-in-action.png)

Executes custom scripts using a scripting language that's very similar to JavaScript and PHP.

For more information about WebhookScript, see the [dedicated page](/webhookscript/index.html).

### Set Variable

Defines (or overwrites) a variable that's available to downstream actions. The variable is not saved permanently as a Global Variable.

There are three modes:

* **Text**: Using the default "Text" mode, the variable is simply set to what's entered in the Text field.
* **Random**: When using the "Random" mode, you can generate a random string for e.g. one-time identifiers and passwords.
* **Date**: Generate date strings specifying a custom input date and an output format - defaults to ISO-8601 format.

<figure markdown="span">
  ![Set Variable Date Mode example](/images/set-variable-date.png){ width="400" }
  <figcaption>Using the Set Variable action in the Date mode to create a date string 30 days in the past</figcaption>
</figure>

### Store Global Variable

Saves (or overwrites) a Global Variable that's saved permanently and available to all URLs in your account. If you don't need to save the variable permanently, you should use the *Set Runtime Variable* instead.

## Multimedia

### Generate PDF

Takes either HTML or markdown input and generates a variable (`$pdf$`) containing the PDF file contents. You can enter this variable in e.g. an Send Email attachment content field, or with the Modify Response action (remember adding a `Content-Type: application/pdf` content type header!)

### Resize Image

Takes an image from either a URL or raw image data from e.g. a file upload, email attachment, request response or another action such as Dropbox.

You can enter both width and height to contrain the image in both dimensions, or enter a single dimension.

Check "Keep Aspect Ratio" so that the image keeps the aspect ratio, but doesn't exceed the height and width constraints.

## Google Sheets

!!! note
    Google Sheets should not be used as a database, and have low usage limits. If you need to import on the order of thousands
    of rows or make thousands of calls a day, Google Sheets cannot be used. We recommend using a database like Postgres in conjunction with the *Database Query* action.

Google Sheets Custom Actions lets you manipulate and retrieve values from a Google Sheet.

The following Google Sheets Custom Actions are available:

* Add Row - appends one or more new rows to an existing spreadsheet
* Update Row - updates one or more cells in an existing spreadsheet
* Get Values - retrieves one or more cell values from an existing spreadsheet

To start, you need to make sure that you have connected a Google account in the Control Panel, [available here](https://webhook.site/providers).

After that, you can select the account in the dropdown when creating the Custom Action.

### Usage Limits

It is important to note that Google will block Write requests (i.e. adding or updating rows) at **60 requests per minute**. After that, the action will temporarily fail with the following error message:

```
Quota exceeded for quota metric 'Write requests' and limit 'Write requests per minute per user' of service 'sheets.googleapis.com' for consumer
```

Therefore, for importing mass amounts of data in a short timespan, Google Sheets is not recommended. Instead, we recommend using the Database Query action.

Additionally, Webhook.site will automatically disable Google Sheets actions that continously fail due to e.g. quota errors.

### Specifying the spreadsheet

When specifying the spreadsheet, you can either just copy/paste the spreadsheet URL or enter the spreadsheet ID. Variables can be used to specify the spreadsheet.

### Ranges

All actions must specify a range, which behaves similar in all actions. For the Add Row action, Google Sheets will automatically find a "table" (e.g. a homogenous mass of data) and add the values at the bottom. 

A range is the same query as in Google Sheets, e.g. to select A1-C3 in Worksheet "Example", enter `'Example'!A1:C3`.

### Values

When inserting or updating values, you can either enter a value in the text field, or supply multiple cells and/or rows using JSON. To insert two rows, the JSON would be `["cell 1", "cell 2"]`.

### Variables

The Get Values Action allows you to define variables based on the output. Since this action can return multiple pieces of data, multiple variables are created.

For example, if you select two columns and two rows, e.g. `A1:B2`, four variables would be defined:

1. `variable_name.0.0` = value of A1
1. `variable_name.0.1` = value of A2
1. `variable_name.1.0` = value of B1
1. `variable_name.1.1` = value of B2

Additionally, the data is available in JSON, with the `variable_name.json` variable being defined, and continuing with the example above, would contain the following JSON:

```json
[
  ["A1","A2"],
  ["B1","B2"]
]
```

## Microsoft

### OneDrive

With Webhook.site, you can now use your Microsoft account to upload and download files in your OneDrive account using the Upload and Download Custom Actions.

### Excel

Using the Add Rows and Get Values actions, Webhook.site now allows using your Microsoft account to append and retrieve data from Excel worksheets in your OneDrive account.

#### Add Rows

To use the Add Rows function, the Microsoft API requires that data is inserted into a Table. Therefore, before starting, make sure you have a Table in your workbook, and enter the correct Table name.

<figure markdown="span">
  ![Finding Table name in Excel](/images/excel-table.png){ width="300" }
  <figcaption>Finding Table name in Excel</figcaption>
</figure>

To create a table, select a range and click Insert -> Table.

<figure markdown="span">
  ![Creating a Table in Excel](/images/excel-create-table.png){ width="300" }
  <figcaption>Creating a Table in Excel</figcaption>
</figure>

#### Error: You do not have permissions to open this file in the browser

This error seems to have started happening around Feburary 2024 for some users. All 3rd parties - including Webhook.site - that connect to Microsoft's API are affected. There is no known solution at the moment. We encourage users experiencing this to contact Microsoft Support.

## Amazon Web Services (AWS)

### S3

The following actions are available for AWS S3:

* Create Bucket
* Create Object
* Delete Object
* Get Object (retrieves object contents to a Variable)

In addition to the "official" Amazon endpoints, Webhook.site also supports S3-compatible storages like Google Cloud Storage, DigitalOcean, MinIO, Wasabi and more. The endpoint can be specified when setting up the account in Control Panel.

#### Using with Google Cloud Storage

To use the S3 action with a Google Cloud Storage bucket, do the following:

1. Go to Google Cloud Console &rarr; Cloud Storage &rarr; Settings &rarr; [Interoperability](https://console.cloud.google.com/storage/settings;tab=interoperability)
3. Create keys for either an existing or a new Google Service Account
4. Copy *Access key* in *AWS IAM Key*
5. Copy *Secret* in *AWS IAM Secret*
6. Enter `https://storage.googleapis.com` in *Custom Endpoint*

<figure markdown="span">
  ![Using S3 with Google Cloud Storage credentials](/images/google-cloud-storage-setup.png){ width="300" }
  <figcaption>Using S3 with Google Cloud Storage credentials</figcaption>
</figure>

When creating the S3 action, you can leave the *Region* field blank.

### CloudFront

The "Create Invalidation" action allows you to dynamically create a CloudFront cache invalidation as a Custom Action. Both the Distribution ID and the paths to be invalidated are replaced with Webhook.site Variables.

## Discord

With the Discord Custom Action, you can send messages to a specified channel (Each bot account uses a specific channel, so you can connect more accounts to send to different channels or servers.) In addition, you can choose a custom username and avatar image for the bot user.

!["Discord" Custom Action screenshot](/images/discord.png)


## Slack

With the Slack Custom Action, you can easily use Slack's Webhook URLs to send messages to a channel.

## Dropbox

The Dropbox integration has access to the entire contents of your dropbox, and currently the following actions are available:

* Create Folder
* Download File
* Upload File
* Delete File
* Delete Folder
* Get Link - creates a temporary download link for any file in your Dropbox, and saves it in a variable.

## HubSpot

With the HubSpot application, you can create Contacts in our HubSpot CRM system. (This action is new, and we're still exploring possibilities - if you want more capabilities for the HubSpot action, please [let us know](https://support.webhook.site)!)

!["HubSpot" Custom Action screenshot](/images/hubspot_action.png)


## X (formerly known as Twitter)

The X Integration supports the following actions using X's API:

* Post Tweet

## RabbitMQ

The RabbitMQ Integration allows you to publish and consume messages from a RabbitMQ queue by specifying the server connection details.

## Pushed

With the Send Push Notification action, you can easily send push notifications to your mobile devices using your Pushed.co account.

!["Pushed" Custom Action screenshot](/images/pushed.png)

With a [free Pushed.co account](https://pushed.co/pricing), you can send up to 1000 push notifications a month.

## ntfy.sh

Allows you to easily send push notifications to your browser, phone, watch, etc. Simply download the ntfy.sh app, subscribe to your topic name and send a message to the topic name via this Custom Action. No account required.

App download links: 

* <a href="https://apps.apple.com/us/app/ntfy/id1625396347" target="_blank">App Store</a> 
* <a href="https://play.google.com/store/apps/details?id=io.heckel.ntfy" target="_blank">Google Play</a>
* [Browser](https://ntfy.sh/app)
