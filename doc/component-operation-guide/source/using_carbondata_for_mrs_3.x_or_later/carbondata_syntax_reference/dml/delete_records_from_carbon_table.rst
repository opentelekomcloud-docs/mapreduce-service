:original_name: mrs_01_1440.html

.. _mrs_01_1440:

DELETE RECORDS from CARBON TABLE
================================

Function
--------

This command is used to delete records from a CarbonData table.

Syntax
------

**DELETE FROM CARBON_TABLE [WHERE expression];**

Parameter Description
---------------------

.. table:: **Table 1** DELETE RECORDS parameters

   +--------------+-------------------------------------------------------------------------+
   | Parameter    | Description                                                             |
   +==============+=========================================================================+
   | CARBON TABLE | Name of the CarbonData table in which the DELETE operation is performed |
   +--------------+-------------------------------------------------------------------------+

Precautions
-----------

-  If a segment is deleted, all secondary indexes associated with the segment are deleted as well.

-  If the **carbon.input.segments** property has been set for the queried table, the DELETE operation fails. To solve this problem, run the following statement before the query:

   Syntax:

   **SET carbon.input.segments. <database_name>.<table_name>=*;**

Examples
--------

-  Example 1:

   **delete from columncarbonTable1 d where d.column1 = 'country';**

-  Example 2:

   **delete from dest where column1 IN ('country1', 'country2');**

-  Example 3:

   **delete from columncarbonTable1 where column1 IN (select column11 from sourceTable2);**

-  Example 4:

   **delete from columncarbonTable1 where column1 IN (select column11 from sourceTable2 where column1 = 'USA');**

-  Example 5:

   **delete from columncarbonTable1 where column2 >= 4;**

System Response
---------------

Success or failure will be recorded in the driver log and on the client.
