:original_name: mrs_01_1691.html

.. _mrs_01_1691:

NameNode Startup Is Slow
========================

Question
--------

The NameNode startup is slow when it is restarted immediately after a large number of files (for example, 1 million files) are deleted.

Answer
------

It takes time for the DataNode to delete the corresponding blocks after files are deleted. When the NameNode is restarted immediately, it checks the block information reported by all DataNodes. If a deleted block is found, the NameNode generates the corresponding INFO log information, as shown below:

.. code-block::

   2015-06-10 19:25:50,215 | INFO  | IPC Server handler 36 on 25000 | BLOCK* processReport:
   blk_1075861877_2121067 on node 10.91.8.218:9866 size 10249 does not belong to any file |
   org.apache.hadoop.hdfs.server.blockmanagement.BlockManager.processReport(BlockManager.java:1854)

A log is generated for each deleted block. A file may contain one or more blocks. Therefore, after startup, the NameNode spends a large amount of time printing logs when a large number of files are deleted. As a result, the NameNode startup becomes slow.

To address this issue, the following operations can be performed to speed up the startup:

#. After a large number of files are deleted, wait until the DataNode deletes the corresponding blocks and then restart the NameNode.

   You can run the **hdfs dfsadmin -report** command to check the disk space and check whether the files have been deleted.

#. If a large number of the preceding logs are generated, you can change the NameNode log level to **ERROR** so that the NameNode stops printing such logs.

   After the NameNode is restarted, change the log level back to **INFO**. You do not need to restart the service after changing the log level.
