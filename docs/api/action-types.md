The following is a list of the API names for Action Types, along with a list of parameters, and their validation requirements.

## Text

### `auto_json` – Extract JSON

Given the source {"value": "example"}, jsonpath set to a blank string or $, and the variable_name 'output', the following variable will be generated: $output.0.value$ which will equal 'example'. There will always be an index in the variable name!

- `source`: string
- `jsonpath`: string
- `variable_name`: string
- `repeat`: boolean

### `extract_regex` – Extract Regex

- `regex`: **required**, string
- `variable_name`: **required**, string
- `source`: string
- `default`: string
- `repeat`: boolean

### `extract_xpath` – Extract XPath

- `xpath`: **required**, string
- `variable_name`: string
- `source`: string
- `default`: string

### `text_decrypt` – Decrypt Text

- `source`: **required**, string
- `password`: **required**, string
- `variable_name`: string

### `text_encrypt` – Encrypt Text

- `source`: **required**, string
- `password`: **required**, string
- `variable_name`: string

### `text_map` – Map/Translate Text

Acts as a translator, e.g. if X is Y then set variable to A, a comparison on a string. variable_name is the result variable. If there is no match, the default value is set to the variable_name variable.

- `source`: string
- `operator`: **required**, string, in:eq,neq,sw,ew,ct,nct,gt,gte,lt,lte
- `variable_name`: string
- `default`: **required**, string
- `mappings`: **required**, array
- `mappings.*.from`: **required**_with:mappings, string
- `mappings.*.to`: **required**_with:mappings, string

### `text_replace` – Replace Text

- `source`: **required**, string
- `variable_name`: **required**, string
- `replacements`: **required**, array

### `text_split` – Split Text

- `delimiter`: min:1, string
- `source`: **required**, string
- `variable_name`: string
- `repeat`: boolean

### `validate_json` – Validate JSON

- `source`: string
- `schema`: string
- `variable_name`: string

## Network

### `database` – Database Query

- `variable_name`: string, default:db
- `repeat`: boolean, default:false
- `type`: **required**, in:mysql,pgsql,sqlsrv,whdb
- `db_id`: **required**_if:type,whdb, string
- `host`: **required**_unless:type,whdb, string
- `port`: integer, min:1, max:65535
- `database`: **required**_unless:type,whdb, string
- `password`: **required**_unless:type,whdb, string
- `username`: **required**_unless:type,whdb, string
- `statement`: **required**, string
- `params`: array
- `charset`: string

### `ftp_download` – FTP(S) Download

- `host`: **required**, string
- `port`: int, min:1, max:65535
- `password`: **required**, string
- `username`: **required**, string
- `path`: **required**, string
- `ssl`: bool
- `passive`: bool
- `variable_name`: string

### `ftp_upload` – FTP(S) Upload

- `host`: **required**, string
- `port`: int, min:1, max:65535
- `password`: **required**, string
- `username`: **required**, string
- `path`: **required**, string
- `content`: **required**, string
- `ssl`: bool
- `passive`: bool

### `http` – HTTP Request

Sends a HTTP request and generates variables $http.content$, $http.status$, $http.header.[header_name]$, $http.error$

- `url`: **required**, string
- `content`: nullable, string
- `method`: nullable, in:POST,GET,OPTIONS,PUT,DELETE,PATCH,TRACE
- `mode`: nullable, in:text,json,multipart,urlencoded,forward
- `auth`: nullable, array
- `auth.mode`: nullable, string, in:basic,digest,ntlm,bearer
- `auth.username`: string
- `auth.password`: string
- `multipart`: array, **required**_if:mode,multipart
- `multipart.*.name`: string
- `multipart.*.filename`: string
- `multipart.*.content-type`: string
- `multipart.*.content`: string
- `urlencoded`: array
- `urlencoded.*.name`: string, **required**_if:mode,urlencoded
- `urlencoded.*.value`: string, **required**_if:mode,urlencoded
- `headers`: nullable, string
- `skip_ssl_verification`: nullable, bool
- `variable_name`: string
- `timeout`: nullable, numeric, max:60
- `retry`: array
- `retry.enabled`: nullable, bool
- `retry.retries`: nullable, numeric, min:1, max:10
- `retry.delay`: nullable, numeric, min:0, max:10
- `retry.require_status`: nullable, string

### `send_email` – Send Email

- `sender`: string
- `recipient`: **required**, string
- `content`: string
- `is_html`: boolean
- `subject`: **required**, string
- `attachments`: array

