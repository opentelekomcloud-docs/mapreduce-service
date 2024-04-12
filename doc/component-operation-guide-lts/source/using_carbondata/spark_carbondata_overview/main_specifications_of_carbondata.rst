:original_name: mrs_01_1403.html

.. _mrs_01_1403:

Main Specifications of CarbonData
=================================


Main Specifications of CarbonData
---------------------------------

.. table:: **Table 1** Main Specifications of CarbonData

   +------------------------------------+------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
   | Entity                             | Tested Value                                                           | Test Environment                                                                                    |
   +====================================+========================================================================+=====================================================================================================+
   | Number of tables                   | 10000                                                                  | 3 nodes. 4 vCPUs and 20 GB memory for each executor. Driver memory: 5 GB, 3 executors.              |
   |                                    |                                                                        |                                                                                                     |
   |                                    |                                                                        | Total columns: 107                                                                                  |
   |                                    |                                                                        |                                                                                                     |
   |                                    |                                                                        | String: 75                                                                                          |
   |                                    |                                                                        |                                                                                                     |
   |                                    |                                                                        | Int: 13                                                                                             |
   |                                    |                                                                        |                                                                                                     |
   |                                    |                                                                        | BigInt: 7                                                                                           |
   |                                    |                                                                        |                                                                                                     |
   |                                    |                                                                        | Timestamp: 6                                                                                        |
   |                                    |                                                                        |                                                                                                     |
   |                                    |                                                                        | Double: 6                                                                                           |
   +------------------------------------+------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
   | Number of table columns            | 2000                                                                   | 3 nodes. 4 vCPUs and 20 GB memory for each executor. Driver memory: 5 GB, 3 executors.              |
   +------------------------------------+------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
   | Maximum size of a raw CSV file     | 200GB                                                                  | 17 cluster nodes. 150 GB memory and 25 vCPUs for each executor. Driver memory: 10 GB, 17 executors. |
   +------------------------------------+------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
   | Number of CSV files in each folder | 100 folders. Each folder has 10 files. The size of each file is 50 MB. | 3 nodes. 4 vCPUs and 20 GB memory for each executor. Driver memory: 5 GB, 3 executors.              |
   +------------------------------------+------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+
   | Number of load folders             | 10000                                                                  | 3 nodes. 4 vCPUs and 20 GB memory for each executor. Driver memory: 5 GB, 3 executors.              |
   +------------------------------------+------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+

The memory required for data loading depends on the following factors:

-  Number of columns
-  Column values
-  Concurrency (configured using **carbon.number.of.cores.while.loading**)
-  Sort size in memory (configured using **carbon.sort.size**)
-  Intermediate cache (configured using **carbon.graph.rowset.size**)

Data loading of an 8 GB CSV file that contains 10 million records and 300 columns with each row size being about 0.8 KB requires about 10 GB executor memory. That is, set **carbon.sort.size** to **100000** and retain the default values for other parameters.

Table Specifications
--------------------

.. table:: **Table 2** Table specifications

   +-----------------------------------------------------------------------------------------------------------+--------------+
   | Entity                                                                                                    | Tested Value |
   +===========================================================================================================+==============+
   | Number of secondary index tables                                                                          | 10           |
   +-----------------------------------------------------------------------------------------------------------+--------------+
   | Number of composite columns in a secondary index table                                                    | 5            |
   +-----------------------------------------------------------------------------------------------------------+--------------+
   | Length of column name in a secondary index table (unit: character)                                        | 120          |
   +-----------------------------------------------------------------------------------------------------------+--------------+
   | Length of a secondary index table name (unit: character)                                                  | 120          |
   +-----------------------------------------------------------------------------------------------------------+--------------+
   | Cumulative length of all secondary index table names + column names in an index table\* (unit: character) | 3800*\*      |
   +-----------------------------------------------------------------------------------------------------------+--------------+

.. note::

   -  \* Characters of column names in an index table refers to the upper limit allowed by Hive or the upper limit of available resources.
   -  \*\* Secondary index tables are registered using Hive and stored in HiveSERDEPROPERTIES in JSON format. The value of **SERDEPROPERTIES** supported by Hive can contain a maximum of 4,000 characters and cannot be changed.
