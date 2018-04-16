# Patreon PHP Example

An example of implementing the [Patreon PHP](https://github.com/1f991/patreon-php)
library to create a website that displays all of the Patrons of a Patreon
Campaign and automatically updates when a Pledge is created, updated or deleted.

You can find a live version of this example at
[patreon.1f991.com](https://patreon.1f991.com) where you can pledge to the test
Campaign to see yourself added in realtime, and you can follow the tutorial
below to set up this example with your own Campaign.

## Requirements

* A Web Server (such as [Wamp](http://www.wampserver.com/en/) or [MAMP](https://www.mamp.info/en/) if you're developing on your own computer)
* PHP >=7.2.0
* [Composer](https://getcomposer.org/download/)
* A [Patreon](https://patreon.com) Campaign

## Getting Started

### Patreon Client

First you will need to create a Patreon API Client to obtain a Patreon
`Creator's Access Token`.

1. Visit [`Clients & API Keys`](https://www.patreon.com/portal/registration/register-clients)
  in the Patreon Platform Portal
2. Click `Create Client`
3. Fill out the fields and save — you don't need to enter real data
4. After your client is created you'll find your `Creator's Access Token` by
  clicking the arrow next to your Client

### Install Example Project

1. Open your terminal
2. Clone this project from GitHub into a directory called `patreon`:

```bash
git clone https://github.com/1f991/patreon-php-example patreon
```

3. Change into the `patreon` directory:

```bash
cd patreon
```

4. Install the dependencies with Composer:

```bash
composer install
```

5. Open the newly created `.env` file and add your `Creator's Access Token`:

```bash
PATREON_ACCESS_TOKEN="your-creators-access-token-here"
```

![Cloning Demo](https://1f991.github.io/patreon-php-example/patreon-php-example-clone.gif)

You're now ready to visit your new Patreon PHP example website!

### Accepting Logins

You will need your Patreon API Client's `Client ID`, `Client Secret` and a
Redirect URI to enable OAuth log ins.

1. Return to  [`Clients & API Keys`](https://www.patreon.com/portal/registration/register-clients)
  in the Patreon Platform Portal
2. Click "Edit Client" and in `Redirect URIs` add the address to your Patreon
  PHP example website with `/login.php` at the end. For example if your website
  is `patreon.localhost` you would enter `http://patreon.localhost/login.php`
3. Click "Update Client"
4. Copy and paste the `Client ID`, `Client Secret` and `Redirect URI` values
  into your `.env` file, for example:

```bash
PATREON_ACCESS_TOKEN="your-creators-access-token-here"
PATREON_WEBHOOK_SECRET=""
PATREON_CLIENT_ID="your-client-id-here"
PATREON_CLIENT_SECRET="your-client-secret-here"
PATREON_REDIRECT_URI="http://patreon.localhost/login.php"
```

Visit your Patreon PHP example website again and click "log in if you're already
a patron →" to confirm everything is working as expected.

### Setting up Webhooks

Your website will need to be accessible online for this step. You can use
[ngrok](https://ngrok.com) to expose a local website to the open internet during
development.

1. Visit [Register Webhooks](https://www.patreon.com/portal/registration/register-webhooks)
  in the Patreon Platform Portal.
2. Paste the URL to your Patreon PHP website and append `/webhook.php`, e.g:

```
https://patreon.1f991.com/webhook.php
```

3. Copy the Secret that is generated by Patreon
4. Open `.env` and add your `PATREON_WEBHOOK_SECRET`:

```bash
PATREON_ACCESS_TOKEN="your-creators-access-token-here"
PATREON_WEBHOOK_SECRET="your-patreon-webhook-secret"
```

You're all set! Patreon will now notify your website every time there's a new
pledge, a pledge is deleted or a pledge is updated, and your website will update
the local database.

You can test out your webhook integration with the helpful Patreon event tests.

1. Next to the `Create Pledge` event click `Send test`
2. Click `Send Test` again — you should see Patreon display `Test Response ---
  Status code: 200`
3. Visit your website again, you should see a new pledge!
4. Next to the `Delete Pledge` event click `Send Test` (and then `Send Test` again)
5. Visit your website again, the test pledge is gone!

## Help

Please visit the [Patreon Developers forum](https://patreondevelopers.com) for
any support.

## Security Vulnerabilities

Please reach out to Samuel Ryan via email (sryan@1f991.com) to report any security
concerns you may have with this example project. Although this project
is intended as an example, it is probable some of the code will be copy and pasted
into production, therefore it is important the example code be free of vulnerabilities. Acknowledgement will be provided within 24 hours.
