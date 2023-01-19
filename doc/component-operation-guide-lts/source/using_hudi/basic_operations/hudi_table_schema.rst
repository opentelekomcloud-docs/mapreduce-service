:original_name: mrs_01_24103.html

.. _mrs_01_24103:

Hudi Table Schema
=================

When writing data, Hudi generates a Hudi table based on attributes such as the storage path, table name, and partition structure.

Hudi table data files can be stored in the OS file system or distributed file system such as HDFS. To ensure analysis performance and data reliability, HDFS is generally used for storage. Using HDFS as an example, Hudi table storage files are classified into two types.

|image1|

-  The **.hoodie** folder stores the log files related to file merging.

   |image2|

-  The path containing **\_partition_key** stores actual data files and metadata by partition.

   Hudi data files of are stored in Parquet base files and Avro log files.

   |image3|

.. |image1| image:: /_static/images/en-us_image_0000001349059713.png
.. |image2| image:: /_static/images/en-us_image_0000001295740060.png
.. |image3| image:: /_static/images/en-us_image_0000001295900028.png
