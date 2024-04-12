:original_name: mrs_01_24503.html

.. _mrs_01_24503:

Changing the Column Name
========================

Function
--------

The **ALTER TABLE ... RENAME COLUMN** command is used to change the column name.

Syntax
------

**ALTER TABLE** *tableName* **RENAME COLUMN** *old_columnName* **TO** *new_columnName*

Parameter Description
---------------------

.. table:: **Table 1** RENAME COLUMN parameters

   ============== ================
   Parameter      Description
   ============== ================
   tableName      Table name.
   old_columnName Old column name.
   new_columnName New column name.
   ============== ================

Example
-------

.. code-block::

   ALTER TABLE table1 RENAME COLUMN a.b.c TO x

**a.b.c** indicates the full path of a nested column. For details about the nested column rules, see :ref:`Adding a Column <mrs_01_24498>`.

.. note::

   After the column name is changed, the change is automatically synchronized to the column comment. The comment is in **rename oldName to newName** format.

Response
--------

You can run the **DESCRIBE** command to view the new column name.
