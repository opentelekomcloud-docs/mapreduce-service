:original_name: mrs_01_1435.html

.. _mrs_01_1435:

REGISTER INDEX TABLE
====================

Function
--------

This command is used to register an index table with the primary table.

Syntax
------

**REGISTER INDEX TABLE** *indextable_name* ON *db_name.maintable_name*;

Parameter Description
---------------------

.. table:: **Table 1** REFRESH INDEX TABLE parameters

   +-----------------+--------------------------------------------------------------------------------------+
   | Parameter       | Description                                                                          |
   +=================+======================================================================================+
   | db_name         | Database name. If this parameter is not specified, the current database is selected. |
   +-----------------+--------------------------------------------------------------------------------------+
   | indextable_name | Index table name.                                                                    |
   +-----------------+--------------------------------------------------------------------------------------+
   | maintable_name  | Primary table name.                                                                  |
   +-----------------+--------------------------------------------------------------------------------------+

Precautions
-----------

Before running this command, run **REFRESH TABLE** to register the primary table and secondary index table with the Hive metastore.

Examples
--------

**REGISTER INDEX TABLE** *productNameIndexTable* ON *productdb*.\ *productSalesTable*;

System Response
---------------

By running this command, the index table will be registered to the primary table.
