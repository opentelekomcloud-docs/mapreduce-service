:original_name: mrs_01_24118.html

.. _mrs_01_24118:

Hive Supporting Cold and Hot Storage of Partitioned Metadata
============================================================

Cold and Hot Storage of Partitioned Metadata
--------------------------------------------

-  The metadata that have not been used for a long time is moved to a backup table to reduce the pressure on metadata databases. This process is called partitioned data freezing. The partitions in which data is moved are cold partitions, partitions that are not frozen are hot partitions. A table with a cold partition is a frozen table. Moving the frozen data back to the original metadata table is called partitioned data unfreezing.
-  When a partition is changed from a hot partition to a cold partition, only metadata is identified. The partition path and data file content on the HDFS service side do not change.

Freezing a Partition
--------------------

The user who creates the table can freeze one or more partitions based on filter criteria. The format is **freeze partitions** *Database name Table name* **where** *Filter criteria*.

Example:

.. code-block::

   freeze partitions testdb.test where year <= 2021;
   freeze partitions testdb.test where year<=2021 and month <= 5;
   freeze partitions testdb.test where year<=2021 and month <= 5 and day <= 27;

Unfreezing a Partition
----------------------

The user who creates the table can unfreeze one or more partitions based on filter criteria. The format is **unfreeze partitions** *Database name Table name* **where** *Filter criteria*. Example:

.. code-block::

   unfreeze partitions testdb.test where year <= 2021;
   unfreeze partitions testdb.test where year<=2021 and month <= 5;
   unfreeze partitions testdb.test where year<=2021 and month <= 5 and day <= 27;

Querying Tables with Frozen Data
--------------------------------

-  Querying all frozen tables in the current database

   **show frozen tables**;

-  Querying all frozen tables in the **dbname** database

   **show frozen tables in dbname**;

Querying Frozen Partitions of a Frozen Table
--------------------------------------------

Querying frozen partitions

**show frozen partitions table**;

.. note::

   -  By default, only partitions of the int, string, varchar, date, or timestamp type can be frozen in the metadata database.
   -  For external metadata databases, only the Postgres database is supported, and only partitions of the int, string, varchar, or timestamp type can be frozen.
   -  You need to unfreeze data to restore the metadata of a frozen table using MSCK. If a frozen table has been backed up, you can run **msck repair** to restore the table, and you can only run this command to unfreeze the table.
   -  You need to unfreeze data before renaming a frozen partition. Otherwise, a message indicating that the partition does not exist is displayed.
   -  When a table that contains frozen data is deleted, the frozen data is also deleted.
   -  When a partition that contains frozen data is deleted, information about the frozen partition and HDFS service data are not deleted.
   -  When you run the **select** command to query data, the criteria for filtering the data in cold partitions is automatically added. The query result does not contain the data in cold partitions.
   -  When you run the **show partitions table** command to query the partitioned data in the table, the query result does not contain the data in cold partitions. You can run the **show frozen partitions table** command to query frozen partitions.
