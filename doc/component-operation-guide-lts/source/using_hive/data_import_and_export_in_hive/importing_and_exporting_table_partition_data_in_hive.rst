:original_name: mrs_01_24741.html

.. _mrs_01_24741:

Importing and Exporting Table/Partition Data in Hive
====================================================

Scenario
--------

In big data application scenarios, data tables in Hive usually need to be migrated to another cluster. You can run the Hive **import** and **export** commands to migrate data in tables. That is, you can run the **export** command to export Hive tables from the source cluster to the HDFS of the target cluster, run the **import** command in the target cluster to import the exported data to the corresponding Hive table.

.. note::

   This section applies to MRS 3.2.0 or later.

   The Hive table import and export function does not support importing or exporting encrypted tables, HBase external tables, transaction tables, Hudi tables, view tables, and materialized view tables.

Prerequisites
-------------

-  If Hive tables or partition data is imported or exported across clusters and Kerberos authentication is enabled for both the source and destination clusters, configure cross-cluster mutual trust.

-  If you want to run the **import** or **export** command to import or export tables or partitions created by other users, grant the corresponding table permission to the users.

   -  If Ranger authentication is not enabled for the cluster, log in to FusionInsight Manager to grant the **Select Authorization** permission of the table corresponding to the role to which the user belongs. For details, see section :ref:`Configuring Permissions for Hive Tables, Columns, or Databases <mrs_01_0950>`.
   -  If Ranger authentication is enabled for the cluster, grant users the permission to import and export tables. For details, see :ref:`Adding a Ranger Access Permission Policy for Hive <mrs_01_1858>`.

-  Enable the inter-cluster copy function in the source cluster and destination cluster.

-  Configure the HDFS service address parameter for the source cluster to access the destination cluster.

   Log in to FusionInsight Manager of the source cluster, click **Cluster**, choose **Services** > **Hive**, and click **Configuration**. On the displayed page, search for **hdfs.site.customized.configs**, add custom parameter **dfs.namenode.rpc-address.haclusterX**, and set its value to *Service IP address of the active NameNode instance node in the destination cluster*:*RPC port*. Add custom parameter **dfs.namenode.rpc-address.haclusterX1** and set its value to *Service IP address of the standby NameNode instance node in the destination cluster*:*RPC port*. The RPC port of NameNode is **25000** by default. After saving the configuration, roll-restart the Hive service.

Procedure
---------

#. .. _mrs_01_24741__li1793444135814:

   Log in to the node where the client is installed in the destination cluster as the Hive client installation user.

#. Run the following command to switch to the client installation directory, for example, **/opt/client**:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. .. _mrs_01_24741__li610182915598:

   If Kerberos authentication is enabled for the cluster, run the following command to authenticate the user. Otherwise, skip this step.

   **kinit** *Hive service user*

#. Run the following command to log in to the Hive client in the destination cluster:

   **beeline**

#. Run the following command to create the **export_test** table:

   **create table** *export_test(id int)* **;**

#. Run the following command to insert data to the **export_test** table:

   **insert into** *export_test values(123)*\ **;**

#. .. _mrs_01_24741__li89938161394:

   Repeat :ref:`1 <mrs_01_24741__li1793444135814>` to :ref:`4 <mrs_01_24741__li610182915598>` in the destination cluster and run the following command to create an HDFS path for storing the exported **export_test** table:

   **dfs -mkdir** */tmp/export*

#. Run the following command to log in to the Hive client:

   **beeline**

