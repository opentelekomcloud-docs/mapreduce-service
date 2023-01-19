:original_name: mrs_01_1446.html

.. _mrs_01_1446:

SHOW SECONDARY INDEXES
======================

Function
--------

This command is used to list all secondary index tables in the CarbonData table.

Syntax
------

**SHOW INDEXES ON db_name.table_name**;

Parameter Description
---------------------

.. table:: **Table 1** SHOW SECONDARY INDEXES parameters

   +------------+-----------------------------------------------------------------------------------------+
   | Parameter  | Description                                                                             |
   +============+=========================================================================================+
   | db_name    | Database name. It consists of letters, digits, and special characters (_).              |
   +------------+-----------------------------------------------------------------------------------------+
   | table_name | Name of the database table. It consists of letters, digits, and special characters (_). |
   +------------+-----------------------------------------------------------------------------------------+

Precautions
-----------

**db_name** is optional.

Examples
--------

**SHOW INDEXES ON productsales.product**;

System Response
---------------

All index tables and corresponding index columns in a given CarbonData table will be listed.
