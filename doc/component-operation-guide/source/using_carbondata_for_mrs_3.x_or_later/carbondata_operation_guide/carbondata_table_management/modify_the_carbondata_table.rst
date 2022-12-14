:original_name: mrs_01_1411.html

.. _mrs_01_1411:

Modify the CarbonData Table
===========================

**SET** and **UNSET**
---------------------

When the **SET** command is executed, the new properties overwrite the existing ones.

-  SORT SCOPE

   The following is an example of the **SET SORT SCOPE** command:

   **ALTER TABLE** *tablename* **SET TBLPROPERTIES('SORT_SCOPE'**\ =\ *'no_sort'*)

   After running the **UNSET SORT SCOPE** command, the default value **NO_SORT** is adopted.

   The following is an example of the **UNSET SORT SCOPE** command:

   **ALTER TABLE** *tablename* **UNSET TBLPROPERTIES('SORT_SCOPE'**)

-  SORT COLUMNS

   The following is an example of the **SET SORT COLUMNS** command:

   **ALTER TABLE** *tablename* **SET TBLPROPERTIES('SORT_COLUMNS'**\ =\ *'column1'*)

   After this command is executed, the new value of **SORT_COLUMNS** is used. Users can adjust the **SORT_COLUMNS** based on the query results, but the original data is not affected. The operation does not affect the query performance of the original data segments which are not sorted by new **SORT_COLUMNS**.

   The **UNSET** command is not supported, but the **SORT_COLUMNS** can be set to empty string instead of using the **UNSET** command.

   **ALTER TABLE** *tablename* **SET TBLPROPERTIES('SORT_COLUMNS'**\ =\ *''*)

   .. note::

      -  The later version will enhance custom compaction to resort the old segments.
      -  The value of **SORT_COLUMNS** cannot be modified in the streaming table.
      -  If the **inverted index** column is removed from **SORT_COLUMNS**, **inverted index** will not be created in this column. However, the old configuration of **INVERTED_INDEX** will be kept.
