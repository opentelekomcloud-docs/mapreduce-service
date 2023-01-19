:original_name: mrs_01_2302.html

.. _mrs_01_2302:

Redis-based CacheStore of HiveMetaStore
=======================================

Scenario
--------

The MetaStore service of Hive can cache the metadata of some tables in Redis.

Prerequisites
-------------

The Redis service has been installed in a cluster.

Configure Parameters Related to Metastore
-----------------------------------------

#. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Hive** > **Configurations** > **All Configurations** > **MetaStore(Role)** > **Customization**. Modify the following parameters to interconnect the cache of MetaStore to the Redis service.

   .. table:: **Table 1** Parameters

      +---------------------------------------------------+---------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                                         | Value                                                         | Description                                                                                                                                                                                       |
      +===================================================+===============================================================+===================================================================================================================================================================================================+
      | hive.metastore.rawstore.impl                      | org.apache.hadoop.hive.metastore.cache.redis.RedisCachedStore | (Mandatory) Implementation class of CachedStore. Use the customized RedisCachedStore.                                                                                                             |
      +---------------------------------------------------+---------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | redis.cluster.host.and.port                       | xxx.xxx.xxx.xxx:22400;xxx.xxx.xxx.xxx.xxx:22401               | (Mandatory) IP address and port number of any node in the Redis cluster. The format is *ip:port. ip:port*. The value cannot end with a semicolon (;).                                             |
      +---------------------------------------------------+---------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | metastore.cached.rawstore.cached.object.whitelist | catalog.database.table,catalog.database.table                 | (Optional) Cache table whitelist. The configured tables are cached to Redis. Multiple tables are separated by commas (,). The default separator is **.\***, that is, all tables are cached.       |
      |                                                   |                                                               |                                                                                                                                                                                                   |
      |                                                   |                                                               | .. note::                                                                                                                                                                                         |
      |                                                   |                                                               |                                                                                                                                                                                                   |
      |                                                   |                                                               |    The table name consists of **catalog.database.table**. The default catalog is **hive**.                                                                                                        |
      +---------------------------------------------------+---------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | metastore.cached.rawstore.cached.object.blacklist | catalog.database.table,catalog.database.table                 | (Optional) Cache table blacklist. Tables that are not configured in the blacklist are not cached in Redis. Multiple tables are separated by commas (,). By default, this parameter is left blank. |
      |                                                   |                                                               |                                                                                                                                                                                                   |
      |                                                   |                                                               | .. note::                                                                                                                                                                                         |
      |                                                   |                                                               |                                                                                                                                                                                                   |
      |                                                   |                                                               |    The table name consists of **catalog.database.table**. The default catalog is **hive**.                                                                                                        |
      +---------------------------------------------------+---------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | redis.cache.prewarm.cron                          | cronTab expression, for example, 0 0 16 \* \*?                | (Optional) Periodically execute the corn expression of prewarm to update the data cached in the metabase to redisCache for synchronization.                                                       |
      +---------------------------------------------------+---------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | metastore.cached.rawstore.catalogs                | hive                                                          | (Optional) Catalog to be cached. The default value is **hive**.                                                                                                                                   |
      +---------------------------------------------------+---------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | jedis.pool.max.wait.mills                         | 30,000                                                        | (Optional) Obtain the Redis connection timeout interval. In security mode, the timeout interval can be longer. The unit is ms. The default value is 30,000 ms.                                    |
      +---------------------------------------------------+---------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | jedis.pool.max.idle                               | 200                                                           | (Optional) Maximum number of idle connections in the Jedis connection pool. You are advised to set this parameter to the value of **max.total**. The default value is 200.                        |
      +---------------------------------------------------+---------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | jedis.pool.max.total                              | 200                                                           | (Optional) Maximum number of connections in the Jedis connection pool. The default value is 200.                                                                                                  |
      +---------------------------------------------------+---------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | redis.security.enabled                            | true or false                                                 | (Optional) Whether to enable the Redis cache security mode. The default value is **true**, indicating that the security mode is enabled.                                                          |
      +---------------------------------------------------+---------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      If the cluster is installed in non-security mode, choose **Cluster** > *Name of the desired cluster* > **Services** > **Redis** > **Configurations** > **All Configurations** > **Redis** > **Security** and check whether the value of **REDIS_SECURITY_ENABLED** is **false**. If not, change it to **false**.Otherwise, the Redis service does not comply with the non-security mode of the current Metastore.

#. Save the configuration and choose **Dashboard** > **More** > **Restart Service** to restart the Hive service.

Precautions
-----------

If Redis is switched back to the native non-cache mode and then switched back after a period of time, the added, deleted, or modified metadata cannot be synchronized to the Redis when the database is used. Therefore, before switching back, you must clear the cache table in the Redis and synchronize the metadata again in either of the following two clearing modes:

-  Log in to the Redis client and run the **flushall** command on all Redis nodes.

-  Log in to the Redis client and run the following commands to change the two Redis identifiers. *{hiveServiceName}* is the value of **HIVE_DEFAULT_GROUP** in the Metastore configuration file **ENV_VARS**. The default value is **hive**.

   **set** *{hiveServiceName}*\ **-hive-isRedisAvailable false**

   **del** *{hiveServiceName}*\ **-hive-isCanPrewarm**
