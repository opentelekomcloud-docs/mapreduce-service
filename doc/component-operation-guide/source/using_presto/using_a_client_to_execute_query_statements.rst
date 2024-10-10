:original_name: mrs_01_0434.html

.. _mrs_01_0434:

Using a Client to Execute Query Statements
==========================================

You can perform an interactive query on an MRS cluster client. For clusters with Kerberos authentication enabled, users who submit topologies must belong to the **presto** group.

The Presto component of MRS 3.x does not support Kerberos authentication.

Prerequisites
-------------

-  The password of user **admin** has been obtained. The password of user **admin** is specified by the user during MRS cluster creation.
-  The client has been updated.
-  The Presto client has been manually installed for MRS 3.\ *x* clusters.

Procedure
---------

#. .. _mrs_01_0434__li17987144152514:

   For clusters with Kerberos authentication enabled, log in to MRS Manager and create a role with the **Hive Admin Privilege** permission.

#. .. _mrs_01_0434__li9368161132311:

   Create a user that belongs to the **Presto** and **Hive** groups, bind the role created in :ref:`1 <mrs_01_0434__li17987144152514>` to the user, and download the user authentication file.

#. .. _mrs_01_0434__li861292619304:

   Upload the downloaded **user.keytab** and **krb5.conf** files to the node where the MRS client resides.

   .. note::

      For clusters with Kerberos authentication enabled, :ref:`2 <mrs_01_0434__li9368161132311>` to :ref:`3 <mrs_01_0434__li861292619304>` must be performed. For normal clusters, start from :ref:`4 <mrs_01_0434__l6bafa992ef354ebc8c1e16387160ae24>`.

#. .. _mrs_01_0434__l6bafa992ef354ebc8c1e16387160ae24:

   Prepare a client based on service conditions and log in to the node where the client is installed.

   For example, if you have updated the client on the Master2 node, log in to the Master2 node to use the client.

#. Run the following command to switch the user:

   **sudo su - omm**

#. Run the following command to switch to the client directory, for example, **/opt/client**.

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. .. _mrs_01_0434__li15202527183812:

   Connect to the Presto Server. The following provides two client connection methods based on the client type.

   -  Using the client provided by MRS

      -  For clusters with Kerberos authentication disabled, run the following command to connect to the Presto Server of the cluster:

         **presto_cli.sh**

      -  For clusters with Kerberos authentication disabled, run the following command to connect to the Presto Server of other clusters. In the command, **ip** indicates the floating IP address of the cluster Presto Server, which can be obtained by searching for **PRESTO_COORDINATOR_FLOAT_IP** in the Presto configuration items. **port** indicates the Presto Server port number and is set to **7520** by default.

         **presto_cli.sh --server http://ip:port**

      -  For clusters with Kerberos authentication enabled, run the following command to connect to the Presto Server of the cluster:

         **presto_cli.sh --krb5-config-path krb5.conf file path --krb5-principal User's principal --krb5-keytab-path user.keytab file path --user presto username**

      -  For clusters with Kerberos authentication enabled, run the following command to connect to the Presto Server of other clusters. In the command, **ip** indicates the floating IP address of the cluster Presto Server, which can be obtained by searching for **PRESTO_COORDINATOR_FLOAT_IP** in the Presto configuration items. **port** indicates the Presto Server port number and is set to **7521** by default.

         **presto_cli.sh --krb5-config-path krb5.conf file path --krb5-principal User's principal --krb5-keytab-path user.keytab file path --server https://ip:port --krb5-remote-service-name Presto Server name**

   -  Using the native client

      The native client of Presto is **Presto/presto/bin/presto** in the client directory.

#. Run a query statement, for example, **show catalogs**.

   .. note::

      For clusters with Kerberos authentication enabled, when querying **Hive Catalog** data, the user who runs the Presto client must have the permission to access Hive tables and run the **grant all on table [table_name] to group hive** command in Hive beeline to grant permissions to the Hive group.

#. After the query is complete, run the following command to exit the client:

   **quit**
