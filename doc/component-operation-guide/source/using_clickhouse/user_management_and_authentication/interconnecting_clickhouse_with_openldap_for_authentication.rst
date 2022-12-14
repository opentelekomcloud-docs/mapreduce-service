:original_name: mrs_01_24109.html

.. _mrs_01_24109:

Interconnecting ClickHouse With OpenLDAP for Authentication
===========================================================

ClickHouse can be interconnected with OpenLDAP. You can manage accounts and permissions in a centralized manner by adding the OpenLDAP server configuration and creating users on ClickHouse. You can use this method to import users from the OpenLDAP server to ClickHouse in batches.

This section applies only to MRS 3.1.0 or later.

Prerequisites
-------------

-  The MRS cluster and ClickHouse instances are running properly, and the ClickHouse client has been installed.
-  OpenLDAP has been installed and is running properly.

Creating a ClickHouse User for Interconnecting with the OpenLDAP Server
-----------------------------------------------------------------------

#. Log in to Manager and choose **Cluster** > **Services** > **ClickHouse**. Click the **Configurations** tab and then **All Configurations**.

#. Choose **ClickHouseServer(Role)** > **Customization**, and add the following OpenLDAP configuration parameters to the **clickhouse-config-customize** configuration item.

   .. table:: **Table 1** OpenLDAP parameters

      +------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
      | Parameter                                      | Description                                                                                                                                | Example Value             |
      +================================================+============================================================================================================================================+===========================+
      | ldap_servers.ldap_server_name.host             | OpenLDAP server host name or IP address. This parameter cannot be empty.                                                                   | localhost                 |
      +------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
      | ldap_servers.ldap_server_name.port             | OpenLDAP server port number.                                                                                                               | 636                       |
      |                                                |                                                                                                                                            |                           |
      |                                                | If **enable_tls** is set to **true**, the default port number is **636**. Otherwise, the default port number is **389**.                   |                           |
      +------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
      | ldap_servers.ldap_server_name.auth_dn_prefix   | Prefix and suffix used to construct the DN to bind to.                                                                                     | uid=                      |
      |                                                |                                                                                                                                            |                           |
      |                                                | The generated DN will be constructed as a string in the following format: **auth_dn_prefix** + **escape(user_name)** + **auth_dn_suffix**. |                           |
      |                                                |                                                                                                                                            |                           |
      |                                                | Use a comma (,) as the first non-space character of **auth_dn_suffix**.                                                                    |                           |
      +------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
      | ldap_servers.ldap_server_name.auth_dn_suffix   |                                                                                                                                            | ,ou=Group,dc=node1,dc=com |
      +------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
      | ldap_servers.ldap_server_name.enable_tls       | A tag to trigger the use of the secure connection to the OpenLDAP server.                                                                  | yes                       |
      |                                                |                                                                                                                                            |                           |
      |                                                | -  Set it to **no** for the plaintext (ldap://) protocol (not recommended).                                                                |                           |
      |                                                | -  Set it to **yes** for the LDAP over SSL/TLS (ldaps://) protocol.                                                                        |                           |
      +------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
      | ldap_servers.ldap_server_name.tls_require_cert | SSL/TLS peer certificate verification behavior.                                                                                            | allow                     |
      |                                                |                                                                                                                                            |                           |
      |                                                | The value can be **never**, **allow**, **try**, or **require**.                                                                            |                           |
      +------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+

   .. note::

      For details about other parameters, see :ref:`<ldap_servers> Parameters <mrs_01_24109__section16259164716419>`.

#. After the configuration is complete, click **Save**. In the displayed dialog box, click **OK**. After the configuration is saved, click **Finish**.

#. On Manager, click **Instance**, select a ClickHouseServer instance, and choose **More** > **Restart Instance**. In the displayed dialog box, enter the password and click **OK**. In the displayed **Restart instance** dialog box, click **OK**. Confirm that the instance is restarted successfully as prompted and click **Finish**.

#. Log in to the ClickHouseServer instance node and go to the **${BIGDATA_HOME}/FusionInsight_ClickHouse\_**\ *Version number*\ **/**\ *x_x*\ **\_ClickHouseServer/etc** directory.

   **cd** **${BIGDATA_HOME}/FusionInsight_ClickHouse\_\*/**\ *x_x*\ \_\ **ClickHouseServer/etc**

#. .. _mrs_01_24109__li111911544142720:

   Run the following command to view the **config.xml** configuration file and check whether the OpenLDAP parameters are configured successfully:

   **cat config.xml**

   |image1|

#. Log in to the node where the ClickHouseServer instance is located as user **root**.

#. .. _mrs_01_24109__li10408141903516:

   Run the following command to obtain the path of the **clickhouse.keytab** file:

   **ls ${BIGDATA_HOME}/FusionInsight_ClickHouse_*/install/FusionInsight-ClickHouse-*/clickhouse/keytab/clickhouse.keytab**

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to go to the ClickHouse client installation directory:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Run the following command to connect to the ClickHouseServer instance:

   -  If Kerberos authentication is enabled for the current cluster, use **clickhouse.keytab** to connect to the ClickHouseServer instance.

      **clickhouse client --host** *IP address of the node where the ClickHouseServer instance is located* **--user clickhouse/hadoop.**\ *<System domain name>* **--password** *clickhouse.keytab path obtained in :ref:`8 <mrs_01_24109__li10408141903516>`* **--port** *ClickHouse port number*

      .. note::

         The default system domain name is **hadoop.com**. Log in to FusionInsight Manager and choose **System** > **Permission** > **Domain and Mutual Trust**. The value of **Local Domain** is the system domain name. Change the letters to lowercase letters when running a command.

   -  If Kerberos authentication is disabled for the current cluster, connect to the ClickHouseServer instance as the **clickhouse** administrator.

      **clickhouse client --host** *IP address of the node where the ClickHouseServer instance is located* **--user clickhouse** **--port** *ClickHouse port number*

#. Create a common user of OpenLDAP.

   Run the following statement to create user **testUser** in cluster **default_cluster** and set **ldap_server** to the OpenLDAP server name in the **<ldap_servers>** tag in :ref:`6 <mrs_01_24109__li111911544142720>`. In this example, the name is **ldap_server_name**.

   **CREATE USER** *testUser* **ON CLUSTER** *default_cluster* **IDENTIFIED WITH ldap_server BY '**\ ldap_server_name\ **';**

   **testUser** indicates an existing username in OpenLDAP. Change it based on the site requirements.

#. Log out of the client, and then log in to the client as the new user to check whether the configuration is successful.

   **exit;**

   **clickhouse client --host** *IP address of the ClickHouseServer instance* **--user** *testUser* **--password** **--port** *ClickHouse port number*

   *Enter the password of testUser.*

.. _mrs_01_24109__section16259164716419:

<ldap_servers> Parameters
-------------------------

-  **host**

   OpenLDAP server host name or IP address. This parameter is mandatory and cannot be empty.

-  **port**

   Port number of the OpenLDAP server. If **enable_tls** is set to **true**, the default value is **636**. Otherwise, the value is **389**.

-  **auth_dn_prefix, auth_dn_suffix**

   Prefix and suffix used to construct the DN to bind to.

   The generated DN will be constructed as a string in the following format: **auth_dn_prefix** + **escape(user_name)** + **auth_dn_suffix**.

   Note that you should use a comma (,) as the first non-space character of **auth_dn_suffix**.

-  **enable_tls**

   A tag to trigger the use of the secure connection to the OpenLDAP server.

   Set it to **no** for the plaintext (ldap://) protocol (not recommended).

   Set it to **yes** for LDAP over SSL/TLS (ldaps://) protocol (recommended and default).

-  **tls_minimum_protocol_version**

   Minimum protocol version of SSL/TLS.

   The value can be **ssl2**, **ssl3**, **tls1.0**, **tls1.1**, or **tls1.2** (default).

-  **tls_require_cert**

   SSL/TLS peer certificate verification behavior.

   The value can be **never**, **allow**, **try**, or **require** (default).

-  **tls_cert_file**

   Certificate file.

-  **tls_key_file**

   Certificate key file.

-  **tls_ca_cert_file**

   CA certificate file.

-  **tls_ca_cert_dir**

   Directory where the CA certificate is stored.

-  **tls_cipher_suite**

   Allowed encryption suite.

.. |image1| image:: /_static/images/en-us_image_0000001296090112.png
