:original_name: mrs_01_24269.html

.. _mrs_01_24269:

ALTER ADD COLUMNS
=================

Function
--------

This command is used to add columns to an existing table.

Syntax
------

**ALTER TABLE** *tableIdentifier* **ADD COLUMNS**\ ``(colAndType (,colAndType)*)``

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   +-----------------+-------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Description                                                                                                       |
   +=================+===================================================================================================================+
   | tableIdentifier | Table name.                                                                                                       |
   +-----------------+-------------------------------------------------------------------------------------------------------------------+
   | colAndType      | Name of a comma-separated column with data types. A column name consists of letters, digits, and underscores (_). |
   +-----------------+-------------------------------------------------------------------------------------------------------------------+

Examples
--------

.. code-block::

   alter table h0_1 add columns(ext0 string);

System Response
---------------

The columns are added to the table. You can run the **DESCRIBE** command to display the columns.
