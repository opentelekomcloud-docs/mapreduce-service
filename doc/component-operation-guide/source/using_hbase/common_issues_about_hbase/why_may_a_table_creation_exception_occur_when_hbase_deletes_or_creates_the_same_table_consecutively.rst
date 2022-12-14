:original_name: mrs_01_1641.html

.. _mrs_01_1641:

Why May a Table Creation Exception Occur When HBase Deletes or Creates the Same Table Consecutively?
====================================================================================================

Question
--------

When HBase consecutively deletes and creates the same table, why may a table creation exception occur?

Answer
------

Execution process: Disable Table > Drop Table > Create Table > Disable Table > Drop Table > And more

#. When a table is disabled, HMaster sends an RPC request to RegionServer, and RegionServer brings the region offline. When the time required for closing a region on RegionServer exceeds the timeout period for HBase HMaster to wait for the region to enter the RIT state, HMaster considers that the region is offline by default. Actually, the region may be in the flush memstore phase.
#. After an RPC request is sent to close a region, HMaster checks whether all regions in the table are offline. If the closure times out, HMaster considers that the regions are offline and returns a message indicating that the regions are successfully closed.
#. After the closure is successful, the data directory corresponding to the HBase table is deleted.
#. After the table is deleted, the data directory is recreated by the region that is still in the flush memstore phase.
#. When the table is created again, the **temp** directory is copied to the HBase data directory. However, the HBase data directory is not empty. As a result, when the HDFS rename API is called, the data directory changes to the last layer of the **temp** directory and is appended to the HBase data directory, for example, **$rootDir/data/$nameSpace/$tableName/$tableName**. In this case, the table fails to be created.

**Troubleshooting Method**

When this problem occurs, check whether the HBase data directory corresponding to the table exists. If it exists, rename the directory.

The HBase data directory consists of **$rootDir/data/$nameSpace/$tableName**, for example, **hdfs://hacluster/hbase/data/default/TestTable**. **$rootDir** is the HBase root directory, which can be obtained by configuring **hbase.rootdir.perms** in **hbase-site.xml**. The **data** directory is a fixed directory of HBase. **$nameSpace** indicates the nameSpace name. **$tableName** indicates the table name.
