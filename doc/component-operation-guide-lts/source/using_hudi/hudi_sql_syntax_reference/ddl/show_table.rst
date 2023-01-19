:original_name: mrs_01_24267.html

.. _mrs_01_24267:

SHOW TABLE
==========

Function
--------

This command is used to display all tables in current database or all tables in a specific database.

Syntax
------

**SHOW TABLES** *[IN db\_name];*

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   +------------+----------------------------------------------------------------------+
   | Parameter  | Description                                                          |
   +============+======================================================================+
   | IN db_name | Name of the specific database whose tables need to be all displayed. |
   +------------+----------------------------------------------------------------------+

Precautions
-----------

**IN db_Name** is optional. It is required only when you need to display all tables of a specific database.

Examples
--------

.. code-block::

   SHOW TABLES IN hudidb;

System Response
---------------

All tables are listed.
