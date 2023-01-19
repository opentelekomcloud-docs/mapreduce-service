:original_name: mrs_01_1430.html

.. _mrs_01_1430:

TABLE RENAME
============

Function
--------

This command is used to rename an existing table.

Syntax
------

**ALTER TABLE** *[db_name.]table_name* **RENAME TO** *new_table_name*;

Parameter Description
---------------------

.. table:: **Table 1** RENAME parameters

   +----------------+--------------------------------------------------------------------------------------+
   | Parameter      | Description                                                                          |
   +================+======================================================================================+
   | db_name        | Database name. If this parameter is not specified, the current database is selected. |
   +----------------+--------------------------------------------------------------------------------------+
   | table_name     | Current name of the existing table                                                   |
   +----------------+--------------------------------------------------------------------------------------+
   | new_table_name | New name of the existing table                                                       |
   +----------------+--------------------------------------------------------------------------------------+

Precautions
-----------

-  Parallel queries (using table names to obtain paths for reading CarbonData storage files) may fail during this operation.
-  The secondary index table cannot be renamed.

Example
-------

**ALTER TABLE** *carbon* **RENAME TO** *carbondata*;

**ALTER TABLE** *test_db.carbon* **RENAME TO** *test_db.carbondata*;

System Response
---------------

The new table name will be displayed in the CarbonData folder. You can run **SHOW TABLES** to view the new table name.
