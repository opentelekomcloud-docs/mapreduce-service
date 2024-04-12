:original_name: mrs_01_24276.html

.. _mrs_01_24276:

DELETE Hudi Data
================

Function
--------

This command is used to delete records from a Hudi table.

Syntax
------

**DELETE from** *tableIdentifier [ WHERE boolExpression]*

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   =============== ==========================================
   Parameter       Description
   =============== ==========================================
   tableIdentifier Name of the Hudi table to delete records.
   boolExpression  Filtering conditions for deleting records.
   =============== ==========================================

Examples
--------

-  Example 1:

   .. code-block::

      delete from h0 where column1 = 'country';

-  Example 2:

   .. code-block::

      delete from h0 where column1 IN ('country1', 'country2');

-  Example 3:

   .. code-block::

      delete from h0 where column1 IN (select column11 from sourceTable2);

-  Example 4:

   .. code-block::

      delete from h0 where column1 IN (select column11 from sourceTable2 where column1 = 'USA');

-  Example 5:

   .. code-block::

      delete from h0;

System Response
---------------

You can view the result in driver logs or on the client.
