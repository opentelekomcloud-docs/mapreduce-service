:original_name: mrs_01_1441.html

.. _mrs_01_1441:

INSERT INTO CARBON TABLE
========================

Function
--------

This command is used to add the output of the SELECT command to a Carbon table.

Syntax
------

**INSERT INTO [CARBON TABLE] [select query]**;

Parameter Description
---------------------

.. table:: **Table 1** INSERT INTO parameters

   +--------------+---------------------------------------------------------------------------------------+
   | Parameter    | Description                                                                           |
   +==============+=======================================================================================+
   | CARBON TABLE | Name of the CarbonData table to be inserted                                           |
   +--------------+---------------------------------------------------------------------------------------+
   | select query | SELECT query on the source table (CarbonData, Hive, and Parquet tables are supported) |
   +--------------+---------------------------------------------------------------------------------------+

Precautions
-----------

-  A table has been created.

-  You must belong to the data loading group in order to perform data loading operations. By default, the data loading group is named **ficommon**.

-  CarbonData tables cannot be overwritten.

-  The data type of the source table and the target table must be the same. Otherwise, data in the source table will be regarded as bad records.

-  The **INSERT INTO** command does not support partial success. If bad records exist, the command fails.

-  When you insert data of the source table to the target table, you cannot upload or update data of the source table.

   To enable data loading or updating during the INSERT operation, set the following parameter to **true**.

   **carbon.insert.persist.enable**\ =\ **true**

   By default, the preceding parameters are set to **false**.

   .. note::

      Enabling this property will reduce the performance of the INSERT operation.

Example
-------

**INSERT INTO CARBON select \* from TABLENAME**;

System Response
---------------

Success or failure will be recorded in the driver logs.
