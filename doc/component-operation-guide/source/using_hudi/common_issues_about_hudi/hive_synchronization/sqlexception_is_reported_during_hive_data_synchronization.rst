:original_name: mrs_01_24081.html

.. _mrs_01_24081:

SQLException Is Reported During Hive Data Synchronization
=========================================================

Question
--------

The following error is reported during Hive data synchronization:

.. code-block::

   Caused by: java.sql.SQLException: Error while processing statement: FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.DDLTask. Unable to alter table. The following columns have types incompatible with the existing columns in their respective positions :
   __col1,__col2

Answer
------

This error usually occurs when you try to add a new column to an existing Hive table using the **HiveSyncTool.java** class. Databases usually do not allow the modification of a column data type from a higher order to lower order or cases where the data types may conflict with the data that is already stored or will be stored in the table. To solve this problem,

set **hive.metastore.disallow.in compatible.col.type.changes** to **false**.
