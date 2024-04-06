---
title: Examples
nav_order: 500
parent: Custom Actions
---

## Adding rows to an Airtable Base

While Webhook.site doesn't have a native integration with Airtable, due to the simple API, it's exceedingly easy to add rows to a so-called Airtable Base.

First, create an API key on your Account page: https://airtable.com/account.

Next, go to Airtable's API documentation and select the Base you want to interact with: https://airtable.com/api. In the upper right corner, make sure **show API key** is checked.

![Creating an Airtable row using the API documentation](/images/airtable-example.png)

If you then scroll down to the **Create records** section, you can essentially copy everything over to a Send Request action.

Things to note:

* The Request Method should be `POST`
* Make sure you copy everything *between* `--data '` and the final `'` (quote) character
* Also make sure that quotes aren't included in the two header lines
