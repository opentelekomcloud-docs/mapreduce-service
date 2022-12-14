:original_name: mrs_01_1442.html

.. _mrs_01_1442:

DELETE SEGMENT by ID
====================

Function
--------

This command is used to delete segments by the ID.

Syntax
------

**DELETE FROM TABLE db_name.table_name WHERE SEGMENT.ID IN (segment_id1,segment_id2)**;

Parameter Description
---------------------

.. table:: **Table 1** DELETE SEGMENT parameters

   +------------+---------------------------------------------------------------------------------+
   | Parameter  | Description                                                                     |
   +============+=================================================================================+
   | segment_id | ID of the segment to be deleted.                                                |
   +------------+---------------------------------------------------------------------------------+
   | db_name    | Database name. If the parameter is not specified, the current database is used. |
   +------------+---------------------------------------------------------------------------------+
   | table_name | The name of the table in a specific database.                                   |
   +------------+---------------------------------------------------------------------------------+

Usage Guidelines
----------------

Segments cannot be deleted from the stream table.

Examples
--------

**DELETE FROM TABLE CarbonDatabase.CarbonTable WHERE SEGMENT.ID IN (0)**;

**DELETE FROM TABLE CarbonDatabase.CarbonTable WHERE SEGMENT.ID IN (0,5,8)**;

System Response
---------------

Success or failure will be recorded in the CarbonData log.
