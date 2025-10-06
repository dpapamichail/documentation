:code-column:
:custom-css: valuation.css
:custom-js: misc.js,valuation-data.js,valuation-journal.js,valuation-accounting.js

=====================
Valuation cheat sheet
=====================

.. rst-class:: full-width

   .. important::
      This documentation is for Odoo 19 or later.
      :ref:`Discover why we changed. <changes-in-19>`


Costing Methods
===============

Odoo supports 3 costing methods configured in accounting's settings and, optionally,
the product's category.

.. rst-class:: alternatives doc-aside

Standard Cost: fixed unit cost, updated manually
  .. list-table::
    :widths: 28 18 18 18 18
    :header-rows: 1
    :stub-columns: 1
    :class: values-table

    * - Operation
      - Unit Cost
      - Qty On Hand
      - Delta Value
      - Inventory Value
    * -
      - $10
      - 0
      -
      - $0
    * - Receive 8 @$10
      - $10
      - 8
      - +8×$10
      - $80
    * - Receive 4 @$16
      - $10
      - 12
      - +4×$10
      - $120
    * - Deliver 10
      - $10
      - 2
      - | -10×$10
        |
      - $20
    * - Receive 2 @$9
      - $10
      - 4
      - +2×$10
      - $40

Average Cost: weighted average of all units
  .. list-table::
    :widths: 28 18 18 18 18
    :header-rows: 1
    :stub-columns: 1
    :class: values-table

    * - Operation
      - Unit Cost
      - Qty On Hand
      - Delta Value
      - Inventory Value
    * -
      - $0
      - 0
      -
      - $0
    * - Receive 8 @$10
      - $10
      - 8
      - +8×$10
      - $80
    * - Receive 4 @$16
      - $12
      - 12
      - +4×$16
      - $144
    * - Deliver 10
      - $12
      - 2
      - | -10×$12
        |
      - $24
    * - Receive 2 @$6
      - $9
      - 4
      - +2×$6
      - $36

FIFO: First In, First Out
  .. list-table::
    :widths: 28 18 18 18 18
    :header-rows: 1
    :stub-columns: 1
    :class: values-table

    * - Operation
      - Unit Cost
      - Qty On Hand
      - Delta Value
      - Inventory Value
    * -
      - $0
      - 0
      -
      - $0
    * - Receive 8 @$10
      - $10
      - 8
      - +8×$10
      - $80
    * - Receive 4 @$16
      - $12
      - 12
      - +4×$16
      - $144
    * - Deliver 10
      - $16
      - 2
      - | -8×$10
        | -2×$16
      - $32
    * - Receive 2 @$6
      - $11
      - 4
      - +2×$6
      - $44


.. rst-class:: alternatives-note

   .. note:: Removal strategies also support :abbr:`LIFO (Last In, First Out)` and
      :abbr:`FEFO (First Expiry, First Out)`, but they only impact which product is first picked, not
      the valuation method. For example, you can pick using LIFO, but using Average Cost for valuation,
      as LIFO is not allowed by :abbr:`IFRS (International Financial Reporting Standards)`.


Inventory vs Accounting
=======================

.. rst-class:: inventory-app-paragraph

   :doc:`The inventory app </applications/inventory_and_mrp/inventory>` keeps track of the inventory
   value in real time as you **receive and deliver goods**. The reporting menu allows analysing
   inventory on hand and values per company, location, product, etc.

.. rst-class:: accounting-app-paragraph

   :doc:`The accounting app </applications/finance/accounting>` updates accounts when you receive
   **invoices or bills**. Even though receipts and invoices differ, it’s not practical for
   accountants to post journal entries for every inventory movement. So, they post a closing entry
   to account for the difference between what has been invoiced and received/delivered. This closing
   process happens usually once a year for SMEs, or once a month for larger companies.

.. role:: good
.. role:: meh
.. role:: bad

