:original_name: mrs_01_1434.html

.. _mrs_01_1434:

REFRESH TABLE
=============

Function
--------

This command is used to register Carbon table to Hive meta store catalogue from exisiting Carbon table data.

Syntax
------

**REFRESH TABLE** *db_name.table_name*;

Parameter Description
---------------------

.. table:: **Table 1** REFRESH TABLE parameters

   +------------+------------------------------------------------------------------------------------------------+
   | Parameter  | Description                                                                                    |
   +============+================================================================================================+
   | db_name    | Name of the database. If this parameter is left unspecified, the current database is selected. |
   +------------+------------------------------------------------------------------------------------------------+
   | table_name | Name of the table.                                                                             |
   +------------+------------------------------------------------------------------------------------------------+

Usage Guidelines
----------------

-  The new database name and the old database name should be same.
-  Before executing this command the old table schema and data should be copied into the new database location.
-  If the table is aggregate table, then all the aggregate tables should be copied to the new database location.
-  For old store, the time zone of the source and destination cluster should be same.
-  If old cluster used HIVE meta store to store schema, refresh will not work as schema file does not exist in file system.

Examples
--------

**REFRESH TABLE** *dbcarbon*.\ *productSalesTable*;

System Response
---------------

By running this command, the Carbon table will be registered to Hive meta store catalogue from exisiting Carbon table data.
