:original_name: mrs_01_24204.html

.. _mrs_01_24204:

ALTER TABLE: Modifying a Table Structure
========================================

This section describes the basic syntax and usage of the SQL statement for modifying a table structure in ClickHouse.

Basic Syntax
------------

**ALTER TABLE** [*database_name*].\ *name* [**ON CLUSTER** *cluster*] **ADD**\ \|\ **DROP**\ \|\ **CLEAR**\ \|\ **COMMENT**\ \|\ **MODIFY** **COLUMN** ...

.. note::

   **ALTER** supports only ``*``\ MergeTree, Merge, and Distributed engine tables.

Example
-------

.. code-block::

   -- Add the test01 column to the t1 table.
   ALTER TABLE t1 ADD COLUMN test01 String DEFAULT 'defaultvalue';
   -- Query the modified table t1.
   desc t1
   ┌─name────┬─type─┬─default_type─┬─default_expression ┬─comment─┬─codec_expression─┬─ttl_expression─┐
   │  id          │ UInt8  │                │                     │           │                    │                  │
   │  name        │ String │                │                     │           │                    │                  │
   │  address     │ String │                │                     │           │                    │                  │
   │  test01      │ String │  DEFAULT       │  'defaultvalue'     │           │                    │                  │
   └───────┴────┴────────┴────────── ┴───── ┴──────────┴─────────┘
   -- Change the type of the name column in the t1 table to UInt8.
   ALTER TABLE t1 MODIFY COLUMN name UInt8;
   -- Query the modified table t1.
   desc t1
   ┌─name────┬─type─┬─default_type─┬─default_expression ┬─comment─┬─codec_expression─┬─ttl_expression─┐
   │  id          │ UInt8  │                │                     │           │                    │                  │
   │  name        │ UInt8  │                │                     │           │                    │                  │
   │  address     │ String │                │                     │           │                    │                  │
   │  test01      │ String │  DEFAULT       │  'defaultvalue'     │           │                    │                  │
   └───────┴────┴────────┴────────── ┴───── ┴──────────┴─────────┘
   -- Delete the test01 column from the t1 table.
   ALTER TABLE t1 DROP COLUMN test01;
   -- Query the modified table t1.
   desc t1
   ┌─name────┬─type─┬─default_type─┬─default_expression ┬─comment─┬─codec_expression─┬─ttl_expression─┐
   │  id          │ UInt8  │                │                     │           │                    │                  │
   │  name        │ UInt8  │                │                     │           │                    │                  │
   │  address     │ String │                │                     │           │                    │                  │
   └───────┴────┴────────┴────────── ┴───── ┴──────────┴─────────┘
