:original_name: mrs_01_24268.html

.. _mrs_01_24268:

ALTER RENAME TABLE
==================

Function
--------

This command is used to rename an existing table.

Syntax
------

**ALTER** **TABLE** *oldTableName* **RENAME** **TO** *newTableName*

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   ============== =========================
   Parameter      Description
   ============== =========================
   oldTableName   Current name of the table
   new_table_name New name of the table
   ============== =========================

Examples
--------

.. code-block::

   alter table h0 rename to h0_1;

System Response
---------------

The table name is changed. You can run the **SHOW TABLES** command to display the new table name.
