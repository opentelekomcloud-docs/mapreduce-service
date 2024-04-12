:original_name: mrs_01_24803.html

.. _mrs_01_24803:

ROLL_BACK
=========

Function
--------

Rolls back a specified commit.

Syntax
------

**call rollback_to_instant(table => '[table_name]', instant_time => '[instant]');**

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   +------------+--------------------------------------------------------------------------+
   | Parameter  | Description                                                              |
   +============+==========================================================================+
   | table_name | Mandatory. Name of the Hudi table to be rolled back.                     |
   +------------+--------------------------------------------------------------------------+
   | instant    | Mandatory. Commit instant timestamp of the Hudi table to be rolled back. |
   +------------+--------------------------------------------------------------------------+

Example
-------

.. code-block::

   call rollback_to_instant(table => 'h1', instant_time=>'20220915113127525');

Precautions
-----------

Only the latest commit timestamps can be rolled back in sequence.

System Response
---------------

You can view command execution results in the driver log or on the client.
