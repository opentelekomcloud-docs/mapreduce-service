:original_name: mrs_01_1688.html

.. _mrs_01_1688:

Improving Read Performance Using Client Metadata Cache
======================================================

Scenario
--------

Improve the HDFS read performance by using the client to cache the metadata for block locations.

.. note::

   This function is recommended only for reading files that are not modified frequently. Because the data modification done on the server side by some other client is invisible to the cache client, which may cause the metadata obtained from the cache to be outdated.

   This section applies to MRS 3.\ *x* or later.

Procedure
---------

**Navigation path for setting parameters:**

On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS** > **Configurations**, select **All Configurations**, and enter the parameter name in the search box.

.. table:: **Table 1** Parameter configuration

   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter                             | Description                                                                                                                                                                                                                                                           | Default Value         |
   +=======================================+=======================================================================================================================================================================================================================================================================+=======================+
   | dfs.client.metadata.cache.enabled     | Enables or disables the client to cache the metadata for block locations. Set this parameter to **true** and use it along with the **dfs.client.metadata.cache.pattern** parameter to enable the cache.                                                               | false                 |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | dfs.client.metadata.cache.pattern     | Indicates the regular expression pattern of the path of the file to be cached. Only the metadata for block locations of these files is cached until the metadata expires. This parameter is valid only when **dfs.client.metadata.cache.enabled** is set to **true**. | ``-``                 |
   |                                       |                                                                                                                                                                                                                                                                       |                       |
   |                                       | Example: **/test.\*** indicates that all files whose paths start with **/test** are read.                                                                                                                                                                             |                       |
   |                                       |                                                                                                                                                                                                                                                                       |                       |
   |                                       | .. note::                                                                                                                                                                                                                                                             |                       |
   |                                       |                                                                                                                                                                                                                                                                       |                       |
   |                                       |    -  To ensure consistency, configure a specific mode to cache only files that are not frequently modified by other clients.                                                                                                                                         |                       |
   |                                       |                                                                                                                                                                                                                                                                       |                       |
   |                                       |    -  The regular expression pattern verifies only the path of the URI, but not the schema and authority in the case of the Fully Qualified path.                                                                                                                     |                       |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | dfs.client.metadata.cache.expiry.sec  | Indicates the duration for caching metadata. The cache entry becomes invalid after its caching time exceeds this duration. Even metadata that is frequently used during the caching process can become invalid.                                                       | 60s                   |
   |                                       |                                                                                                                                                                                                                                                                       |                       |
   |                                       | Time suffixes **s**/**m**/**h** can be used to indicate second, minute, and hour, respectively.                                                                                                                                                                       |                       |
   |                                       |                                                                                                                                                                                                                                                                       |                       |
   |                                       | .. note::                                                                                                                                                                                                                                                             |                       |
   |                                       |                                                                                                                                                                                                                                                                       |                       |
   |                                       |    If this parameter is set to **0s**, the cache function is disabled.                                                                                                                                                                                                |                       |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | dfs.client.metadata.cache.max.entries | Indicates the maximum number of non-expired data items that can be cached at a time.                                                                                                                                                                                  | 65536                 |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

.. note::

   Call *DFSClient#clearLocatedBlockCache()* to completely clear the client cache before it expires.

   The sample usage is as follows:

   .. code-block::

          FileSystem fs = FileSystem.get(conf);
          DistributedFileSystem dfs = (DistributedFileSystem) fs;
          DFSClient dfsClient = dfs.getClient();
          dfsClient.clearLocatedBlockCache();
