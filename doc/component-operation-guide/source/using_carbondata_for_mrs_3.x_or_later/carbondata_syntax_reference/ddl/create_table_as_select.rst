:original_name: mrs_01_1426.html

.. _mrs_01_1426:

CREATE TABLE As SELECT
======================

Function
--------

This command is used to create a CarbonData table by specifying the list of fields along with the table properties.

Syntax
------

**CREATE TABLE**\ * [IF NOT EXISTS] [db_name.]table_name* **STORED AS carbondata** *[TBLPROPERTIES (key1=val1, key2=val2, ...)] AS select_statement;*

Parameter Description
---------------------

.. table:: **Table 1** CREATE TABLE parameters

   +---------------+----------------------------------------------------------------------------------------------------------------------------+
   | Parameter     | Description                                                                                                                |
   +===============+============================================================================================================================+
   | db_name       | Database name that contains letters, digits, and underscores (_).                                                          |
   +---------------+----------------------------------------------------------------------------------------------------------------------------+
   | table_name    | Table name of a database that contains letters, digits, and underscores (_).                                               |
   +---------------+----------------------------------------------------------------------------------------------------------------------------+
   | STORED AS     | Used to store data in CarbonData format.                                                                                   |
   +---------------+----------------------------------------------------------------------------------------------------------------------------+
   | TBLPROPERTIES | List of CarbonData table properties. For details, see :ref:`Precautions <mrs_01_1425__s4539dafd333c46ae855caaa175609f60>`. |
   +---------------+----------------------------------------------------------------------------------------------------------------------------+

Precautions
-----------

N/A

Examples
--------

**CREATE TABLE** ctas_select_parquet **STORED AS** carbondata as select \* from parquet_ctas_test;

System Response
---------------

This example will create a Carbon table from any Parquet table and load all the records from the Parquet table.
