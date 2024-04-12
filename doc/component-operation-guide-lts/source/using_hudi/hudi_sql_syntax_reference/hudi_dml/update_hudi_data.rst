:original_name: mrs_01_24275.html

.. _mrs_01_24275:

UPDATE Hudi Data
================

Function
--------

This command is used to update the Hudi table based on the column expression and optional filtering conditions.

Syntax
------

**UPDATE** *tableIdentifier SET column = EXPRESSION(,column = EXPRESSION) [ WHERE boolExpression]*

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   +-----------------+--------------------------------------------------------------------------+
   | Parameter       | Description                                                              |
   +=================+==========================================================================+
   | tableIdentifier | Name of the Hudi table to be updated.                                    |
   +-----------------+--------------------------------------------------------------------------+
   | column          | Target column to be updated.                                             |
   +-----------------+--------------------------------------------------------------------------+
   | EXPRESSION      | Expression of the source table column to be updated in the target table. |
   +-----------------+--------------------------------------------------------------------------+
   | boolExpression  | Filtering condition expression.                                          |
   +-----------------+--------------------------------------------------------------------------+

Examples
--------

.. code-block::

   update h0 set price = price + 20 where id = 1;
   update h0 set price = price *2, name = 'a2' where id = 2;

System Response
---------------

You can view the result in driver logs or on the client.
