:original_name: mrs_08_00123.html

.. _mrs_08_00123:

Hue Enhanced Open Source Features
=================================


Hue Enhanced Open Source Features
---------------------------------

-  Storage policy: The number of HDFS file copies varies depending on the storage media. This feature allows you to manually set an HDFS directory storage policy or can automatically adjust the file storage policy, modify the number of file copies, move the file directory, and delete files based on the latest access time and modification time of HDFS files to fully utilize storage capacity and improve storage performance.

-  MR engine: You can use the MapReduce engine to execute Hive SQL statements.
-  Reliability enhancement: Hue is deployed in active/standby mode. When interconnecting with HDFS, Oozie, Hive, and YARN, Hue can work in failover or load balancing mode.
