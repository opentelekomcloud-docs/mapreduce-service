:original_name: mrs_01_1428.html

.. _mrs_01_1428:

SHOW TABLES
===========

Function
--------

**SHOW TABLES** command is used to list all tables in the current or a specific database.

Syntax
------

**SHOW TABLES** *[IN db\_name];*

Parameter Description
---------------------

.. table:: **Table 1** SHOW TABLE parameters

   +------------+---------------------------------------------------------------------------------------------------------------+
   | Parameter  | Description                                                                                                   |
   +============+===============================================================================================================+
   | IN db_name | Name of the database. This parameter is required only when tables of this specific database are to be listed. |
   +------------+---------------------------------------------------------------------------------------------------------------+

Usage Guidelines
----------------

IN db_Name is optional.

Examples
--------

**SHOW TABLES IN ProductDatabase;**

System Response
---------------

All tables are listed.
