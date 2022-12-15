:original_name: mrs_08_0026.html

.. _mrs_08_0026:

Related Services
================

Relationships with Other Services
---------------------------------

.. table:: **Table 1** Relationships with other services

   +--------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | Service                              | Relationships                                                                                                                             |
   +======================================+===========================================================================================================================================+
   | Virtual Private Cloud (VPC)          | MRS clusters are created in the subnets of a VPC. VPCs provide a secure, isolated, and logical network environment for your MRS clusters. |
   +--------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | Object Storage Service (OBS)         | OBS stores the following user data:                                                                                                       |
   |                                      |                                                                                                                                           |
   |                                      | -  MRS job input data, such as user programs and data files                                                                               |
   |                                      | -  MRS job output data, such as result files and log files of jobs                                                                        |
   |                                      |                                                                                                                                           |
   |                                      | In MRS clusters, HDFS, Hive, MapReduce, YARN, Spark, Flume, and Loader can import or export data from OBS.                                |
   |                                      |                                                                                                                                           |
   |                                      | MRS uses the parallel file system of OBS to provide services.                                                                             |
   +--------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | Elastic Cloud Server (ECS)           | MRS uses elastic cloud servers (ECSs) as cluster nodes.                                                                                   |
   +--------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | Relational Database Service (RDS)    | RDS stores MRS system running data, including MRS cluster metadata.                                                                       |
   +--------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | Identity and Access Management (IAM) | IAM provides authentication for MRS.                                                                                                      |
   +--------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | Simple Message Notification (SMN)    | MRS uses SMN to provide one-to-multiple message subscription and notification over a variety of protocols.                                |
   +--------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | Cloud Trace Service (CTS)            | CTS provides you with operation records of MRS resource operation requests and request results for querying, auditing, and backtracking.  |
   +--------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 2** MRS operations recorded by CTS

   =================== ============= ===============
   Operation           Resource Type Trace Name
   =================== ============= ===============
   Creating a cluster  cluster_mrs   createCluster
   Deleting a cluster  cluster_mrs   deleteCluster
   Expanding a cluster cluster_mrs   scaleOutCluster
   Shrinking a cluster cluster_mrs   scaleInCluster
   =================== ============= ===============

After you enable CTS, the system starts recording operations on cloud resources. You can view operation records of the last 7 days on the CTS management console. For details, see **Cloud Trace Service** > **Getting Started** > **Querying Real-Time Traces**.
