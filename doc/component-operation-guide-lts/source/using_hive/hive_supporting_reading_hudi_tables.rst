:original_name: mrs_01_24040.html

.. _mrs_01_24040:

Hive Supporting Reading Hudi Tables
===================================

Hive External Tables Corresponding to Hudi Tables
-------------------------------------------------

A Hudi source table corresponds to a copy of HDFS data. The Hudi table data can be mapped to a Hive external table through the Spark component, Flink component, or Hudi client. Based on the external table, Hive can easily perform real-time query, read-optimized view query, and incremental view query.

.. note::

   -  Different view queries are provided for different types of Hudi source tables:

      -  When the Hudi source table is a Copy-On-Write (COW) table, it can be mapped to a Hive external table. The table supports real-time query and incremental view query.
      -  When the Hudi source table is a Merge-On-Read (MOR) table, it can be mapped to two Hive external tables (RO table and RT table). The RO table supports read-optimized view query, and the RT table supports real-time view query and incremental view query.

   -  Hive external tables cannot be added, deleted, or modified (including **insert**, **update**, **delete**, **load**, **merge**, **alter** and **msck**). Only the query operation (**select**) is supported.

   -  Granting table permissions: The update, alter, write, and all permissions cannot be modified.

   -  Backup and restoration: The RO and RT tables are mapped from the same Hudi source table. When one table is backed up, the other table is also backed up. The same applies to restoration. Therefore, only one table needs to be backed up.

   -  Hudi bootstrap tables: The storage mode of bootstrap tables is different from that of common Hudi tables. Therefore, you need to configure **hive.user.aux.jars.path** for the Tez query engine. Log in to FusionInsight Manager, choose **Cluster** > **Services** > **Hive** > **Configurations** > **All Configurations**, and add the following paths to the value of **hive.user.aux.jars.path** (use commas (,) as separators):

      -  ${BIGDATA_HOME}/FusionInsight_HD\_8.1.2.2/install/FusionInsight-Hive-3.1.0/hive-3.1.0/lib/hbase-shaded-miscellaneous-xxx.jar
      -  ${BIGDATA_HOME}/FusionInsight_HD\_8.1.2.2/install/FusionInsight-Hive-3.1.0/hive-3.1.0/lib/hbase-metrics-api-xxx.jar
      -  ${BIGDATA_HOME}/FusionInsight_HD\_8.1.2.2/install/FusionInsight-Hive-3.1.0/hive-3.1.0/lib/hbase-metrics-xxx.jar
      -  ${BIGDATA_HOME}/FusionInsight_HD\_8.1.2.2/install/FusionInsight-Hive-3.1.0/hive-3.1.0/lib/hbase-protocol-shaded-xxx.jar
      -  ${BIGDATA_HOME}/FusionInsight_HD\_8.1.2.2/install/FusionInsight-Hive-3.1.0/hive-3.1.0/lib/hbase-shaded-protobuf-xxx.jar
      -  ${BIGDATA_HOME}/FusionInsight_HD\_8.1.2.2/install/FusionInsight-Hive-3.1.0/hive-3.1.0/lib/htrace-core4-4.2.0-incubatin-xxx.jar

      Replace *xxx* with the actual version in the path of the HiveServer node. For example, if the name of **hbase-shaded-miscellaneous-**\ *xxx*\ **.jar** in the actual environment is **hbase-shaded-miscellaneous-3.3.0.jar**, replace *xxx* with **3.3.0**.

   -  Component versions:

      -  Hive: FusionInsight_HD\_8.1.2.2; Hive kernel version 3.1.0.
      -  Spark2x: FusionInsight_Spark2x\_8.1.2.2; Hudi kernel version: 0.9.0.

Creating Hive External Tables Corresponding to Hudi Tables
----------------------------------------------------------

Generally, Hudi table data is synchronized to Hive external tables when the data is imported to the lake. In this case, you can directly query the corresponding Hive external tables in Beeline. If the data is not synchronized to the Hive external tables, you can use the Hudi client tool **run_hive_sync_tool.sh** to synchronize data manually.

Querying Hive External Tables Corresponding to Hudi Tables
----------------------------------------------------------

**Prerequisites**

Set **hive.input.format** before using Hive to query a Hudi table.

In addition, you need to set another three parameters for incremental query. The three parameters are table-level parameters. Each Hudi source table corresponds to three parameters, where **hudisourcetablename** indicates the name of the Hudi source table (not the name of the Hive external table).

