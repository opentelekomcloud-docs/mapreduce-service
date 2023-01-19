:original_name: mrs_01_1761.html

.. _mrs_01_1761:

Error Reported When the WHERE Condition Is Used to Query Tables with Excessive Partitions in FusionInsight Hive
===============================================================================================================

Question
--------

When a table with more than 32,000 partitions is created in Hive, an exception occurs during the query with the WHERE partition. In addition, the exception information printed in **metastore.log** contains the following information:

.. code-block::

   Caused by: java.io.IOException: Tried to send an out-of-range integer as a 2-byte value: 32970
           at org.postgresql.core.PGStream.SendInteger2(PGStream.java:199)
           at org.postgresql.core.v3.QueryExecutorImpl.sendParse(QueryExecutorImpl.java:1330)
           at org.postgresql.core.v3.QueryExecutorImpl.sendOneQuery(QueryExecutorImpl.java:1601)
           at org.postgresql.core.v3.QueryExecutorImpl.sendParse(QueryExecutorImpl.java:1191)
           at org.postgresql.core.v3.QueryExecutorImpl.execute(QueryExecutorImpl.java:346)

Answer
------

During a query with partition conditions, HiveServer optimizes the partitions to avoid full table scanning. All partitions whose metadata meets the conditions need to be queried. However, the **sendOneQuery** interface provided by GaussDB limits the parameter value to **32767** in the **sendParse** method. If the number of partition conditions exceeds **32767**, an exception occurs.
