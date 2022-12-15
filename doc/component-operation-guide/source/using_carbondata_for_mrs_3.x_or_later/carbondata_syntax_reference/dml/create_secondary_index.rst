:original_name: mrs_01_1445.html

.. _mrs_01_1445:

CREATE SECONDARY INDEX
======================

Function
--------

This command is used to create secondary indexes in the CarbonData tables.

Syntax
------

**CREATE INDEX** *index_name*

**ON TABLE** *[db_name.]table_name (col_name1, col_name2)*

**AS** *'carbondata*'

**PROPERTIES** *('table_blocksize'='256')*;

Parameter Description
---------------------

.. table:: **Table 1** CREATE SECONDARY INDEX parameters

   +-----------------+--------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Description                                                                                                              |
   +=================+==========================================================================================================================+
   | index_name      | Index table name. It consists of letters, digits, and special characters (_).                                            |
   +-----------------+--------------------------------------------------------------------------------------------------------------------------+
   | db_name         | Database name. It consists of letters, digits, and special characters (_).                                               |
   +-----------------+--------------------------------------------------------------------------------------------------------------------------+
   | table_name      | Name of the database table. It consists of letters, digits, and special characters (_).                                  |
   +-----------------+--------------------------------------------------------------------------------------------------------------------------+
   | col_name        | Name of a column in a table. Multiple columns are supported. It consists of letters, digits, and special characters (_). |
   +-----------------+--------------------------------------------------------------------------------------------------------------------------+
   | table_blocksize | Block size of a data file. For details, see :ref:`•Block Size <mrs_01_1425__l053c6fa1a366488ea6410cb4bb4fc5d1>`.         |
   +-----------------+--------------------------------------------------------------------------------------------------------------------------+

Precautions
-----------

**db_name** is optional.

Examples
--------

**create table** **productdb.productSalesTable(id int,price int,productName string,city string) stored** **as** **carbondata;**

**CREATE INDEX productNameIndexTable on table productdb.productSalesTable (productName,city) as 'carbondata' ;**

In this example, a secondary table named **productdb.productNameIndexTable** is created and index information of the provided column is loaded.

System Response
---------------

A secondary index table will be created. Index information related to the provided column will be loaded into the secondary index table. The success message will be recorded in system logs.