.. table:: **Table 1** Parameter description

   +-----------------------------------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                                           | Default Value         | Description                                                                                                                                                                                                                                                   |
   +=====================================================+=======================+===============================================================================================================================================================================================================================================================+
   | hoodie. hudisourcetablename.consume.mode            | None                  | Query mode of the Hudi table.                                                                                                                                                                                                                                 |
   |                                                     |                       |                                                                                                                                                                                                                                                               |
   |                                                     |                       | -  Incremental query: Set it to **INCREMENTAL**.                                                                                                                                                                                                              |
   |                                                     |                       | -  Non-incremental query: Do not set this parameter or set it to **SNAPSHOT**.                                                                                                                                                                                |
   +-----------------------------------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hoodie. hudisourcetablename.consume.start.timestamp | None                  | Start time of the incremental query on the Hudi table.                                                                                                                                                                                                        |
   |                                                     |                       |                                                                                                                                                                                                                                                               |
   |                                                     |                       | -  Incremental query: start time of the incremental query.                                                                                                                                                                                                    |
   |                                                     |                       | -  Non-incremental query: Do not set this parameter.                                                                                                                                                                                                          |
   +-----------------------------------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hoodie. hudisourcetablename.consume.max.commits     | None                  | The incremental query on the Hudi table is based on the number of commits after **hoodie.hudisourcetablename.consume.start.timestamp**.                                                                                                                       |
   |                                                     |                       |                                                                                                                                                                                                                                                               |
   |                                                     |                       | -  Incremental query: number of commits. For example, if this parameter is set to **3**, data after three commits from the specified start time is queried. If this parameter is set to **-1**, all data committed after the specified start time is queried. |
   |                                                     |                       | -  Non-incremental query: Do not set this parameter.                                                                                                                                                                                                          |
   +-----------------------------------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Querying a Hudi COW Table**

For example, the name of a Hudi source table of the COW type is **hudicow**, and the name of the mapped Hive external table is **hudicow**.

-  Real-time view query on the COW table: After **hive.input.format** is set, query the COW table as a common Hive table.

   **set hive.input.format= org.apache.hadoop.hive.ql.io.HiveInputFormat;**

   **Select \* from hudicow;**

-  Incremental query on the COW table: In addition to **hive.input.format**, you need to set three incremental query parameters based on the name of the Hudi source table. The **where** clause of the incremental query statements must contain **\`_hoodie_commit_time`>'**\ *xxx*\ **'**, where *xxx* indicates the value of **hoodie.hudisourcetablename.consume.start.timestamp**.

   **set hive.input.format= org.apache.hadoop.hive.ql.io.HiveInputFormat;**

   **set hoodie.hudicow.consume.mode= INCREMENTAL;**

   **set hoodie.hudicow.consume.max.commits=3;**

   **set hoodie.hudicow.consume.start.timestamp= 20200427114546;**

   **select count(*) from hudicow where \`_hoodie_commit_time`>'20200427114546';**

**Querying a Hudi MOR Table**

For example, the name of a Hudi source table of the MOR type is **hudimor**, and the two mapped Hive external tables are **hudimor_ro** (RO table) and **hudimor_rt** (RT table).

-  Read-optimized view query on the RO table: After **hive.input.format** is set, query the COW table as a common Hive table.

   **set hive.input.format= org.apache.hadoop.hive.ql.io.HiveInputFormat;**

   **Select \* from hudicow_ro;**

-  Real-time view query on the RT table: After **hive.input.format** is set, the latest data of the Hudi source table can be queried.

   **set hive.input.format= org.apache.hadoop.hive.ql.io.HiveInputFormat;**

   **Select \* from hudicow_rt;**

-  Incremental query on the RT table: In addition to **hive.input.format**, you need to set three incremental query parameters based on the name of the Hudi source table. The **where** clause of the incremental query statements must contain **\`_hoodie_commit_time`>'**\ *xxx*\ **'**, where *xxx* indicates the value of **hoodie.hudisourcetablename.consume.start.timestamp**.

   **set hive.input.format=org.apache.hudi.hadoop.hive.HoodieCombineHiveInputFormat;**

   **set hoodie.hudimor.consume.mode=INCREMENTAL;**

   **set hoodie.hudimor.consume.max.commits=-1;**

   **set hoodie.hudimor.consume.start.timestamp=20210207144611;**

   **select \* from hudimor_rt where \`_hoodie_commit_time`>'20210207144611';**

   .. note::

      -  **set hive.input.format=org.apache.hudi.hadoop.hive.HoodieCombineHiveInputFormat;** is used only for the incremental query on the RT table and cannot be used for other tables. Therefore, after the incremental query on the RT table is complete, run **set hive.input.format=org.apache.hadoop.hive.ql.io.HiveInputFormat;**. Alternatively, run **set hive.input.format=org.apache.hadoop.hive.ql.io.CombineHiveInputFormat;** to change the value to the default value for the queries on other tables.
      -  **set hoodie.hudisourcetablename.consume.mode=INCREMENTAL;** is used only for the incremental query on the table. To switch to another query mode, run **set hoodie.hudisourcetablename.consume.mode=SNAPSHOT;**.
