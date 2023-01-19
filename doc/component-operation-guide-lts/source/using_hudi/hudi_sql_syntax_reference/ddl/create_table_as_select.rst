:original_name: mrs_01_24265.html

.. _mrs_01_24265:

CREATE TABLE AS SELECT
======================

Function
--------

This command is used to create a Hudi table by specifying the list of fields along with the table options.

Syntax
------

**CREATE TABLE** *[ IF NOT EXISTS] [database_name.]table_name*

**USING hudi**

*[ COMMENT table_comment ]*

*[ LOCATION location_path ]*

*[ OPTIONS (options_list) ]*

*[ AS query_statement ]*

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   +-----------------+-------------------------------------------------------------------------------------------+
   | Parameter       | Description                                                                               |
   +=================+===========================================================================================+
   | database_name   | Database name that contains letters, digits, and underscores (_).                         |
   +-----------------+-------------------------------------------------------------------------------------------+
   | table_name      | Database table name that contains letters, digits, and underscores (_).                   |
   +-----------------+-------------------------------------------------------------------------------------------+
   | using           | Uses **hudi** to define and create a Hudi table.                                          |
   +-----------------+-------------------------------------------------------------------------------------------+
   | table_comment   | Description of the table.                                                                 |
   +-----------------+-------------------------------------------------------------------------------------------+
   | location_path   | HDFS path. If this parameter is set, the Hudi table will be created as an external table. |
   +-----------------+-------------------------------------------------------------------------------------------+
   | options_list    | List of Hudi table options.                                                               |
   +-----------------+-------------------------------------------------------------------------------------------+
   | query_statement | SELECT statement                                                                          |
   +-----------------+-------------------------------------------------------------------------------------------+

Examples
--------

-  Create a partitioned table.

   .. code-block::

      create table h2 using hudi
      options (type = 'cow', primaryKey = 'id')
      partitioned by (dt)
      as
      select 1 as id, 'a1' as name, 10 as price, 1000 as dt;

-  Create a non-partitioned table.

   .. code-block::

      create table h3 using hudi
      as
      select 1 as id, 'a1' as name, 10 as price;

      Load data from a parquet table to the Hudi table.
      # Create a parquet table.
      create table parquet_mngd using parquet options(path='hdfs:///tmp/parquet_dataset/*.parquet');

      # Create a Hudi table by Creating a Table from Query Results (CTAS).
      create table hudi_tbl using hudi location 'hdfs:///tmp/hudi/hudi_tbl/' options (
      type = 'cow',
      primaryKey = 'id',
      preCombineField = 'ts'
      )
      partitioned by (datestr) as select * from parquet_mngd;

Precautions
-----------

For better data loading performance, CTAS uses **bulk insert** to write data.

System Response
---------------

The table is successfully created, and the success message is logged in the system.
