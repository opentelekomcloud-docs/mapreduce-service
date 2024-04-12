:original_name: mrs_01_24742.html

.. _mrs_01_24742:

Importing and Exporting Hive Databases
======================================

Scenario
--------

In big data application scenarios, Hive databases and all tables in these databases are usually migrated to another cluster. You can run the Hive database **export** and **import** commands to migrate a complete database.

.. note::

   This section applies to MRS 3.2.0 or later.

   The Hive database import and export function does not support importing or exporting encrypted tables, transaction tables, HBase external tables, Hudi tables, view tables, and materialized view tables.

Prerequisites
-------------

-  If Hive databases are imported or exported across clusters and Kerberos authentication is enabled for both the source and destination clusters, configure cross-cluster mutual trust.

-  If you want to run the **dump** or **load** command to import or export databases created by other users, grant the corresponding database permission to the users.

   -  If Ranger authentication is not enabled for the cluster, log in to FusionInsight Manager to grant the administrator rights of the role to which the user belongs. For details, see section :ref:`Creating a Hive Role <mrs_01_0949>`.
   -  If Ranger authentication is enabled for the cluster, grant users the permission to dump and load databases. For details, see :ref:`Adding a Ranger Access Permission Policy for Hive <mrs_01_1858>`.

-  Enable the inter-cluster copy function in the source cluster and destination cluster.

-  Configure the HDFS service address parameter for the source cluster to access the destination cluster.

   Log in to FusionInsight Manager of the source cluster, click **Cluster**, choose **Services** > **Hive**, and click **Configuration**. On the displayed page, search for **hdfs.site.customized.configs**, add custom parameter **dfs.namenode.rpc-address.haclusterX**, and set its value to *Service IP address of the active NameNode instance node in the destination cluster*:*RPC port*. Add custom parameter **dfs.namenode.rpc-address.haclusterX1** and set its value to *Service IP address of the standby NameNode instance node in the destination cluster*:*RPC port*. The RPC port of NameNode is **25000** by default. After saving the configuration, roll-restart the Hive service.

Procedure
---------

#. Log in to the node where the client is installed in the source cluster as the Hive client installation user.

#. .. _mrs_01_24742__li2282114610113:

   Run the following command to switch to the client installation directory, for example, **/opt/client**:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If Kerberos authentication is enabled for the cluster, run the following command to authenticate the user. Otherwise, skip this step.

   **kinit** *Hive service user*

#. .. _mrs_01_24742__li9282204611111:

   Run the following command to log in to the Hive client:

   **beeline**

#. Run the following command to create the **dump_db** database:

   **create database** *dump_db*\ **;**

#. Run the following command to switch to the **dump_db** database:

   **use** *dump_db*\ **;**

#. Run the following command to create the **test** table in the **dump_db** database:

   **create table** *test*\ **(**\ *id int*\ **);**

#. Run the following command to insert data to the **test** table:

   **insert into** *test* **values(**\ *123*\ **);**

#. Run the following command to set the **dump_db** database as the source of the replication policy:

   **alter database** *dump_db* **set dbproperties** **('**\ *repl.source.for*\ **'='**\ replpolicy1\ **');**

   .. note::

      -  Perform the following steps to set permissions for users when the **alter** command is used to modify database attributes:

         -  If Ranger authentication is not enabled for the cluster, log in to FusionInsight Manager to grant the administrator rights of the role to which the user belongs. For details, see section :ref:`Creating a Hive Role <mrs_01_0949>`.
         -  If Ranger authentication is enabled for the cluster, grant users the permission to dump and load databases. For details, see :ref:`Adding a Ranger Access Permission Policy for Hive <mrs_01_1858>`.

      -  Databases with replication policy sources configured can be deleted only after their replication policy sources are set to null. To do so, run the following command:

         **alter database** *dump_db* **set dbproperties** **('**\ *repl.source.for*\ **'='');**

#. Run the following command to export the **dump_db** database to the **/user/hive/test** directory of the destination cluster:

   **repl dump** *dump_db* **with ('hive.repl.rootdir'='hdfs://hacluster**\ *X/user/hive/test*\ **');**

   .. note::

      -  **hacluster X** is the value of **haclusterX** in new custom parameter\ **dfs.namenode.rpc-address.haclusterX**.
      -  Ensure that the current user has the read and write permissions on the export directory to be specified.

#. Log in to the node where the client is installed in the destination cluster as the Hive client installation user, and perform :ref:`2 <mrs_01_24742__li2282114610113>` to :ref:`5 <mrs_01_24742__li9282204611111>`.

#. Run the following command to import data from the **dump_db** database in the **/user/hive/test** directory to the **load_db** database:

   **repl load** *load_db* **from '**\ */user/hive/repl*\ **';**

   .. note::

      When the **repl load** command is used to import a database, pay attention to the following points when specifying the database name:

      -  If the specified database does not exist, the database will be created during the import.
      -  If the specified database exists and the value of **hive.repl.ckpt.key** of the database is the same as the imported path, skip the import operation.
      -  If the specified database already exists and no table or function exists in this database, only the tables in the source database are imported to the current database during the import. Otherwise, the import fails.
