:original_name: admin_guide_000093.html

.. _admin_guide_000093:

Resource Overview
=================

MRS cluster resources are classified into computing resources and storage resources. The multi-tenant architecture implements resource isolation.

-  **Computing resources**

   Computing resources include CPUs and memory. One tenant cannot occupy the computing resources of another tenant.

-  **Storage resources**

   Storage resources include disks and third-party storage systems. One tenant cannot access the data of another tenant.

Computing Resources
-------------------

Computing resources are divided into static service resources and dynamic resources.

-  **Static Service Resources**

   Static service resources are computing resources allocated to each service and are not shared between services. The total computing resources of each service are fixed. These services include Flume, HBase, HDFS, and Yarn.

-  **Dynamic Resources**

   Dynamic resources are computing resources dynamically scheduled to a job queue by the distributed resource management service Yarn. Yarn dynamically schedules resources for the job queues of MapReduce, Spark2x, Flink, and Hive.

.. note::

   The resources allocated to Yarn in a big data cluster are static service resources but can be dynamically allocated to job queues by Yarn.

Storage Resources
-----------------

Storage resources are data storage resources that can be allocated by the distributed file storage service HDFS. Directory is the basic unit of allocating HDFS storage resources. Tenants can obtain storage resources from the specified directories in the HDFS file system.
