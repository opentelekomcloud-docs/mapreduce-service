:original_name: mrs_01_24799.html

.. _mrs_01_24799:

SHOW_HOODIE_PROPERTIES
======================

Function
--------

Displays the configuration in the **hoodie.properties** file of a specified Hudi table.

Syntax
------

**call show_hoodie_properties(table => '[table_name]');**

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   +------------+-----------------------------------------------------------------------------------------+
   | Parameter  | Description                                                                             |
   +============+=========================================================================================+
   | table_name | Name of the table to be queried. The value can be in the **database.tablename** format. |
   +------------+-----------------------------------------------------------------------------------------+

Example
-------

.. code-block::

   call show_hoodie_properties(table => "hudi_table5");

System Response
---------------

You can view query results on the client.
