:original_name: mrs_01_1699.html

.. _mrs_01_1699:

Why Data in the Buffer Is Lost If a Power Outage Occurs During Storage of Small Files
=====================================================================================

Question
--------

Why data in the buffer is lost if a power outage occurs during storage of small files?

Answer
------

Because of a power outage, the blocks in the buffer are not written to the disk immediately after the write operation is completed. To enable synchronization of blocks to the disk, set **dfs.datanode.synconclose** to **true** in the **hdfs-site.xml** file.

By default, **dfs.datanode.synconclose** is set to **false**. This improves the performance but can cause a buffer data loss in the case of a power outage, and therefore, it is recommended that **dfs.datanode.synconclose** be set to **true** even if this may affect the performance. You can determine whether to enable the synchronization function based on your actual situation.
