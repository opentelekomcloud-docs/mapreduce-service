:original_name: mrs_01_24266.html

.. _mrs_01_24266:

DROP Hudi TABLE
===============

Function
--------

This command is used to delete an existing table.

Syntax
------

**DROP TABLE** *[IF EXISTS] [db_name.]table_name;*

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   +------------+--------------------------------------------------------------------------------------+
   | Parameter  | Description                                                                          |
   +============+======================================================================================+
   | db_name    | Database name. If this parameter is not specified, the current database is selected. |
   +------------+--------------------------------------------------------------------------------------+
   | table_name | Name of the table to be deleted.                                                     |
   +------------+--------------------------------------------------------------------------------------+

Precautions
-----------

In this command, **IF EXISTS** and **db_name** are optional.

Examples
--------

**DROP TABLE IF EXISTS hudidb.h1;**

System Response
---------------

The table will be deleted.
