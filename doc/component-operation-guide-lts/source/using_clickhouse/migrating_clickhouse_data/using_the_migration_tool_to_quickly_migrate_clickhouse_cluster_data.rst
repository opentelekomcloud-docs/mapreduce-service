:original_name: mrs_01_24508.html

.. _mrs_01_24508:

Using the Migration Tool to Quickly Migrate ClickHouse Cluster Data
===================================================================

.. note::

   This section applies only to MRS 3.2.0 or later.

Scenario
--------

Scenario 1: As the number of MRS ClickHouse services increases, the storage and compute resources of clusters cannot meet service requirements. Thus, the clusters need to be split so that part of user service and database data can be migrated to new clusters.

Scenario 2: The data center where the backend hosts of MRS ClickHouse clusters are located needs to be migrated, so does the ClickHouse cluster data.

To meet the migration requirements, MRS provides a one-click data migration tool for migrating the databases, table objects (DDL), and service data of ClickHouse from a source cluster to the new cluster.

Migration Mechanism
-------------------

-  Replicated*MergeTree table migration

   In this migration solution, ClickHouse uses ZooKeeper to automatically synchronize the data of Replicated*MergeTree tables of different replicas in the same shard. The logical procedure is as follows:

   First, add the ZooKeeper information of the source cluster to the configuration file of the destination cluster as the auxiliary ZooKeeper. Then, in the destination cluster, create a temporary table that has the same ZooKeeper path and structure as the source cluster but different replicas from it. After the temporary table is created, data in the source cluster will be automatically synchronized to the temporary table. Once data synchronization is complete, copy data from the temporary table to the formal table.


   .. figure:: /_static/images/en-us_image_0000001587840761.png
      :alt: **Figure 1** Replicated*MergeTree table migration architecture

      **Figure 1** Replicated*MergeTree table migration architecture

-  Distributed table migration

   During the migration of a replicated table, its metadata in the source cluster is exported and changed to the ZooKeeper path and replica of the destination cluster. Then, you can create a table in the destination cluster based on the modified metadata.

-  Non-replicated table and materialized view migration

   To migrate data in the non-replicated tables and materialized views, you can call the **remote** function.

The preceding migration operations are encapsulated using the migration tool script. In this way, you can modify the related configuration files and run the migration scripts to complete the migration by one click. For details, see the procedure description.

Prerequisites
-------------

-  The status of the source ClickHouse cluster to be migrated is normal and the cluster in the security mode.
-  The destination ClickHouse cluster of MRS 3.1.3 or later has been created for data migration. The cluster must be in the security mode. The number of ClickHouserver instances in the ClickHouse cluster is greater than or equal to that of the source cluster.
-  Currently, logical clusters support only data migration to clusters with the same number of replicas.

Constraints
-----------

-  Only table data and table object metadata (DDL) can be migrated. SQL statements like ETL need to be manually migrated.
-  To ensure data consistency before and after the migration, stop the ClickHouse service of the source cluster before the migration. For details, see the procedure description.
-  If the table of the source cluster is deleted during the migration, this issue can only be solved manually.

Procedure
---------

The overall migration procedure is as follows:


.. figure:: /_static/images/en-us_image_0000001532516862.png
   :alt: **Figure 2** Migration flowchart

   **Figure 2** Migration flowchart

