:original_name: mrs_01_0587.html

.. _mrs_01_0587:

Querying an OpenTSDB Table
==========================

This **SELECT** command is used to query data in an OpenTSDB table.

Syntax
------

.. code-block::

   SELECT * FROM table_name WHERE tagk=tagv LIMIT number;

Keyword
-------

========= ================================
Parameter Description
========= ================================
LIMIT     Used to limit the query results.
number    Only the INT type is supported.
========= ================================

Precautions
-----------

-  The to-be-queried table must exist. Otherwise, an error is reported.
-  The value of **tagv** must exist. Otherwise, an error occurs.

Example
-------

Query data in the **opentsdb_table** table.

.. code-block::

   SELECT * FROM opentsdb_table LIMIT 100;
   SELECT * FROM opentsdb_table WHERE city='city1';
