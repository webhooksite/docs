---
title: Custom Actions
nav_order: 400
---

# Custom Actions

<a href="/images/custom-actions.png">
    ![Custom Actions editor screenshot](/images/custom-actions.png)</a>

With Custom Actions, it is possible to create a workflow out of a set of actions that are executed whenever a Webhook.site URL receives a request or email.

Using this functionality, you can connect APIs that aren't compatible, convert a HTTP request to an email or vice versa, build workflows that would otherwise require a developer, and much, much more.

## Demos

### JavaScript, X and Schedules

In this video I'm doing a quick demo of how I used Webhook.site to set up a workflow to post updates from my news page automatically to my X/Twitter account. I used the actions JavaScript, Conditions, X Post, and Store Global Variable. 

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/wg08ny5bh9w" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

### JSONPath and Google Sheets

In the following demo, webshop order details are received in a webhook. We then use Extract JSONPath and Google Sheets actions to insert their name in a Google Sheet. It also shows how variables interact with downstream actions.

<center><iframe width="100%" height="315" src="https://www.youtube.com/embed/9Cbuf5T6Tqo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>


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

This is useful when you need your Webhook.site URL to respond quickly, but your Custom Actions are taking a long time to run. For example, if your Webhook.site URL should respond in 5 seconds, but you need to call an endpoint with a HTTP Request action that responds in 10 seconds, you can queue the HTTP Request action. 

Additionally, you can specify an amount of seconds to wait until the action is executed. To do this, enter an amount of seconds in the Seconds textbox next to the Queue checkbox.

As the queued action will inherit the execution scope *up until* the action, there are a few things to be aware of when using Queued Actions:

* Variables defined in non-queued actions ordered *before* the queued action will be available to the action.
* If several consecutive actions are marked as queued, and their delay is identical, they are considered a group and will pass variables and execute in order.
* Variables defined by a queued action are not available to *non-queued* actions. You cannot, for example, mark a *HTTP Request* action as queued and use the response in a *Modify Response* action.
* The amount of time until the queued actions are executed can vary by a few seconds.
* Groups of queued actions have a total timeout of 120 seconds, at which the execution will be terminated.