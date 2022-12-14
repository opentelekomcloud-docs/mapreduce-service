:original_name: mrs_01_1435.html

.. _mrs_01_1435:

REGISTER INDEX TABLE
====================

Function
--------

This command is used to register an index table with the primary table.

Syntax
------

**REGISTER INDEX TABLE** *indextable_name* ON *db_name.maintable_name*;

Parameter Description
---------------------

.. table:: **Table 1** REFRESH INDEX TABLE parameters

   +-----------------+--------------------------------------------------------------------------------------+
   | Parameter       | Description                                                                          |
   +=================+======================================================================================+
   | db_name         | Database name. If this parameter is not specified, the current database is selected. |
   +-----------------+--------------------------------------------------------------------------------------+
   | indextable_name | Index table name.                                                                    |
   +-----------------+--------------------------------------------------------------------------------------+
   | maintable_name  | Primary table name.                                                                  |
   +-----------------+--------------------------------------------------------------------------------------+

Precautions
-----------

Before running this command, run **REFRESH TABLE** to register the primary table and secondary index table with the Hive metastore.

Examples
--------

**create database** **productdb;**

**use productdb;**

**CREATE TABLE productSalesTable(a int,b string,c string) stored as carbondata;**

**create index productNameIndexTable on table productSalesTable(c) as 'carbondata';**

**insert into table productSalesTable select 1,'a','aaa';**

**create database productdb2;**

Run the **hdfs** command to copy **productSalesTable** and **productNameIndexTable** in the **productdb** database to the **productdb2** database.

**refresh table productdb2.productSalesTable ;**

**refresh table productdb2.productNameIndexTable ;**

**explain select \* from productdb2.productSalesTable where c = 'aaa';** / The query command does not use an index table.

**REGISTER INDEX TABLE productNameIndexTable ON productdb2.productSalesTable;**

**explain select \* from productdb2.productSalesTable where c = 'aaa';** // The query command uses an index table.

System Response
---------------

By running this command, the index table will be registered to the primary table.
