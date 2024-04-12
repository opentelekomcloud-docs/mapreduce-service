:original_name: mrs_01_24501.html

.. _mrs_01_24501:

Changing a Table Name
=====================

Function
--------

The **ALTER TABLE ... RENAME** command is used to change the table name.

Syntax
------

**ALTER TABLE** *tableName* **RENAME TO** *newTableName*

Parameter Description
---------------------

.. table:: **Table 1** RENAME parameters

   ============ ===============
   Parameter    Description
   ============ ===============
   tableName    Table name.
   newTableName New table name.
   ============ ===============

Example
-------

.. code-block::

   ALTER TABLE table1 RENAME TO table2

Response
--------

You can run the **SHOW TABLES** command to view the new table name.
