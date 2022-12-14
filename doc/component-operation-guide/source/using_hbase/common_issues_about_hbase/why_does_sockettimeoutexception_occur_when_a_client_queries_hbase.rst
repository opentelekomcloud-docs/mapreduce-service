:original_name: mrs_01_1646.html

.. _mrs_01_1646:

Why Does SocketTimeoutException Occur When a Client Queries HBase?
==================================================================

Question
--------

Why does the following exception occur on the client when I use the HBase client to operate table data?

.. code-block::

   2015-12-15 02:41:14,054 | WARN  | [task-result-getter-2] | Lost task 2.0 in stage 58.0 (TID 3288, linux-175):
   org.apache.hadoop.hbase.client.RetriesExhaustedException: Failed after attempts=36, exceptions:
   Tue Dec 15 02:41:14 CST 2015, null, java.net.SocketTimeoutException: callTimeout=60000, callDuration=60303:
   row 'xxxxxx' on table 'xxxxxx' at region=xxxxxx,\x05\x1E\x80\x00\x00\x00\x80\x00\x00\x00\x00\x00\x00\x00\x80\x00\x00\x00\x00\x00\x00\x000\x00\x80\x00\x00\x00\x80\x00\x00\x00\x80\x00\x00,
   1449912620868.6a6b7d0c272803d8186930a3bfdb10a9., hostname=xxxxxx,16020,1449941841479, seqNum=5
   at org.apache.hadoop.hbase.client.RpcRetryingCallerWithReadReplicas.throwEnrichedException(RpcRetryingCallerWithReadReplicas.java:275)
   at org.apache.hadoop.hbase.client.ScannerCallableWithReplicas.call(ScannerCallableWithReplicas.java:223)
   at org.apache.hadoop.hbase.client.ScannerCallableWithReplicas.call(ScannerCallableWithReplicas.java:61)
   at org.apache.hadoop.hbase.client.RpcRetryingCaller.callWithoutRetries(RpcRetryingCaller.java:200)
   at org.apache.hadoop.hbase.client.ClientScanner.call(ClientScanner.java:323)

At the same time, the following log is displayed on RegionServer:

.. code-block::

   2015-12-15 02:45:44,551 | WARN  | PriorityRpcServer.handler=7,queue=1,port=16020 | (responseTooSlow): {"call":"Scan(org.apache.hadoop.hbase.protobuf.generated.ClientProtos$ScanRequest)
   ","starttimems":1450118730780,"responsesize":416,"method":"Scan","processingtimems":13770,"client":"10.91.8.175:41182","queuetimems":0,"class":"HRegionServer"} |
   org.apache.hadoop.hbase.ipc.RpcServer.logResponse(RpcServer.java:2221)
   2015-12-15 02:45:57,722 | WARN  | PriorityRpcServer.handler=3,queue=1,port=16020 | (responseTooSlow):
   {"call":"Scan(org.apache.hadoop.hbase.protobuf.generated.ClientProtos$ScanRequest)","starttimems":1450118746297,"responsesize":416,
   "method":"Scan","processingtimems":11425,"client":"10.91.8.175:41182","queuetimems":1746,"class":"HRegionServer"} | org.apache.hadoop.hbase.ipc.RpcServer.logResponse(RpcServer.java:2221)
   2015-12-15 02:47:21,668 | INFO  | LruBlockCacheStatsExecutor | totalSize=7.54 GB, freeSize=369.52 MB, max=7.90 GB, blockCount=406107,
   accesses=35400006, hits=16803205, hitRatio=47.47%, , cachingAccesses=31864266, cachingHits=14806045, cachingHitsRatio=46.47%,
   evictions=17654, evicted=16642283, evictedPerRun=942.69189453125 | org.apache.hadoop.hbase.io.hfile.LruBlockCache.logStats(LruBlockCache.java:858)
   2015-12-15 02:52:21,668 | INFO  | LruBlockCacheStatsExecutor | totalSize=7.51 GB, freeSize=395.34 MB, max=7.90 GB, blockCount=403080,
   accesses=35685793, hits=16933684, hitRatio=47.45%, , cachingAccesses=32150053, cachingHits=14936524, cachingHitsRatio=46.46%,
   evictions=17684, evicted=16800617, evictedPerRun=950.046142578125 | org.apache.hadoop.hbase.io.hfile.LruBlockCache.logStats(LruBlockCache.java:858)

Answer
------

The memory allocated to RegionServer is too small and the number of Regions is too large. As a result, the memory is insufficient during the running, and the server responds slowly to the client. Modify the following memory allocation parameters in the **hbase-site.xml** configuration file of RegionServer:

.. table:: **Table 1** RegionServer memory allocation parameters

   +------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | Parameter              | Description                                                                                         | Default Value                                                                                                           |
   +========================+=====================================================================================================+=========================================================================================================================+
   | GC_OPTS                | Initial memory and maximum memory allocated to RegionServer in startup parameters.                  | -Xms8G -Xmx8G                                                                                                           |
   +------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | hfile.block.cache.size | Percentage of the maximum heap (-Xmx setting) allocated to the block cache of HFiles or StoreFiles. | When **offheap** is disabled, the default value is **0.25**. When **offheap** is enabled, the default value is **0.1**. |
   +------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
