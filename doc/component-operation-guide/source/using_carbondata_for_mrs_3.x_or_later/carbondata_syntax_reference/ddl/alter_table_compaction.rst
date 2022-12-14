:original_name: mrs_01_1429.html

.. _mrs_01_1429:

ALTER TABLE COMPACTION
======================

Function
--------

The **ALTER TABLE COMPACTION** command is used to merge a specified number of segments into a single segment. This improves the query performance of a table.

Syntax
------

**ALTER TABLE**\ *[db_name.]table_name COMPACT 'MINOR/MAJOR/SEGMENT_INDEX';*

**ALTER TABLE**\ *[db_name.]table_name COMPACT 'CUSTOM' WHERE SEGMENT.ID IN (id1, id2, ...);*

Parameter Description
---------------------

.. table:: **Table 1** ALTER TABLE COMPACTION parameters

   +---------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter     | Description                                                                                                                                                                                                                                                                                                       |
   +===============+===================================================================================================================================================================================================================================================================================================================+
   | db_name       | Database name. If this parameter is not specified, the current database is selected.                                                                                                                                                                                                                              |
   +---------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | table_name    | Table name.                                                                                                                                                                                                                                                                                                       |
   +---------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | MINOR         | Minor compaction. For details, see :ref:`Combining Segments <mrs_01_1415>`.                                                                                                                                                                                                                                       |
   +---------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | MAJOR         | Major compaction. For details, see :ref:`Combining Segments <mrs_01_1415>`.                                                                                                                                                                                                                                       |
   +---------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | SEGMENT_INDEX | This configuration enables you to merge all the CarbonData index files (**.carbonindex**) inside a segment to a single CarbonData index merge file (**.carbonindexmerge**). This enhances the first query performance. For more information, see :ref:`Table 1 <mrs_01_1415__t9ba7557f991f4d6caad3710c4a51b9f2>`. |
   +---------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | CUSTOM        | Custom compaction. For details, see :ref:`Combining Segments <mrs_01_1415__li68503712544>`.                                                                                                                                                                                                                       |
   +---------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Precautions
-----------

N/A

Examples
--------

**ALTER TABLE ProductDatabase COMPACT 'MINOR';**

**ALTER TABLE ProductDatabase COMPACT 'MAJOR';**

**ALTER TABLE ProductDatabase COMPACT 'SEGMENT_INDEX';**

**ALTER TABLE ProductDatabase COMPACT 'CUSTOM' WHERE SEGMENT.ID IN (0, 1);**

System Response
---------------

**ALTER TABLE COMPACTION** does not show the response of the compaction because it is run in the background.

If you want to view the response of minor and major compactions, you can check the logs or run the **SHOW SEGMENTS** command.

Example:

.. code-block::

   +------+------------+--------------------------+------------------+------------+------------+-------------+--------------+--+
   |  ID  |   Status   |     Load Start Time      | Load Time Taken  | Partition  | Data Size  | Index Size  | File Format  |
   +------+------------+--------------------------+------------------+------------+------------+-------------+--------------+--+
   | 3    | Success    | 2020-09-28 22:53:26.336  | 3.726S           | {}         | 6.47KB     | 3.30KB      | columnar_v3  |
   | 2    | Success    | 2020-09-28 22:53:01.702  | 6.688S           | {}         | 6.47KB     | 3.30KB      | columnar_v3  |
   | 1    | Compacted  | 2020-09-28 22:51:15.242  | 5.82S            | {}         | 6.50KB     | 3.43KB      | columnar_v3  |
   | 0.1  | Success    | 2020-10-30 20:49:24.561  | 16.66S           | {}         | 12.87KB    | 6.91KB      | columnar_v3  |
   | 0    | Compacted  | 2020-09-28 22:51:02.6    | 6.819S           | {}         | 6.50KB     | 3.43KB      | columnar_v3  |
   +------+------------+--------------------------+------------------+------------+------------+-------------+--------------+--+

In the preceding information:

-  **Compacted** indicates that data has been compacted.
-  **0.1** indicates the compacting result of segment 0 and segment 1.

The compact operation does not incur any change to other operations.

Compacted segments, such as segment 0 and segment 1, become useless. To save space, before you perform other operations, run the **CLEAN FILES** command to delete compacted segments. For more information about the **CLEAN FILES** command, see :ref:`CLEAN FILES <mrs_01_1448>`.
