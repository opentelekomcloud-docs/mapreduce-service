:original_name: mrs_01_24462.html

.. _mrs_01_24462:

What Should I Do If Data Failed to Be Synchronized to an ORC or Parquet Table Using hive-table?
===============================================================================================

Question
--------

What should I do if data failed to be synchronized to the ORC or parquet table using hive-table and error message that contains the **kite-sdk** package name is displayed?

Answer
------

Change **-hive-table** to **-hcatalog-table**.
