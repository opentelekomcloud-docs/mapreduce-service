:original_name: mrs_01_1995.html

.. _mrs_01_1995:

Optimizing Small Files
======================

Scenario
--------

A Spark SQL table may have many small files (far smaller than an HDFS block), each of which maps to a partition on the Spark by default. In other words, each small file is a task. In this way, Spark has to start many such tasks. If a shuffle operation is involved in the SQL logic, the number of hash buckets soars, severely hindering system performance.

In case of massive number of small files, when DataSource creates an RDD, it splits small files in the Spark SQL table to PartitionedFiles and then merges the PartitionedFiles to a partition to avoid generating too many hash buckets during the shuffle operation. See :ref:`Figure 1 <mrs_01_1995__fc95571bfb3be4f21b9f7dbcdcf493ebb>`.

.. _mrs_01_1995__fc95571bfb3be4f21b9f7dbcdcf493ebb:

.. figure:: /_static/images/en-us_image_0000001349170393.jpg
   :alt: **Figure 1** Merging small files

   **Figure 1** Merging small files

Procedure
---------

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
