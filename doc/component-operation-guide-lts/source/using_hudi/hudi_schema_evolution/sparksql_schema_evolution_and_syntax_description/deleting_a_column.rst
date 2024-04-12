:original_name: mrs_01_24500.html

.. _mrs_01_24500:

Deleting a Column
=================

Function
--------

The **ALTER TABLE ... DROP COLUMN** command is used to delete a column.

Syntax
------

**ALTER TABLE** *tableName* **DROP COLUMN|COLUMNS** *cols*

Parameter Description
---------------------

.. table:: **Table 1** DROP COLUMN parameters

   ========= ========================================================
   Parameter Description
   ========= ========================================================
   tableName Table name.
   cols      Columns to be deleted. You can specify multiple columns.
   ========= ========================================================

Example
-------

.. code-block::

   ALTER TABLE table1 DROP COLUMN a.b.c
   ALTER TABLE table1 DROP COLUMNS a.b.c, x, y

**a.b.c** indicates the full path of a nested column. For details about the nested column rules, see :ref:`Adding a Column <mrs_01_24498>`.

Response
--------

You can run the **DESCRIBE** command to check which column is deleted.