### `send_email_smtp` – Send Email (SMTP)

- `sender_name`: string
- `sender_email`: string
- `recipient`: **required**, string
- `content`: string
- `is_html`: boolean
- `subject`: **required**, string
- `encryption`: string, in:none,ssl,tls
- `port`: int
- `username`: string, **required**
- `password`: string, **required**
- `host`: string, **required**
- `attachments`: array

### `sftp_download` – SFTP Download

- `provider_id`: string
- `host`: **required**, string
- `port`: int, min:1, max:65535
- `username`: **required**, string
- `password`: string
- `path`: **required**, string
- `variable_name`: string

### `sftp_upload` – SFTP Upload

- `provider_id`: string
- `host`: **required**, string
- `port`: int, min:1, max:65535
- `username`: **required**, string
- `password`: string
- `path`: **required**, string
- `content`: **required**, string

### `ssh_run_command` – Run SSH Command

- `provider_id`: string
- `host`: **required**, string
- `port`: int, min:1, max:65535
- `username`: **required**, string
- `password`: string
- `command`: **required**, string
- `variable_name`: string

## Behavior

### `auth_basic` – Basic Auth

- `username`: string
- `password`: **required**, string

### `dont_save` – Don't Save

*No parameters for `dont_save`.*

### `log` – Log

Adds a log message for the user to see. If mode is markdown, it is presented as markdown for the user

- `text`: **required**, string
- `mode`: nullable, string, in:text,markdown
- `error`: boolean

### `modify_response` – Modify Response

Sets the response content of the Webhook.site URL

- `content`: string
- `status`: string
- `headers`: string
- `stop`: bool

### `rate_limit` – Rate Limit

- `period`: **required**, int
- `count`: **required**, int
- `key`: string

### `sleep` – Sleep

- `delay`: **required**

### `stop` – Stop

*No parameters for `stop`.*

### `template` – Include Template

- `template_id`: **required**, int
- `variables`: array

## Mock

### `mock` – Mock OpenAPI/Swagger

- `source`: **required**, string
- `path`: string
- `method`: string
- `status`: string
- `content_type`: string

## Logic

### `conditions` – Conditions

- `conditions`: **required**, array
- `mode`: **required**, string, in:one,all,none
- `action`: **required**, string, in:stop,continue,noop

### `set_variable` – Set Variable

- `name`: string
- `value`: nullable, string
- `mode`: nullable, in:text,random,date,math
- `random`: array
- `random.length`: int, max:10000, **required**_if:mode,random
- `random.characters`: array, in:lowercase,uppercase,digits,symbols,user
- `random.alphabet`: string
- `random_number`: array
- `random_number.from`: int
- `random_number.to`: int
- `date`: array
- `date.input`: string
- `date.timezone`: string
- `date.format`: string, in:iso8601,mysql,unix,unixmicro,user
- `date.user_format`: string

### `store_global_variable` – Store Global Variable

- `name`: **required**, string
- `value`: nullable, string

## Scripting

### `javascript` – JavaScript

Runs JavaScript script in Node.js sandbox. Can interact with Variables using e.g. get('request.content') or set('varname', value). Global Variables retrieved using global('varname') and store('varname', value). The following libraries can be included via require(): axios, lodash, dayjs, cheerio, jsonpath, crypto, faker, nats, supabase, moment, form-data, fetch

- `script`: **required**, string

### `script` – WebhookScript

- `script`: **required**, string

## Multimedia

### `image_resize` – Resize Image

- `source`: string, **required**
- `width`: string, **required**_without:height
- `height`: string, **required**_without:width
- `aspect_ratio`: bool, **required**
- `variable_name`: string

### `pdf_generate` – Generate PDF

- `content`: string
- `mode`: string, in:html,markdown
- `paper`: string, in:a4,letter
- `orientation`: string, in:portrait,landscape
- `variable_name`: string

## Webhook.site

### `webhook_get_requests` – Get Requests

- `variable_name`: string, default:req
- `repeat`: boolean
- `token_id`: **required**, string
- `sorting`: string
- `query`: string
- `max`: int, default:100

## Google Sheets

### `google_sheets_add_row` – Add Row

- `provider_id`: string, **required**
- `spreadsheet_id`: string, **required**
- `range`: string, **required**
- `values`: string, **required**
- `formula_mode`: bool

### `google_sheets_get_values` – Get Values

- `provider_id`: string, **required**
- `spreadsheet_id`: string, **required**
- `range`: string, **required**
- `variable_name`: **required**, string

