The following is a list of the API names for Action Types, along with a list of parameters, and their validation requirements.



### `auto_json`
- `source`: string
- `jsonpath`: string
- `variable_name`: **required**, string

### `aws_cf_invalidate`
- `provider_id`: **required**, int
- `distribution_id`: **required**, string
- `paths`: **required**, string

### `aws_s3_create_bucket`
- `provider_id`: string, **required**
- `region`: string, **required**
- `bucket_name`: string, **required**
- `canned_acl`: string, in:private,public-read,public-read-write,authenticated-read

### `aws_s3_delete_object`
- `provider_id`: string, **required**
- `region`: string
- `bucket_name`: string, **required**
- `object_key`: string, **required**

### `aws_s3_get_object`
- `provider_id`: string, **required**
- `region`: string
- `bucket_name`: string, **required**
- `object_key`: string, **required**
- `variable_name`: string, **required**, min:1

### `aws_s3_put_object`
- `provider_id`: string, **required**
- `region`: string, **required**
- `bucket_name`: string
- `object_key`: string, **required**
- `body`: string, **required**
- `canned_acl`: string, in:private,public-read,public-read-write,authenticated-read

### `condition`
- `input`: string
- `operator`: **required**, string, in:eq,neq,sw,ew,ct,nct,gt,gte,lt,lte
- `value`: string
- `action`: **required**, string, in:stop,continue,noop

### `conditions`
- `conditions`: **required**, array
- `mode`: **required**, string, in:one,all,none
- `action`: **required**, string, in:stop,continue,noop

### `database`
- `type`: **required**, in:mysql,pgsql
- `host`: **required**, string
- `port`: number, min:1, max:65535
- `database`: **required**, string
- `password`: string
- `username`: **required**, string
- `statement`: **required**, string
- `params`: array
- `variable_name`: string
- `charset`: string

### `discord_send_message`
- `provider_id`: **required**, string
- `content`: **required**, string
- `username`: string
- `avatar_url`: url
- `embed_type`: string, in:link,image,video
- `embed_url`: url

### `dont_save`
*No parameters for `dont_save`.*

### `dropbox_create_folder`
- `provider_id`: string, **required**
- `path`: string, **required**

### `dropbox_delete`
- `provider_id`: string, **required**
- `path`: string, **required**

### `dropbox_download_file`
- `provider_id`: string, **required**
- `path`: string, **required**
- `variable_name`: string, **required**

### `dropbox_get_link`
- `provider_id`: string, **required**
- `path`: string, **required**
- `variable_name`: string, **required**

### `dropbox_upload_file`
- `provider_id`: string, **required**
- `path`: string, **required**
- `body`: string, **required**
- `mode`: string, **required**, in:add,overwrite,update

### `extract_jsonpath`
- `jsonpath`: **required**, string
- `variable_name`: **required**, string
- `source`: string
- `default`: string
- `repeat`: boolean

### `extract_regex`
- `regex`: **required**, string
- `variable_name`: **required**, string
- `source`: string
- `default`: string
- `repeat`: boolean

### `extract_xpath`
- `xpath`: **required**, string
- `variable_name`: **required**, string
- `source`: string
- `default`: string

### `ftp_upload`
- `host`: **required**, string
- `port`: number, min:1, max:65535
- `password`: **required**, string
- `username`: **required**, string
- `path`: **required**, string
- `content`: **required**, string
- `ssl`: bool
- `passive`: bool

### `google_sheets_add_row`
- `provider_id`: string, **required**
- `spreadsheet_id`: string, **required**
- `range`: string, **required**
- `values`: string, **required**
- `formula_mode`: bool

### `google_sheets_get_values`
- `provider_id`: string, **required**
- `spreadsheet_id`: string, **required**
- `range`: string, **required**
- `variable_name`: **required**, string

### `google_sheets_update_row`
- `provider_id`: string, **required**
- `spreadsheet_id`: string, **required**
- `range`: string, **required**
- `values`: string, **required**
- `formula_mode`: bool