.. h:div:: feature-table doc-aside

  +------------------+------------+-----------+
  |                  | Accounting | Inventory |
  +==================+============+===========+
  | Purchase Order   | :meh:`/`   | :meh:`/`  |
  +------------------+------------+-----------+
  | Receipt          | :meh:`/`   | :good:`✓` |
  +------------------+------------+-----------+
  | Vendor Bill      | :good:`✓`  | :meh:`/`  |
  +------------------+------------+-----------+
  | Sales Order      | :meh:`/`   | :meh:`/`  |
  +------------------+------------+-----------+
  | Customer Invoice | :good:`✓`  | :meh:`/`  |
  +------------------+------------+-----------+
  | Delivery         | :meh:`/`   | :good:`✓` |
  +------------------+------------+-----------+
  | Closing Entry    | :good:`✓`  | :meh:`/`  |
  +------------------+------------+-----------+


Accounting Methods
==================

There are two accounting practices on how to maintain your accounts:

**Periodic:** Post vendor bills as expenses by nature, and update stock valuation in the closing
entry by reducing expenses (stock variation). It’s the best practice in Europe.

**Perpetual:** Post vendor bills as assets (stock valuation), report expenses when goods are sold
(cost of goods sold). It’s the best practice in countries that follow Anglo-Saxon accounting, like
the USA and India.

.. role:: yellow
.. role:: green
.. role:: blue
.. role:: darkblue
.. role:: purple
.. role:: washed
.. role:: washed-green
  :class: washed green
.. role:: washed-darkblue
  :class: washed darkblue
.. role:: washed-purple
  :class: washed purple

* :purple:`Stock Account` on the product's category
* :yellow:`Stock Variation` on the stock account
* :blue:`Expense/Cost of Goods Sold` on the product/category
* :green:`Inventory Adjustment` on the Inventory Loss location
  (optional, recommended for Anglo-Saxon accounting)
* :darkblue:`Expense` on the stock account
  (for perpetual Continental accounting only)

