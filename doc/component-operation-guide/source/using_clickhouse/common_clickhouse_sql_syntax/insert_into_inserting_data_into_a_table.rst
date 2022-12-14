:original_name: mrs_01_24202.html

.. _mrs_01_24202:

INSERT INTO: Inserting Data into a Table
========================================

This section describes the basic syntax and usage of the SQL statement for inserting data to a table in ClickHouse.

Basic Syntax
------------

-  Method 1: Inserting data in standard format

   **INSERT INTO** *[database_name.]table* [(*c1, c2, c3*)] **VALUES** (*v11, v12, v13*), (*v21, v22, v23*), ...

-  Method 2: Using the **SELECT** result to insert data

   **INSERT INTO** *[database_name.]table* [(c1, c2, c3)] **SELECT** ...

Example
-------

.. code-block::

   -- Insert data into the test2 table.
   insert into test2 (id, name) values (1, 'abc'), (2, 'bbbb');
   -- Query data in the test2 table.
   select * from test2;
   ┌─id─┬─name─┐
   │  1   │ abc    │
   │  2   │ bbbb   │
   └───┴────┘
