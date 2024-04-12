:original_name: mrs_01_24765.html

.. _mrs_01_24765:

Planning IoTDB Capacity
=======================

IoTDB has the multi-replica mechanism. By default, both schema regions and data regions have three replicas. The ConfigNode stores the mapping between regions and the IoTDBServer. The IoTDBServer stores region data and uses the file system of the OS to manage metadata and data files.

Capacity Specifications
-----------------------

-  ConfigNode capacity specifications

   When a new storage group is created, IoTDB allocates 10,000 slots to it by default. When data is written, IoTDB allocates or creates a data region and mounts it to a slot based on the device name and time value. Therefore, the memory usage of a ConfigNode is related to the number of storage groups and the continuous write time of the storage groups.

   ========================== ==================
   Objects of Slot Allocation Object Size (Byte)
   ========================== ==================
   TTimePartitionSlot         4
   TSeriesPartitionSlot       8
   TConsensusGroupId          4
   ========================== ==================

   According to the preceding table, creating one storage group that keeps running for 10 years requires about 0.68 GB of memory on a ConfigNode.

   10,000 (slots) x 10 (years) x 365 (partitions) x (TTimePartitionSlot size + TSeriesPartitionSlot size + TConsensusGroupId size) = 0.68 GB

-  IoTDBServer capacity specifications

   Data in IoTDB is allocated to IoTDBServers by region. By default, a region stores data as three replicas, and therefore three files are stored in the IoTDBServer file system. The upper limit of the IoTDBServer capacity is the maximum number of files that can be stored in the OS. For Linux, the upper limit is the number of inodes.
