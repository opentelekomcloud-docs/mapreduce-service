:original_name: mrs_08_00071.html

.. _mrs_08_00071:

HDFS Basic Principles
=====================

Hadoop Distributed File System (HDFS) implements reliable and distributed read/write of massive amounts of data. HDFS is applicable to the scenario where data read/write features "write once and read multiple times". However, the write operation is performed in sequence, that is, it is a write operation performed during file creation or an adding operation performed behind the existing file. HDFS ensures that only one caller can perform write operation on a file but multiple callers can perform read operation on the file at the same time.

Architecture
------------

HDFS consists of active and standby NameNodes and multiple DataNodes, as shown in :ref:`Figure 1 <mrs_08_00071__fig1245232216814>`.

HDFS works in master/slave architecture. NameNodes run on the master (active) node, and DataNodes run on the slave (standby) node. ZKFC should run along with the NameNodes.

The communication between NameNodes and DataNodes is based on Transmission Control Protocol (TCP)/Internet Protocol (IP). The NameNode, DataNode, ZKFC, and JournalNode can be deployed on Linux servers.

.. _mrs_08_00071__fig1245232216814:

.. figure:: /_static/images/en-us_image_0000001349110533.png
   :alt: **Figure 1** HA HDFS architecture

   **Figure 1** HA HDFS architecture

:ref:`Table 1 <mrs_08_00071__table144529223812>` describes the functions of each module shown in :ref:`Figure 1 <mrs_08_00071__fig1245232216814>`.

.. _mrs_08_00071__table144529223812:

.. table:: **Table 1** Module description

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Module                            | Description                                                                                                                                                                                                                                                                            |
   +===================================+========================================================================================================================================================================================================================================================================================+
   | NameNode                          | A NameNode is used to manage the namespace, directory structure, and metadata information of a file system and provide the backup mechanism. The NameNode is classified into the following two types:                                                                                  |
   |                                   |                                                                                                                                                                                                                                                                                        |
   |                                   | -  Active NameNode: manages the namespace, maintains the directory structure and metadata of file systems, and records the mapping relationships between data blocks and files to which the data blocks belong.                                                                        |
   |                                   | -  Standby NameNode: synchronizes with the data in the active NameNode, and takes over services from the active NameNode when the active NameNode is faulty.                                                                                                                           |
   |                                   | -  Observer NameNode: synchronizes with the data in the active NameNode, and processes read requests from the client.                                                                                                                                                                  |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DataNode                          | A DataNode is used to store data blocks of each file and periodically report the storage status to the NameNode.                                                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | JournalNode                       | In HA cluster, synchronizes metadata between the active and standby NameNodes.                                                                                                                                                                                                         |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ZKFC                              | ZKFC must be deployed for each NameNode. It monitors NameNode status and writes status information to ZooKeeper. ZKFC also has permissions to select the active NameNode.                                                                                                              |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ZK Cluster                        | ZooKeeper is a coordination service which helps the ZKFC to elect the active NameNode.                                                                                                                                                                                                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | HttpFS gateway                    | HttpFS is a single stateless gateway process which provides the WebHDFS REST API for external processes and FileSystem API for the HDFS. HttpFS is used for data transmission between different versions of Hadoop. It is also used as a gateway to access the HDFS behind a firewall. |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  **HDFS HA Architecture**

   HA is used to resolve the SPOF problem of NameNode. This feature provides a standby NameNode for the active NameNode. When the active NameNode is faulty, the standby NameNode can quickly take over to continuously provide services for external systems.

   In a typical HDFS HA scenario, there are usually two NameNodes. One is in the active state, and the other in the standby state.

   A shared storage system is required to support metadata synchronization of the active and standby NameNodes. This version provides Quorum Journal Manager (QJM) HA solution, as shown in :ref:`Figure 2 <mrs_08_00071__fig1517714182104>`. A group of JournalNodes are used to synchronize metadata between the active and standby NameNodes.

   Generally, an odd number (2N+1) of JournalNodes are configured, and at least three JournalNodes are required. For one metadata update message, data writing is considered successful as long as data writing is successful on N+1 JournalNodes. In this case, data writing failure of a maximum of N JournalNodes is allowed. For example, when there are three JournalNodes, data writing failure of one JournalNode is allowed; when there are five JournalNodes, data writing failure of two JournalNodes is allowed.

   JournalNode is a lightweight daemon process and shares a host with other services of Hadoop. It is recommended that the JournalNode be deployed on the control node to prevent data writing failure on the JournalNode during massive data transmission.

   .. _mrs_08_00071__fig1517714182104:

   .. figure:: /_static/images/en-us_image_0000001296590686.png
      :alt: **Figure 2** QJM-based HDFS architecture

      **Figure 2** QJM-based HDFS architecture

Principle
---------

MRS uses the HDFS copy mechanism to ensure data reliability. One backup file is automatically generated for each file saved in HDFS, that is, two copies are generated in total. The number of HDFS copies can be queried using the **dfs.replication** parameter.

-  When the Core node specification of the MRS cluster is set to non-local hard disk drive (HDD) and the cluster has only one Core node, the default number of HDFS copies is 1. If the number of Core nodes in the cluster is greater than or equal to 2, the default number of HDFS copies is 2.
-  When the Core node specification of the MRS cluster is set to local disk and the cluster has only one Core node, the default number of HDFS copies is 1. If there are two Core nodes in the cluster, the default number of HDFS copies is 2. If the number of Core nodes in the cluster is greater than or equal to 3, the default number of HDFS copies is 3.


.. figure:: /_static/images/en-us_image_0000001296430834.png
   :alt: **Figure 3** HDFS architecture

   **Figure 3** HDFS architecture

The HDFS component of MRS supports the following features:

-  Supports erasure code, reducing data redundancy to 50% and improving reliability. In addition, the striped block storage structure is introduced to maximize the use of the capability of a single node and multiple disks in an existing cluster. After the coding process is introduced, the data write performance is improved, and the performance is close to that with the multi-copy redundancy.
-  Supports balanced node scheduling on HDFS and balanced disk scheduling on a single node, improving HDFS storage performance after node or disk scale-out.

For details about the Hadoop architecture and principles, see `https://hadoop.apache.org/ <http://hadoop.apache.org/>`__.
