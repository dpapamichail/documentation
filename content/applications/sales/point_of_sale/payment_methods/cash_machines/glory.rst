=====
Glory
=====

**Glory** :doc:`cash machines <../cash_machines>` enable the automation of cash transactions.

.. note::
   The integration with the Glory cash machine currently only supports basic operations, such as
   making payments and checking the current cash counts.

   Operations such as filling and emptying the machine must be performed directly using the cash
   machine interface.

.. _pos/glory/configuration:

Configuration
=============

Cash machine settings
---------------------

.. important::
   This section requires knowledge of the Glory hardware - your Glory integration partner should be
   able to configure these settings for you.

#. Power on the cash machine, which briefly displays its IP address at the bottom of the screen. The
   IP address should be structured as follow: `###.###.#.##` (e.g., `192.168.0.25`). Note it down to
   use later.
#. Navigate to the cash machine homepage by typing its IP address as URL in `HTTPS` (e.g.,
   `https://192.168.0.25`), and log in with your credentials.
#. As long as the certificate is not imported, a warning page is displayed when trying to reach the
   machine homepage. Force the connection by clicking :guilabel:`Advanced` and :guilabel:`Proceed to
   [IP address] (unsafe)`.
#. Go to :guilabel:`Host Configuration` and ensure the :guilabel:`Network` setting is set to
   :guilabel:`MANUAL`, meaning the IP address is static.
#. Go to :guilabel:`SSL Configuration` and scroll down to the :guilabel:`HTTPS Server Setting`
   section.

   #. In parallel, open the terminal and ensure OpenSSL is installed. Type `openssl` and press
      enter. When installed, this command generates a `Help` menu suggesting all available OpenSSL
      commands. Install it if nothing happens.
   #. Then, paste the following command and press `Enter` to generate and download the certificate
      and private key; ensure to replace the demo IP address with your cash machine's.

      .. code-block:: bash

         openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -sha256 -days 3650 -nodes -subj "/CN=192.168.0.25" -addext "subjectAltName = IP:192.168.0.25"

      .. note::
         The self-signed SSL certificate and key pair must use the same static IP address as the
         cash machine.

#. Once the files are generated, upload `cert.pem` as the :guilabel:`Certificate` and `key.pem` as
   the :guilabel:`Private Key`.
#. Go to :guilabel:`WebApp Configuration` a ensure the :guilabel:`Interface` setting is set to
   :guilabel:`Enable`. Then, adjust some settings depending on the POS setup:

   - If multiple POS are connected to the same cash machine, set the following:

      - Go to :guilabel:`App Configuration`, scroll down to the :guilabel:`SOAP IF Setting` and
        ensure :guilabel:`Session mode` and :guilabel:`Occupy mode` are both set to
        :guilabel:`Enable`
   - If a dedicated user has been setup on the cash machine for Odoo, also set the following:

      - Go to :guilabel:`App Configuration`, scroll down to the :guilabel:`SOAP IF Setting` and
        :guilabel:`Enable` the :guilabel:`User check` setting.
#. Restart the cash machine to apply the new settings.

Payment method
--------------

#. Install the :ref:`POS Glory Cash Machines module <general/install>`.
#. :doc:`Associate a cash payment method <../../payment_methods>`:

   - Go to :menuselection:`Point of Sale --> Configuration --> Payment Methods`. Create a new
     :guilabel:`Cash` payment method, or modify an existing one for the desired POS.
   - Select :guilabel:`Cash Machine (Glory)` in the :guilabel:`Integration` field.
   - Fill in the :guilabel:`Cash Machine IP` field with the the cash machine IP address.
   - If the cash machine was configured to use :guilabel:`User check` in the previous section,
     fill in the :guilabel:`Cash Machine Username` and :guilabel:`Cash Machine Password`.

Certificate settings
--------------------

At this point the cash machine payment method is configured, but for it to work properly the HTTPS
certificate that was generated earlier must be added to the configuration of the machine that will
be using the Point of Sale. You can refer to the **Export** and **Import** sections of the
:ref:`ePOS documentation <epos_ssc/instructions>` for specific instructions.
