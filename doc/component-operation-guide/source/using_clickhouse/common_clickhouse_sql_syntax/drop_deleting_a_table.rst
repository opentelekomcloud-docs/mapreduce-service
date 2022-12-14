:original_name: mrs_01_24208.html

.. _mrs_01_24208:

DROP: Deleting a Table
======================

This section describes the basic syntax and usage of the SQL statement for deleting a ClickHouse table.

Basic Syntax
------------

**DROP** [**TEMPORARY**] **TABLE** [**IF EXISTS**] [*database_name*.]\ *name* [**ON CLUSTER** *cluster*]

Example
-------

.. code-block::

   -- Delete the t1 table.
   drop table t1;
