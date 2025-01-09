---
title: Custom Actions
nav_order: 400
---

# Custom Actions

<a href="/images/custom-actions.png">
    ![Custom Actions editor screenshot](/images/custom-actions.png)</a>

With Custom Actions, it is possible to create a workflow out of a set of actions that are executed whenever a Webhook.site URL receives a request or email.

Using this functionality, you can connect APIs that aren't compatible, convert a HTTP request to an email or vice versa, build workflows that would otherwise require a developer, and much, much more.

The general principle of Custom Actions is that they are always executed in a chain. As they run, [Variables](/custom-actions/variables.html) are exchanged between them. 

Additionally, the [Conditions](/custom-actions/action-types.html#conditions) action can define certain conditions that are used to decide whether specific actions run or not. 

Even though actions are run in a chain, it's still possible to branch out and run actions in an asynchronous manner via [queued actions](/custom-actions.html#queued-actions), or loop over sets of data using actions that can be [repeated](https://docs.webhook.site/custom-actions.html#repeating-actions).

On each request, the output for all the different actions is collected so you can go back and see what happened. If the action sends HTTP Requests, both the request and response details are shown.

<figure markdown="span">
  ![Auto JSON in action](/images/kCuUKnGNu1NNGv4j7Y3UXTyV.png){ width="300" }
  <figcaption>Action output shown on individual requests along with HTTP Request data</figcaption>
</figure>

If actions fail, the request they ran on is marked. It is possible to set up [notifications](https://webhook.site/notifications) for when actions (and Schedules) fail. In Control Panel, [Error Log](https://webhook.site/control-panel/error-log) provides a convenient way to search for errors occurring across all URLs and Schedules associated with the Webhook.site account. 

With [Replay](/custom-actions.html#replay), it's possible to run the actions again, e.g. for actions that failed previously.

<figure markdown="span">
  ![Auto JSON in action](/images/ZxJHuOqDle5GG5kzDyc2WyPt.png){ width="300" }
  <figcaption>Error Log is a convenient way to monitor Schedules and Custom Actions</figcaption>
</figure>

## Demos

### JavaScript, X and Schedules

In this video I'm doing a quick demo of how I used Webhook.site to set up a workflow to post updates from my news page automatically to my X/Twitter account. I used the actions JavaScript, Conditions, X Post, and Store Global Variable. 

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/wg08ny5bh9w" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

### JSONPath and Google Sheets

In the following demo, webshop order details are received in a webhook. We then use Extract JSONPath and Google Sheets actions to insert their name in a Google Sheet. It also shows how variables interact with downstream actions.

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/9Cbuf5T6Tqo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

### Forward to multiple endpoints, Looping

A quick demo of how to use the Split Text action to loop over a list of URLs and forward the incoming request to them.

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/9LYjKPgO6Gk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

## Templates

If you use the same set of Custom Actions often, you can create a Template that contains a copy of one or more Custom Actions, along with a set of Predefined Variables. 

You can then use this template by creating an *Import Template* action.

### Creating a Template

To create a Template, click the *Create Template* button at the bottom of the Custom Actions overlay. Then enter a name for the template and select which actions should be copied to the template. If your template actions e.g. depend on variables pre-existing, like configuration data, you can add one or more Predefined Variables. These are available to the actions in the Template, but also to any subsequent actions coming after the Import Template action.

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
* a Custom Actions flow takes longer than 30 seconds to run. As Webhook.site's timeout for Webhook.site URLs is 30 seconds, to run flows longer than that, you can mark the action as Queued to let it run for up to 120 seconds.

Additionally, you can specify an amount of seconds to wait until the action is executed. To do this, enter an amount of seconds in the Seconds textbox next to the Queue checkbox.

As the queued action will inherit the execution scope *up until* the action, there are some things that are important to be aware of when using Queued Actions:

* Variables defined by a queued action are not available to *non-queued* actions. You cannot, for example, mark a *HTTP Request* action as queued and use the response in a *Modify Response* action (which can't be queued.)
* Variables defined in non-queued actions ordered *before* the queued action will be available to the action.
* If several consecutive actions are marked as queued, and their delay is identical, they are considered a group and will pass variables and execute in order.
* The amount of time until the queued actions are executed can vary by a few seconds.
* Groups of queued actions have a total timeout of 120 seconds, at which the execution will be terminated.

## Replay

With Replay, you can easily run Custom Actions again for either all or a subset of incoming requests. 

For example, if you've made changes to your flow, want to import data again, fixed an error – there's a lot of reasons you might want to run your flow again for the requests on your Webhook.site URL, and now you can do it in Webhook.site with a few easy clicks. 

If the filter matches more than 50 requests, a warning will be shown.

<a href="/images/replay.png">
    ![Custom Actions Replay screenshot](/images/replay.png)</a>

Existing action output stored on a request is overwritten by the replay action output.

Actions that are marked as queued will also be run as queued when replaying actions.

While Webhook.site starts processing oldest requests first, actions are run in batches and execution order is not guaranteed.