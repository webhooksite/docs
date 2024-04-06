---
title: Install
order: 20
nav_order: 300
---

# Webhook.site Open Source

## About the Open Source version

There are two separate editions of Webhook.site: 

* The code for the completely open-source, MIT-licensed version described on this page is available on [https://github.com/webhooksite/webhook.site](https://github.com/webhooksite/webhook.site), and can be self-hosted using e.g. Docker, is great for testing Webhooks, but doesn't include Webhook.site Pro features like Custom Actions.

* The cloud version of Webhook.site at [https://webhook.site](https://webhook.site) which has more features, some of them requiring a paid subscription.

You can choose to run the Open Source version of Webhook.site either via Docker, or install it on any Web server with PHP7 support. 

## Realtime updates

[laravel-echo-server](https://github.com/tlaverdure/laravel-echo-server) or Pusher can be used to enable realtime updates. Take a look at the `.env.example` to see the environment variables required to configure it.

For `laravel-echo-server`, the app expects socket.io to be available at the `/socket.io` path relative to the index page. This can be done with nginx like so:

```
    location /socket.io {
        proxy_pass http://127.0.0.1:6001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
```

## Installation

### Docker (Recommended)

[The provided Docker Compose file](https://github.com/webhooksite/webhook.site/blob/master/docker-compose.yml) sets up a complete environment that runs the Webhook.site image and all dependencies (Redis, Laravel Echo Server, etc.). Note that if running this in production, you should probably run a Redis server that persists data to disk. The Docker image is also not tuned for large amounts of traffic.

#### Installation Guide

1. Run `docker-compose up`
2. The app will be available on [http://127.0.0.1:8084](http://127.0.0.1:8084).

### Kubernetes

A set of Kubernetes configuration files can be found in the [`kubernetes` subfolder](https://github.com/webhooksite/webhook.site/tree/master/kubernetes). 

#### Installation Guide

Configure the resources, and apply with `kubectl apply -f ./`.

### Web Server

#### Requirements

* PHP 7
* Redis
* Composer
* Web server – e.g. nginx, apache2

DigitalOcean has a guide on [how to configure nginx](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-laravel-application-with-nginx-on-ubuntu-16-04#step-5-—-configuring-nginx).

#### Installation Guide

1. Run the following commands:
   1. `composer install`
   2. `cp .env.example .env` - adjust settings as needed
   3. `php artisan key:generate`
2. Setup virtual host pointing to the `/public` folder. 

