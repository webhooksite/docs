---
title: Databases
nav_order: 390
---

# Webhook.site Databases

Store and process data in the Webhook.site Cloud using Databases. Built right in to Webhook.site, Databases provide a fully-featured PostgreSQL-compatible database. You can create and remove tables, create columns and run queries in the Console. 

With Webhook.site Custom Actions, you can interact with your Database to store, update, retrieve and remove data by SQL Query whenever a Webhook.site URL or E-mail Address receives a hit.

Additionally, with Webhook.site's simple API, you can manage your Database, including running SQL queries.

<figure markdown="span">
  ![Webhook.site Database Console](/images/database_console.png){ width="500" }
  <figcaption>Webhook.site Database Console</figcaption>
</figure>

<figure markdown="span">
  ![Webhook.site Database in Custom Action editor](/images/database_action_editor.png){ width="500" }
  <figcaption>Webhook.site Database in Custom Action editor</figcaption>
</figure>

## Under the hood

Webhook.site Databases are powered by CockroachDB, providing a fault-tolerant, secure and highly available PostgreSQL-compatible environment for your data. With Webhook.site Databases, you don't have to worry about maintenance, uptime, backups as Webhook.site Cloud continually manages and scales the database clusters upon demand to ensure performance.

## Pricing and availability

!!! news
    As an introductory offer, each Webhook.site Pro & Enterprise subscription automatically comes with a `DB-S` Webhook.site Database instance included. Additional databases can be ordered by contacting Support.

### Pricing Table

|         | `DB-S` Small | `DB-M` Medium      | `DB-L` Large       | `DB-X` Custom   |
|---------|--------------|--------------------|--------------------|-----------------|
| Storage | 100 mb       | 5 gb               | 20 gb              | Custom          |
| Tables  | 1            | 3                  | 10                 | Custom          |
| Pricing | $0/mo        | $10/mo ($100/year) | $25/mo ($250/year) | Contact [Support](https://support.webhook.site) |

To purchase or provision a Database, go to [Databases](https://webhook.site/control-panel/databases) in Control Panel.

To upgrade a database instance, Contact [Support](https://support.webhook.site).