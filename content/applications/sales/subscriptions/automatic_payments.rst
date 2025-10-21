====================================
Subscriptions and automatic payments
====================================

By default, the **Subscriptions** app will automatically generate quotations and invoices for
customers, but it can also support automatic payments. Setting up automatic payments requires
additional configuration, including choosing an automatic payment provider and either setting up a
customer portal or an eCommerce website. Here's an overview of how to get started.

Choosing an automatic payment provider
======================================

Setting up automatic recurring payments requires using a payment provider that supports
:ref:`tokenization <payment_providers/tokenization>`, which lets customers save their payment
details with a chosen provider. The following payment providers support tokenization:

- Adyen
- Authorize.net
- Flutterwave
- Razorpay
- Stripe
- Worldline
- Xendit

Once a payment provider has been selected, an account must be created on their website and API
credentials must be requested. The API credentials allow Odoo to communicate with the payment
provider's services. Once the API credentials have been generated, payment providers can be
:ref:`enabled <payment_providers/add_new>` and made available to customers in either the Accounting
or Sales apps.

Setting up customer portals and eCommerce websites
==================================================

Once you've set up an automatic payment provider, customers can sign up for automatic payments
through an eCommerce website or through an online customer portal. An eCommerce website allows
customers to view the product catalog and make purchases directly through the website. Granting
customers portal access lets them view their quotations and sales orders, pay invoices, manage
subscriptions, and more.

.. important::
   Building an eCommerce website requires the :doc:`Website <../../websites/website>` app.

Contract in exception
=====================

On rare occasions, automatic payments can fail to register properly, which results in a
:guilabel:`Payment Failure` tag on the sales order and the :guilabel:`Contract in exception`
checkbox being automatically ticked in the :guilabel:`Subscription` section of the sales order's
:guilabel:`Other Info` tab.

Being marked :guilabel:`Contract in exception` prevents scheduled actions from running, which
keeps the system from accidentally double-charging the customer if the automatic payment actually
went through. Because the status of the payment failed to register with the system, users must
manually check if the payment has been made before automatic payments and other scheduled actions
can resume.

To do this, navigate to :menuselection:`Subscriptions app --> Subscriptions --> Quotations`.
Click into the desired subscription, then check the Chatter to see if the payment was made.

If the payment *was not* made, first enter :doc:`developer mode <../../general/developer_mode>`.
Then, click the :guilabel:`Other Info` tab, and untick the checkbox next to :guilabel:`Contract
in exception`. Reload the sales order and confirm that the :guilabel:`Payment Failure` tag is
gone.

If the payment *was* made, a new invoice must be made and posted manually. This automatically
updates the next invoice date of the subscription. Once the invoice is created, enter
:doc:`developer mode <../../general/developer_mode>` and navigate to the new sales order. Click
the :guilabel:`Other Info` tab, and untick the checkbox next to :guilabel:`Contract in
exception`. Reload the sales order and confirm that the :guilabel:`Payment Failure` tag is gone.

.. figure:: renewals/contract-in-exception.png
   :alt: The contract in exception option selected with the payment failure tag shown.

The :guilabel:`Contract in exception` option selected with the :guilabel:`Payment Failure` tag
shown.

In both cases, once the :guilabel:`Contract in exception` checkbox is no longer ticked, Odoo
handles renewals automatically again. If the subscription remains in :guilabel:`Payment Failure`,
it is ignored by Odoo until the sales order is closed.

.. seealso::
  - :doc:`../../finance/payment_providers`
  - :doc:`../../general/users/portal`
