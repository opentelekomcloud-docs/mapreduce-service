:original_name: mrs_01_1446.html

.. _mrs_01_1446:

SHOW SECONDARY INDEXES
======================

Function
--------

This command is used to list all secondary index tables in the CarbonData table.

Syntax
------

**SHOW INDEXES ON db_name.table_name**;

Parameter Description
---------------------

.. table:: **Table 1** SHOW SECONDARY INDEXES parameters

   +------------+-----------------------------------------------------------------------------------------+
   | Parameter  | Description                                                                             |
   +============+=========================================================================================+
   | db_name    | Database name. It consists of letters, digits, and special characters (_).              |
   +------------+-----------------------------------------------------------------------------------------+
   | table_name | Name of the database table. It consists of letters, digits, and special characters (_). |
   +------------+-----------------------------------------------------------------------------------------+

Precautions
-----------

**db_name** is optional.

Examples
--------

**create table productdb.productSalesTable(id int,price int,productName string,city string) stored as carbondata;**

**CREATE INDEX productNameIndexTable on table productdb.productSalesTable (productName,city) as 'carbondata' ;**

**SHOW INDEXES ON productdb.productSalesTable**;

System Response
---------------

All index tables and corresponding index columns in a given CarbonData table will be listed.
