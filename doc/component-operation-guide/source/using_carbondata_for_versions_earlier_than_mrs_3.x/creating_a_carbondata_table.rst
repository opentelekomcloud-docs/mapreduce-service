:original_name: mrs_01_0388.html

.. _mrs_01_0388:

Creating a CarbonData Table
===========================

Scenario
--------

A CarbonData table must be created to load and query data.

Creating a Table with Self-Defined Columns
------------------------------------------

Users can create a table by specifying its columns and data types. For analysis clusters with Kerberos authentication enabled, if a user wants to create a CarbonData table in a database other than the **default** database, the **Create** permission of the database must be added to the role to which the user is bound in Hive role management.

Sample command:

**CREATE TABLE** **IF NOT EXISTS productdb.productSalesTable (**

**productNumber Int,**

**productName String,**

**storeCity String,**

**storeProvince String,**

**revenue Int)**

**STORED BY** *'*\ **org.apache.carbondata.format'**

**TBLPROPERTIES (**

**'table_blocksize'='128',**

**'DICTIONARY_EXCLUDE'='productName',**

**'DICTIONARY_INCLUDE'='productNumber');**

The following table describes parameters of preceding commands.

.. table:: **Table 1** Parameter description

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                                                                                                                                                                                                                                |
   +===================================+============================================================================================================================================================================================================================================================================================================================================================================+
   | productSalesTable                 | Table name. The table is used to load data for analysis.                                                                                                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | The table name consists of letters, digits, and underscores (_).                                                                                                                                                                                                                                                                                                           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | productdb                         | Database name. The database maintains logical connections with tables stored in it to identify and manage the tables.                                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | The database name consists of letters, digits, and underscores (_).                                                                                                                                                                                                                                                                                                        |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | productNumber                     | Columns in the table. The columns are service entities for data analysis.                                                                                                                                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                            |
   | productName                       | The column name (field name) consists of letters, digits, and underscores (_).                                                                                                                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                            |
   | storeCity                         | .. note::                                                                                                                                                                                                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                            |
   | storeProvince                     |    In CarbonData, you cannot configure a column's NOT NULL or default value, or the primary key of the table.                                                                                                                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                            |
   | revenue                           |                                                                                                                                                                                                                                                                                                                                                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | table_blocksize                   | Block size of data files used by the CarbonData table. The value ranges from 1 MB to 2048 MB. The default is 1024 MB.                                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | -  If the value of **table_blocksize** is too small, a large number of small files will be generated when data is loaded. This may affect the performance in using HDFS.                                                                                                                                                                                                   |
   |                                   | -  If the value of **table_blocksize** is too large, a large volume of data must be read from a block and the read concurrency is low when data is queried. As a result, the query performance deteriorates.                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | You are advised to set the block size based on the data volume. For example, set the block size to 256 MB for GB-level data, 512 MB for TB-level data, and 1024 MB for PB-level data.                                                                                                                                                                                      |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DICTIONARY_EXCLUDE                | Specifies the columns that do not generate dictionaries. This function is optional and applicable to columns of high complexity. By default, the system generates dictionaries for columns of the String type. However, as the number of values in the dictionaries increases, conversion operations by the dictionaries increase and the system performance deteriorates. |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | Generally, if a column has over 50,000 unique data records, it is considered as a highly complex column and dictionary generation must be disabled.                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | .. note::                                                                                                                                                                                                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   |    Non-dictionary columns support only the String and Timestamp data types.                                                                                                                                                                                                                                                                                                |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DICTIONARY_INCLUDE                | Specifies the columns that generate dictionaries. This function is optional and applicable to columns of low complexity. It improves the performance of queries with the **groupby** condition. Generally, the complexity of a dictionary column cannot exceed 50,000.                                                                                                     |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
