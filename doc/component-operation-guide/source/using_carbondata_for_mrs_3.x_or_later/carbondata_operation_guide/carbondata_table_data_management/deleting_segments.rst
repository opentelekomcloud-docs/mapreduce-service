:original_name: mrs_01_1414.html

.. _mrs_01_1414:

Deleting Segments
=================

Scenario
--------

If you want to modify and reload the data because you have loaded wrong data into a table, or there are too many bad records, you can delete specific segments by segment ID or data loading time.

.. note::

   The segment deletion operation only deletes segments that are not compacted. You can run the **CLEAN FILES** command to clear compacted segments.

Deleting a Segment by Segment ID
--------------------------------

Each segment has a unique ID. This segment ID can be used to delete the segment.

#. Obtain the segment ID.

   Command:

   **SHOW SEGMENTS FOR Table** *dbname.tablename LIMIT number_of_loads;*

   Example:

   **SHOW SEGMENTS FOR TABLE** *carbonTable;*

   Run the preceding command to show all the segments of the table named **carbonTable**.

   **SHOW SEGMENTS FOR TABLE** *carbonTable LIMIT 2;*

   Run the preceding command to show segments specified by *number_of_loads*.

   The command output is as follows:

   .. code-block::

      +-----+----------+--------------------------+------------------+------------+------------+-------------+--------------+--+
      | ID  |  Status  |     Load Start Time      | Load Time Taken  | Partition  | Data Size  | Index Size  | File Format  |
      +-----+----------+--------------------------+------------------+------------+------------+-------------+--------------+--+
      | 3   | Success  | 2020-09-28 22:53:26.336  | 3.726S           | {}         | 6.47KB     | 3.30KB      | columnar_v3  |
      | 2   | Success  | 2020-09-28 22:53:01.702  | 6.688S           | {}         | 6.47KB     | 3.30KB      | columnar_v3  |
      +-----+----------+--------------------------+------------------+------------+------------+-------------+--------------+--+

   .. note::

      The output of the **SHOW SEGMENTS** command includes ID, Status, Load Start Time, Load Time Taken, Partition, Data Size, Index Size, and File Format. The latest loading information is displayed in the first line of the command output.

#. Run the following command to delete the segment after you have found the Segment ID:

   Command:

   **DELETE FROM TABLE tableName WHERE SEGMENT.ID IN (load_sequence_id1, load_sequence_id2, ....)**;

   Example:

   **DELETE FROM TABLE carbonTable WHERE SEGMENT.ID IN (1,2,3)**;

   For details, see :ref:`DELETE SEGMENT by ID <mrs_01_1442>`.

Deleting a Segment by Data Loading Time
---------------------------------------

You can delete a segment based on the loading time.

Command:

**DELETE FROM TABLE db_name.table_name WHERE SEGMENT.STARTTIME BEFORE date_value**;

Example:

**DELETE FROM TABLE carbonTable WHERE SEGMENT.STARTTIME BEFORE '2017-07-01 12:07:20'**;

The preceding command can be used to delete all segments before 2017-07-01 12:07:20.

For details, see :ref:`DELETE SEGMENT by DATE <mrs_01_1443>`.

Result
------

Data of corresponding segments is deleted and is unavailable for query. You can run the **SHOW SEGMENTS** command to display the segment status and check whether the segment has been deleted.

.. note::

   -  Segments are not physically deleted after the execution of the **DELETE SEGMENT** command. Therefore, if you run the **SHOW SEGMENTS** command to check the status of a deleted segment, it will be marked as **Marked for Delete**. If you run the **SELECT \* FROM tablename** command, the deleted segment will be excluded.

   -  The deleted segment will be deleted physically only when the next data loading reaches the maximum query execution duration, which is configured by the **max.query.execution.time** parameter. The default value of the parameter is 60 minutes.

   -  If you want to forcibly delete a physical segment file, run the **CLEAN FILES** command.

      Example:

      **CLEAN FILES FOR TABLE table1;**

      This command will physically delete the segment file in the **Marked for delete** state.

      If this command is executed before the time specified by **max.query.execution.time** arrives, the query may fail. **max.query.execution.time** indicates the maximum time allowed for a query, which is set in the **carbon.properties** file.