### `google_sheets_update_row` – Update Row

- `provider_id`: string, **required**
- `spreadsheet_id`: string, **required**
- `range`: string, **required**
- `values`: string, **required**
- `formula_mode`: bool

## Microsoft Excel

### `microsoft_excel_add_rows` – Add Rows

- `provider_id`: **required**, string
- `path`: string
- `table`: string
- `index`: int
- `values`: **required**, array

### `microsoft_excel_get_values` – Get Values

- `provider_id`: **required**, string
- `path`: **required**, string
- `worksheet`: **required**, string
- `range`: **required**, string
- `variable_name`: **required**, string

## Microsoft OneDrive

### `microsoft_drive_download` – Download File

- `provider_id`: **required**, string
- `path`: **required**, string
- `variable_name`: **required**, string

### `microsoft_drive_upload` – Upload File

- `provider_id`: **required**, string
- `path`: **required**, string
- `content_type`: string
- `content`: string
- `variable_name`: string

## AWS S3 & Compatible

### `aws_s3_create_bucket` – Create Bucket

- `provider_id`: string, **required**
- `region`: string, **required**
- `bucket_name`: string, **required**
- `canned_acl`: string, in:private,public-read,public-read-write,authenticated-read

### `aws_s3_delete_object` – Delete Object

- `provider_id`: string, **required**
- `region`: string
- `bucket_name`: string, **required**
- `object_key`: string, **required**

### `aws_s3_get_object` – Get Object

- `provider_id`: string, **required**
- `region`: string
- `bucket_name`: string, **required**
- `object_key`: string, **required**
- `variable_name`: string, **required**, min:1

### `aws_s3_put_object` – Create Object

- `provider_id`: string, **required**
- `region`: string
- `bucket_name`: string
- `object_key`: string, **required**
- `body`: string, **required**
- `canned_acl`: string, in:private,public-read,public-read-write,authenticated-read

## AWS CloudFront

### `aws_cf_invalidate` – Create Invalidation

- `provider_id`: **required**, int
- `distribution_id`: **required**, string
- `paths`: **required**, string

## Discord

### `discord_send_message` – Send Message

- `provider_id`: **required**, string
- `content`: **required**, string
- `username`: string
- `avatar_url`: url
- `embed_type`: string, in:link,image,video
- `embed_url`: url

## Slack

### `slack_send_message` – Send Message

- `webhook_url`: **required**, url
- `raw`: bool
- `content`: **required**, string

## Dropbox

### `dropbox_create_folder` – Create Folder

- `provider_id`: string, **required**
- `path`: string, **required**

### `dropbox_delete` – Delete

- `provider_id`: string, **required**
- `path`: string, **required**

### `dropbox_download_file` – Download

- `provider_id`: string, **required**
- `path`: string, **required**
- `variable_name`: string, **required**

### `dropbox_get_link` – Get Link

- `provider_id`: string, **required**
- `path`: string, **required**
- `variable_name`: string
- `type`: string, in:share_link,temporary
- `share_audience`: string, in:public,team,no_one

### `dropbox_upload_file` – Upload

- `provider_id`: string, **required**
- `path`: string, **required**
- `body`: string, **required**
- `mode`: string, **required**, in:add,overwrite,update

## HubSpot

### `hubspot_create_contact` – Create Contact

- `provider_id`: **required**, string
- `properties`: **required**, array

## X/Twitter

### `twitter_tweet` – Post Tweet

- `provider_id`: **required**, string
- `tweet`: **required**, string

## Pushed

### `pushed_send` – Send Push Notification

- `app_key`: string, **required**
- `app_secret`: string, **required**
- `target_type`: string, **required**
- `target`: string, **required**
- `message`: string, **required**

## ntfy.sh

### `ntfy` – Send Push Notification

- `topic`: string, **required**
- `title`: string
- `icon`: string
- `link`: string
- `message`: string, **required**

## RabbitMQ

### `rabbitmq_get` – Get Message

- `host`: string, **required**
- `port`: int
- `username`: string, **required**
- `password`: string, **required**
- `vhost`: string
- `queue`: string, **required**
- `ssl`: boolean
- `variable_name`: string

### `rabbitmq_publish` – Publish Message

- `host`: string, **required**
- `port`: int
- `username`: string, **required**
- `password`: string, **required**
- `vhost`: string
- `queue`: string, **required**
- `ssl`: boolean
- `message`: string, **required**
- `properties`: array

