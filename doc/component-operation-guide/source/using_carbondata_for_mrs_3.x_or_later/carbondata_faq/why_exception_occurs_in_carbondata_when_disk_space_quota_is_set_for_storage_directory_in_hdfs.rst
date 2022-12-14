:original_name: mrs_01_1473.html

.. _mrs_01_1473:

Why Exception Occurs in CarbonData When Disk Space Quota is Set for Storage Directory in HDFS?
==============================================================================================

Question
--------

Why exception occurs in CarbonData when Disk Space Quota is set for the storage directory in HDFS?

Answer
------

The data will be written to HDFS when you during create table, load table, update table, and so on. If the configured HDFS directory does not have sufficient disk space quota, then the operation will fail and throw following exception.

.. code-block::

   org.apache.hadoop.hdfs.protocol.DSQuotaExceededException:
   The DiskSpace quota of /user/tenant is exceeded:
   quota = 314572800 B = 300 MB but diskspace consumed = 402653184 B = 384 MB at
   org.apache.hadoop.hdfs.server.namenode.DirectoryWithQuotaFeature.verifyStoragespaceQuota(DirectoryWithQuotaFeature.java:211) at
   org.apache.hadoop.hdfs.server.namenode.DirectoryWithQuotaFeature.verifyQuota(DirectoryWithQuotaFeature.java:239) at
   org.apache.hadoop.hdfs.server.namenode.FSDirectory.verifyQuota(FSDirectory.java:941) at
   org.apache.hadoop.hdfs.server.namenode.FSDirectory.updateCount(FSDirectory.java:745)

If such exception occurs, configure a sufficient disk space quota for the tenant.

For example:

If the HDFS replication factor is 3 and HDFS default block size is 128 MB, then at least 384 MB (no. of block x block_size x replication_factor of the schema file = 1 x 128 x 3 = 384 MB) disk space quota is required to write a table schema file to HDFS.

.. note::

   In case of fact files, as the default block size is 1024 MB, the minimum space required is 3072 MB per fact file for data load.
