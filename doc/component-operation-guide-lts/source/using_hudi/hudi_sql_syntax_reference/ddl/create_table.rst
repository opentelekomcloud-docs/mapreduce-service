:original_name: mrs_01_24264.html

.. _mrs_01_24264:

CREATE TABLE
============

Function
--------

This command is used to create a Hudi table by specifying the list of fields along with the table options.

Syntax
------

**CREATE TABLE** *[ IF NOT EXISTS] [database_name.]table_name*

*[ (columnTypeList)]*

**USING hudi**

*[ COMMENT table_comment ]*

*[ LOCATION location_path ]*

*[ OPTIONS (options_list) ]*

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   +----------------+-----------------------------------------------------------------------------------------------------------------+
   | Parameter      | Description                                                                                                     |
   +================+=================================================================================================================+
   | database_name  | Database name that contains letters, digits, and underscores (_).                                               |
   +----------------+-----------------------------------------------------------------------------------------------------------------+
   | table_name     | Database table name that contains letters, digits, and underscores (_).                                         |
   +----------------+-----------------------------------------------------------------------------------------------------------------+
   | columnTypeList | List of comma-separated columns with data types. The column name contains letters, digits, and underscores (_). |
   +----------------+-----------------------------------------------------------------------------------------------------------------+
   | using          | Uses **hudi** to define and create a Hudi table.                                                                |
   +----------------+-----------------------------------------------------------------------------------------------------------------+
   | table_comment  | Description of the table.                                                                                       |
   +----------------+-----------------------------------------------------------------------------------------------------------------+
   | location_path  | HDFS path. If this parameter is set, the Hudi table will be created as an external table.                       |
   +----------------+-----------------------------------------------------------------------------------------------------------------+
   | options_list   | List of Hudi table options.                                                                                     |
   +----------------+-----------------------------------------------------------------------------------------------------------------+

.. table:: **Table 2** Table options

   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Description                                                                                                                                                                                                                                     |
   +=================+=================================================================================================================================================================================================================================================+
   | primaryKey      | Name of the primary key with fields separated by commas (,).                                                                                                                                                                                    |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | type            | Type of the table. **'cow'** indicates a copy-on-write (COW) table, and **'mor'** indicates a merge-on-read (MOR) table. If this parameter is not specified, the default value is **'cow'**.                                                    |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | preCombineField | Pre-Combine field in the table.                                                                                                                                                                                                                 |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | payloadClass    | Payload classes for data filtering, including default **OverwriteWithLatestAvroPayload** and multiple preset payloads, such as **OverwriteNonDefaultsWithLatestAvroPayload**, **DefaultHoodieRecordPayload**, and **EmptyHoodieRecordPayload**. |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Examples
--------

-  **Create a non-partitioned table**.

   .. code-block::

      -- Create an internal COW table.
      create table if not exists hudi_table0 (
      id int,
      name string,
      price double
      )  using hudi
      options (
      type = 'cow',
      primaryKey = 'id'
      );

   .. code-block::

      -- Create an external MOR table.
      create table if not exists hudi_table1 (
      id int,
      name string,
      price double,
      ts bigint
      )  using hudi
      location '/tmp/hudi/hudi_table1'
      options (
      type = 'mor',
      primaryKey = 'id,name',
      preCombineField = 'ts'
      );

   .. code-block::

      -- Create a table without primary keys.
      create table if not exists hudi_table2(
      id int,
      name string,
      price double
      )  using hudi
      options (
      type = 'cow'
      );

-  **Create a partitioned table**.

   .. code-block::

      create table if not exists hudi_table_p0 (
      id bigint,
      name string,
      ts bigint,
      dt string,
      hh string
      )  using hudi
      location '/tmp/hudi/hudi_table_p0'
      options (
      type = 'cow',
      primaryKey = 'id',
      preCombineField = 'ts'
      )
      partitioned by (dt, hh);

-  **Create an external table for the Hudi table created using spark-shell or deltastreamer before Hudi 0.9.0.**

   .. code-block::

      create table h_p1
      using hudi
      options (
      primaryKey = 'id',
      preCombineField = 'ts'
      )
      partitioned by (dt)
      location '/path/to/hudi';

-  Create a table and specify table options.

   .. code-block::

      create table if not exists h3(
      id bigint,
      name string,
      price double
      ) using hudi
      options (
      primaryKey = 'id',
      type = 'mor',
      hoodie.cleaner.fileversions.retained = '20',
      hoodie.keep.max.commits = '20'
      );

Precautions
-----------

Currently, Hudi does not support the CHAR, VARCHAR, TINYINT, and SMALLINT data types. You are advised to use the string or INT data type.

System Response
---------------

The table is successfully created, and the success message is logged in the system.
