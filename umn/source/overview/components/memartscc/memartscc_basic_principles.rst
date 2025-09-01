:original_name: mrs_08_0117.html

.. _mrs_08_0117:

MemArtsCC Basic Principles
==========================

MemArtsCC is a distributed lightweight caching system deployed on the compute side in the storage-compute decoupled architecture. It prefetches data from remote object storage to accelerate caching and computing jobs.

MemArtsCC shards objects on remote OBS and creates indexes, greatly improving the performance of reading cached data. ZooKeeper enables lightweight service discovery and provides ultra-high availability. The lifecycle management of sharded data is based on the LRU algorithm.

Main Features of MemArtsCC
--------------------------

-  The decentralized architecture enables all instances to provide same service capabilities.
-  The lightweight design ensures ultra-low resource usage.
-  MemArtsCC is decoupled from applications and therefore is transparent to them and can be used without adaptation.
-  MemArtsCC ensures high availability in case of node failures.

MemArtsCC Structure
-------------------

There are CCSideCar and CCWorker roles of MemArtsCC instances.

In a storage-compute decoupled architecture, data of computing and analytics applications such as Spark and Hive is stored in OBS. In a MemArtsCC cluster, a service instance is called a worker. Workers cache some or all of the object data in OBS to local persistent storage (SSD/HDD). When an application reads an object through the MemArtsCC SDK, the application reads sharded data from a specific worker based on the shard index. If the cache is hit, the worker returns the shards. If the cache is not hit, the application directly reads data from OBS. The worker asynchronously loads the shards that are not hit to local storage for subsequent use.


.. figure:: /_static/images/en-us_image_0000002381596168.png
   :alt: **Figure 1** MemArtsCC Structure

   **Figure 1** MemArtsCC Structure

.. table:: **Table 1** MemArtsCC architecture

   +---------------+--------------------------------------------------------------------------------------------------------------------------------+
   | Name          | Description                                                                                                                    |
   +===============+================================================================================================================================+
   | MemArtsCC SDK | An SDK used by OBSA (a Hadoop client plug-in) to access OBS server objects.                                                    |
   +---------------+--------------------------------------------------------------------------------------------------------------------------------+
   | CCSideCar     | The management plane service. It monitors MemArtsCC, collects data, delivers configurations, and starts and stops the service. |
   +---------------+--------------------------------------------------------------------------------------------------------------------------------+
   | CCWorker      | The data plane service. It reads, writes, stores, and deletes data cached by MemArtsCC.                                        |
   +---------------+--------------------------------------------------------------------------------------------------------------------------------+