.. table:: **Table 1** Migration description

   +---------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Step                                                                                                                                                          | Description                                                                                                                                                                                                 |
   +===============================================================================================================================================================+=============================================================================================================================================================================================================+
   | :ref:`Step 1: Connect the source cluster to the destination cluster. <mrs_01_24508__section132661749155412>`                                                  | This step ensures that the source and target ClickHouse clusters as well as their nodes can communicate with each other.                                                                                    |
   +---------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Step 2: Add the ZooKeeper information of the source cluster to the configuration file of the destination cluster. <mrs_01_24508__section1669382893718>` | By doing so, ZooKeeper in the source cluster can be used as the auxiliary ZooKeeper during data migration.                                                                                                  |
   +---------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Step 3: Migrate metadata of databases and tables in the source ClickHouse cluster to the destination cluster. <mrs_01_24508__section16918183315128>`    | You can run the corresponding script to migrate metadata such as the database name, table name, and table structure of the ClickHouse database and tables in the source cluster to the destination cluster. |
   +---------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Step 4: Migrate data of the databases and tables in the source ClickHouse cluster to the destination cluster. <mrs_01_24508__section18047266428>`       | You can run the corresponding script to migrate the ClickHouse database and table data from the source cluster to the destination cluster.                                                                  |
   +---------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_01_24508__section132661749155412:

Connecting the Source Cluster to the Destination Cluster
--------------------------------------------------------

#. Connect the source cluster to the destination cluster so that the ClickHouse instance nodes in the two clusters can communicate with each other.
#. Add the host configurations of the source cluster to all nodes in the destination cluster.

   a. Log in to FusionInsight Manager of the source ClickHouse cluster, choose **Cluster** > **ClickHouse**, click the **Instance** tab, and view the service IP address of the ClickHouseServer instance node.

   b. .. _mrs_01_24508__li1990635315277:

      Log in to any ClickHouseServer node using SSH and run the following command to check the host configurations of the ClickHouse instance in the source cluster:

      **cat /etc/hosts**

      The following figure shows the host configurations of the ClickHouse instance:

      |image1|

   c. Log in to FusionInsight Manager of the destination ClickHouse cluster, choose **Cluster** > **ClickHouse**, click the **Instance** tab, and view the service IP address of the ClickHouseServer instance node in the destination cluster.

   d. Log in to all ClickHouse nodes in the destination cluster as user **root** and run the following command to modify the **/etc/hosts** configuration of the nodes:

      **vi** **/etc/hosts**

      Copy the host information of the ClickHouse instance of the source cluster obtained in :ref:`2.b <mrs_01_24508__li1990635315277>` to the **hosts** file.

#. Configure mutual trust between the source and destination clusters.

.. _mrs_01_24508__section1669382893718:

Adding the ZooKeeper Information of the Source Cluster to the Configuration File of the Destination Cluster
-----------------------------------------------------------------------------------------------------------

#. .. _mrs_01_24508__li13474131194310:

   Log in to FusionInsight Manager of the source cluster, choose **Cluster** > **Services** > **ZooKeeper**, and click the **Instance** tab. On the displayed page, view the service IP addresses of the ZooKeeper quorumpeer instance , as shown in :ref:`Figure 3 <mrs_01_24508__fig39818132540>`.

   .. _mrs_01_24508__fig39818132540:

   .. figure:: /_static/images/en-us_image_0000001537090654.png
      :alt: **Figure 3** Addresses of the source Zookeeper quorumpeer instance

      **Figure 3** Addresses of the source Zookeeper quorumpeer instance

#. .. _mrs_01_24508__li1315311694620:

   Log in to FusionInsight Manager of the destination cluster, choose **Cluster** > **Services** > **ClickHouse** and click the **Configurations** tab and then **All Configurations**. On the displayed page, search for the **clickhouse-config-customize** parameter.

#. .. _mrs_01_24508__li16763133318475:

   Add ZooKeeper instance information of the source cluster to the **clickhouse-config-customize** parameter by referring to :ref:`Table 2 <mrs_01_24508__table6772947124819>`.

   .. _mrs_01_24508__table6772947124819:

   .. table:: **Table 2** Configurations of **clickhouse-config-customize**

      +----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                                    | Value                                                                                                                                                                                                                   |
      +==============================================+=========================================================================================================================================================================================================================+
      | auxiliary_zookeepers.zookeeper2.node[1].host | Service IP address of the first ZooKeeper quorumpeer instance in the source cluster obtained in :ref:`1 <mrs_01_24508__li13474131194310>`. Currently, only the IP address of the ZooKeeper instance can be configured.  |
      +----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | auxiliary_zookeepers.zookeeper2.node[1].port | 2181                                                                                                                                                                                                                    |
      +----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | auxiliary_zookeepers.zookeeper2.node[2].host | Service IP address of the second ZooKeeper quorumpeer instance in the source cluster obtained in :ref:`1 <mrs_01_24508__li13474131194310>`. Currently, only the IP address of the ZooKeeper instance can be configured. |
      +----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | auxiliary_zookeepers.zookeeper2.node[2].port | 2181                                                                                                                                                                                                                    |
      +----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | auxiliary_zookeepers.zookeeper2.node[3].host | Service IP address of the third ZooKeeper quorumpeer instance in the source cluster obtained in :ref:`1 <mrs_01_24508__li13474131194310>`. Currently, only the IP address of the ZooKeeper instance can be configured.  |
      +----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | auxiliary_zookeepers.zookeeper2.node[3].port | 2181                                                                                                                                                                                                                    |
      +----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. After the configuration is complete, click **Save**. In the displayed dialog box, click **OK**.

#. .. _mrs_01_24508__li17679261131:

   Log in to any ClickHouseServer node of the destination cluster as user **root**. Run the following command to view the ClickHouseServer instance information:

   **ps -ef \|grep clickhouse**

   Obtain the value of **--config-file**, that is, the configuration file directory of the ClickHouseServer, from the query result.


   .. figure:: /_static/images/en-us_image_0000001537413022.png
      :alt: **Figure 4** Obtaining the configuration file directory of ClickHouseServer

      **Figure 4** Obtaining the configuration file directory of ClickHouseServer

#. Run the corresponding command to check whether the information about **<auxiliary_zookeepers>** is added in the ClickHouse configuration file **config.xml**.

   **cat** *Directory of the config.xml file obtained in :ref:`5 <mrs_01_24508__li17679261131>`*


   .. figure:: /_static/images/en-us_image_0000001583195985.png
      :alt: **Figure 5** Viewing the added ZooKeeper information of the source cluster

      **Figure 5** Viewing the added ZooKeeper information of the source cluster

#. .. _mrs_01_24508__li11758429194015:

   In the configuration file directory obtained in :ref:`5 <mrs_01_24508__li17679261131>`, run the following command to obtain the ZooKeeper authentication information of the source cluster:

   **cat ENV_VARS \| grep ZK**

   |image2|

   Obtain the values of **ZK_SERVER_FQDN**, **ZK_USER_PRINCIPAL** and **ZK_USER_REALM**.

#. Log in to FusionInsight Manager of the destination cluster, choose **Cluster** > **Services** > **ClickHouse**, click the **Configurations** tab and then **All Configurations**. In the navigation pane on the left, choose **ClickHouseServer(Role)** > **Backup** and set the parameters by referring to the following table.

   .. table:: **Table 3** Configuring the cluster authentication information

      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Value                                                                                                                       |
      +===================================+=============================================================================================================================+
      | AUXILIARY_ZK_SERVER_FQDN          | Value of **ZK_SERVER_FQDN** obtained in :ref:`7 <mrs_01_24508__li11758429194015>`                                           |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
      | AUXILIARY_ZK_SERVER_PRINCIPAL     | Value of **ZK_USER_PRINCIPAL** obtained in :ref:`7 <mrs_01_24508__li11758429194015>`                                        |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
      | AUXILIARY_ZK_SERVER_REALM         | Value of **ZK_USER_REALM** obtained in :ref:`7 <mrs_01_24508__li11758429194015>`                                            |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
      | METADATA_COLLECTION_TIMEOUT       | **180**.                                                                                                                    |
      |                                   |                                                                                                                             |
      |                                   | This parameter specifies the timeout interval for waiting for the completion of metadata backup on other nodes, in seconds. |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+


   .. figure:: /_static/images/en-us_image_0000001532676354.png
      :alt: **Figure 6** Configuring the cluster authentication information

      **Figure 6** Configuring the cluster authentication information

#. Click **Save**. In the dialog box that is displayed, click **OK**.

#. On the ClickHouse service page, click the **Instance** tab. On this tab page, select the ClickHouseServer instance from the instance list, and choose **More** > **Restart Instance** in the **Operation** column to restart the ClickHouseServer instance.

.. _mrs_01_24508__section16918183315128:

Migrating Metadata of Databases and Tables in the Source ClickHouse Cluster to the Destination Cluster
------------------------------------------------------------------------------------------------------

#. .. _mrs_01_24508__li1162843314242:

   Log in to FusionInsight Manager of the source and destination clusters, and create the username and password required for the migration. The procedure is as follows:

   a. Log in to Manager and choose **System** > **Permission** > **Role**. On the displayed page, click **Create Role**.

   b. .. _mrs_01_24508__li11670123433010:

      Specify **Role Name**, for example, **ckrole**. In the **Configure Resource Permission** area, click the cluster name. On the displayed service list page, click the ClickHouse service.

   c. Select **SUPER_USER_GROUP** and click **OK**.

   d. Choose **System**. On the navigation pane on the left, choose **Permission** > **User** and click **Create**.

   e. Select **Human-Machine** for **User Type** and set **Password** and **Confirm Password** to the password of the user.

      .. note::

         -  Username: The username cannot contain hyphens (-). Otherwise, the authentication will fail.
         -  Password: The password cannot contain special characters $, ., and #. Otherwise, the authentication will fail.

   f. In the **Role** area, click **Add** . In the displayed dialog box, select the role name in :ref:`1.b <mrs_01_24508__li11670123433010>` and click **OK** to add the role. Then, click **OK**.

   g. After the user is created, click the user name in the upper right corner to log out of the system. Log in to FusionInsight Manager as the new user and change its password as prompted.

#. Download the ClickHouse client and install it as user **omm** to the destination cluster.

#. Log in to the client node as user **omm**, go to the *Client installation directory*\ **/ClickHouse/clickhouse_migration_tool/clickhouse-metadata-migration** directory, and configure migration information. Run the following command to modify the **example_config.yaml** configuration file by referring to :ref:`Table 4 <mrs_01_24508__table16816744680>`:

   **cd** *Client installation directory*\ **/ClickHouse/clickhouse_migration_tool/clickhouse-metadata-migration**

   **vi example_config.yaml**

   After the configuration is modified, you must delete all comment with number sign(#) and retain only valid configurations. Otherwise, an error may occur during script migration.

   .. _mrs_01_24508__table16816744680:

   .. table:: **Table 4** Parameters in **the example_config.yaml** file

      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Configuration Item    | Sub-item              | Value and Description                                                                                                                                                                                                                                                                                                           |
      +=======================+=======================+=================================================================================================================================================================================================================================================================================================================================+
      | source_cluster        | host                  | IP address of any ClickHouseServer node in the source cluster.                                                                                                                                                                                                                                                                  |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | cluster_name          | Name of the source ClickHouse cluster. You can log in to the ClickHouse client by referring to :ref:`Using ClickHouse from Scratch <mrs_01_2345>` and run the following command to obtain the value. If the source cluster name has not been changed, the default value is **default_cluster**.                                 |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                 |
      |                       |                       | **select cluster,shard_num,replica_num,host_name from system.clusters;**                                                                                                                                                                                                                                                        |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | https_port            | To obtain the port number, log in to FusionInsight Manager of the source cluster, choose **Cluster** > **Services** > **ClickHouse**, and click the **Configurations** tab and then **All Configurations**. In the displayed page, search for **https_port**.                                                                   |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | zookeeper_root_path   | To obtain the value, log in to FusionInsight Manager of the source cluster, choose **Cluster** > **Services** > **ClickHouse**, and click the **Configurations** tab and then **All Configurations**. In the displayed page, search for **clickhouse.zookeeper.root.path**.                                                     |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | system                | System parameter. Retain the default value.                                                                                                                                                                                                                                                                                     |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | databases             | Optional.                                                                                                                                                                                                                                                                                                                       |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                 |
      |                       |                       | -  If this parameter is specified, data in the specified database of the source ClickHouse cluster is migrated. You can specify multiple databases. The following configuration is for your reference:                                                                                                                          |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                 |
      |                       |                       |    .. code-block::                                                                                                                                                                                                                                                                                                              |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                 |
      |                       |                       |       databases:                                                                                                                                                                                                                                                                                                                |
      |                       |                       |           - "database"                                                                                                                                                                                                                                                                                                          |
      |                       |                       |           - "database_1"                                                                                                                                                                                                                                                                                                        |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                 |
      |                       |                       |    Data in the **database** and **database_1** databases of the source cluster is migrated.                                                                                                                                                                                                                                     |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                 |
      |                       |                       | -  If this parameter is not specified, table data of all databases in the source ClickHouse cluster is migrated. Leave the **databases** parameter empty. The following is an example:                                                                                                                                          |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                 |
      |                       |                       |    .. code-block::                                                                                                                                                                                                                                                                                                              |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                 |
      |                       |                       |       databases:                                                                                                                                                                                                                                                                                                                |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                 |
      |                       |                       |    Table information of all databases in the source ClickHouse cluster is migrated.                                                                                                                                                                                                                                             |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | tables                | Optional. The value is in the format of *Database name.Table name*. The database name must be in the databases parameter list.                                                                                                                                                                                                  |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                 |
      |                       |                       | -  If this parameter is specified, data in specified tables in the source ClickHouse cluster database is migrated. You can configure multiple tables. The following configuration is for your reference:                                                                                                                        |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                 |
      |                       |                       |    .. code-block::                                                                                                                                                                                                                                                                                                              |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                 |
      |                       |                       |       tables:                                                                                                                                                                                                                                                                                                                   |
      |                       |                       |           - "database.table_1"                                                                                                                                                                                                                                                                                                  |
      |                       |                       |           - "database_1.table_2"                                                                                                                                                                                                                                                                                                |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                 |
      |                       |                       |    Data in **table_1** of **database** and **table_2** of database_1 of the source cluster is migrated.                                                                                                                                                                                                                         |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                 |
      |                       |                       | -  If this parameter is not specified and the **databases** parameter is specified, all table data in the **databases** database is migrated. If the **databases** parameter is not specified, all table data in all databases of the source ClickHouse cluster is migrated. The following configuration is for your reference: |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                 |
      |                       |                       |    .. code-block::                                                                                                                                                                                                                                                                                                              |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                 |
      |                       |                       |       tables:                                                                                                                                                                                                                                                                                                                   |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | destination_cluster   | host                  | IP address of any ClickHouseServer node in the destination cluster.                                                                                                                                                                                                                                                             |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | cluster_name          | Name of the destination ClickHouse cluster. You can log in to the ClickHouse client by referring to :ref:`Using ClickHouse from Scratch <mrs_01_2345>` and run the following command to obtain the value. If the destination cluster name has not been changed, the default value is **default_cluster**.                       |
      |                       |                       |                                                                                                                                                                                                                                                                                                                                 |
      |                       |                       | **select cluster,shard_num,replica_num,host_name from system.clusters;**                                                                                                                                                                                                                                                        |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | user                  | Username created in :ref:`1 <mrs_01_24508__li1162843314242>` for logging in to FusionInsight Manager of the destination ClickHouse cluster.                                                                                                                                                                                     |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | https_port            | To obtain the port number, log in to FusionInsight Manager of the destination cluster, choose **Cluster** > **Services** > **ClickHouse**, and click the **Configurations** tab and then **All Configurations**. In the displayed page, search for **https_port**.                                                              |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | zookeeper_root_path   | To obtain the value, log in to FusionInsight Manager of the destination cluster, choose **Cluster** > **Services** > **ClickHouse**, and click the **Configurations** tab and then **All Configurations**. In the displayed page, search for **clickhouse.zookeeper.root.path**.                                                |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | system                | System parameter. Retain the default value.                                                                                                                                                                                                                                                                                     |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Run the following command to migrate data and wait until the script execution is complete:

   **./clickhouse_migrate_metadata.sh -f yaml_file**

   Enter the usernames and passwords of the source and destination clusters.

   |image3|

.. note::

   If metadata migration fails, perform the following steps:

   #. Locate the failure cause. Specifically, check whether any parameters in the configuration file are incorrectly configured.

      -  If yes, reconfigure the parameters and perform metadata migration.
      -  If no, go to :ref:`2 <mrs_01_24508__li19763810133612>`.

   #. .. _mrs_01_24508__li19763810133612:

      Set the names of the tables that fail to be migrated in the metadata migration configuration file based on the **databases** and **tables** parameters in :ref:`Table 4 <mrs_01_24508__table16816744680>` and run the metadata migration command again. If the migration fails, contact O&M personnel.

.. _mrs_01_24508__section18047266428:

Migrating Data of the Databases and Tables in the Source ClickHouse Cluster to the Destination Cluster
------------------------------------------------------------------------------------------------------

#. Log in to the ClickHouse client node in the destination cluster as user **omm** and go to *Client installation directory*\ **/ClickHouse/clickhouse_migration_tool/clickhouse-data-migration**.

   **cd** *Client installation directory*\ **/ClickHouse/clickhouse_migration_tool/clickhouse-data-migration**

#. Run the following command to modify the **example_config.yaml** configuration file by referring to :ref:`Table 5 <mrs_01_24508__table993412163478>`:

   **vi example_config.yaml**

   After the configuration is modified, you must delete all comment with number sign(#) and retain only valid configurations. Otherwise, an error may occur during script migration.

   .. _mrs_01_24508__table993412163478:

   .. table:: **Table 5** Parameters in **example_config.yaml**

      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Configuration Item                | Sub-item              | Value and Description                                                                                                                                                                                                                                                                                                                                                                      |
      +===================================+=======================+============================================================================================================================================================================================================================================================================================================================================================================================+
      | source_cluster                    | host                  | IP address of any ClickHouseServer node in the source cluster.                                                                                                                                                                                                                                                                                                                             |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                                   | cluster_name          | Name of the source ClickHouse cluster. You can log in to the ClickHouse client by referring to :ref:`Using ClickHouse from Scratch <mrs_01_2345>` and run the following command to obtain the value. If the source cluster name has not been changed, the default value is **default_cluster**.                                                                                            |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       | **select cluster,shard_num,replica_num,host_name from system.clusters;**                                                                                                                                                                                                                                                                                                                   |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                                   | user                  | Username created in :ref:`1 <mrs_01_24508__li1162843314242>` for logging in to FusionInsight Manager of the source ClickHouse cluster.                                                                                                                                                                                                                                                     |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                                   | https_port            | To obtain the port number, log in to FusionInsight Manager of the source cluster, choose **Cluster** > **Services** > **ClickHouse**, and click the **Configurations** tab and then **All Configurations**. In the displayed page, search for **https_port**.                                                                                                                              |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                                   | tcp_port              | To obtain the value, log in to FusionInsight Manager of the source cluster, choose **Cluster** > **Services** > **ClickHouse**, and click the **Configurations** tab and then **All Configurations**. In the displayed page, search for **tcp_port_secure** if the cluster is in security mode. Otherwise, search for **tcp_port**.                                                        |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                                   | zookeeper_root_path   | To obtain the value, log in to FusionInsight Manager of the source cluster, choose **Cluster** > **Services** > **ClickHouse**, and click the **Configurations** tab and then **All Configurations**. In the displayed page, search for **clickhouse.zookeeper.root.path**.                                                                                                                |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                                   | system                | System parameter. Retain the default value.                                                                                                                                                                                                                                                                                                                                                |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                                   | databases             | Optional.                                                                                                                                                                                                                                                                                                                                                                                  |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       | -  If this parameter is specified, data in the specified database of the source ClickHouse cluster is migrated. You can specify multiple databases. The following configuration is for your reference:                                                                                                                                                                                     |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       |    .. code-block::                                                                                                                                                                                                                                                                                                                                                                         |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       |       databases:                                                                                                                                                                                                                                                                                                                                                                           |
      |                                   |                       |           - "database"                                                                                                                                                                                                                                                                                                                                                                     |
      |                                   |                       |           - "database_1"                                                                                                                                                                                                                                                                                                                                                                   |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       |    Data in the **database** and **database_1** databases of the source cluster is migrated.                                                                                                                                                                                                                                                                                                |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       | -  If this parameter is not specified, table data of all databases in the source ClickHouse cluster is migrated. Leave the **databases** parameter empty. The following is an example:                                                                                                                                                                                                     |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       |    .. code-block::                                                                                                                                                                                                                                                                                                                                                                         |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       |       databases:                                                                                                                                                                                                                                                                                                                                                                           |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       |    Table information of all databases in the source ClickHouse cluster is migrated.                                                                                                                                                                                                                                                                                                        |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                                   | tables                | Optional. The value is in the format of *Database name.Table name*. The database name must be in the databases parameter list.                                                                                                                                                                                                                                                             |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       | -  If this parameter is specified, data in specified tables in the source ClickHouse cluster database is migrated. You can configure multiple tables. The following configuration is for your reference:                                                                                                                                                                                   |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       |    .. code-block::                                                                                                                                                                                                                                                                                                                                                                         |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       |       tables:                                                                                                                                                                                                                                                                                                                                                                              |
      |                                   |                       |           - "database.table_1"                                                                                                                                                                                                                                                                                                                                                             |
      |                                   |                       |           - "database_1.table_2"                                                                                                                                                                                                                                                                                                                                                           |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       |    Data in **table_1** of **database** and **table_2** of database_1 of the source cluster is migrated.                                                                                                                                                                                                                                                                                    |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       | -  If this parameter is not specified and the **databases** parameter is specified, all table data in the **databases** database is migrated. If the **databases** parameter is not specified, all table data in all databases of the source ClickHouse cluster is migrated. The following configuration is for your reference:                                                            |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       |    .. code-block::                                                                                                                                                                                                                                                                                                                                                                         |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       |       tables:                                                                                                                                                                                                                                                                                                                                                                              |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | destination_cluster               | host                  | IP address of any ClickHouseServer node in the destination cluster.                                                                                                                                                                                                                                                                                                                        |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                                   | cluster_name          | Name of the destination ClickHouse cluster. You can log in to the ClickHouse client by referring to :ref:`Using ClickHouse from Scratch <mrs_01_2345>` and run the following command to obtain the value. If the destination cluster name has not been changed, the default value is **default_cluster**.                                                                                  |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       | **select cluster,shard_num,replica_num,host_name from system.clusters;**                                                                                                                                                                                                                                                                                                                   |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                                   | user                  | Username created in :ref:`1 <mrs_01_24508__li1162843314242>` for logging in to FusionInsight Manager of the destination ClickHouse cluster.                                                                                                                                                                                                                                                |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                                   | https_port            | To obtain the port number, log in to FusionInsight Manager of the destination cluster, choose **Cluster** > **Services** > **ClickHouse**, and click the **Configurations** tab and then **All Configurations**. In the displayed page, search for **https_port**.                                                                                                                         |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                                   | tcp_port              | To obtain the value, log in to FusionInsight Manager of the destination cluster, choose **Cluster** > **Services** > **ClickHouse**, and click the **Configurations** tab and then **All Configurations**. In the displayed page, search for **tcp_port_secure** if the cluster is in security mode. Otherwise, search for **tcp_port**.                                                   |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                                   | zookeeper_root_path   | To obtain the value, log in to FusionInsight Manager of the destination cluster, choose **Cluster** > **Services** > **ClickHouse**, and click the **Configurations** tab and then **All Configurations**. In the displayed page, search for **clickhouse.zookeeper.root.path**.                                                                                                           |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                                   | system                | System parameter. Retain the default value.                                                                                                                                                                                                                                                                                                                                                |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | auxiliary_zookeepers              | name                  | ZooKeeper name of the source ClickHouse cluster configured in :ref:`3 <mrs_01_24508__li16763133318475>`, for example, **zookeeper2**.                                                                                                                                                                                                                                                      |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                                   | hosts                 | IP address of the ZooKeeper instance of the source ClickHouse. To obtain the IP address, log in to FusionInsight Manager of the source cluster, choose **Cluster** > **Services** > **ZooKeeper**, and click the **Instance** tab. On the displayed page, view the service IP addresses of the ZooKeeper quorumpeer instance , as shown in :ref:`Figure 3 <mrs_01_24508__fig39818132540>`. |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       | The format is as follows:                                                                                                                                                                                                                                                                                                                                                                  |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       | .. code-block::                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       |    hosts:                                                                                                                                                                                                                                                                                                                                                                                  |
      |                                   |                       |        - "192.168.1.2"                                                                                                                                                                                                                                                                                                                                                                     |
      |                                   |                       |        - "192.168.1.3"                                                                                                                                                                                                                                                                                                                                                                     |
      |                                   |                       |        - "192.168.1.4"                                                                                                                                                                                                                                                                                                                                                                     |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                                   | port                  | 2181                                                                                                                                                                                                                                                                                                                                                                                       |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | execution_procedure               | ``-``                 | This parameter is left blank by default, indicating that the script is executed once to synchronize service data. Value options are **firststep** and **secondstep**.                                                                                                                                                                                                                      |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       | -  **firststep**: Only the temporary replication table is created. The auxiliary ZooKeeper can synchronize data from the original cluster to the temporary table in real time.                                                                                                                                                                                                             |
      |                                   |                       | -  **secondstep**: data in the temporary replication table is attached to the local table of the destination cluster.                                                                                                                                                                                                                                                                      |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       |    .. caution::                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       |                                                                                                                                                                                                                                                                                                                                                                                            |
      |                                   |                       |       CAUTION:                                                                                                                                                                                                                                                                                                                                                                             |
      |                                   |                       |       If this parameter is set to **secondstep**, O&M personnel and users need to confirm that ClickHouse-related services have been stopped before script execution.                                                                                                                                                                                                                      |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | onereplica_use_auxiliaryzookeeper | ``-``                 | -  If this parameter is set to **1**, temporary tables are created for only one replica of each shard.                                                                                                                                                                                                                                                                                     |
      |                                   |                       | -  If this parameter is set to **0**, temporary tables are created for two replicas of each shard.                                                                                                                                                                                                                                                                                         |
      +-----------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Stop the ClickHouse service of the source cluster.

#. Run the following command to migrate data and wait until the script execution is complete:

   **./clickhouse_migrate_data.sh -f yaml_file**

   Enter the usernames and passwords of the source and destination clusters.

#. After the script is executed successfully, perform the following steps to check whether the migrated data in the source cluster is consistent with that in the destination cluster based on the migration result logs:

   Log in to the ClickHouse client node in the destination cluster and go to the *Client installation directory*\ **/ClickHouse/clickhouse_migration_tool/clickhouse-data-migration/comparison_result** directory.

   Compare the following result file information to check the data consistency between the source cluster and the destination cluster:

   -  **source_cluster_table_info**: statistics of data migrated from the source cluster
   -  **destination_cluster_table_info**: statistics of data migrated to the destination cluster
   -  **compare_result_file.txt**: data consistency comparison result before and after migration

   If the data is inconsistent before and after the migration, clear the data in the table of the destination cluster and migrate the data in the table separately or manually.

   In addition, you can log in to the ClickHouse databases of the source and destination clusters to manually check whether the number of table data records and partitions are consistent.

#. Log in to FusionInsight Manager of the destination cluster and delete the ZooKeeper information added to **clickhouse-config-customize** in :ref:`2 <mrs_01_24508__li1315311694620>`.

   Click **Save**. In the displayed dialog box, click **OK**.

#. After data migration is complete, switch services to the target ClickHouse cluster.

#. Go to *Client installation directory*\ **/ClickHouse/clickhouse_migration_tool/clickhouse-data-migration** and *Client installation directory*\ **/ClickHouse/clickhouse_migration_tool/clickhouse-metadata-migration** on the ClickHouse node in the destination cluster.

   **vi example_config.yaml**

   Delete the password from the configuration file to prevent password leakage.

.. note::

   If service data migration fails, perform the following steps:

   #. Locate the failure cause. Specifically, check whether any parameters in the configuration file are incorrectly configured.

      -  If yes, reconfigure the parameters and perform service data migration.
      -  If no, go to :ref:`2 <mrs_01_24508__li2481155164115>`.

   #. .. _mrs_01_24508__li2481155164115:

      Run the **drop table** *table_name* command to delete the data tables related to the table from the node that fails to be migrated in the destination cluster.

   #. Run the **show create table** *table_name* command to query the table creation statements related to the table in the source cluster and create the table in the destination cluster again.

   #. Set the names of the tables that fail to be migrated in the service data migration configuration file based on the **databases** and **tables** parameters in :ref:`Table 5 <mrs_01_24508__table993412163478>` and run the service data migration command again. If the command fails to execute, contact O&M personnel.

.. |image1| image:: /_static/images/en-us_image_0000001532836098.png
.. |image2| image:: /_static/images/en-us_image_0000001583316321.png
.. |image3| image:: /_static/images/en-us_image_0000001537269552.png
