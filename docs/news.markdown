---
title: News & Changelog
nav_order: 50
---

# News

Subscribe below to receive updates about improvements and new features on Webhook.site as well as infrastructure changes like new IP addresses for e.g. firewall whitelisting. Expect a newsletter a few times a year at most.

<link href="//cdn-images.mailchimp.com/embedcode/horizontal-slim-10_7.css" rel="stylesheet" type="text/css">
<style type="text/css">
	#mc_embed_signup form {text-align: left;padding: 0;}
</style>
<div id="mc_embed_signup">
<form action="https://site.us19.list-manage.com/subscribe/post?u=a4698f7ac47cff759ecdcca24&amp;id=6c5386b81d" method="post" id="mc-embedded-subscribe-form" name="mc-embedded-subscribe-form" class="validate" target="_blank" novalidate>
    <div id="mc_embed_signup_scroll">
  	  <input type="email" value="" name="EMAIL" class="email" id="mce-EMAIL" placeholder="email address" required>
      <!-- real people should not fill this in and expect good things - do not remove this or risk form bot signups-->
      <div style="position: absolute; left: -5000px;" aria-hidden="true"><input type="text" name="b_a4698f7ac47cff759ecdcca24_6c5386b81d" tabindex="-1" value=""></div>
      <div class="clear"><input type="submit" value="Subscribe" name="subscribe" id="mc-embedded-subscribe" class="button"></div>
    </div>
</form>
</div>

## 25 September 2024

