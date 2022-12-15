:original_name: mrs_01_0585.html

.. _mrs_01_0585:

Creating a Table and Associating It with OpenTSDB
=================================================

Function
--------

MRS Spark can be used to access the data source of OpenTSDB, create and associate tables in the Spark, and query and insert the OpenTSDB data.

Use the **CREATE TABLE** command to create a table and associate it with an existing metric in OpenTSDB.

.. note::

   If no metric exists in OpenTSDB, an error will be reported when the corresponding table is queried.

Syntax
------

.. code-block::

   CREATE TABLE [IF NOT EXISTS] OPENTSDB_TABLE_NAME   USING OPENTSDB OPTIONS (
   'metric' = 'METRIC_NAME',
   'tags' = 'TAG1,TAG2'
   );

Keyword
-------

+-----------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Parameter | Description                                                                                                                                                                                                                                                     |
+===========+=================================================================================================================================================================================================================================================================+
| metric    | Indicates the name of the metric in OpenTSDB corresponding to the table to be created.                                                                                                                                                                          |
+-----------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| tags      | Indicates the tags corresponding to the metric. The tags are used for classification, filtering, and quick retrieval. You can set 1 to 8 tags, which are separated by commas (,). The parameter value includes values of all tagKs in the corresponding metric. |
+-----------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Precautions
-----------

When creating a table, you do not need to specify the **timestamp** and **value** fields. The system automatically builds the following fields based on the specified tags. The fields **TAG1** and **TAG2** are specified by tags.

-  TAG1 String
-  TAG2 String
-  timestamp Timestamp
-  value double

Example
-------

Create table **opentsdb_table** and associate it with metric **city.temp** of the OpenTSDB component.

.. code-block::

   CREATE table opentsdb_table using opentsdb OPTIONS ('metric'='city.temp',  'tags'='city,location');
