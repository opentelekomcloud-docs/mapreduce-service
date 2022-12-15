:original_name: mrs_01_1431.html

.. _mrs_01_1431:

ADD COLUMNS
===========

Function
--------

This command is used to add a column to an existing table.

Syntax
------

**ALTER TABLE** *[db_name.]table_name* **ADD COLUMNS** *(col_name data_type,...)* **TBLPROPERTIES**\ *(''COLUMNPROPERTIES.columnName.shared_column'='sharedFolder.sharedColumnName,...', 'DEFAULT.VALUE.COLUMN_NAME'='default_value')*;

Parameter Description
---------------------

.. table:: **Table 1** ADD COLUMNS parameters

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                                       |
   +===================================+===================================================================================================================================================================================+
   | db_name                           | Database name. If this parameter is not specified, the current database is selected.                                                                                              |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | table_name                        | Table name.                                                                                                                                                                       |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | col_name data_type                | Name of a comma-separated column with a data type. It consists of letters, digits, and underscores (_).                                                                           |
   |                                   |                                                                                                                                                                                   |
   |                                   | .. note::                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                   |
   |                                   |    When creating a CarbonData table, do not name columns as tupleId, PositionId, and PositionReference because they will be used in UPDATE, DELETE, and secondary index commands. |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Precautions
-----------

-  Only **shared_column** and **default_value** are read. If any other property name is specified, no error will be thrown and the property will be ignored.
-  If no default value is specified, the default value of the new column is considered null.
-  If filter is applied to the column, new columns will not be added during sort. New columns may affect query performance.

Examples
--------

-  **ALTER TABLE** *carbon* **ADD COLUMNS** *(a1 INT, b1 STRING)*;
-  **ALTER TABLE** *carbon* **ADD COLUMNS** *(a1 INT, b1 STRING)* **TBLPROPERTIES**\ *('COLUMNPROPERTIES.b1.shared_column'='sharedFolder.b1')*;
-  ALTER TABLE *carbon* **ADD COLUMNS** *(a1 INT, b1 STRING)* **TBLPROPERTIES**\ *('DEFAULT.VALUE.a1'='10')*;

System Response
---------------

The newly added column can be displayed by running the **DESCRIBE** command.
