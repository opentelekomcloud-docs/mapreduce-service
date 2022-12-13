:original_name: mrs_01_24205.html

.. _mrs_01_24205:

DESC: Querying a Table Structure
================================

This section describes the basic syntax and usage of the SQL statement for querying a table structure in ClickHouse.

Basic Syntax
------------

**DESC**\ \|\ **DESCRIBE** **TABLE** [*database_name*.]\ *table* [**INTO** OUTFILE filename] [FORMAT format]

Example
-------

.. code-block::

   -- Query the t1 table structure.
   desc t1;
   ┌─name────┬─type─┬─default_type─┬─default_expression ┬─comment─┬─codec_expression─┬─ttl_expression─┐
   │  id          │ UInt8  │                │                     │           │                    │                  │
   │  name        │ UInt8  │                │                     │           │                    │                  │
   │  address     │ String │                │                     │           │                    │                  │
   └───────┴────┴────────┴────────── ┴───── ┴──────────┴─────────┘
