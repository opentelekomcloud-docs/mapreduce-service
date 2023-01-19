:original_name: mrs_01_1409.html

.. _mrs_01_1409:

Creating a CarbonData Table
===========================

Scenario
--------

A CarbonData table must be created to load and query data. You can run the **Create Table** command to create a table. This command is used to create a table using custom columns.

Creating a Table with Self-Defined Columns
------------------------------------------

Users can create a table by specifying its columns and data types.

Sample command:

**CREATE TABLE** *IF NOT EXISTS productdb.productSalesTable (*

*productNumber Int,*

*productName String,*

*storeCity String,*

*storeProvince String,*

*productCategory String,*

*productBatch String,*

*saleQuantity Int,*

*revenue Int)*

STORED AS *carbondata*

*TBLPROPERTIES (*

*'table_blocksize'='128');*

The following table describes parameters of preceding commands.

.. table:: **Table 1** Parameter description

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                                                                                       |
   +===================================+===================================================================================================================================================================================================================================+
   | productSalesTable                 | Table name. The table is used to load data for analysis.                                                                                                                                                                          |
   |                                   |                                                                                                                                                                                                                                   |
   |                                   | The table name consists of letters, digits, and underscores (_).                                                                                                                                                                  |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | productdb                         | Database name. The database maintains logical connections with tables stored in it to identify and manage the tables.                                                                                                             |
   |                                   |                                                                                                                                                                                                                                   |
   |                                   | The database name consists of letters, digits, and underscores (_).                                                                                                                                                               |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | productName                       | Columns in the table. The columns are service entities for data analysis.                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                   |
   | storeCity                         | The column name (field name) consists of letters, digits, and underscores (_).                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                   |
   | storeProvince                     |                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                   |
   | procuctCategory                   |                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                   |
   | productBatch                      |                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                   |
   | saleQuantity                      |                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                   |
   | revenue                           |                                                                                                                                                                                                                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | table_blocksize                   | Indicates the block size of data files used by the CarbonData table, in MB. The value ranges from **1** to **2048**. The default value is **1024**.                                                                               |
   |                                   |                                                                                                                                                                                                                                   |
   |                                   | If **table_blocksize** is too small, a large number of small files will be generated when data is loaded. This may affect the performance of HDFS.                                                                                |
   |                                   |                                                                                                                                                                                                                                   |
   |                                   | If **table_blocksize** is too large, during data query, the amount of block data that matches the index is large, and some blocks contain a large number of blocklets, affecting read concurrency and lowering query performance. |
   |                                   |                                                                                                                                                                                                                                   |
   |                                   | You are advised to set the block size based on the data volume. For example, set the block size to 256 MB for GB-level data, 512 MB for TB-level data, and 1024 MB for PB-level data.                                             |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   -  Measurement of all integer data is processed and displayed using the **BigInt** data type.
   -  CarbonData parses data strictly. Any data that cannot be parsed is saved as **null** in the table. For example, if the user loads the **double** value (3.14) to the BigInt column, the data is saved as **null**.
   -  The Short and Long data types used in the **Create Table** command are shown as smallint and bigint in the **DESCRIBE** command, respectively.
   -  You can run the **DESCRIBE** command to view the table data size and table index size.

Operation Result
----------------

Run the command to create a table.
