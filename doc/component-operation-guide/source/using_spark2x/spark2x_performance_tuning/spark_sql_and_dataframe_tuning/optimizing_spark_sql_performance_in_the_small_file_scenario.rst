:original_name: mrs_01_1988.html

.. _mrs_01_1988:

Optimizing Spark SQL Performance in the Small File Scenario
===========================================================

Scenario
--------

A Spark SQL table may have many small files (far smaller than an HDFS block), each of which maps to a partition on the Spark by default. In other words, each small file is a task. If the small files are great in number, Spark must initiate a large number of tasks. If shuffle operations exist in Spark SQL, the number of hash buckets increases, affecting performance.

In this scenario, you can manually specify the split size of each task to avoid an excessive number of tasks and improve performance.

.. note::

   If the SQL logic does not involve shuffle operations, this optimization does not improve performance.

Configuration
-------------

If you want to enable small file optimization, configure the **spark-defaults.conf** file on the Spark client.

.. table:: **Table 1** Parameter description

   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter                         | Description                                                                                                                                                                                                                                                                               | Default Value         |
   +===================================+===========================================================================================================================================================================================================================================================================================+=======================+
   | spark.sql.files.maxPartitionBytes | The maximum number of bytes that can be packed into a single partition when a file is read.                                                                                                                                                                                               | 134217728 (128 MB)    |
   |                                   |                                                                                                                                                                                                                                                                                           |                       |
   |                                   | Unit: byte                                                                                                                                                                                                                                                                                |                       |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | spark.files.openCostInBytes       | The estimated cost to open a file, measured by the number of bytes that can be scanned in the same time. This is used when putting multiple files into a partition. It is better to over estimate, then the partitions with small files will be faster than partitions with larger files. | 4 MB                  |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
