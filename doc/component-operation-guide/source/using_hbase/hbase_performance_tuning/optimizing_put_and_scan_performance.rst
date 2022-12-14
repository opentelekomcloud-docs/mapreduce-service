:original_name: mrs_01_1016.html

.. _mrs_01_1016:

Optimizing Put and Scan Performance
===================================

Scenario
--------

HBase has many configuration parameters related to read and write performance. The configuration parameters need to be adjusted based on the read/write request loads. This section describes how to optimize read and write performance by modifying the RegionServer configurations.

.. note::

   This section applies to MRS 3.\ *x* and later versions.

Procedure
---------

-  JVM GC parameters

   Suggestions on setting the RegionServer **GC_OPTS** parameter:

   -  Set **-Xms** and **-Xmx** to the same value based on your needs. Increasing the memory can improve the read and write performance. For details, see the description of **hfile.block.cache.size** in :ref:`Table 2 <mrs_01_1016__tcd04a4cfd9f94a80a47de3ccb824175e>` and **hbase.regionserver.global.memstore.size** in :ref:`Table 1 <mrs_01_1016__t5194159aa9d34637bba4cdd0aa3b925e>`.
   -  Set **-XX:NewSize** and **-XX:MaxNewSize** to the same value. You are advised to set the value to **512M** in low-load scenarios and **2048M** in high-load scenarios.
   -  Set **X-XX:CMSInitiatingOccupancyFraction** to be less than and equal to 90, and it is calculated as follows: **100 x (hfile.block.cache.size + hbase.regionserver.global.memstore.size + 0.05)**.
   -  **-XX:MaxDirectMemorySize** indicates the non-heap memory used by the JVM. You are advised to set this parameter to **512M** in low-load scenarios and **2048M** in high-load scenarios.

      .. note::

         The **-XX:MaxDirectMemorySize** parameter is not used by default. If you need to set this parameter, add it to the **GC_OPTS** parameter.

-  Put parameters

   RegionServer processes the data of the put request and writes the data to memstore and HLog.

   -  When the size of memstore reaches the value of **hbase.hregion.memstore.flush.size**, memstore is updated to HDFS to generate HFiles.
   -  Compaction is triggered when the number of HFiles in the column cluster of the current region reaches the value of **hbase.hstore.compaction.min**.
   -  If the number of HFiles in the column cluster of the current region reaches the value of **hbase.hstore.blockingStoreFiles**, the operation of refreshing the memstore and generating HFiles is blocked. As a result, the put request is blocked.

   .. _mrs_01_1016__t5194159aa9d34637bba4cdd0aa3b925e:

   .. table:: **Table 1** Put parameters

      +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Parameter                                  | Description                                                                                                                                                                                                                                                                                                                                                                                        | Default Value         |
      +============================================+====================================================================================================================================================================================================================================================================================================================================================================================================+=======================+
      | hbase.wal.hsync                            | Indicates whether each WAL is persistent to disks.                                                                                                                                                                                                                                                                                                                                                 | true                  |
      |                                            |                                                                                                                                                                                                                                                                                                                                                                                                    |                       |
      |                                            | For details, see :ref:`Improving Put Performance <mrs_01_1637>`.                                                                                                                                                                                                                                                                                                                                   |                       |
      +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | hbase.hfile.hsync                          | Indicates whether HFile write operations are persistent to disks.                                                                                                                                                                                                                                                                                                                                  | true                  |
      |                                            |                                                                                                                                                                                                                                                                                                                                                                                                    |                       |
      |                                            | For details, see :ref:`Improving Put Performance <mrs_01_1637>`.                                                                                                                                                                                                                                                                                                                                   |                       |
      +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | hbase.hregion.memstore.flush.size          | If the size of MemStore (unit: Byte) exceeds a specified value, MemStore is flushed to the corresponding disk. The value of this parameter is checked by each thread running **hbase.server.thread.wakefrequency**. It is recommended that you set this parameter to an integer multiple of the HDFS block size. You can increase the value if the memory is sufficient and the put load is heavy. | 134217728             |
      +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | hbase.regionserver.global.memstore.size    | Updates the size of all MemStores supported by the RegionServer before locking or forcible flush. It is recommended that you set this parameter to **hbase.hregion.memstore.flush.size x Number of regions with active writes/RegionServer GC -Xmx**. The default value is **0.4**, indicating that 40% of RegionServer GC -Xmx is used.                                                           | 0.4                   |
      +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | hbase.hstore.flusher.count                 | Indicates the number of memstore flush threads. You can increase the parameter value in heavy-put-load scenarios.                                                                                                                                                                                                                                                                                  | 2                     |
      +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | hbase.regionserver.thread.compaction.small | Indicates the number of small compaction threads. You can increase the parameter value in heavy-put-load scenarios.                                                                                                                                                                                                                                                                                | 10                    |
      +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | hbase.hstore.blockingStoreFiles            | If the number of HStoreFile files in a Store exceeds the specified value, the update of the HRegion will be locked until a compression is completed or the value of **base.hstore.blockingWaitTime** is exceeded. Each time MemStore is flushed, a StoreFile file is written into MemStore. Set this parameter to a larger value in heavy-put-load scenarios.                                      | 15                    |
      +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

-  Scan parameters

   .. _mrs_01_1016__tcd04a4cfd9f94a80a47de3ccb824175e:

   .. table:: **Table 2** Scan parameters

      +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------+
      | Parameter                           | Description                                                                                                                                                                                                                                                                                                   | Default Value                                                                                                   |
      +=====================================+===============================================================================================================================================================================================================================================================================================================+=================================================================================================================+
      | hbase.client.scanner.timeout.period | Client and RegionServer parameters, indicating the lease timeout period of the client executing the scan operation. You are advised to set this parameter to an integer multiple of 60000 ms. You can set this parameter to a larger value when the read load is heavy. The unit is milliseconds.             | 60000                                                                                                           |
      +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------+
      | hfile.block.cache.size              | Indicates the data cache percentage in the RegionServer GC -Xmx. You can increase the parameter value in heavy-read-load scenarios, in order to improve cache hit ratio and performance. It indicates the percentage of the maximum heap (-Xmx setting) allocated to the block cache of HFiles or StoreFiles. | When offheap is disabled, the default value is **0.25**. When offheap is enabled, the default value is **0.1**. |
      +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------+

-  Handler parameters

   .. table:: **Table 3** Handler parameters

      +--------------------------------------+------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Parameter                            | Description                                                                                                                  | Default Value |
      +======================================+==============================================================================================================================+===============+
      | hbase.regionserver.handler.count     | Indicates the number of RPC server instances on RegionServer. The recommended value ranges from 200 to 400.                  | 200           |
      +--------------------------------------+------------------------------------------------------------------------------------------------------------------------------+---------------+
      | hbase.regionserver.metahandler.count | Indicates the number of program instances for processing prioritized requests. The recommended value ranges from 200 to 400. | 200           |
      +--------------------------------------+------------------------------------------------------------------------------------------------------------------------------+---------------+
