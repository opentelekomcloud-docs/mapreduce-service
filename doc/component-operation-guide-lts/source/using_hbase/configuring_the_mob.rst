:original_name: mrs_01_1631.html

.. _mrs_01_1631:

Configuring the MOB
===================

Scenario
--------

In the actual application scenario, data in various sizes needs to be stored, for example, image data and documents. Data whose size is smaller than 10 MB can be stored in HBase. HBase can yield the best read-and-write performance for data whose size is smaller than 100 KB. If the size of data stored in HBase is greater than 100 KB or even reaches 10 MB and the same number of data files are inserted, the total data amount is large, causing frequent compaction and split, high CPU consumption, high disk I/O frequency, and low performance.

MOB data (100 KB to 10 MB data) is stored in a file system (such as the HDFS) in the HFile format. Files are centrally managed using the expiredMobFileCleaner and Sweeper tools. The addresses and size of files are stored in the HBase store as values. This greatly decreases the compaction and split frequency in HBase and improves performance.

The MOB function of HBase is enabled by default. For details about related configuration items, see :ref:`Table 1 <mrs_01_1631__en-us_topic_0000001219230677_t19912a272c204245856b9698b6f04877>`. To use the MOB function, you need to specify the MOB mode for storing data in the specified column family when creating a table or modifying table attributes.

Configuration Description
-------------------------

To enable the HBase MOB function, you need to specify the MOB mode for storing data in the specified column family when creating a table or modifying table attributes.

Use code to declare that the MOB mode for storing data is used:

.. code-block::

   HColumnDescriptor hcd = new HColumnDescriptor("f");
   hcd.setMobEnabled(true);

Use code to declare that the MOB mode for storing data is used, the unit of MOB_THRESHOLD is byte:

.. code-block::

   hbase(main):009:0> create 't3',{NAME => 'd', MOB_THRESHOLD => '102400', IS_MOB => 'true'}

   0 row(s) in 0.3450 seconds

   => Hbase::Table - t3
   hbase(main):010:0> describe 't3'
   Table t3 is ENABLED


   t3


   COLUMN FAMILIES DESCRIPTION


   {NAME => 'd', MOB_THRESHOLD => '102400', VERSIONS => '1', KEEP_DELETED_CELLS => 'FALSE', DATA_BLOCK_ENCODING => 'NONE',
   TTL => 'FOREVER', MIN_VERSIONS => '0', REPLICATION_SCOPE => '0', BLOOMFILTER => 'ROW',
   IN_MEMORY => 'false', IS_MOB => 'true', COMPRESSION => 'NONE', BLOCKCACHE => 'true', BLOCKSIZE => '65536'}

   1 row(s) in 0.0170 seconds

**Navigation path for setting parameters:**

On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase** > **Configurations** > **All Configurations**. Enter a parameter name in the search box.

.. _mrs_01_1631__en-us_topic_0000001219230677_t19912a272c204245856b9698b6f04877:

.. table:: **Table 1** Parameter description

   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter                           | Description                                                                                                                                                                                                                                                                                                                                       | Default Value         |
   +=====================================+===================================================================================================================================================================================================================================================================================================================================================+=======================+
   | hbase.mob.file.cache.size           | Size of the opened file handle cache. If this parameter is set to a large value, more file handles can be cached, reducing the frequency of opening and closing files. However, if this parameter is set to a large value, too many file handles will be opened. The default value is **1000**. This parameter is configured on the ResionServer. | 1000                  |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | hbase.mob.cache.evict.period        | Expiration time of cached MOB files in the MOB cache, in seconds.                                                                                                                                                                                                                                                                                 | 3600                  |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | hbase.mob.cache.evict.remain.ratio  | Ratio of the number of retained files after MOB cache reclamation to the number of cached files. **hbase.mob.cache.evict.remain.ratio** is an algorithm factor. When the number of cached MOB files reaches the product of **hbase.mob.file.cache.size** **hbase.mob.cache.evict.remain.ratio**, cache reclamation is triggered.                  | 0.5                   |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | hbase.master.mob.ttl.cleaner.period | Interval for deleting expired files, in seconds. The default value is one day (86,400 seconds).                                                                                                                                                                                                                                                   | 86400                 |
   |                                     |                                                                                                                                                                                                                                                                                                                                                   |                       |
   |                                     | .. note::                                                                                                                                                                                                                                                                                                                                         |                       |
   |                                     |                                                                                                                                                                                                                                                                                                                                                   |                       |
   |                                     |    If the validity period of an MOB file expires, that is, the file has been created for more than 24 hours, the MOB file will be deleted by the tool for deleting expired MOB files.                                                                                                                                                             |                       |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
