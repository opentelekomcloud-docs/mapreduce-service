:original_name: mrs_01_24271.html

.. _mrs_01_24271:

TRUNCATE TABLE
==============

Function
--------

This command is used to clear all data in a specific table.

Syntax
------

**TRUNCATE TABLE** *tableIdentifier*

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   =============== ===========
   Parameter       Description
   =============== ===========
   tableIdentifier Table name.
   =============== ===========

Examples
--------

.. code-block::

   truncate table h0_1;

System Response
---------------

Data in the table is cleared. You can run the **QUERY** statement to check whether data in the table has been deleted.
