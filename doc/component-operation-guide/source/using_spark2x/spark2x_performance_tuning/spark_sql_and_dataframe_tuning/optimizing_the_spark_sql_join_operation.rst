:original_name: mrs_01_1986.html

.. _mrs_01_1986:

Optimizing the Spark SQL Join Operation
=======================================

Scenario
--------

When two tables are joined in Spark SQL, the broadcast function (see section "Using Broadcast Variables") can be used to broadcast tables to each node. This minimizes shuffle operations and improves task execution efficiency.

.. note::

   The join operation refers to the inner join operation only.

Procedure
---------

The following describes how to optimize the join operation in Spark SQL. Assume that both tables A and B have the **name** column. Join tables A and B as follows:

#. Estimate the table sizes.

   Estimate the table size based on the size of data loaded each time.

   You can also check the table size in the directory of the Hive database. In the **hive-site.xml** configuration file of Spark, view the Hive database directory, which is **/user/hive/warehouse** by default. The default Hive database directory for multi-instance Spark is **/user/**\ *hive*\ **/warehouse**, for example, **/user/hive1/warehouse**.

   .. code-block::

      <property>
         <name>hive.metastore.warehouse.dir</name>
        <value>${test.warehouse.dir}</value>
        <description></description>
      </property>

   Run the **hadoop** command to check the size of the table. For example, run the following command to view the size of table **A**:

   .. code-block::

      hadoop fs -du -s -h ${test.warehouse.dir}/a

   .. note::

      To perform the broadcast operation, ensure that at least one table is not empty.

#. Configure a threshold for automatic broadcast.

   The threshold for triggering broadcast for a table is 10485760 (that is, 10 MB) in Spark. If either of the table sizes is smaller than 10 MB, skip this step.

   :ref:`Table 1 <mrs_01_1986__te463b16123694e6fa752df6986dc3e0a>` lists configuration parameters of the threshold for automatic broadcasting.

   .. _mrs_01_1986__te463b16123694e6fa752df6986dc3e0a:

   .. table:: **Table 1** Parameter description

      +--------------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                            | Default Value         | Description                                                                                                                                            |
      +======================================+=======================+========================================================================================================================================================+
      | spark.sql.autoBroadcastJoinThreshold | 10485760              | Indicates the maximum value for the broadcast configuration when two tables are joined.                                                                |
      |                                      |                       |                                                                                                                                                        |
      |                                      |                       | -  When the size of a field in a table involved in an SQL statement is less than the value of this parameter, the system broadcasts the SQL statement. |
      |                                      |                       | -  If the value is set to **-1**, broadcast is not performed.                                                                                          |
      |                                      |                       |                                                                                                                                                        |
      |                                      |                       | For details, visit https://archive.apache.org/dist/spark/docs/3.1.1/sql-programming-guide.html.                                                        |
      +--------------------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+

   Methods for configuring the threshold for automatic broadcasting:

   -  Set **spark.sql.autoBroadcastJoinThreshold** in the **spark-defaults.conf** configuration file of Spark.

      .. code-block::

         spark.sql.autoBroadcastJoinThreshold = <size>

   -  Run the Hive command to set the threshold. Before joining the tables, run the following command:

      .. code-block::

         SET spark.sql.autoBroadcastJoinThreshold=<size>;

#. Join the tables.

   -  The size of each table is smaller than the threshold.

      -  If the size of table A is smaller than that of table B, run the following command:

         .. code-block::

            SELECT A.name FROM B JOIN A ON A.name = B.name;

      -  If the size of table B is smaller than that of table A, run the following command:

         .. code-block::

            SELECT A.name FROM A JOIN B ON A.name = B.name;

   -  One table size is smaller than the threshold, while the other table size is greater than the threshold.

      Broadcast the smaller table.

   -  The size of each table is greater than the threshold.

      Compare the size of the field involved in the query with the threshold.

      -  If the values of the fields in a table are smaller than the threshold, the corresponding data in the table is broadcast.
      -  If the values of the fields in the two tables are greater than the threshold, do not broadcast either of the table.

#. (Optional) In the following scenarios, you need to run the Analyze command (**ANALYZE TABLE tableName COMPUTE STATISTICS noscan;**) to update metadata before performing the broadcast operation:

   -  The table to be broadcasted is a newly created partitioned table and the file type is non-Parquet.
   -  The table to be broadcasted is a newly updated partitioned table.

Reference
---------

A task is ended if a timeout occurs during the execution of the to-be-broadcasted table.

By default, BroadCastJoin allows only 5 minutes for the to-be-broadcasted table calculation. If the time is exceeded, a timeout will occur. However, the broadcast task of the to-be-broadcasted table calculation is still being executed, resulting in resource waste.

The following methods can be used to address this issue:

-  Modify the value of **spark.sql.broadcastTimeout** to increase the timeout duration.
-  Reduce the value of **spark.sql.autoBroadcastJoinThreshold** to disable the optimization of BroadCastJoin.
