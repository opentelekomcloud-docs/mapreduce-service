:original_name: mrs_01_1425.html

.. _mrs_01_1425:

CREATE TABLE
============

Function
--------

This command is used to create a CarbonData table by specifying the list of fields along with the table properties.

Syntax
------

**CREATE TABLE** *[IF NOT EXISTS] [db_name.]table_name*

*[(col_name data_type, ...)]*

**STORED AS** *carbondata*

*[TBLPROPERTIES (property_name=property_value, ...)];*

Additional attributes of all tables are defined in **TBLPROPERTIES**.

Parameter Description
---------------------

.. table:: **Table 1** CREATE TABLE parameters

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                                                  |
   +===================================+==============================================================================================================================================================================================+
   | db_name                           | Database name that contains letters, digits, and underscores (_).                                                                                                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | col_name data_type                | List with data types separated by commas (,). The column name contains letters, digits, and underscores (_).                                                                                 |
   |                                   |                                                                                                                                                                                              |
   |                                   | .. note::                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                              |
   |                                   |    When creating a CarbonData table, do not use tupleId, PositionId, and PositionReference as column names because columns with these names are internally used by secondary index commands. |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | table_name                        | Table name of a database that contains letters, digits, and underscores (_).                                                                                                                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | STORED AS                         | The **carbondata** parameter defines and creates a CarbonData table.                                                                                                                         |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | TBLPROPERTIES                     | List of CarbonData table properties.                                                                                                                                                         |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_01_1425__s4539dafd333c46ae855caaa175609f60:

Precautions
-----------

Table attributes are used as follows:

-  .. _mrs_01_1425__l053c6fa1a366488ea6410cb4bb4fc5d1:

   Block size

   The block size of a data file can be defined for a single table using **TBLPROPERTIES**. The larger one between the actual size of the data file and the defined block size is selected as the actual block size of the data file in HDFS. The unit is MB. The default value is 1024 MB. The value ranges from 1 MB to 2048 MB. If the value is beyond the range, the system reports an error.

   Once the block size reaches the configured value, the write program starts a new block of CarbonData data. Data is written in multiples of the page size (32,000 records). Therefore, the boundary is not strict at the byte level. If the new page crosses the boundary of the configured block, the page is written to the new block instead of the current block.

   *TBLPROPERTIES('table_blocksize'='128')*

   .. note::

      -  If a small block size is configured in the CarbonData table while the size of the data file generated by the loaded data is large, the block size displayed in HDFS is different from the configured value. This is because when data is written to a local block file for the first time, even though the size of the to-be-written data is larger than the configured value of the block size, data will still be written into the block. Therefore, the actual value of block size in HDFS is the larger value between the size of the data to be written and the configured block size.
      -  If **block.num** is less than the parallelism, the blocks are split into new blocks so that new blocks.num is greater than parallelism and all cores can be used. This optimization is called block distribution.

-  **SORT_SCOPE** specifies the sort scope during table creation. There are four types of sort scopes:

   -  **GLOBAL_SORT**: It improves query performance, especially for point queries. *TBLPROPERTIES('SORT_SCOPE'='GLOBAL_SORT'*)
   -  **LOCAL_SORT**: Data is sorted locally (task-level sorting).
   -  **NO_SORT**: The default sorting mode is used. Data is loaded in unsorted manner, which greatly improves loading performance.

-  SORT_COLUMNS

   This table property specifies the order of sort columns.

   *TBLPROPERTIES('SORT_COLUMNS'='column1, column3')*

   .. note::

      -  If this attribute is not specified, no columns are sorted by default.
      -  If this property is specified but with empty argument, then the table will be loaded without sort. For example, *('SORT_COLUMNS'='')*.
      -  **SORT_COLUMNS** supports the string, date, timestamp, short, int, long, byte, and boolean data types.

-  RANGE_COLUMN

   This property is used to specify a column to partition the input data by range. Only one column can be configured. During data import, you can use **global_sort_partitions** or **scale_factor** to avoid generating small files.

   *TBLPROPERTIES('RANGE_COLUMN'='column1')*

-  LONG_STRING_COLUMNS

   The length of a common string cannot exceed 32,000 characters. To store a string of more than 32,000 characters, set **LONG_STRING_COLUMNS** to the target column.

   *TBLPROPERTIES('LONG_STRING_COLUMNS'='column1, column3')*

   .. note::

      **LONG_STRING_COLUMNS** can be set only for columns of the STRING, CHAR, or VARCHAR type.

Scenarios
---------

Creating a Table by Specifying Columns

The **CREATE TABLE** command is the same as that of Hive DDL. The additional configurations of CarbonData are provided as table properties.

**CREATE TABLE** *[IF NOT EXISTS] [db_name.]table_name*

*[(col_name data_type , ...)]*

STORED AS *carbondata*

*[TBLPROPERTIES (property_name=property_value, ...)];*

Examples
--------

**CREATE TABLE** *IF NOT EXISTS productdb.productSalesTable (*

*productNumber Int,*

*productName String,*

*storeCity String,*

*storeProvince String,*

*productCategory String,*

*productBatch String,*

*saleQuantity Int,*

*revenue Int)*

*STORED AS carbondata*

*TBLPROPERTIES (*

*'table_blocksize'='128',*

*'SORT_COLUMNS'='productBatch, productName')*

System Response
---------------

A table will be created and the success message will be logged in system logs.