#. Import and export the **export_test** table.

   The Hive **import** and **export** commands can be used to migrate table data in the following modes. Select a proper data migration mode as required.

   -  Mode 1: Table export and import

      a. .. _mrs_01_24741__li422755591415:

         Run the following command in the source cluster to export the metadata and service data of the **export_test** table to the directory created in :ref:`8 <mrs_01_24741__li89938161394>`:

         **export table** *export_test* **to** **'hdfs://hacluster**\ *X/tmp/export*\ **';**

      b. Run the following command in the destination cluster to import the table data exported in :ref:`10.a <mrs_01_24741__li422755591415>` to the **export_test** table:

         **import from '**\ */tmp/export*\ **';**

   -  Mode 2: Renaming a table during the import

      a. .. _mrs_01_24741__li207111134162118:

         Run the following command in the source cluster to export the metadata and service data of the **export_test** table to the directory created in :ref:`8 <mrs_01_24741__li89938161394>`:

         **export table** *export_test* **to** **'hdfs://hacluster**\ *X/tmp/export*\ **';**

      b. Run the following command in the destination cluster to import the table data exported in :ref:`10.a <mrs_01_24741__li207111134162118>` to the **import_test** table:

         **import table** *import_test* **from '**\ */tmp/export*\ **';**

   -  Mode 3: Partition export and import

      a. .. _mrs_01_24741__li77435347346:

         Run the following commands in the source cluster to export the **pt1** and **pt2** partitions of the **export_test** table to the directory created in :ref:`8 <mrs_01_24741__li89938161394>`:

         **export table** *export_test* **partition** **(**\ *pt1*\ **="**\ *in*\ **"**, *pt2*\ **="**\ *ka*\ **")** **to** **'hdfs://hacluster**\ **X**\ */tmp/export*\ **';**

      b. Run the following command in the destination cluster to import the table data exported in :ref:`10.a <mrs_01_24741__li77435347346>` to the **export_test** table:

         **import from '**\ */tmp/export*\ **';**

   -  Mode 4: Exporting table data to a Partition

      a. .. _mrs_01_24741__li19785214114715:

         Run the following command in the source cluster to export the metadata and service data of the **export_test** table to the directory created in :ref:`8 <mrs_01_24741__li89938161394>`:

         **export table** *export_test* **to 'hdfs://hacluster**\ *X/tmp/export*\ **';**

      b. Run the following command in the destination cluster to import the table data exported in :ref:`10.a <mrs_01_24741__li19785214114715>` to the **pt1** and **pt2** partitions of the **import_test** table:

         **import table** *import_test* **partition (**\ *pt1*\ **="**\ *us*\ **",** *pt2*\ **="**\ *tn*\ **") from '**\ */tmp/export*\ **';**

   -  Mode 5: Specifying the table location during the import

      a. .. _mrs_01_24741__li11635456135510:

         Run the following command in the source cluster to export the metadata and service data of the **export_test** table to the directory created in :ref:`8 <mrs_01_24741__li89938161394>`:

         **export table** *export_test* **to 'hdfs://hacluster**\ *X/tmp/export*\ **';**

      b. Run the following command in the destination cluster to import the table data exported in :ref:`10.a <mrs_01_24741__li11635456135510>` to the **import_test** table and specify its location as **tmp/export**:

         **import table** *import_test* **from '**\ */tmp*' **location** **'**/*tmp/export*\ **';**

   -  Mode 6: Exporting data to an external table

      a. .. _mrs_01_24741__li437611737:

         Run the following command in the source cluster to export the metadata and service data of the **export_test** table to the directory created in :ref:`8 <mrs_01_24741__li89938161394>`:

         **export table** *export_test* **to 'hdfs://hacluster**\ *X/tmp/export*\ **';**

      b. Run the following command in the destination cluster to import the table data exported in :ref:`10.a <mrs_01_24741__li437611737>` to external table **import_test**:

         **import external table** *import_test* **from '**\ */tmp/export*\ **';**

   .. note::

      Before exporting table or partition data, ensure that the HDFS path for storage has been created and is empty. Otherwise, the export fails.

      When partitions are exported or imported, the exported or imported table must be a partitioned table, and data of multiple partition values of the same partition field cannot be exported.

      During the data import:

      -  If the **import from '**\ */tmp/export*\ **';** statement is used to import a table, the table name is not specified, and the imported data is saved to the table path with the same name as the source table. Pay attention to the following points:

         -  If there is no table with the same name as that in the source cluster in the destination cluster, such a table will be created during the table import.
         -  Otherwise, the HDFS directory of the table must be empty, or the import fails.

      -  If the **import external table** *import_test* **from '**\ */tmp/export*\ **';** statement is used to import a table, the exported table is imported to the specified table. Pay attention to the following points:

         -  If there is no table with the same name as the specified table exists in the destination cluster, such a table will be created during the table import.
         -  Otherwise, the HDFS directory of the table must be empty, or the import fails.

      **hacluster X** is the value of **haclusterX** in new custom parameter\ **dfs.namenode.rpc-address.haclusterX**.
