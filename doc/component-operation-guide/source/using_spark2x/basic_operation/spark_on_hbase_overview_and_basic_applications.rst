:original_name: mrs_01_1933.html

.. _mrs_01_1933:

Spark on HBase Overview and Basic Applications
==============================================

Scenario
--------

Spark on HBase allows users to query HBase tables in Spark SQL and to store data for HBase tables by using the Beeline tool. You can use HBase APIs to create, read data from, and insert data into tables.

Procedure
---------

#. Log in to Manager and choose **Cluster** > *Name of the desired cluster* > **Cluster Properties** to check whether the cluster is in security mode.

   -  If yes, go to :ref:`2 <mrs_01_1933__ld2cb5a391f5e4625bbe0de71686c6bb6>`.
   -  If no, go to :ref:`5 <mrs_01_1933__lca2e4c1523a4428f89fd147c1041a231>`.

#. .. _mrs_01_1933__ld2cb5a391f5e4625bbe0de71686c6bb6:

   Choose **Cluster >** *Name of the desired cluster* **>** **Service > Spark2x > Configuration > All Configurations > JDBCServer2x > Default**, and modify the following parameter.

   .. table:: **Table 1** Parameter list 1

      ============================================= ============= ==========
      Parameter                                     Default Value Changed To
      ============================================= ============= ==========
      spark.yarn.security.credentials.hbase.enabled false         true
      ============================================= ============= ==========

   .. note::

      To ensure that Spark2x can access HBase for a long time, do not modify the following parameters of the HBase and HDFS services:

      -  dfs.namenode.delegation.token.renew-interval
      -  dfs.namenode.delegation.token.max-lifetime
      -  hbase.auth.key.update.interval
      -  hbase.auth.token.max.lifetime (The value is fixed to **604800000** ms, that is, 7 days.)

      If the preceding parameter configuration must be modified based on service requirements, ensure that the value of the HDFS parameter **dfs.namenode.delegation.token.renew-interval** is not greater than the values of the HBase parameters **hbase.auth.key.update.interval**, **hbase.auth.token.max.lifetime**, and **dfs.namenode.delegation.token.max-lifetime**.

#. Choose **SparkResource2x** > **Default** and modify the following parameters.

   .. table:: **Table 2** Parameter list 2

      ============================================= ============= ==========
      Parameter                                     Default Value Changed To
      ============================================= ============= ==========
      spark.yarn.security.credentials.hbase.enabled false         true
      ============================================= ============= ==========

#. Restart the Spark2x service for the configuration to take effect.

   .. note::

      To use the Spark on HBase function on the Spark2x client, you need to download and install the Spark2x client again.

#. .. _mrs_01_1933__lca2e4c1523a4428f89fd147c1041a231:

   On the Spark2x client, use the spark-sql or spark-beeline connection to query tables created by Hive on HBase. You can create an HBase table by running SQL commands or create an external table to associate the HBase table. Before creating tables, ensure that HBase tables exist in HBase. The HBase table **table1** is used as an example.

   a. Run the following commands to create the HBase table using the Beeline tool:

      **create table** *hbaseTable*

      **(**

      *id string,*

      *name string,*

      *age int*

      **)**

      **using org.apache.spark.sql.hbase.HBaseSource**

      **options(**

      **hbaseTableName** *"table1"*\ **,**

      **keyCols** *"id"*\ **,**

      **colsMapping "**

      *name=cf1.cq1,*

      *age=cf1.cq2*

      **");**

      .. note::

         -  **hbaseTable**: name of the created Spark table
         -  **id string,name string**, **age int**: field name and field type of the Spark table
         -  **table1**: name of the HBase table
         -  *id*: row key column name of the HBase table
         -  *name=cf1.cq1*, *age=cf1.cq2*: mapping between columns in the Spark table and columns in the HBase table. The **name** column of the Spark table maps the **cq1** column in the **cf1** column family of the HBase table, and the **age** column of the Spark table maps the **cq2** column in the **cf1** column family of the HBase table.

   b. Run the following command to import data to the HBase table using a CSV file:

      **hbase org.apache.hadoop.hbase.mapreduce.ImportTsv** **-Dimporttsv.separator="," -Dimporttsv.columns=HBASE_ROW_KEY,**\ *cf1:cq1,cf1:cq2,cf1:cq3,cf1:cq4,cf1:cq5* *table1 /hperson*

      Where **table1** indicates the name of the HBase table, and **/hperson** indicates the path where the CSV file is stored.

   c. Run the following command to query data in spark-sql or spark-beeline, where *hbaseTable* is the corresponding Spark table name: The command is as follows:

      **select \* from** *hbaseTable;*
