:original_name: mrs_01_0981.html

.. _mrs_01_0981:

Optimizing Data Storage
=======================

Scenario
--------

**ORC** is an efficient column storage format and has higher compression ratio and reading efficiency than other file formats.

You are advised to use **ORC** as the default Hive table storage format.

Prerequisites
-------------

You have logged in to the Hive client. For details, see :ref:`Using a Hive Client <mrs_01_0952>`.

Procedure
---------

-  Recommended: **SNAPPY** compression, which applies to scenarios with even compression ratio and reading efficiency requirements.

   **Create table xx (col_name data_type) stored as orc tblproperties ("orc.compress"="SNAPPY");**

-  Available: **ZLIB** compression, which applies to scenarios with high compression ratio requirements.

   **Create table xx (col_name data_type) stored as orc tblproperties ("orc.compress"="ZLIB");**

.. note::

   *xx* indicates the specific Hive table name.
