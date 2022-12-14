:original_name: mrs_01_24103.html

.. _mrs_01_24103:

Hudi Table Schema
=================

When writing data, Hudi generates a Hudi table based on attributes such as the storage path, table name, and partition structure.

Hudi table data files can be stored in the OS file system or distributed file system such as HDFS. To ensure analysis performance and data reliability, HDFS is generally used for storage. Using HDFS as an example, Hudi table storage files are classified into two types.

-  The **.hoodie** folder stores the log files related to file merging.

   |image1|

-  The path containing **\_partition_key** stores actual data files and metadata by partition.

   Hudi data files of are stored in Parquet base files and Avro log files.

   |image2|

.. |image1| image:: /_static/images/en-us_image_0000001439498673.png
.. |image2| image:: /_static/images/en-us_image_0000001439380285.png
