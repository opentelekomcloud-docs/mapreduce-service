:original_name: mrs_01_24491.html

.. _mrs_01_24491:

Why Cannot I Query Newly Inserted Data in an ORC Hive Table Using Spark SQL?
============================================================================

Question
--------

Why cannot I query newly inserted data in an ORC Hive table using Spark SQL? This problem occurs in the following scenarios:

-  For partitioned tables and non-partitioned tables, after data is inserted on the Hive client, the latest inserted data cannot be queried using Spark SQL.
-  After data is inserted into a partitioned table using Spark SQL, if the partition information remains unchanged, the newly inserted data cannot be queried using Spark SQL.

Answer
------

To improve Spark performance, ORC metadata is cached. When the ORC table is updated by Hive or another means, the cached metadata remains unchanged, resulting in Spark SQL failing to query the newly inserted data.

For an ORC Hive partition table, if the partition information remains unchanged after data is inserted, the cached metadata is not updated. As a result, the newly inserted data cannot be queried by Spark SQL.

**Solution**

#. To solve the query problem, update metadata before starting a Spark SQL query.

   **REFRESH TABLE** *table_name*\ **;**

   *table_name* indicates the name of the table to be updated. The table must exist. Otherwise, an error is reported.

   When the query statement is executed, the latest inserted data can be obtained.

#. Run the following command to disable Spark optimization when using Spark:

   **set spark.sql.hive.convertMetastoreOrc=false;**
