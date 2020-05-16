# dj-stripe

[![Build Status](https://travis-ci.org/dj-stripe/dj-stripe.svg?branch=master)](https://travis-ci.org/dj-stripe/dj-stripe)

[![Documentation Status](https://readthedocs.org/projects/dj-stripe/badge/)](https://dj-stripe.readthedocs.io/)

Stripe Models for Django.

## Introduction

dj-stripe implements all of the Stripe models, for Django. Set up your
webhook and start receiving model updates. You will then have a copy of
all the Stripe models available in Django models, no API traffic
required\!

The full documentation is available here:
<https://dj-stripe.readthedocs.io/>

## Features

  - Subscriptions
  - Individual charges
  - Stripe Sources
  - Stripe v2 and v3 support
  - Supports SCA regulations, Checkout Sessions, and Payment Intents
  - Tested with Stripe API <span class="title-ref">2019-09-09</span>
    (see <https://dj-stripe.readthedocs.io/en/latest/api_versions.html>
    )

## Requirements

  - Django \>= 2.2
  - Python \>= 3.6
  - Supports Stripe exclusively. See "Similar Libraries" below for other
    solutions.
  - PostgreSQL engine (recommended): \>= 9.4
  - MySQL engine: MariaDB \>= 10.2 or MySQL \>= 5.7

## Similar libraries

  - [dj-paypal](https://github.com/HearthSim/dj-paypal)
    ([PayPal](https://www.paypal.com/))
  - [dj-paddle](https://github.com/dj-paddle/dj-paddle)
    ([Paddle](https://paddle.com/))

## Quickstart

Install dj-stripe:

``` bash
pip install dj-stripe
```

Add `djstripe` to your `INSTALLED_APPS`:

``` python
INSTALLED_APPS =(
    ...
    "djstripe",
    ...
)
```

Add to urls.py:

``` python
path("stripe/", include("djstripe.urls", namespace="djstripe")),
```

Tell Stripe about the webhook (Stripe webhook docs can be found
[here](https://stripe.com/docs/webhooks)) using the full URL of your
endpoint from the urls.py step above (e.g.
`https://example.com/stripe/webhook`).

Add your Stripe keys and set the operating mode:

``` python
STRIPE_LIVE_PUBLIC_KEY = os.environ.get("STRIPE_LIVE_PUBLIC_KEY", "<your publishable key>")
STRIPE_LIVE_SECRET_KEY = os.environ.get("STRIPE_LIVE_SECRET_KEY", "<your secret key>")
STRIPE_TEST_PUBLIC_KEY = os.environ.get("STRIPE_TEST_PUBLIC_KEY", "<your publishable key>")
STRIPE_TEST_SECRET_KEY = os.environ.get("STRIPE_TEST_SECRET_KEY", "<your secret key>")
STRIPE_LIVE_MODE = False  # Change to True in production
DJSTRIPE_WEBHOOK_SECRET = "whsec_xxx"  # Get it from the section in the Stripe dashboard where you added the webhook endpoint
```

Add some payment plans via the Stripe.com dashboard.

Run the commands:

    python manage.py migrate

    python manage.py djstripe_init_customers

    python manage.py djstripe_sync_plans_from_stripe

See <https://dj-stripe.readthedocs.io/en/latest/stripe_elements_js.html>
for notes about usage of the Stripe Elements frontend JS library.

## Running the Tests

Assuming the tests are run against PostgreSQL:

    createdb djstripe
    pip install tox
    tox

# Follows Best Practices

[![Two Scoops of Django](https://twoscoops.smugmug.com/Two-Scoops-Press-Media-Kit/i-C8s5jkn/0/O/favicon-152.png)](https://www.twoscoopspress.org/products/two-scoops-of-django-1-11)

This project follows best practices as espoused in [Two Scoops of Django: Best Practices for Django 1.11](https://twoscoopspress.org/products/two-scoops-of-django-1-11).
