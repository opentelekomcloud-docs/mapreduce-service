:original_name: mrs_01_1461.html

.. _mrs_01_1461:

Why Does INSERT INTO CARBON TABLE Command Fail?
===============================================

Question
--------

Why does the **INSERT INTO CARBON TABLE** command fail and the following error message is displayed?

.. code-block::

   Data load failed due to bad record

Answer
------

The **INSERT INTO CARBON TABLE** command fails in the following scenarios:

-  If the data type of source and target table columns are not the same, the data from the source table will be treated as bad records and the **INSERT INTO** command fails.

-  If the result of aggregation function on a source column exceeds the maximum range of the target column, then the **INSERT INTO** command fails.

   Solution:

   You can use the cast function on corresponding columns when inserting records.

   For example:

   #. Run the **DESCRIBE** command to query the target and source table.

      **DESCRIBE** *newcarbontable*;

      Result:

      .. code-block::

         col1 int
         col2 bigint

      **DESCRIBE** *sourcetable*;

      Result:

      .. code-block::

         col1 int
         col2 int

   #. Add the cast function to convert bigint value to integer.

      **INSERT INTO** *newcarbontable select col1, cast(col2 as integer) from sourcetable;*
