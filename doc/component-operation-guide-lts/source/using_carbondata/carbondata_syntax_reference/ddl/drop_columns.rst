:original_name: mrs_01_1432.html

.. _mrs_01_1432:

DROP COLUMNS
============

Function
--------

This command is used to delete one or more columns from a table.

Syntax
------

**ALTER TABLE** *[db_name.]table_name* **DROP COLUMNS** *(col_name, ...)*;

Parameter Description
---------------------

.. table:: **Table 1** DROP COLUMNS parameters

   +------------+-------------------------------------------------------------------------------------------------------------------+
   | Parameter  | Description                                                                                                       |
   +============+===================================================================================================================+
   | db_name    | Database name. If this parameter is not specified, the current database is selected.                              |
   +------------+-------------------------------------------------------------------------------------------------------------------+
   | table_name | Table name.                                                                                                       |
   +------------+-------------------------------------------------------------------------------------------------------------------+
   | col_name   | Name of a column in a table. Multiple columns are supported. It consists of letters, digits, and underscores (_). |
   +------------+-------------------------------------------------------------------------------------------------------------------+

Precautions
-----------

After a column is deleted, at least one key column must exist in the schema. Otherwise, an error message is displayed, and the column fails to be deleted.

Examples
--------

Assume that the table contains four columns named a1, b1, c1, and d1.

-  Delete a column:

   **ALTER TABLE** *carbon* **DROP COLUMNS** *(b1)*;

   **ALTER TABLE** *test_db.carbon* **DROP COLUMNS** *(b1)*;

-  Delete multiple columns:

   **ALTER TABLE** *carbon* **DROP COLUMNS** *(b1,c1)*;

   **ALTER TABLE** *test_db.carbon* **DROP COLUMNS** *(b1,c1)*;

System Response
---------------

If you run the **DESCRIBE** command, the deleted columns will not be displayed.