.. h:div:: doc-aside

  .. list-table::
    :stub-columns: 1
    :header-rows: 1
    :class: config-table

    * -
      - EU Periodic
      - EU Perpetual
      - US Periodic
      - US Perpetual
    * - ADJUSTMENT
      -
      - :purple:`Stock`
      -
      - :purple:`Stock`
    * -
      -
      - :green:`LOSS`
      -
      - :green:`Shrinkage`
    * -
      -
      -
      -
      -
    * - BILL
      - :blue:`Expense`
      - :purple:`Stock`
      - :blue:`COGS`
      - :purple:`Stock`
    * -
      - :washed:`Payable`
      - :washed:`Payable`
      - :washed:`Payable`
      - :washed:`Payable`
    * -
      -
      -
      -
      -
    * - INVOICE
      -
      - :blue:`Expense`
      -
      - :blue:`COGS`
    * -
      -
      - :purple:`Stock`
      -
      - :purple:`Stock`
    * -
      - :washed:`Income`
      - :washed:`Income`
      - :washed:`Income`
      - :washed:`Income`
    * -
      - :washed:`Receivable`
      - :washed:`Receivable`
      - :washed:`Receivable`
      - :washed:`Receivable`
    * -
      -
      -
      -
      -
    * - Closing
      - :purple:`Stock`
      - :washed-purple:`Stock`
      - :purple:`Stock`
      - :washed-purple:`Stock`
    * - [#closing1]_
      - :yellow:`Variation`
      - :washed-darkblue:`Expense`
      - :yellow:`Variation`
      - :yellow:`Variation`
    * - [#closing2]_
      - :washed-green:`LOSS`
      -
      - :washed-green:`Shrinkage`
      -
    * - [#closing3]_
      -
      - :yellow:`Variation`
      -
      -
    * -
      -
      - :darkblue:`Expense`
      -
      -

  .. [#closing1] Inventory valuation - Accounting valuation

  .. [#closing2] Inventory valuation lost,
     only if an account is set on the loss location

  .. [#closing3] Accounting valuation end of period -
     Valuation beginning of period


.. _accounting-entries:

Accounting Entries
==================

.. h:div:: accounting-entries doc-aside

   .. placeholder


.. _journal-entries:

Journal Entries Configuration
=============================


.. h:div:: journal-entries doc-aside

    .. placeholder


Reporting
=========

In Inventory
------------

Open :menuselection:`Reporting --> Stock` to view your current inventory level and valuation for
each product, or to review historical data as of a previous date.

.. h:div:: doc-aside

  .. image:: cheat_sheet/valuation-stock.png


Unit cost
~~~~~~~~~

You can click on :guilabel:`Unit Cost` to check all existing updates and their origins. In
:abbr:`AVCO (Average Cost)` this allows you to understand how the currently used value was
calculated.

.. h:div:: doc-aside

  .. image:: cheat_sheet/unit-cost.png


Total value
~~~~~~~~~~~

By opening :guilabel:`Total Value`, you can see all incoming quantities for which you still have a
remaining quantity and the value used for their valuation. In AVCO or standard cost, the used value
is always the current average unit cost. In FIFO, remaining units from each previous incoming move
keep their own individual valuation.

In FIFO or AVCO remaining quantities from a previous incoming move can have their value adjusted if
necessary.

.. image:: cheat_sheet/total-value.png
   :scale: 90%

.. h:div:: doc-aside

  .. image:: cheat_sheet/total-value2.png


In Accounting
-------------

Open :menuselection:`Review --> Inventory Valuation` to have a look at the difference between the
accounting stock value and the current inventory value recorded thanks to the incoming moves with a
remaining quantity.

Click on :guilabel:`Generate Entry` to get a new accounting entry to review and post.

Open
:menuselection:`Review --> Invoices not received, Invoices to be issued, Prepaid expenses and Deferred Revenues`
to easily record these entries.

With Anglo-Saxon perpetual accounting, this will also help to distribute recorded Inventory
Variations to accounts such as Bill to Receive/:abbr:`GRNI (Goods Received Not Invoiced)` or
:abbr:`COGS (Cost of Goods Sold)` as shown in the :ref:`Accounting Entries <accounting-entries>`
and :ref:`Journal Entries Configuration <journal-entries>` sections.

.. h:div:: doc-aside

  .. image:: cheat_sheet/valuation-accounting.png


.. _changes-in-19:

Changes in Odoo 19
==================

Before Odoo 19, the Perpetual accounting method was implemented by posting real-time accounting
entries at each stock movement. That created a lot of journal items in accounting, which was an
issue for performance, general ledger clarity and auditability.

Since Odoo 19, the Perpetual method impacts the stock valuation account at the invoice level. The
closing entry is then used to manage bills to receive, invoices to issue, deferred revenues, prepaid
expenses, and other gaps between inventory values and accounting ones.

.. h:div:: feature-table doc-aside

  +-----------------------+--------------------------------+--------------------------------+
  |                       | Odoo 18                        | Odoo 19                        |
  +=======================+================================+================================+
  | Periodic Continental  | :meh:`Manual closing`          | :good:`Automated closing`      |
  +-----------------------+--------------------------------+--------------------------------+
  | Periodic Anglo-Saxon  | :bad:`Not supported`           | :good:`Fully supported`        |
  +-----------------------+--------------------------------+--------------------------------+
  | Perpetual Continental | :meh:`Manual closing`          | :good:`✓`                      |
  +-----------------------+--------------------------------+--------------------------------+
  | Perpetual Anglo-Saxon | :meh:`Manual closing`          | :good:`✓`                      |
  +-----------------------+--------------------------------+--------------------------------+
  | Accounting valuation  | :meh:`Requires inventory`      | :good:`Accounting only`        |
  +-----------------------+--------------------------------+--------------------------------+
  | Perpetual Entries     | :good:`Invoices + every moves` | :good:`Invoices + one closing` |
  +-----------------------+--------------------------------+--------------------------------+
  | Invoices to issue     | :bad:`✗`                       | :good:`✓`                      |
  +-----------------------+--------------------------------+--------------------------------+
  | Prepaid expenses      | :bad:`✗`                       | :good:`✓`                      |
  +-----------------------+--------------------------------+--------------------------------+
  | Bills to receive      | :bad:`✗`                       | :good:`✓`                      |
  +-----------------------+--------------------------------+--------------------------------+
  | Deferred revenues     | :bad:`✗`                       | :good:`✓`                      |
  +-----------------------+--------------------------------+--------------------------------+
  | Performance           | :bad:`Slower`                  | :good:`Faster`                 |
  +-----------------------+--------------------------------+--------------------------------+
  | General ledger        | :good:`More journal entries`   | :good:`Fewer journal entries`  |
  +-----------------------+--------------------------------+--------------------------------+
