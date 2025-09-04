=================
Customer accounts
=================

Using customer accounts for an ecommerce shop enables you to :ref:`manage customers
<ecommerce/customer_accounts/account-creation>`, :ref:`control access to the shop
<ecommerce/customer_accounts/shop-access>`, the :ref:`checkout
<ecommerce/customer_accounts/checkout-access>` or the :ref:`customer portal <portal/access>`,
and support both B2B and B2C operations.

After logging in, customers can access their documents by clicking their username in the top-right
corner of the screen selecting :guilabel:`My Account`. From there, they can view all their
documents in one place, such as :guilabel:`quotations`, :guilabel:`orders`,
:guilabel:`invoices` and more.

.. image:: customer_accounts/account-log.png
   :alt: Customer account access

.. tip::
   Similarly to the rest of the website, the customer account page can be customized with building
   blocks and other features through the :doc:`website builder <../website/web_design>`.

.. _ecommerce/customer_accounts/account-creation:

Customer account creation
=========================

You can choose whether customer accounts and document access are available to everyone or restricted
to invited users only. To do so, go to :menuselection:`Website --> Configuration --> Settings`,
then scroll down to the :guilabel:`Privacy` section. Under :guilabel:`Customer Account`, select one
of the following options:

- :guilabel:`On invitation`: Customers can only create an account if the website owner sends them
  an invitation.
- :guilabel:`Free sign up`: Every website visitor can create an account and sign in. They will
  get access to the :doc:`portal <../../general/users/portal>` by default.

If account creation is restricted to invited customers only, go to :menuselection:`Website -->
eCommerce --> Customers`, switch to the :guilabel:`List` view, and select the customers who
should gain access to the :doc:`portal <../../general/users/portal>`.
Click the :icon:`fa-cog` :guilabel:`Actions` button, then :guilabel:`Grant portal access`.
In the :guilabel:`Portal Access Management`, review the selected customers and click
:guilabel:`Grant Access` to confirm.

Once done, the relevant customers receive an email confirming their account creation, including
instructions on setting a password and activating their account.

.. note::
   - When selecting the :guilabel:`Free sign up`, a clickable :guilabel:`Don't have an account?`
     link appears under the login form on the website.
   - The :guilabel:`On invitation` option is especially useful for B2B businesses that prefer
     to keep prices hidden on the website. Only customers who have been granted portal access are
     able to view their pricing.

.. tip::
   It is possible to configure a website form with a :guilabel:`Create a Customer` :ref:`action
   <website/building_blocks/form>` to automatically create a customer record in the backend when
   filled in.

Access restriction
==================

Once a customer account is created, it is still possible to adjust the access rights
either globally or for individual users:

- :ref:`Revoke access or re-invite a customer <portal/access>`
  using the related buttons in the :guilabel:`Portal Access Management` pop-up.
- Restrict :ref:`access to the shop <ecommerce/customer_accounts/shop-access>`;
- Decide whether customers need to create an account to :ref:`complete the checkout
  <ecommerce/customer_accounts/checkout-access>`.

.. note::
   Users can only have one :doc:`portal access <../../general/users/portal>` per email.

.. tip::
   It is also possible to define the types of documents customers have access to. To do so, open
   the :doc:`website builder <../website/web_design>`, then enable or disable access to specific
   documents as needed.

.. _ecommerce/customer_accounts/shop-access:

Shop access
-----------

To restrict access to the entire online shop, go to :menuselection:`Website
--> Configuration --> Settings`, scroll to :guilabel:`Privacy` and under :guilabel:`Ecommerce
Access`, restrict shop access to :guilabel:`All users` or :guilabel:`Logged in users`.

.. note::
   Customers with access to the portal also have access to the shop. Without portal access,
   customers are not able to log in.

.. tip::
   To restrict access to the shop's pricing, use :ref:`pricelists <ecommerce/prices/pricelists>`
   with :ref:`country groups <ecommerce/prices/country-groups>`.

.. _ecommerce/customer_accounts/checkout-access:

Checkout access
---------------

To allow customers to checkout as guests or force them to sign in/create an account, go to
:menuselection:`Website --> Configuration --> Settings`, scroll down to the :guilabel:`Shop -
Checkout Process` section, and configure the :guilabel:`Sign in/up at checkout` setting. The
following options are available:

- :guilabel:`Optional`: Customers can check out as guests and register later via the order
  confirmation email to track their order.
- :guilabel:`Disabled (buy as guest)`: Customers can checkout as guests without creating an account.
- :guilabel:`Mandatory (no guest checkout)`: Customers must sign in or create an account at the
  :ref:`Review Order <ecommerce/checkout/review_order>` step to complete their purchase.

.. note::
   - Settings are specific to each website, allowing you to configure a B2C website with guest
     checkout and a B2B website that requires customers to sign in.
   - To use the :ref:`wishlist <ecommerce/products/wishlists>` feature, customers must
     create an account to save their favorite items for later.

Multi-website account
=====================

When managing multiple websites, it is possible to make customer accounts available across *all*
websites, allowing each customer to use a single account. To do so, go to :menuselection:`Website
--> Configuration --> Settings`, in the :guilabel:` Privacy` section, enable :guilabel:`Shared
Customer Accounts` option.

.. note::
   When operating both B2B and B2C online shops, it's recommended to use separate websites for each
   business model.
