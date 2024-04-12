:original_name: mrs_01_24502.html

.. _mrs_01_24502:

Modifying Table Properties
==========================

Function
--------

The **ALTER TABLE ... SET|UNSET** command is used to modify table properties.

Syntax
------

**ALTER TABLE** *Table name* **SET|UNSET** *tblproperties*

Parameter Description
---------------------

.. table:: **Table 1** SET|UNSET parameters

   ============= =================
   Parameter     Description
   ============= =================
   tableName     Table name.
   tblproperties Table properties.
   ============= =================

Example
-------

.. code-block::

   ALTER TABLE table SET TBLPROPERTIES ('table_property' = 'property_value')
   ALTER TABLE table UNSET TBLPROPERTIES [IF EXISTS] ('comment', 'key')

Response
--------

You can run the **DESCRIBE** command to view new table properties.
