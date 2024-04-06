---
title: Schedules
nav_order: 395
---

# Webhook.site Schedules

Included in your Webhook.site Pro subscription is **Webhook.site Schedules**, which enables you to periodically send requests to specified URLs (also including your Webhook.site URLs, so your Custom Actions can be executed periodially) with a custom method, headers, and interval.

Schedules can be used for a variety of purposes, including cache warming, uptime monitoring, automatic data transfer, etc.

After creating the Schedule, you can view the logs for the last 100 scheduled requests.

Per default, the timeout for the Schedule requests is 5 seconds, but can range from 1 to 30 seconds. 

A timeout or server error will trigger a Schedule error notification email, if enabled in Control Panel -> Settings.

Schedules can also be managed using the [Schedules API](/api/schedules.html).

![Schedules editor](/images/schedules-editor.png)

## Uptime monitoring & Requirements

If you create a Schedule and enable the <i><a href="https://webhook.site/notifications">When an error happens during a Schedule run</a></i> setting, Webhook.site will automatically send an email notification when a URL has a timeout longer than the one specified, or when one of the requirements aren't met. It is possible to specify requirements for the response body containing a string, and the response status code being within a certain range.

## Schedule Intervals

In addition to be able to use a custom `cron`-style expression string, Schedules can be executed at the following preset intervals:

* 1 minute
* 5 minutes
* 10 minutes
* 1 hour
* 24 hours (at 00:00)
* Every week (mondays at 00:00)
* Every month (1st day at 00:00)

Schedule intervals are based on UTC time.

For building cron-style expressions, we recommend https://crontab.guru.