* `moment` library added to the JavaScript Custom Action. [More info here](/custom-actions/action-types.html#utility-modules)

## 10 September 2024

* When creating a date variable using the Set Variable action, it's now possible to specify an output timezone format.
* We've had to remove the spreadsheet selector dropdown due to changes in Google's API terms. It's still possible to copy/paste a spreadsheet URL and select it like that.

## 30 August 2024

* New Feature: Replay Custom Actions. Replaces the *Run Now* button. Easily run Custom Actions again for either all or a subset of incoming requests. [More info here](/custom-actions.html#replay) 
* Requests API: It's now possible to see and search for which Custom Actions returned an error using the new `custom_action_errors` field in the API. [More info here](/api/requests.html#search-query-examples)
* Actions API: The Execute Action endpoint has been changed so that the output and errors are now saved (overwritten) on the specified request. Additionally, error notification emails are disabled when running actions using the endpoint.

## 29 August 2024

* Webhook.site had partial downtime from approx 01:19 to 05:23 UTC. We've identified the fault to be the MariaDB "max connect errors" configuration option, which per default blocks a server IP after very a low number of errors, causing Webhook.site Web servers to lose contact to the DB servers. We've also identified an information leak in an error message which has also been remediated. We apologize.

## 26 August 2024

* New Operators added to *Conditions* action: is variable defined, is int, is json, is email, etc. [Full list here](/custom-actions/action-types.html#operators-with-value-argument).
* New output variables for *Database* action: `*.rows` and `*.error`, to allow e.g. making conditions actions based in the success of the database query. [More info here](/custom-actions/action-types.html#fetching-data).
* Added `.upper` and `.lower` Variable Modifiers. [More info here](/custom-actions/variables.html#variable-modifiers).

## 10 August 2024

* NATS and Supabase clients added to JavaScript sandbox. [More info here](/custom-actions/action-types.html#utility-modules)

## 2 August 2024

* As we're planning to add more capacity, the Webhook.site IPs have partially changed. The IP `88.99.82.58` is no longer used by us. The full list of IPs that need to be whitelisted are the following: `178.63.67.106`, `178.63.67.153`, `46.4.105.116`. 

## 23 July 2024

* New Custom Actions: FTP(S) and SFTP Download, in addition to existing Upload actions.

## 17 July 2024

* New Feature: Webhook.site Form Builder, a quick way to build HTML forms with custom fields that send data to your Webhook.site URL. Makes it easy to create e.g. a Contact Form in conjunction with Custom Actions. [Go to Form Builder](https://webhook.site/form-builder).

## 16 July 2024

* New Custom Action: Generate PDF, working with either Markdown or HTML content, can be used in e.g. Send Email, Modify Response actions. [More info here](/custom-actions/action-types.html#generate-pdf)

## 15 July 2024

* As of version 0.2.0, the Webhook CLI `forward` command now works bidirectionally, forwarding the response back to your Webhook.site URL, acting as a proxy. [More info here](/cli.html#bidirectional-forwarding)
* Webhook.site URLs can now also be used as subdomains. `https://webhook.site/my-url` and `https://my-url.webhook.site` are now equivalent. Custom domains are currently not supported.

## 9 July 2024

* New Custom Action: HubSpot Create Contact, which lets you easily create new leads in the HubSpot CRM system. [More info here](/custom-actions/action-types.html#hubspot)

## 28 June 2024

* Database Action: Added support for Microsoft SQL Server (`sqlsrv`), in addition to existing support for MySQL/MariaDB and PostgresQL.
* Fixed an issue in CSV export where lines containing the string `\"` would cause the CSV to be formatted incorrectly.
* We've been seeing some issues with our CDN provider, Cloudflare. We've added a link to disable CDN at the top of the page in case CDN-hosted resources (scripts and stylesheets) won't load.

## 25 June 2024

* JavaScript editor now has autocomplete and snippets for common structures (if, while, etc.)
* When downloading files (multipart, email attachments, etc.), the original filename is now used when possible
* In Control Panel, individual URLs are now marked with a unique color so they're easier to find

## 21 June 2024

* It's now possible to add a note to individual requests both via the app and [the API](/api/requests.html#update-request)
* In Control Panel, URL list now has ordering capabilities
* In Custom Actions editor, default variables (e.g. $request.uuid$) are ordered last
* Fixed copying DNSHook to clipboard
* Fixed Custom Actions editor layout problems

## 10 June 2024

* We've moved Tokens to a new datastore. The switch should have been unnoticable, but if you've started to see bugs in e.g. Control Panel or Tokens API, please contact support.
* It's now possible to search your URLs in Control Panel by ID and Alias.
* Fixed an issue where Error Log was not loading when a Token was deleted.
* Fixed an issue where Global Variables couldn't be edited in Control Panel.
* Fixed an issue where the correct group wouldn't be selected when editing a Token.
* A proper error is now returned when an API Key is invalid.

## 7 May 2024

* New Feature: Error Log, which lets you see the latest errors for your URLs and Schedules in a single, searchable, list. [Go to Error Log](https://webhook.site/control-panel/error-log)

## 3 May 2024

* New Action Type: Basic Auth, for easily adding secure authentication to your Webhook.site URL. [More info here](/custom-actions/action-types.html#basic-auth)
* It's now possible to hide requests marked as *Don't Save* from the UI. Simply click *More* and select *Hide "Don't Save" Requests*.

## 1 May 2024

* [Webhook.site Newsletter May 2024 has been released](https://www.reddit.com/r/webhooksite/comments/1chik6o/webhooksite_may_2024_update/).

## 25 April 2024

* Retry functionality has been added to the HTTP Request action. When enabled, Webhook.site will retry a HTTP request in case of timeouts. A status code can be specified as a retry condition. [More info here](/custom-actions/action-types.html#retry)
* The timeout of Queued actions have been increased to 120 seconds. This means that a series of queued actions have 120 seconds to complete.

## 24 April 2024

* For incoming emails, in addition to text and raw content, HTML content is now shown separately.
* New Base Variable for emails: `$request.html_content$` which contains only the HTML content of the e-mail.

## 22 April 2024

* If a default Custom Domain is specified and is validated for email, it's now used as the sender address in the Send Email action (applies to new URLs only.)
* Improved display of text content of incoming emails - links are now clickable and quotes are indented.
* Fixed "401 Missing Password" error when saving configuration of Tokens that have a password set.

## 15 April 2024

* Webhook.site now uses the domain `emailhook.site` for email receiving and sending. The old domain, `email.webhook.site`, continues to work.
* JavaScript action now supports Global Variables via the built-in `store()` and `global()` functions. [More info and examples here](/custom-actions/action-types.html#javascript)
* JavaScript action no longer considered in beta.
* New API: Global Variables. [More info here](/api/global-variables.html)
* Webhook.site CLI forward command now defaults to `https://localhost` for the `--target` parameter.

## 9 April 2024

* Action Editor improvements: drag and drop to change order of actions is now supported, improved renaming of actions, textboxes have been set to proper sizes

## 18 March 2024

* New Feature: DNSHooks, which will automatically show all DNS requests to your unique DNS name, and all its subdomains. It can be used to send data solely via DNS, or as a canary token. [More info here](/dnshook.html)

## 13 March 2024

* HTTP headers with underscores are no longer ignored. However, underscores are converted to dashes due to a technical limitation.
* When a search query is set, Webhook.site will now only show incoming requests and emails that match the search query. 
* Search queries are now stored in the browser's local storage, so it will be saved even after closing the browser.

## 1 March 2024

* Fixed a bug where the `$request.query$` Base Variable not being generated.

## 29 Feburary 2024

* Webhook.site now automatically decompresses `gzip` encoded request bodies.

## 26 Feburary 2024

* New features for "Set Variable" action: The Set Variable action can now generate random strings, date strings and timestamps. [More info here](/custom-actions/action-types.html#set-variable)

## 20 Feburary 2024

* New Feature: Templates, which are created out of existing Custom Actions, and can be reused via the Import Template Custom Action. [More info here](/custom-actions.html#templates)  [Template API](/api/templates.html)
* Webhook.site CLI: Better logging and can now be used for free users without API key.

## 7 Feburary 2024

* `faker` library added to the JavaScript Custom Action. [More info here](/custom-actions/action-types.html#utility-modules)

## 6 Feburary 2024

* Tokens now support timeouts up to 30 seconds, from 10 before, which allows more flexibility when testing application timeouts. 
* Tokens with timeouts are now have a dynamic rate limit. [More info here](/api/requests.html#capture-request)
* Updates to our Terms of Service and Privacy Policy. Summary:
    * Adding language specifically prohibiting submitting illegal content to Webhook.site
    * Fair Use policy has been updated to a "requests per minute" metric (from 10000 requests per day), and a guideline for 100 Tokens created per day when the "expiry" option is used
    * Added language about intellectual property rights, disclaimer of warranties, limitation of liability, indemnification, modification of terms, termination and governing law and jurisdiction.
   
## 29 January 2024

* Split Text action now supports repeating. [More info here](https://docs.webhook.site/custom-actions.html#repeating-actions)
* Split Text action now recognizes the string `\n` as a newline, allowing splitting strings by line.

## 15 January 2024

* Dynamic Request Limits: Webhook.site URLs/Tokens can now have custom request limits, from 1 to 10000, which is great when you're concerned about the data stored on Webhook.site. With this, you can limit the request history to the amount you choose.

## 11 January 2024

* New `$request.path$` (contains any subpath after the Webhook.site URL ID) and `$request.query$` (contains the query string) variables added. [More info here](/custom-actions/variables.html#base-variables)
* Don't Save, Rate Limit and Modify Response actions can no longer be marked as Queued.

## 10 January 2024

* Requests API: It's now possible to delete a subset of requests using the `date_from`, `date_to`, and `query` parameters. [More info here](/api/requests.html#delete-multiple-requests).

## 9 January 2024

* HTTP Request action: Fixed an issue where headers wouldn't be forwarded when using the `Forward` mode.

## 3 January 2024

* Happy New Year :-)
* Webhook.site now supports 2-factor authentication via TOTP. To enable, go to Control Panel -> User Profile.

## 27 December 2023

* New WebhookScript function: `http()`, which replaces the `request()` function and allows for more flexibility as well as sending e.g. form/multipart requests as the new HTTP Request Custom Action also allows. [More info here](/webhookscript/functions/network.html#httpstring-url-array-options-array)

## 22 December 2023

* The new Custom Action [HTTP Request](/custom-actions/action-types.html#http-request) has replaced Send Request, which has several benefits:
    * HTTP Request has different modes: text, multipart, etc., which lets you build more forms of HTTP requests that couldn't be done using Send Request.
    * The Forward mode is now able to forward Multipart requests.
    * Both the request and response are now saved so you can see exactly what was sent to the URL in HTTP Request.
    * The HTTP Request has a handy Format JSON button.
* It is still possible to make changes to existing Send Request actions, but it is no longer possible to create new Send Request actions.

## 7 December 2023

* Image files are now previewed in the file list, e.g. for email attachments
* Binary requests with content-types including `image/*`, `video/*` and `application/pdf` are now shown as linked files in the file list, not binary data.

## 6 December 2023

* Token (URL) expiry is now configurable with an amount of seconds. [More info here](/api/tokens.html#create-token)

## 28 November 2023

* New Custom Action: JavaScript. It is now possible to run JavaScript/Node.js code in your Custom Actions. This action is marked as beta as some limitations apply. [More info and examples here](/custom-actions/action-types.html#javascript-beta)

## 7 November 2023

* New Custom Actions: Microsoft Excel. Webhook.site now allows using your Microsoft account to append and retrieve data from Excel worksheets in your OneDrive account.
* New Custom Actions: Microsoft OneDrive. With Webhook.site, you can now use your Microsoft account to upload and download files in your OneDrive account.
* It's now possible to test IPv6-only traffic using the `ipv6.webhook.site` hostname. [More info here](/faq.html#how-can-i-test-an-ipv6-only-request)

## 31 October 2023

* New feature when testing actions: Test Until Here, which allows testing only the actions up until and including the currently selected action. This is useful when, for example, testing a flow that extracts data and sends an email, but you just want to test how data is extracted, and not sending the email (which is usually the last action.)

## 25 October 2023

* Schedules now have support for requirements which will send an error notification emails when they don't pass, making it an easy option for e.g. uptime monitoring. Currently supported requirements are "Response body must contain" and "Response status code must be in range". [More info here](/schedules.html)
* Webhook.site will now highlight the last viewed URL after logging in.

## 19 October 2023

* Queued Custom Actions that share the same delay are now run in groups, so they can share data and variables. This makes it possible to create more advanced workflows that run in the future.

## 12 October 2023

* New Custom Action: Auto JSON. Automatically converts JSON data into Webhook.site Variables. [More info here](/custom-actions/action-types.html#auto-json)

## 11 October 2023

* Custom Actions editor modal dialog has been changed to an overlay, which allows for more space to edit actions.
* Moved Delete Action button to avoid accidentally deleting actions.
* WebhookScript editor and action output panel can now be resized.

## 22 September 2023

* New update for Webhook.site CLI, a tool for interacting with the Webhook.site API and allows forwarding requests from your Webhook.site URL to your local network. [More info here](/cli.html)

## 21 September 2023

* New Custom Action: Split Text. Takes a source, delimiter and variable name prefix and splits text into X amount of variables.
* New Custom Action: Map Text. Takes a source, an operator (like the Conditions action) and a series of mappings and sets the resulting variable name to whether one of the mappings are a match to the source text.

## 15 September 2023

* It's now possible to name individual Custom Actions, so you can keep track of which action does what. To change the name of an action, click the dashed name at the top of the action editor when creating or editing an action.
* The Variables dropdown shows all available variables after clicking the Test button.
* Variables section of the Custom Actions editor now allows copying each variable name.

## 14 September 2023

* New Custom Action: SFTP Upload
* The Run SSH Command action now supports regular password authentication in addition to standard keypair authentication.

## 30 August 2023

* Send Email action: It's now possible to add attachments to the email being sent. 
* Send Email (SMTP) action: It's now possible to add attachments to the email being sent. 
* WebhookScript: The json_encode function now allows disabling JSON formatting.

## 11 August 2023

* WebhookScript: New delete() function added for deleting Global Variables.

## 4 August 2023

* Improvements to Dark Mode.

## 29 July 2023

* Custom Actions: Maintenance was carried out on the underlying database system storing Custom Actions, and this may have resulted in 500 errors for around a minute starting 14:10 UTC.

## 20 July 2023

* New WebhookScript function: `multipart()`, for sending HTTP multipart requests. [More info here](/webhookscript/functions/network.html#multipartstring-url-array-items-string-method-post-array-headers-num-timeout-array).
* Webhook.site can now send browser notifications to alert you of new emails or requests.
* Added "Mark all as read" button.

## 29 June 2023

* For teams using Custom Domains, it's now possible to specify a default domain in Control Panel that will be shown anywhere the Webhook.site URL can be copied, for example.

## 16 June 2023

* Dark Mode has been added to the user interface for Webhook.site.

## 7 June 2023

* New Custom Action: Send Push Notification via ntfy.sh. Allows you to easily send push notifications to your browser, phone, watch, etc. Simply download the ntfy.sh app, subscribe to your topic name and send a message to the topic name via this Custom Action. No account required.

## 22 May 2023

* Webhook.site was down from approximately 10:45 to 11:30 UTC. The cause was a customer abusing the Delay Action feature which caused a buildup of data. As a result, we've had to reset the "delayed action" queue, meaning that any delayed actions not executed at 10:00 UTC today have been lost. Any newly created delayed actions will still be run as of 12:00 UTC. We apologize for the inconvenience.

## 21 May 2023

* We've carried out an upgrade of some of the underlying software powering Webhook.site. As a result, Webhook.site should generally perform faster.<br>Beginning 10:45 UTC, there may have been instances of increased error rates. As of 12:00 UTC, these issues have been resolved. We apologize for the inconvenience. As always, if you experience issues with your Webhook.site URLs, Custom Actions, etc., please let us know at [support.webhook.site](https://support.webhook.site).

## 20 May 2023

* Custom Domains now show the exact error reason in Control Panel.

## 18 May 2023

* Fixed an issue where the Custom Domain setup email wouldn't show the correct DNS entries.

## 28 April 2023

* Free URLs now accept a maximum of 500 requests in *total*. Deleting requests won't allow the URL to accept more requests. We encourage upgrading to Webhook.site Pro or Enterprise to avoid these limitations.

## 26 April 2023

* New API for Groups. [More info here](/api/groups.html).
* It's now possible to use Unicode characters like emojis in user names, group names, etc.
* WebhookScript: `xml2array()` logs more helpful errors.

## 16 April 2023

* New WebhookScript function: `xml2array()`. [More info here](/webhookscript/functions/string.html#xml2arraystring-xml-array).
* Conditions action: It's now possible to delete individual conditions.

## 21 March 2023

* Repeat: Fixed a bug where only the last output of a repeated action would be shown in the action's output. 
* Fixed link to Extract JSONPath examples.
* Added example for making queries using fields that contain spaces.

## 14 March 2023

* WebhookScript: Fixed issue where floats would be parsed as strings (and not numbers, as they're supposed to), in some instances.

## 3 March 2023

* New WebhookScript string functions: `string_random()`, `uuid()`. [More info here](/webhookscript/functions/string.html).

## 23 Febuary 2023

* For WebhookScript actions, the first line of the script is now shown in the action list. It allows easily adding a title to the script by making the first line a comment.

## 6 Feburary 2023

* New WebhookScript cryptography functions: `sign()`, `digest()`, `verify()`. [More info here](/webhookscript/functions/string.html#cryptography). [JWT example here.](/webhookscript/examples.html#jwt)
* New WebhookScript base64 functions: `base64url_encode()`, `base64url_decode()`. [More info here.](/webhookscript/functions/string.html#base64url_decodestring-string-string)

## 1 Feburary 2023

* New Custom Action: Send Email (SMTP) - send an email using your own email provider.

## 20 January 2023

* XPath: Improvements to the XPath action have been made so that it's now able to parse both XML and HTML-style documents.
* WebhookScript: Fixed a bug in the set_response() function where it wasn't possible to set the response headers.
* WebhookScript: Fixed a bug where internal errors would be returned when using array functions on arrays containing specific strings.
* CSV Export: When exporting to CSV, the search query is now used so you get the same items in the CSV as you see in the request list.
* WebhookScript: Added `array_splice` and `array_range` functions. [More info here](/webhookscript/functions/array.html#array_splicearray-array-int-offset-int-length-array-replacement-array)

## 14 December 2022

* Fixed a bug where Extract XPath and WebhookScript `xpath` functions would not match correctly in all cases.

## 30 November 2022

* WebhookScript: stop() function now stops entire Custom Action flow and returns respond rather than simply exiting the current script.

## 28 November 2022

* Discord: Added an Embed URL action to Discord Custom Action for attaching videos, images, articles, etc.  to a chat message.

## 10 November 2022

* Schedules: Control Panel now shows Schedule IDs.
* Removed "Amount of requests to keep for Auto Cleanup" (configuring this didn't actually do anything.) As an alternative, you could use the *Don't Save* Custom Action.
* Send Request: Header Names are replaced with Variables.
* Global Variables: It's now possible to search for Global Variables.

## 6 November 2022

* Schedules/API: It's now possible to fetch Schedule Logs. [More info here](/api/schedules.html#get-schedule-logs)
* Schedules: Added "Run Now" button to all Schedules.

## 31 October 2022

* Control Panel: Category selector dropdown now sorted by name.

## 26 October 2022

* Improvements to Schedules
* Ability to rename Groups
* Group selection is now automatically remembered

## 30 September 2022

* New WebhookScript function: `is_empty()` [More info here](/webhookscript/functions/bool.html#is_emptyany-value-bool)
* New WebhookScript function: `is_null()` - handy for checking if a value is null without type checking issues. [More info here](/webhookscript/functions/bool.html#is_nullany-value-bool)

## 21 September 2022

* API: It's now possible to sort tokens returned by the Get Tokens endpoint. More info here: [More info here](/api/tokens.html#get-tokens)

## 8 September 2022

* Fixed a bug in Webhook.site CLI ("TypeError: Echo is not a constructor" error.) - please upgrade the NPM package to 0.1.5.
* Please do not use [async-http-client](https://github.com/AsyncHttpClient/async-http-client) (User-Agent AHC/2.1.) It is abandoned and contains bugs that creates too many HTTP requests. We may block users of this package in the future. 

## 17 August 2022

* As a result of customer abuse, we have decided to introduce rate limits on creation of URLs. The rate limit will be initially set to 10 per minute. After reaching this limit, the POST /token endpoint will return a `429 Too Many Requests` response.

## 28 June 2022

* New Custom Action Type: Send push messages with Pushed.co. [More info here](/custom-actions/action-types.html#pushed).

## 24 June 2022

* New WebhookScript function: preg_match() - allows matching regex with custom regex options [More info here](/webhookscript/functions/string.html#preg_matchstring-regex-string-subject-arrayfalse)
* New WebhookScript function: html_to_text() - converts html to text. A more aggressive version of html_strip_tags() [More info here](/webhookscript/functions/string.html#html_to_textstring-string-string)
* WebhookScript: regex_extract_first() now has a default parameter that is returned when there's no matches. The function still returns `false` by default when this third parameter is not set. [More info here](/webhookscript/functions/string.html#regex_extract_firstregex-regex-string-subject-any-default-stringfalse)

## 21 May 2022

* New Custom Actions feature: It is now possible to delay queued actions by a specified amount of seconds. [More info here](/custom-actions.html#queued-actions)

## 20 May 2022

* New WebhookScript function: is_numeric(). [More info here](/webhookscript/functions/math.html)
* Rate Limit Custom Action: It is now possible to specify a key to let you rate limit on a custom parameter. The request IP address (`$request.ip$`) is still the default key.
* Action and Schedule error reports now specify the name, ID or alias of the Schedule or URL in question.
* Fixed a bug with Webhook.site Enterprise Custom Domain email validation.

## 19 April 2022

* Fixed a bug that prevented action error notifications from being sent to the users.

## 14 April 2022

* It is now possible to search requests and emails, using either the frontend or the API. The data can be filtered by a wide range of fields, queries. [More info here](/api/tokens.html#query-string-search-examples).

## 30 March 2022

* Added documentation for the [Test Action endpoint](/api/custom-actions.html#test-custom-action).

## 20 March 2022

* New Variables for Files: `$request.file.[name].id$` and `$request.file.[name].link$` (which returns direct link to download the file.)

## 14 March 2022

* Added `num2hex`, `hex2num` and `hex2bin` functions.

## 19 January 2022

* New Custom Actions: RabbitMQ Get & Publish, allows consuming and publishing to RabbitMQ Queues via Webhook.site Custom Actions.

## 21 December 2021

* Improved handling of binary data received from Send Request actions. 
* Added a `group_id` parameter when creating or updating Tokens.
* Fixed an issue with the Twitter Custom Action.
* Requests to `/token/:tokenId/requests` are now throttled at 60 requests/minute.

## 24 November 2021

* WebhookScript: Fixed an issue that would cause strings to be interpreted as integers when encoding JSON.

## 30 October 2021

* Webhook.site's requests to itself, e.g. via Send Request action or Schedules by Webhook.site, now shows more clearly as coming from Webhook.site in the request list. Outgoing requests are now sent with a User-Agent header of `Webhook.site/1.0`, which can be overwrited if specifying a User-Agent header manually.
* Error deleting Global Variables fixed.
* It is now possible for Webhook.site Enterprise customers to manage their Custom Domains from the control panel.

## 15 October 2021

* Fix invalid charset configurations causing issues saving requests.

## 4 October 2021

* Webhook.site now supports multiple sub-users on an account, with different access permissions, available to Webhook.site Enterprise users. For more information, please [contact us](https://support.webhook.site).

## 29 September 2021

* Webhook.site CLI: New minor version, fixes a bug causing `Invalid namespace` errors.

## 17 September 2021

* New Custom Action Variable Modifiers: `.html_decode`, `.url_encode`, and `.url_decode`. [More info here](/custom-actions.html#variable-modifiers)

## 12 September 2021

* New WebhookScript function: array_merge(), that merges two arrays into one. [More info here](/webhookscript/functions/array.html)
* New WebhookScript function: array_chunk(), that splits an array into chunks. [More info here](/webhookscript/functions/array.html)
* Functions dd(), dump() and echo() can now take a variable amount of arguments. [More info here](/webhookscript/functions/general.html)
* New WebhookScript date function: now(), which returns the current date in ISO format. [More info here](/webhookscript/functions/date.html)
* The date_interval() and date_interval_human() functions now defaults to "now" if the second parameter isn't specified.
* Script editor now has more space for outputs in full screen mode.

## 18 August 2021

* New API Endpoint: Get tokens, which returns a list of all tokens belonging to the account. [More info here](/api/tokens.html#get-tokens)
* Fixed a bug that caused logins to be slow on especially older accounts.
* Fixed a bug that caused the FTP Upload action to error when the Port field was missing.

## 12 August 2021

* Google Sheet actions that consistently cause errors are now disabled automatically. Users are sent an email when this occurs.

## 30 July 2021

* New WebhookScript function: hmac(), which allows easily verifying strings using the HMAC method.  [More info here](/webhookscript/functions/string.html#hmacstring-value-string-algo-string-secret-stringfalse)

## 14 July 2021

* New Custom Action: Replace Text, which allows easily making text replacements from variable input, and either overwrites an existing variable or creates a new one with the replaced content.

## 4 July 2021

* Fixed bug causing the "Use Request Content" checkbox in the Send Email action to not work.

## 15 June 2021

* New Custom Action: Twitter, so you can easily send tweets using Webhook.site.
* New WebhookScript functions: convert_kana(), string_slice(), string_upper(), string_lower(), string_title() [More info here](/webhookscript/functions/string.html).

## 10 June 2021

* Individual Custom Actions can now be set as *queued*, which causes them to be run in the background, or asynchronously. [More info here](/custom-actions.html#queued)

## 7 June 2021

* Raised the limit for the amount of items processed by repeating actions to 100.
* Fixed a bug that would cause an error when updating notification settings in Control Panel.
* Fixed a bug where emails containing attachments would be stored.

## 23 May 2021

* API: It's now possible to filter requests by date. [More info here](/api/tokens.html#query-string-parameters)

## 13 May 2021

* Documented `clone_from` option when using the API to create Tokens (URLs)
* WebhookScript: `json_decode` / `json_encode` now output error messages if they fail due to e.g. bad data.

## 1 May 2021

* Webhook.site Schedules now has an API. [More info here](/api/schedules.html)
* Fixed a bug where URLs could be in two groups at the same time.

## 20 April 2021

* Added base64 encoding and decoding *variable modifiers*. [More info here](/custom-actions.html#variable-modifiers)

## 11 April 2021

* New Custom Action and WebhookScript function: Don't Save, which marks the request so it is not saved in Webhook.site. The request can still be seen when it comes in, but will not be available through through the app later, or through the API. 
* New Custom Action: Stop, which immediately stops Custom Action execution and returns the default response.
* The Extract Regex now supports the Repeat function. [More info here](/custom-actions.html#repeating-actions-beta).

## 7 April 2021

* New powerful feature: Repeating actions. Currently supported by the Extract JSONPath action, it is now possible to "loop over" items in a JSON array. [More info here](/custom-actions.html#repeating-actions-beta)

## 2 April 2021

* It is now possible to enable or disable Custom Actions on a specific Token with the API. [More info here](/api/custom-actions.html#toggle-custom-actions) or [here](/api/tokens.html#create-token).
* When exporting CSVs, the sorting selected in the application is now used automatically.

## 28 March 2021

* Today we've released the first version of the Webhook.site Command-line Interface (CLI), which allows you to forward requests from your Webhook.site URL to your local machine. [More info here](/cli.html)

## 24 March 2021

* WebhookScript: Added `array_sort`, `array_join` and `json_escape` functions.
* Added *modifiers* for variables. [More info here](/custom-actions.html#variable-modifiers)

## 23 March 2021

* Control Panel: It's now possible to clone URLs, including their Custom Actions and other configuration.
* Control Panel: URLs with a password can be deleted more easily.

## 13 March 2021

* Control Panel: It's now possible to set a password for a Webhook.site URL in the Control Panel. Additionally, it's now possible to easily select and delete multiple URLs at once.

## 11 March 2021

* API: It's now possible to specify an alias when creating a URL via the API. [More info here](/api/tokens.html)

## 6 March 2021

* New Action: Database Query - allows running database queries on PostgreSQL and MySQL servers, inserting, changing and fetching data in specific variables or JSON format. [More info here](/custom-actions.html#database-query)

## 3 March 2021

* Webhook.site Premium has changed name to Webhook.site Pro. Functionality, pricing and everything else remains the same; it's a cosmetic change.
* More currencies are now supported for Webhook.site Pro subscriptions: GBP and EUR. To change the currency of an existing subscription, please contact [Webhook.site Support](https://support.webhook.site).
* Custom Action output is now included in CSV Exports.

## 17 Feburary 2021

* New Action: FTP(S) Upload - allows easy file upload to FTP servers.

## 5 Feburary 2021

* New WebhookScript functions: html_strip_tags, html_decode, html_encode, markdown_to_html. For more information, [see here](/webhookscript/functions/string.html).

## 1 Feburary 2021

* Webhook.site has had intermittent downtime today due abuse from a user. We've identified them and blocked them from our systems. We're very sorry for the inconvenience.

## 31 January 2021

* We have discontinued support for subscriptions via Patreon, who will need to create a new subscription. For more information please contact [support](https://support.webhook.site).

## 19 January 2021

* Happy new year!
* New Action Type: Conditions 2.0. Now supports adding multiple conditions in a single action.
* New Action Type: Set Variable. Working similarly to the Store Global Variable action, this action sets a runtime variable that is not persisted.
* Actions can now individually be executed depending on a previous set of conditions.
* The Debug Output section in the Custom Actions builder now shows the action number and type from where it came.
* The Modify Response action now supports returning the response immediately.

## 5 December 2020

* Added new Custom Action: Store Global Variable, which does what it says on the tin.
* Bug fix: In Control Panel, the update date for each Global Variable now actually updates when a Global Variable is updated.

## 26 November 2020

* Webhook.site had downtime during the night. The problem has been fixed.

## 25 November 2020

* WebhookScript: It's now possible to store non-string values in set(). If the value is an array, however, it is JSON encoded first.
* WebhookScript: Added more examples for the date functions.

## 1 November 2020

* Added new Custom Action: Rate Limit, which lets you specify the maximum amount of requests in a given duration per IP to allow to request the Webhook.URL.
* Dates shown in the application now include seconds.

## 29 October 2020

* Added new Custom Action: Run SSH Command, which allows you to run SSH commands on your server.

## 22 October 2020

* WebhookScript: Added `array_keys` and `array_values` functions. For more information, [see here](/webhookscript/functions/array.html).

## 19 October 2020

* It's now possible to set a timeout for the Send Request action. A new `timeout` parameter can also be given to the `request()` function in WebhookScript. Both places accept a value in seconds, with decimals.
* When exporting Custom Actions, if the URL has an alias, this is now used for the resulting filename.

## 11 October 2020

* It's now possible to export and import Custom Actions to a file using the new Import/Export buttons in the Custom Actions builder.

## 7 October 2020

* Added documentation for managing Custom Actions via the API. For more information, [see here](/api/custom-actions.html).
* Fixed a bug causing the Operator of an action to be reset to "is equal to" when testing.

## 6 October 2020

* Action output is no longer displayed twice when testing Condition actions.

## 24 September 2020

* New feature: Customize Auto-Cleanup threshold. This lets you specify how many requests or emails to keep for your URLs, if you want to keep fewer than the default amount of 10.000 for e.g. data protection reasons. Available from the brand new Settings page in Control Panel. The setting applies to all URLs that have the Auto Cleanup feature enabled - click Edit on a URL to enable it.
* New feature: URL groups, which lets you categorize your URLs into groups. Available from the URLs page in Control Panel. Click Edit on a URL to change its group.
* The URLs page in Control Panel has a new design which is less cluttered and allows you to more quickly change certain settings, URL aliases, and the description of a URL.

## 23 September 2020

* Regrettably, we saw a long period of downtime again from approx 20:00 to 05.40 UTC. The cause of the downtime was a user flooding their Webhook.site URLs with many gigabytes of data, causing the system to be overloaded. The same user was responsible for the downtime at 15 September 2020 and we've now terminated their license to use Webhook.site. We are also going prioritize changes that will automatically limit this kind of abuse, as well as move to another database system that will be more resilient.

## 15 September 2020

* We've seen spurious instances of downtime in the last 24 hours, the longest one lasting from approx. 14:00 to 14:50 UTC. We apologize for the inconvenience.

## 13 September 2020

* WebhookScript: Added `override` parameter to request(), which prevents content from the source request from being included.

## 3 September 2020

* WebhookScript: It is now possible to set a default for the `var()` function.
## 29 August 2020

* A bug in the Extract JSONPath action has been fixed so that it is now also possible to filter for keys containing punctuation, e.g. `.data[?(@.Employee.FirstName)]`.

## 18 August 2020

* WebhookScript: The `to_date` and `date_format` functions have been improved with timezone handling capabilities.

## 15 August 2020

* It's now possible to set a custom timeout for Schedules, up to 30 seconds.

## 8 August 2020

* You can now specify a custom Cron expression for your Webhook.site Schedule, in addition to the predefined intervals. This lets you decide exactly the hour, day and minute, etc., of when the schedule runs (based on UTC time.)
* It's now possible to enable email notifications for whenever a Schedule run fails to execute. To enable this, simply check the checkbox in [Notification Settings.](https://webhook.site/notifications).

## 7 August 2020

* It's now possible to change the name of your Provider accounts to e.g. something that's easier to remember.

## 5 August 2020

* Webhook.site had an unplanned outage starting at 03.30 UTC. The site was down for around an hour.

## 2 August 2020

* It is now possible to specify a default value in the Extract JSONPath, Extract Regex and Extract XPath actions, so that if the extraction could not find the item, the variable is set to the default value that is defined. This field also takes variables.
* Request list is now sorted by Newest First per default.
* Custom Action number and type is now shown next to the output in the request details. If the Action was deleted, the UUID is shown instead.

## 1 August 2020

* It is now possible to enable email notifications for whenever a Custom Action encountered an error. To enable this, simply check the checkbox in [Notification Settings.](https://webhook.site/notifications).

## 29 July 2020

* New WebhookScript function: `trim(string)`, which removes space, newline and tab characters from the beginning and end of a string, similar to PHP's own trim() function.
* New Schedule intervals: weekly (every monday), monthly (every 1st day of month)

## 25 July 2020

* New WebhookScript function: `action(action_type, parameters)`, to run Custom Actions inside a WebhookScript. [More info here.](/webhookscript/functions.html#actionstring-action_type-array-parameters-array)
* It's now possible to download email attachments or uploaded files directly from the Webhook.site app.
* When sending a request using either the Send Request Custom Action or the request() function, the response is now truncated if the response content is over 20KiB. This means the whole contents is not visible in the app, but is still available to Actions.

## 16 July 2020

* Better file handling for emails: attached files are now also extracted as variables
* New file management functions for WebhookScript: `files()` retrieves a an array of all files, `file_content(fileId)` returns the content of a specific file. [More info here.](/webhookscript/functions.html#files)

## 5 July 2020

* New "Resize Image" action added for resizing images from either a file upload, email attachment or other Action. 
* Better handling of downloaded files: the contents won't be shown in the debug overlay to prevent very large files from crashing the browser.
* Fixed a bug in the Dropbox provider returning creating an empty variable when downloading large files.

## 3 July 2020

* Webhook.site was down for about 30 minutes starting 07:20 UTC due to a memory upgrade.
* Max request size has been increased to 10 MB from 2 MB.

## 23 June 2020

* Added new Dropbox Custom Actions: Create Folder, Download, Upload, Delete, Get Link. 

## 14 June 2020

* WebhookScript editor syntax highlighting improved with regards to multiline strings, escape characters and more
* New WebhookScript editor keyboard shortcut for saving (Mac: Cmd-S, Windows: Ctrl-S.)
* Fix WebhookScript fullscreen mode not being disengaged when saving
* URLs can now accept file uploads via multipart. File contents are available via variables: `request.file.<formname>.content`, `request.file.<formname>.size`, `request.file.<formname>.filename`
* New WebhookScript function: `csv_to_array()`, which converts a CSV file from a string to an array that can easily be parsed.
* Added an [example script](/webhookscript/examples#uploading-and-parsing-csv-file) demoing file uploads and CSV parsing

## 7 June 2020

* Added new Slack Send Message Custom Action, which lets you send Slack messages via a Slack Webhook URL.

## 5 June 2020

* Added "Formula Mode" checkbox for Add and Update Row Google Sheets actions, which parses values like entered in a cell, and allows inserting formulas.

## 4 June 2020

* Added new endpoints to fetch the content and information about the latest request on a URL. See [here](/api#get-single-request) and [here](/api#get-raw-request-content).

## 2 June 2020

* Added Amazon Web Services CloudFront Cache Invalidation Custom Action.
* Added ability to toggle Auto Cleanup, which automatically cleans up requests/emails.

## 30 May 2020

* Added Discord Custom Action for sending messages. [Read more in the docs](/custom-actions#discord)

## 29 May 2020

* New set of date functions added to WebhookScript, namely: `to_date()`, `date_format()`, `date_to_array()`, `date_interval()`, `date_interval_human()`. [Read more in the docs](webhookscript/functions#date-manipulation)

## 25 May 2020

* New set of Amazon Web Services S3 actions: Create Bucket, Put Object, Delete Object and Get Object (which retrieves object contents to a Variable.)

## 22 May 2020

* New Schedule intervals: every 1 minute and every 10 minutes, in addition to the already [existing ones](/schedules).

## 17 May 2020

* New WebhookScript function: `delay()`, which lets you delay and execute WebhookScript code a set amount of seconds in the future.
* New WebhookScript function: `exec()`, which lets you dynamically execute code in a string.
* New WebhookScript function: `import()`, which downloads and executes code from a URL - great if you want to reuse your code, just put it on Github and import it with the URL!

## 16 May 2020

* It's now possible to set a Token (URL or email address) to expire automatically, even for Premium users. This is useful for creating tokens for automated testing.

## 3 May 2020

* New Google Sheets Custom Actions (Beta). 3 initial actions are available: Append Row, Update Row and Get Values, which allow you to manipulate or retrieve the values of a Google Sheet without writing any code.

## 24 April 2020

* New fullscreen mode in WebhookScript editor
* Ability to edit your user profile
* New WebhookScript functions: `base64_encode()`, `base64_decode()`.

## 21 April 2020

* New WebhookScript function: store() - creates or updates an existing Global Variable

## 20 April 2020

* New Global Variables section in Control Panel.

## 19 April 2020

* New WebhookScript math functions: max(), min(), mod(), pi(), rand() - for more, see the [Reference](/webhookscript/reference)

## 28 March 2020

* New feature: Webhook.site Schedules lets you request any URL – including Webhook.site URLs – automatically on an interval, so you can for example run Custom Actions every 5 minutes, or make a health check for your Web site.
* Send Request action request timeout has been raised from 5 to 10 seconds. Applies to both the Custom Action and the WebhookScript request() function.

## 24 March 2020

* New feature: API Keys can now be created so you can use the API with URLs that have the "Require Authentication" or "Password" options set.
* Fix: It's now possible to test Send Email actions before creating them. Prior to this, the Test button would not do anything for the Send Email action.

## 6 March 2020

* New feature: Extract XPath Custom Action with accompanying xpath() WebhookScript function. [Read more.](/custom-actions#extract-xpath)

## 29 Feburary 2020

* Values are no longer required for Condition actions, so it's possible to compare an empty string or missing value.
* Fixed an issue where a tooltip in the Custom Actions modal would not disappear.
* Removed Beta label from WebhookScript.

## 27 Feburary 2020

* Fixed a bug where slashes at the end of Webhook.site Single Page App URLs didn't work.
* Fixed a bug where Copy To CURL sometimes wouldn't return a valid CURL command.

## 26 Feburary 2020

* It's no longer a requirement to specify a variable for the Send Request action.

## 25 Feburary 2020

* New feature: It's now possible to receive emails, which are treated like Webhooks – so you can automate emails with Custom Actions on Webhook.site. You can also test email deliverability using DKIM, DMARC and SPF validation.
* JSON formatting is now always enabled per default.
* The requests view is cleared after deleting the last request, and the tutorial text is shown.

## 16 Feburary 2020

* WebhookScript: Added `regex_extract` and `regex_extract_first` functions.

## 15 Feburary 2020

* WebhookScript: Added `hash` function.

## 14 Feburary 2020

* New feature: Export to CSV lets you export all requests on a given URL to a CSV file.
* Fixed a bug where duplicate in-app notifications would appear on new requests.

## 12 Feburary 2020

* WebhookScript: Added `url_encode`, `url_decode`, and `query` functions.

## 8 Febuary 2020

* New Custom Action type: Condition, which lets you conditionally stop a set of actions based on comparisons.

## 28 January 2020

* WebhookScript now supports newline literals (`\\n`) in strings, escaped by 2 backslashes.

## 25 January 2020

* Global Variables are now available in the Control Panel, which lets you keep configuration like API keys in a separate place from your Custom Actions and scripts while managing them at a central place.

* Changed the font of the WebhookScript editor, which resulted in uneven selection of text.

## 23 January 2020

* You can now specify a source variable for JSONPath and Regex actions, so you can extract text from not only the request content.

## 12 January 2020

* Switched to using Ace as editor for WebhookScript.
