=======
smspool
=======


.. image:: https://img.shields.io/pypi/v/smspool.svg
        :target: https://pypi.python.org/pypi/smspool

.. image:: https://img.shields.io/travis/AG4lyf/smspool.svg
        :target: https://travis-ci.com/AG4lyf/smspool

.. image:: https://readthedocs.org/projects/smspool/badge/?version=latest
        :target: https://smspool.readthedocs.io/en/latest/?version=latest
        :alt: Documentation Status


.. image:: https://pyup.io/repos/github/AG4lyf/smspool/shield.svg
     :target: https://pyup.io/repos/github/AG4lyf/smspool/
     :alt: Updates



A simple Python wrapper for the `smspool.net <https://www.smspool.net/>`__ API — a service
that rents temporary phone numbers for receiving SMS verification codes. The library wraps
the REST endpoints in a clean ``smspool`` client class.


* Free software: MIT license
* Documentation: https://smspool.readthedocs.io.


Install
-------

.. code-block:: bash

    pip install smspool


Quick start
-----------

.. code-block:: python

    from smspool import smspool

    client = smspool("YOUR_API_KEY")

    # Account / catalog
    client.get_balance()
    client.get_countries()
    client.get_services(country="United States")
    client.get_service_price(country, service)

    # Buy a number and receive a code
    order = client.purchase_sms(country, service)
    client.check_sms(order_id)        # poll until the code arrives
    client.resend_sms(order_id)
    client.cancel_sms(order_id)

    # Long-term rentals
    rental = client.purchase_rental(...)
    client.get_rental_message(rental_id)
    client.extend_rental(rental_id)
    client.refund_rental(rental_id)


Available methods
-----------------

**SMS:** ``get_countries``, ``get_services``, ``get_balance``, ``get_order_history``,
``get_active_orders``, ``get_service_price``, ``get_suggested_countries``,
``purchase_sms``, ``check_sms``, ``resend_sms``, ``cancel_sms``, ``archive_sms_orders``,
``carrier_lookup``.

**Rentals:** ``get_rentals``, ``purchase_rental``, ``get_rental_message``,
``get_rental_status``, ``refund_rental``, ``extend_rental``.

Each call returns the parsed JSON response, or raises an exception with the API's error text
on a non-200 status.

