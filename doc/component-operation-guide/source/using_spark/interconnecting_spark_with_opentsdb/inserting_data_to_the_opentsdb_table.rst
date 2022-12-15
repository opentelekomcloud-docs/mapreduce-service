:original_name: mrs_01_0586.html

.. _mrs_01_0586:

Inserting Data to the OpenTSDB Table
====================================

Function
--------

Run the **INSERT INTO** statement to insert the data in the table to the associated OpenTSDB metric.

Syntax
------

.. code-block::

   INSERT INTO TABLE_NAME SELECT * FROM SRC_TABLE;
   INSERT INTO TABLE_NAME VALUES(XXX);

Keyword
-------

+------------+---------------------------------------------------------------------------------------------------------------------+
| Parameter  | Description                                                                                                         |
+============+=====================================================================================================================+
| TABLE_NAME | Indicates the name of the associated OpenTSDB table.                                                                |
+------------+---------------------------------------------------------------------------------------------------------------------+
| SRC_TABLE  | Indicates the name of the table from which data is obtained. This parameter can be set to a name of a common table. |
+------------+---------------------------------------------------------------------------------------------------------------------+

Precautions
-----------

-  The inserted data cannot be **null**. If the inserted data is the same as the original data or only the **value** is different, the inserted data overwrites the original data.
-  **INSERT OVERWRITE** is not supported.
-  You are advised not to concurrently insert data into a table. If you concurrently insert data into a table, there is a possibility that conflicts occur, leading to data insertion failures.
-  The **TIMESTAMP** format supports only yyyy-MM-dd hh:mm:ss.

Example
-------

Insert data into table **opentsdb_table**.

.. code-block::

   insert into opentsdb_table values('city1','futian','2018-05-03 00:00:00',21);
