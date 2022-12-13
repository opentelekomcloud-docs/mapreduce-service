:original_name: mrs_01_24487.html

.. _mrs_01_24487:

Configuring a Hive Data Connection
==================================

This section describes how to switch the Hive metadata of an active cluster to the metadata stored in a local database or RDS database after you create a cluster. This operation enables multiple MRS clusters to share the same metadata, and the metadata will not be deleted when the clusters are deleted. In this way, Hive metadata migration is not required during cluster migration.

.. note::

   -  When Hive metadata is switched between different clusters, MRS synchronizes only the permissions in the metadata database of the Hive component. The permission model on MRS is maintained on MRS Manager. Therefore, when Hive metadata is switched between clusters, the permissions of users or user groups cannot be automatically synchronized to MRS Manager of another cluster.
   -  For clusters whose version is earlier than MRS 3.\ *x*, if the selected data connection is **RDS MySQL database**, ensure that the database user is **root**. If the user is not **root**, create a user and grant permissions to the user by referring to :ref:`Performing Operations Before Data Connection <mrs_01_0633__section311713549458>`.
   -  For clusters whose version is MRS 3.\ *x* or later, if the selected data connection is **RDS MySQL database**, the database user cannot be user **root**. In this case, create a user and grant permissions to the user by following the instructions provided in :ref:`Performing Operations Before Data Connection <mrs_01_0633__section311713549458>`.


Configuring a Hive Data Connection
----------------------------------

This function is not supported in MRS 3.0.5.

#. Log in to the MRS console. In the navigation pane on the left, choose **Clusters** > **Active Clusters**.
#. Click the name of a cluster to go to the cluster details page.
#. On the **Dashboard** tab page, click **Manage** next to **Data Connection**.
#. On the **Data Connection** dialog box, the data connections associated with the cluster are displayed. You can click **Edit** or **Delete** to edit or delete the data connections.
#. If there is no associated data connection on the **Data Connection** dialog box, click **Configure Data Connection** to add a connection.

   .. note::

      Only one data connection can be configured for a module type. For example, after a data connection is configured for Hive metadata, no other data connection can be configured for it. If no module type is available, the **Configure Data Connection** button is unavailable.

   .. table:: **Table 1** Configuring a Hive data connection

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                                                                                                                                          |
      +===================================+======================================================================================================================================================================================================================================================================================================================================================================================================================================+
      | Component                         | Hive                                                                                                                                                                                                                                                                                                                                                                                                                                 |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Module Type                       | Hive metadata                                                                                                                                                                                                                                                                                                                                                                                                                        |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Data Connection Type              | -  RDS MySQL database                                                                                                                                                                                                                                                                                                                                                                                                                |
      |                                   | -  Local database                                                                                                                                                                                                                                                                                                                                                                                                                    |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Instance                          | This parameter is valid only when **Data Connection Type** is set to **RDS PostgreSQL database** or **RDS MySQL database**. Select the name of the connection between the MRS cluster and the RDS database. This instance must be created before being referenced here. You can click **Create Data Connection** to create a data connection. For details, see :ref:`Creating a Data Connection <mrs_01_0633__section813712431913>`. |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Test** to test connectivity of the data connection.
#. After the data connection is successful, click **OK**.

   .. note::

      -  After Hive metadata is configured, restart Hive. Hive will create necessary database tables in the specified database. (If tables already exist, they will not be created.)
      -  Before restarting the Hive service, ensure that the driver package has been installed on all nodes where Metastore instances are located.

         -  Postgres: Use the open source Postgres driver package to replace the existing one of the cluster. Upload the Postgres driver package **postgresql-42.2.5.jar** to the *${BIGDATA_HOME}*\ **/third_lib/Hive** directory on all MetaStore instance nodes. To download the open-source driver package, visit https://repo1.maven.org/maven2/org/postgresql/postgresql/42.2.5/.
         -  MySQL: Go to the MySQL official website (https://www.mysql.com/). Choose **DOWNLOADS** and click **MySQL Community (GPL) Downloads**. On the displayed page, click **Connector/J** to download the driver package of the corresponding version and upload the driver package to the **/opt/Bigdata/FusionInsight_HD_*/install/FusionInsight-Hive-*/hive-*/lib/** directory on all RDSMetastore nodes.
