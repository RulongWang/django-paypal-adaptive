Django Paypal Adaptive
===

[![Build Status](https://travis-ci.org/FundedByMe/django-paypal-adaptive.png?branch=master)](https://travis-ci.org/FundedByMe/django-paypal-adaptive)
[![Downloads](https://pypip.in/v/django-paypal-adaptive/badge.png)](https://pypi.python.org/pypi/django-paypal-adaptive)

The API and the modules in this repository might be subject to smaller
changes and not all Paypal Adaptive endpoints are covered. FundedByMe
will help make the covering of the Pay, Preapproval and IPN endpoints as good
as possible but we might not have the resources to perfect this project.

Making Preapprovals and using them to create Payments is fully supported
together with Paypal's IPN push API. Please reach out to us if you're
interested in helping maintaining this package.

Installation
============

Install package from PyPI:

    pip install django-paypal-adaptive
    
Add to your project's `INSTALLED_APPS` setting:

    INSTALLED_APPS = (
        …
        'paypaladaptive',
    )

Sync the database:
    
    $ python manage.py syncdb
    
Or if you're using __South__ you might want to add an initial migration for future changes:
    
    $ python manage.py schemamigration paypaladaptive --initial
    $ python manage.py syncdb --migrate

Models
===

Payment
---

__Status__

Possible values are:

    'new'  # Payment only exists locally
    'created'  # Payment exists on Paypal
    'error'  # Something along the process has gone wrong. Check status_detail
             # for more info.
    'returned'  # User has returned via the Payment return_url
    'completed'  # The Payment is complete
    'refunded'  # The Payment is refunded
    'canceled'  # The Payment has been canceled

Preapproval
---

__Status__

Possible values are:

    'new'  # Preapproval only exists locally — not known to Paypal
    'created'  # Preapproval has been saved on Paypal
    'error'  # Something has gone wrong, check status_detail for more info
    'returned'  # User has returned via the Preapproval return_url
    'approved'  # Preapproval is completed — ready to be used in payment
    'canceled'  # Preapproval has been canceled
    'used'  # Preapproval has been used in payment

The status describes

Settings
========

django.conf.settings.PAYPAL_APPLICATION_ID
------------------------------------------

Your Paypal application ID. Will default to `APP-80W284485P519543T` if 
`DEBUG` is set to `True`.

django.conf.settings.PAYPAL_USERID
----------------------------------

Paypal User ID

django.conf.settings.PAYPAL_PASSWORD
----------------------------------

Paypal password

django.conf.settings.PAYPAL_SIGNATURE
----------------------------------

Paypal signature

django.conf.settings.PAYPAL_EMAIL
----------------------------------

Paypal Email

django.conf.settings.DEFAULT_CURRENCY
----------------------------------

Used by python-money, will default to USD

django.conf.settings.PAYPAL_DECIMAL_PLACES
------------------------------------------

Number of decimal places assigned to the MoneyField (used by Payment and
Preapproval models).

django.conf.settings.PAYPAL_MAX_DIGITS
--------------------------------------

Max number of digits assigned to the Moneyfield (used by Payment and Preapproval
models).

django.conf.settings.PAYPAL_TEST_WITH_MOCK
-----------------------------------------

Set whether tests should be run with built-in mocking responses and requests
or if the testing should spawn requests that hits Paypal's APIs directly.
Defaults to True. Override in your settings file like this:

    PAYPAL_TEST_WITH_MOCK = False

Run tests
=========

To run the tests, first install the test requirements:

    $ [sudo] pip install -r requirements_test.txt --use-mirrors
    
The script that runs the tests simulates an installed Django app and is located
in `paypaladaptive-testrunner/runtests.py`. Execute it like this:

    $ python paypaladaptive-testrunner/runtests.py paypaladaptive paypaladaptive

Contributing
============

Do you want to contribute? We'll gladly accept pull requests as long as your code
is well tested and contributes to the goal of this library.

License
=======

<a rel="license" href="http://creativecommons.org/licenses/by/3.0/deed.sv"><img alt="Creative Commons-licens" style="border-width:0" src="http://i.creativecommons.org/l/by/3.0/80x15.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">django-paypal-adaptive</span> av <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/FundedByMe/django-paypal-adaptive" property="cc:attributionName" rel="cc:attributionURL">FundedByMe</a> är licensierad under en <a rel="license" href="http://creativecommons.org/licenses/by/3.0/deed.sv">Creative Commons Erkännande 3.0 Unported licens</a>.<br />Based on a work at <a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/gmcguire/django-paypal-adaptive" rel="dct:source">https://github.com/gmcguire/django-paypal-adaptive</a>.
