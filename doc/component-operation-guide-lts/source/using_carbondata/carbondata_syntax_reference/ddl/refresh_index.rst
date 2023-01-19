:original_name: mrs_01_1436.html

.. _mrs_01_1436:

REFRESH INDEX
=============

Function
--------

This command is used to merge all segments for data files in the secondary index table.

Syntax
------

-  **REFRESH INDEX** *indextable_name* ON TABLE *maintable_name*

   This command is used to merge all segments for which data files are to be merged.

-  **REFRESH INDEX** *indextable_name* ON TABLE *maintable_name* WHERE SEGMENT.ID IN (0,1,2..N)

   This command is used to merge a batch of specified segments.

Parameter Description
---------------------

.. table:: **Table 1** REFRESH INDEX parameters

   =============== =========================
   Parameter       Description
   =============== =========================
   indextable_name Name of an index table
   maintable_name  Name of the primary table
   =============== =========================

Precautions
-----------

To clear the data file of compacted segments, run the **CLEAN FILES** command on the secondary index table.

Examples
--------

**REFRESH INDEX** *productNameIndexTable*;

System Response
---------------

After this command is executed, the number of data files in the secondary index table will be reduced.