### `http`
- `url`: **required**, string
- `content`: nullable, string
- `method`: nullable, in:POST,GET,OPTIONS,PUT,DELETE,PATCH,TRACE
- `mode`: nullable, in:text,json,multipart,urlencoded,forward
- `auth`: nullable, object
- `auth.mode`: string, in:basic,digest,ntlm
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
- `timeout`: nullable, numeric, max:15

### `image_resize`
- `source`: string, **required**
- `width`: string, **required**_without:height
- `height`: string, **required**_without:width
- `aspect_ratio`: bool, **required**
- `variable_name`: string, **required**

### `javascript`
- `script`: **required**, string

### `log`
- `text`: **required**, string

### `microsoft_drive_download`
- `provider_id`: **required**, string
- `path`: **required**, string
- `variable_name`: string

### `microsoft_drive_upload`
- `provider_id`: **required**, string
- `path`: **required**, string
- `content_type`: string
- `content`: string
- `variable_name`: string

### `microsoft_excel_add_rows`
- `provider_id`: **required**, string
- `path`: string
- `table`: string
- `index`: int
- `values`: **required**, array

### `microsoft_excel_get_values`
- `provider_id`: **required**, string
- `path`: **required**, string
- `worksheet`: **required**, string
- `range`: **required**, string
- `variable_name`: **required**, string

### `modify_response`
- `content`: string
- `status`: string
- `headers`: string
- `stop`: bool

### `ntfy`
- `topic`: string, **required**
- `title`: string
- `message`: string, **required**

### `pushed_send`
- `app_key`: string, **required**
- `app_secret`: string, **required**
- `target_type`: string, **required**
- `target`: string, **required**
- `message`: string, **required**

### `rabbitmq_get`
- `host`: string, **required**
- `port`: int
- `username`: string, **required**
- `password`: string, **required**
- `vhost`: string
- `queue`: string, **required**
- `ssl`: boolean
- `variable_name`: string

### `rabbitmq_publish`
- `host`: string, **required**
- `port`: int
- `username`: string, **required**
- `password`: string, **required**
- `vhost`: string
- `queue`: string, **required**
- `ssl`: boolean
- `message`: string, **required**

### `rate_limit`
- `period`: **required**, int
- `count`: **required**, int
- `key`: string

### `script`
- `script`: **required**, string

### `send_email`
- `sender`: string
- `recipient`: **required**, string
- `content`: string
- `is_html`: boolean
- `subject`: **required**, string
- `attachments`: array

### `send_email_smtp`
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
- `host`: string_**required**
- `attachments`: array

### `send_request`
- `url`: **required**, string
- `content`: nullable, string
- `method`: nullable, in:POST,GET,OPTIONS,PUT,DELETE
- `headers`: nullable, string
- `skip_ssl_verification`: nullable, bool
- `variable_name`: string
- `timeout`: nullable, numeric, max:30

### `set_variable`
- `name`: **required**, string
- `value`: nullable, string

### `sftp_upload`
- `provider_id`: string
- `host`: **required**, string
- `port`: number, min:1, max:65535
- `username`: **required**, string
- `password`: string
- `path`: **required**, string
- `content`: **required**, string

### `slack_send_message`
- `webhook_url`: **required**, url
- `raw`: bool
- `content`: **required**, string

### `ssh_run_command`
- `provider_id`: string
- `host`: **required**, string
- `port`: number, min:1, max:65535
- `username`: **required**, string
- `password`: string
- `command`: **required**, string
- `variable_name`: string

### `stop`
*No parameters for `stop`.*

### `store_global_variable`
- `name`: **required**, string
- `value`: nullable, string

### `template`
- `template_id`: **required**, int
- `variables`: array

### `text_map`
- `source`: **required**, string
- `operator`: **required**, string
- `variable_name`: **required**, string
- `default`: **required**, string
- `mappings`: **required**, array

### `text_replace`
- `source`: **required**, string
- `variable_name`: **required**, string
- `replacements`: **required**, array

### `text_split`
- `delimiter`: **required**, string
- `source`: **required**, string
- `variable_name`: **required**, string
- `repeat`: boolean

### `twitter_tweet`
- `provider_id`: **required**, string
- `tweet`: **required**, string
