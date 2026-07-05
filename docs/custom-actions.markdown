---
title: Custom Actions
nav_order: 400
---

# Custom Actions

<a href="/images/custom-actions.png">
    ![Custom Actions editor screenshot](/images/custom-actions.png)</a>

With Custom Actions, it is possible to create a workflow out of a set of actions that are executed whenever a Webhook.site URL receives a request or email. Custom Actions run on the Webhook.site Cloud.

Using this functionality, you can connect APIs that aren't compatible, convert a HTTP request to an email or vice versa, build workflows that would otherwise require a developer, and much, much more.

The general principle of Custom Actions is that they are always executed in a chain. As they run, [Variables](/custom-actions/variables.html) are exchanged between them.

Additionally, the [Conditions](/custom-actions/action-types.html#conditions) action can define certain conditions that are used to decide whether specific actions run or not. 

Even though actions are run in a chain, it's still possible to branch out and run actions in an asynchronous manner via [queued actions](/custom-actions.html#queued-actions), or loop over sets of data using actions that can be [repeated](https://docs.webhook.site/custom-actions.html#repeating-actions).

On each request, the output for all the different actions is collected so you can go back and see what happened. If the action sends HTTP Requests, both the request and response details are shown.

<figure markdown="span">
  ![Extract JSON in action](/images/kCuUKnGNu1NNGv4j7Y3UXTyV.png){ width="700" }
  <figcaption>Action output shown on individual requests along with HTTP Request data</figcaption>
</figure>

If actions fail, the request they ran on is marked. It is possible to set up [notifications](https://webhook.site/notifications) for when actions (and Schedules) fail. In Control Panel, [Error Log](https://webhook.site/control-panel/error-log) provides a convenient way to search for errors occurring across all URLs and Schedules associated with the Webhook.site account. 

With [Replay](/custom-actions.html#replay), it's possible to run the actions again, e.g. for actions that failed previously.

<figure markdown="span" id="error-log">
  ![Extract JSON in action](/images/ZxJHuOqDle5GG5kzDyc2WyPt.png){ width="700" }
  <figcaption>Error Log is a convenient way to monitor Schedules and Custom Actions</figcaption>
</figure>

### Shortcut Keys

The following shortcut keys can be used in the Custom Actions editor.

* **Alt-R** - test action
* **Alt-S** - save/create action

## Demos

### Using Databases in your Custom Action workflows and automations

A quick demo of how to setup and manage a Webhook.site Database as well as run queries to retrieve or store data using either the Database Custom Action or WebhookScript/JavaScript actions.

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/76dRU4zH5Kg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

### Get Requests action & Repeat

It's nice to be able to interact with the data that a Webhook.site URL has received - the new Get Requests action does exactly this. In this example, we use 1 URL for collecting newsletter signups and another "runner" URL for sending a newsletter to each of the subscribers collected. 

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/TinUURtIBrg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

### JavaScript, X and Schedules

In this video I'm doing a quick demo of how I used Webhook.site to set up a workflow to post updates from my news page automatically to my X/Twitter account. I used the actions JavaScript, Conditions, X Post, and Store Global Variable. 

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/wg08ny5bh9w" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

### JSONPath and Google Sheets

In the following demo, webshop order details are received in a webhook. We then use Extract JSONPath and Google Sheets actions to insert their name in a Google Sheet. It also shows how variables interact with downstream actions.

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/9Cbuf5T6Tqo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

### Forward to multiple endpoints, Looping

A quick demo of how to use the Split Text action to loop over a list of URLs and forward the incoming request to them.

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/9LYjKPgO6Gk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

### Mock OpenAPI and Swagger specifications using Mock action

The [Mock](/custom-actions/action-types.html#mock) action lets you upload an OpenAPI or Swagger specification, and your Webhook.site URL will automatically act as a mock server, creating responses based on the paths and schemas in the specification.

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/QIEzn4i_P-M" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

### Using Queue Profiles to rate limit and control Custom Actions execution

In this video, we're going to see how you can use the new Queue Profiles features to control the flow of your Custom Actions automations & workflows, a useful feature when sending data to an API or service that's rate limited, and you have more data than it can accept. 

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/clp4am_o6a0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

## Templates

If you use the same set of Custom Actions often, you can create a Template that contains a copy of one or more Custom Actions, along with a set of Predefined Variables. 

You can then use this template by creating an *Import Template* action.

### Creating a Template

To create a Template, click the *Create Template* button in the Custom Actions editor. Then enter a name for the template and select which actions should be copied to the template. If your template actions e.g. depend on variables pre-existing, like configuration data, you can add one or more Predefined Variables. These are available to the actions in the Template, but also to any subsequent actions coming after the Import Template action.

Predefined Variables can be updated in the Control Panel.

Changes to the actions that the Template was created from do not automatically carry over to the template. Instead, Templates can be updated post-creation by overwriting them with a new set of actions.

Templates can also be managed using the [Template API](/api/templates.html).

## Repeating Actions

Webhook.site allows some action types to be repeating, which makes Webhook.site "loop over" one or more values without needing to use scripts.

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/PDNSHyhMWcQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

Repetition is supported by the Extract JSONPath, Extract Regex and Split Text action types.

The maximum amount of items that are supported is **100** to prevent abuse. 

The repeating action must be ordered *before* the actions that are to be repeated.

## Queued Actions

<a href="/images/queue-and-delay.png">
    ![Custom Actions editor screenshot](/images/queue-and-delay.png)</a>

By checking the *Queued* checkbox when creating a Custom Action, Webhook.site will run the action in an asynchronous background queue. 

This is useful when:

* a Webhook.site URL should respond quickly, but a Custom Actions flow takes a long time to run. For example, if a Webhook.site URL should respond in 5 seconds, but an endpoint with a HTTP Request action that responds in 10 seconds is called, you can queue the HTTP Request action so it's run in the background queue.
* a Custom Actions flow takes longer than 30 seconds to run. As Webhook.site's timeout for Webhook.site URLs is 30 seconds, to run flows longer than that, you can mark the action as Queued to let it run for up to 120 seconds, or 300 seconds for Enterprise subscribers.

Additionally, you can specify an amount of seconds to wait until the action is executed. To do this, enter an amount of seconds in the Seconds textbox next to the Queue checkbox.

As the queued action will inherit the execution scope *up until* the action, there are some things that are important to be aware of when using Queued Actions:

* Variables defined by a queued action are not available to *non-queued* actions. You cannot, for example, mark a *HTTP Request* action as queued and use the response in a *Modify Response* action (which can't be queued.)
* Variables defined in non-queued actions ordered *before* the queued action will be available to the action.
* If several consecutive actions are marked as queued, and their delay is identical, they are considered a group and will pass variables and execute in order.
* The amount of time until the queued actions are executed can vary by a few seconds.
* Groups of queued actions have a total timeout of 120 seconds (300 seconds for Enterprise subscribers), at which the execution will be terminated.

For Webhook.site Enterprise subscribers, additional, separate, queue compute is available to run Queued Actions faster and with less delay.

### Queue Profiles

Per default, Custom Actions marked as Queued are run in a default queue - on a best-effort basis - with no limit on how many Custom Actions can run in a given time period. 

Queue Profiles allows you to use a shared configuration and control exactly how many jobs can run in a given period. This can useful when, for example, running actions that interact with APIs that have rate limits. 

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/clp4am_o6a0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

Actions that can't run due to the rate limit are retried automatically until their expiry.

Another benefit of Queue Profiles is that actions with the same Queue Profile are guaranteed to always run grouped, in order. This means they share variables down the chain.

Queue Profiles are available for Pro and Enterprise customers.

<a href="/images/queue-profile.png">
    ![Custom Actions Queue Profile](/images/queue-profile.png)</a>

Here's what the configuration fields mean when setting up a Queue Profile:

* **Initial Delay:** This waits a specified amount of seconds before the Action is executed the first time. This can be used, for example, to wait for a data source to consolidate. Unless there's a specific reason to wait, this should be set to zero seconds.
* **Rate Limit:** Specify the maximum amount of jobs that can be run in a given period. For example, if the actions are running against an API that has a rate limit of 100 requests per minute, this can be set to *`100` jobs every `1` minute*. This makes sure that no more than 100 jobs will be executed per 60 seconds. If there are more jobs, they are retried continuously.
* **Job Lifetime**: Measured from when the job is first run, this sets the maximum period the job is retried until it is deleted and fails. For example, if there's a million jobs with the aforementioned *100 per minute* rate limit, it would take days to execute them all. To prevent jobs staying in the queue indefinitely, the maximum Job Lifetime is 1 day or 7 days for Enterprise subscribers.

Actions that fail due to job lifetime expiry are marked as such, and shown in [Error Log](#error-log).

The accuracy of the rate limit can depend on various factors, including other customer activity and the execution time of the actions, causing actions to run a few seconds later than the mathematical optimum. However, the maximum limit is never exceeded. For example, if the Queue Profile is configured to *`100` jobs every `1` minute*, only 99 jobs may run in practice, but never 101.

## Replay

With Replay, you can easily run Custom Actions again for either all or a subset of incoming requests. 

For example, if you've made changes to your flow, want to import data again, fixed an error – there's a lot of reasons you might want to run your flow again for the requests on your Webhook.site URL, and now you can do it in Webhook.site with a few easy clicks. 

If the filter matches more than 50 requests, a warning will be shown.

<a href="/images/replay.png">
    ![Custom Actions Replay screenshot](/images/replay.png)</a>

Existing action output stored on a request is overwritten by the replay action output.

Actions that are marked as queued will also be run as queued when replaying actions.

While Webhook.site starts processing oldest requests first, actions are run in batches and execution order is not guaranteed.