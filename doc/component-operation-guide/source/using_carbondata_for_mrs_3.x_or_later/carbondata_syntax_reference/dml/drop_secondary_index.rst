:original_name: mrs_01_1447.html

.. _mrs_01_1447:

DROP SECONDARY INDEX
====================

Function
--------

This command is used to delete the existing secondary index table in a specific table.

Syntax
------

**DROP INDEX** *[IF EXISTS] index_name*\ ** ON** *[db_name.]table_name*;

Parameter Description
---------------------

.. table:: **Table 1** DROP SECONDARY INDEX parameters

   +------------+----------------------------------------------------------------------------------------+
   | Parameter  | Description                                                                            |
   +============+========================================================================================+
   | index_name | Name of the index table. Table name contains letters, digits, and underscores (_).     |
   +------------+----------------------------------------------------------------------------------------+
   | db_Name    | Name of the database. If the parameter is not specified, the current database is used. |
   +------------+----------------------------------------------------------------------------------------+
   | table_name | Name of the table to be deleted.                                                       |
   +------------+----------------------------------------------------------------------------------------+

Usage Guidelines
----------------

In this command, **IF EXISTS** and **db_name** are optional.

Examples
--------

**DROP INDEX** *if exists productNameIndexTable* **ON** *productdb.productSalesTable*;

System Response
---------------

Secondary Index Table will be deleted. Index information will be cleared in CarbonData table and the success message will be recorded in system logs.
