:original_name: mrs_01_1427.html

.. _mrs_01_1427:

DROP TABLE
==========

Function
--------

This command is used to delete an existing table.

Syntax
------

**DROP TABLE** *[IF EXISTS] [db_name.]table_name;*

Parameter Description
---------------------

.. table:: **Table 1** DROP TABLE parameters

   +------------+--------------------------------------------------------------------------------------+
   | Parameter  | Description                                                                          |
   +============+======================================================================================+
   | db_name    | Database name. If this parameter is not specified, the current database is selected. |
   +------------+--------------------------------------------------------------------------------------+
   | table_name | Name of the table to be deleted                                                      |
   +------------+--------------------------------------------------------------------------------------+

Precautions
-----------

In this command, **IF EXISTS** and **db_name** are optional.

Example
-------

**DROP TABLE IF EXISTS productDatabase.productSalesTable;**

System Response
---------------

The table will be deleted.
