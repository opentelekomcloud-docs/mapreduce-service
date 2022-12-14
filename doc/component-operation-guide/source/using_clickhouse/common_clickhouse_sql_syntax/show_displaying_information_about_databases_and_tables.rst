:original_name: mrs_01_24207.html

.. _mrs_01_24207:

SHOW: Displaying Information About Databases and Tables
=======================================================

This section describes the basic syntax and usage of the SQL statement for displaying information about databases and tables in ClickHouse.

Basic Syntax
------------

**show databases**

**show tables**

Example
-------

.. code-block::

   -- Query database information.
   show databases;
   ┌─name────┐
   │ default      │
   │ system       │
   │ test         │
   └───────┘
   -- Query table information.
   show tables;
   ┌─name──┐
   │ t1       │
   │ test     │
   │ test2    │
   │ test5    │
   └─────┘
