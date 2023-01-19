:original_name: mrs_01_1433.html

.. _mrs_01_1433:

CHANGE DATA TYPE
================

Function
--------

This command is used to change the data type from INT to BIGINT or decimal precision from lower to higher.

Syntax
------

**ALTER TABLE** *[db_name.]table_name* **CHANGE** *col_name col_name changed_column_type*;

Parameter Description
---------------------

.. table:: **Table 1** CHANGE DATA TYPE parameters

   +---------------------+------------------------------------------------------------------------------------------------+
   | Parameter           | Description                                                                                    |
   +=====================+================================================================================================+
   | db_name             | Name of the database. If this parameter is left unspecified, the current database is selected. |
   +---------------------+------------------------------------------------------------------------------------------------+
   | table_name          | Name of the table.                                                                             |
   +---------------------+------------------------------------------------------------------------------------------------+
   | col_name            | Name of columns in a table. Column names contain letters, digits, and underscores (_).         |
   +---------------------+------------------------------------------------------------------------------------------------+
   | changed_column_type | The change in the data type.                                                                   |
   +---------------------+------------------------------------------------------------------------------------------------+

Usage Guidelines
----------------

-  Change of decimal data type from lower precision to higher precision will only be supported for cases where there is no data loss.

   Example:

   -  **Invalid scenario** - Change of decimal precision from (10,2) to (10,5) is not valid as in this case only scale is increased but total number of digits remain the same.
   -  **Valid scenario** - Change of decimal precision from (10,2) to (12,3) is valid as the total number of digits are increased by 2 but scale is increased only by 1 which will not lead to any data loss.

-  The allowed range is 38,38 (precision, scale) and is a valid upper case scenario which is not resulting in data loss.

Examples
--------

-  Changing data type of column a1 from INT to BIGINT.

   **ALTER TABLE** *test_db.carbon* **CHANGE** *a1 a1 BIGINT*;

-  Changing decimal precision of column a1 from 10 to 18.

   **ALTER TABLE** *test_db.carbon* **CHANGE** *a1 a1 DECIMAL(18,2)*;

System Response
---------------

By running DESCRIBE command, the changed data type for the modified column is displayed.
