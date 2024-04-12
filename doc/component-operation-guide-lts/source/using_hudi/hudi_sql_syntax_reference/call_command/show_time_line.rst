:original_name: mrs_01_24782.html

.. _mrs_01_24782:

SHOW_TIME_LINE
==============

Function
--------

Displays the effective or archived Hudi timelines and details of a specified instant time.

Syntax
------

-  Viewing the list of effective timelines of a table:

   **call show_active_instant_list(table => '[table_name]');**

-  Viewing the list of effective timelines after a timestamp in a table:

   **call show_active_instant_list(table => '[table_name]', instant => '[instant]');**

-  Viewing information about an instant that takes effect in a table:

   **call show_active_instant_detail(table => '[table_name]', instant => '[instant]');**

-  Viewing the list of archived instant timelines in a table:

   **call show_archived_instant_list(table => '[table_name]');**

-  Viewing the list of archived instant timelines after a timestamp in a table:

   **call show_archived_instant_list(table => '[table_name]', instant => '[instant]');**

-  Viewing information about archived instants in a table:

   **call show_archived_instant_detail(table => '[table_name], instant => '[instant]');**

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   +------------+-----------------------------------------------------------------------------------------+
   | Parameter  | Description                                                                             |
   +============+=========================================================================================+
   | table_name | Name of the table to be queried. The value can be in the **database.tablename** format. |
   +------------+-----------------------------------------------------------------------------------------+
   | instant    | Instant timestamp to be queried                                                         |
   +------------+-----------------------------------------------------------------------------------------+

Example
-------

.. code-block::

   call show_active_instant_detail(table => 'hudi_table1', instant => '20220913144936897'");

System Response
---------------

You can view query results on the client.
