:original_name: mrs_01_24499.html

.. _mrs_01_24499:

Altering a Column
=================

Function
--------

The **ALTER TABLE ... ALTER COLUMN** command is used to change the attributes of a column, such as the column type, position, and comment.

Syntax
------

**ALTER TABLE** *Table name* **ALTER**

**[COLUMN]** *col_old_name* **TYPE** *column_type*

**[COMMENT]** *col_comment*

**[FIRST|AFTER]** *column_name*

Parameter Description
---------------------

.. table:: **Table 1** ALTER COLUMN parameters

   +--------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter    | Description                                                                                                                                   |
   +==============+===============================================================================================================================================+
   | tableName    | Table name.                                                                                                                                   |
   +--------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | col_old_name | Name of the column to be altered.                                                                                                             |
   +--------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | column_type  | Type of the target column.                                                                                                                    |
   +--------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | col_comment  | Column comment.                                                                                                                               |
   +--------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | column_name  | New position to place the target column. For example, **AFTER column_name** indicates that the target column is placed after **column_name**. |
   +--------------+-----------------------------------------------------------------------------------------------------------------------------------------------+

Example
-------

-  Changing the column type

   .. code-block::

      ALTER TABLE table1 ALTER COLUMN a.b.c TYPE bigint

   **a.b.c** indicates the full path of a nested column. For details about the nested column rules, see :ref:`Adding a Column <mrs_01_24498>`.

   The following changes on column types are supported:

   -  int => long/float/double/string/decimal
   -  long => float/double/string/decimal
   -  float => double/String/decimal
   -  From double to string or decimal
   -  From decimal to decimal or string
   -  From string to date or decimal
   -  From date to string

-  Altering other attributes

   .. code-block::

      ALTER TABLE table1 ALTER COLUMN a.b.c DROP NOT NULL
      ALTER TABLE table1 ALTER COLUMN a.b.c COMMENT 'new comment'
      ALTER TABLE table1 ALTER COLUMN a.b.c FIRST
      ALTER TABLE table1 ALTER COLUMN a.b.c AFTER x

   **a.b.c** indicates the full path of a nested column. For details about the nested column rules, see :ref:`Adding a Column <mrs_01_24498>`.

Response
--------

You can run the **DESCRIBE** command to view the modified column.
