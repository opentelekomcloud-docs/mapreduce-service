:original_name: mrs_01_1443.html

.. _mrs_01_1443:

DELETE SEGMENT by DATE
======================

Function
--------

This command is used to delete segments by loading date. Segments created before a specific date will be deleted.

Syntax
------

**DELETE FROM TABLE db_name.table_name WHERE SEGMENT.STARTTIME BEFORE date_value**;

Parameter Description
---------------------

.. table:: **Table 1** DELETE SEGMENT by DATE parameters

   +------------+----------------------------------------------------------------------------------------------+
   | Parameter  | Description                                                                                  |
   +============+==============================================================================================+
   | db_name    | Database name. If this parameter is not specified, the current database is used.             |
   +------------+----------------------------------------------------------------------------------------------+
   | table_name | Name of a table in the specified database                                                    |
   +------------+----------------------------------------------------------------------------------------------+
   | date_value | Valid date when segments are started to be loaded. Segments before the date will be deleted. |
   +------------+----------------------------------------------------------------------------------------------+

Precautions
-----------

Segments cannot be deleted from the stream table.

Example
-------

**DELETE FROM TABLE db_name.table_name WHERE SEGMENT.STARTTIME BEFORE '2017-07-01 12:07:20'**;

**STARTTIME** indicates the loading start time of different loads.

System Response
---------------

Success or failure will be recorded in CarbonData logs.
