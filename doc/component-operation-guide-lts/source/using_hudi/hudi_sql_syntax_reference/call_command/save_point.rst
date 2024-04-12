:original_name: mrs_01_24800.html

.. _mrs_01_24800:

SAVE_POINT
==========

Function
--------

Manages savepoints of Hudi tables.

Syntax
------

-  Creating a savepoint:

   **call create_savepoints('[table_name]', '[commit_Time]', '[user]', '[comments]');**

-  Viewing all existing savepoints

   **call show_savepoints(table =>'[table_name]');**

-  Rolling back a savepoint:

   **call rollback_savepoints('[table_name]', '[commit_Time]');**

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   +-------------+-----------------------------------------------------------------------------------------+-----------+
   | Parameter   | Description                                                                             | Mandatory |
   +=============+=========================================================================================+===========+
   | table_name  | Name of the table to be queried. The value can be in the **database.tablename** format. | Yes       |
   +-------------+-----------------------------------------------------------------------------------------+-----------+
   | commit_Time | Specified creation or rollback timestamp                                                | Yes       |
   +-------------+-----------------------------------------------------------------------------------------+-----------+
   | user        | User who creates a savepoint                                                            | No        |
   +-------------+-----------------------------------------------------------------------------------------+-----------+
   | comments    | Description of the savepoint                                                            | No        |
   +-------------+-----------------------------------------------------------------------------------------+-----------+

Example
-------

.. code-block::

   call create_savepoints('hudi_test1', '20220908155421949');
   call show_savepoints(table =>'hudi_test1');
   call rollback_savepoints('hudi_test1', '20220908155421949');

Precautions
-----------

-  MOR tables do not support savepoints.
-  The commit-related files before the latest savepoint are not cleaned.
-  If there are multiple savepoints, perform the rollback from the latest savepoint. The logic is as follows: roll back the latest savepoint; delete the savepoint; and roll back the next savepoint.

System Response
---------------

You can view query results on the client.
