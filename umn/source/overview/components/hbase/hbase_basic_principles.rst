:original_name: mrs_08_00101.html

.. _mrs_08_00101:

HBase Basic Principles
======================

HBase undertakes data storage. HBase is an open source, column-oriented, distributed storage system that is suitable for storing massive amounts of unstructured or semi-structured data. It features high reliability, high performance, and flexible scalability, and supports real-time data read/write. For more information about HBase, see https://hbase.apache.org/.

Typical features of a table stored in HBase are as follows:

-  Big table (BigTable): One table contains hundred millions of lines and millions of columns.
-  Column-oriented: Column-oriented storage, retrieval, and permission control
-  Sparse: Null columns in the table do not occupy any storage space.

The HBase component of MRS separates computing from storage. Data can be stored in cloud storage services at low cost, for example, Object Storage Service (OBS), and can be backed up across AZs. MRS supports secondary indexes for HBase and allows adding indexes for column values to filter data by column through native HBase APIs.

HBase architecture
------------------

An HBase cluster consists of active and standby HMaster processes and multiple RegionServer processes, as shown in :ref:`Figure 1 <mrs_08_00101__fb06af549b46f4156a4efed4bde54463e>`.

.. _mrs_08_00101__fb06af549b46f4156a4efed4bde54463e:

.. figure:: /_static/images/en-us_image_0000001296590642.png
   :alt: **Figure 1** HBase architecture

   **Figure 1** HBase architecture

.. table:: **Table 1** Module description

   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Module                            | Description                                                                                                                                                                                                                                                                                           |
   +===================================+=======================================================================================================================================================================================================================================================================================================+
   | Master                            | Master is also called HMaster. In HA mode, HMaster consists of an active HMaster and a standby HMaster.                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                                                                                       |
   |                                   | -  Active Master: manages RegionServer in HBase, including the creation, deletion, modification, and query of a table, balances the load of RegionServer, adjusts the distribution of Region, splits Region and distributes Region after it is split, and migrates Region after RegionServer expires. |
   |                                   | -  Standby Master: takes over services when the active HMaster is faulty. The original active HMaster demotes to the standby HMaster after the fault is rectified.                                                                                                                                    |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Client                            | Client communicates with Master for management and with RegionServer for data protection by using the Remote Procedure Call (RPC) mechanism of HBase.                                                                                                                                                 |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RegionServer                      | RegionServer provides read and write services of table data as a data processing and computing unit in HBase.                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                                                                       |
   |                                   | RegionServer is deployed with DataNodes of HDFS clusters to store data.                                                                                                                                                                                                                               |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ZooKeeper cluster                 | ZooKeeper provides distributed coordination services for processes in HBase clusters. Each RegionServer is registered with ZooKeeper so that the active Master can obtain the health status of each RegionServer.                                                                                     |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | HDFS cluster                      | HDFS provides highly reliable file storage services for HBase. All HBase data is stored in the HDFS.                                                                                                                                                                                                  |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

HBase Principles
----------------

-  **HBase Data Model**

   HBase stores data in tables, as shown in :ref:`Figure 2 <mrs_08_00101__fig29501314327>`. Data in a table is divided into multiple Regions, which are allocated by Master to RegionServers for management.

   Each Region contains data within a RowKey range. An HBase data table contains only one Region at first. As the number of data increases and reaches the upper limit of the Region capacity, the Region is split into two Regions. You can define the RowKey range of a Region when creating a table or define the Region size in the configuration file.

   .. _mrs_08_00101__fig29501314327:

   .. figure:: /_static/images/en-us_image_0000001440610749.png
      :alt: **Figure 2** HBase data model

      **Figure 2** HBase data model

   .. table:: **Table 2** Concepts

      +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Module        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
      +===============+============================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
      | RowKey        | Similar to the primary key in a relationship table, which is the unique ID of the data in each row. A RowKey can be a string, integer, or binary string. All records are stored after being sorted by RowKey.                                                                                                                                                                                                                                                                                                                                                                                                              |
      +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Timestamp     | The timestamp of a data operation. Data can be specified with different versions by time stamp. Data of different versions in each cell is stored by time in descending order.                                                                                                                                                                                                                                                                                                                                                                                                                                             |
      +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Cell          | Minimum storage unit of HBase, consisting of keys and values. A key consists of six fields, namely row, column family, column qualifier, timestamp, type, and MVCC version. Values are the binary data objects.                                                                                                                                                                                                                                                                                                                                                                                                            |
      +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Column Family | One or multiple horizontal column families form a table. A column family can consist of multiple random columns. A column is a label under a column family, which can be added as required when data is written. The column family supports dynamic expansion so the number and type of columns do not need to be predefined. Columns of a table in HBase are sparsely distributed. The number and type of columns in different rows can be different. Each column family has the independent time to live (TTL). You can lock the row only. Operations on the row in a column family are the same as those on other rows. |
      +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Column        | Similar to traditional databases, HBase tables also use columns to store data of the same type.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
      +---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  **RegionServer Data Storage**

   RegionServer manages the regions allocated by HMaster. :ref:`Figure 3 <mrs_08_00101__fd8c05b438f4e419a845ac4086068129e>` shows the data storage structure of RegionServer.

   .. _mrs_08_00101__fd8c05b438f4e419a845ac4086068129e:

   .. figure:: /_static/images/en-us_image_0000001349190357.png
      :alt: **Figure 3** RegionServer data storage structure

      **Figure 3** RegionServer data storage structure

   :ref:`Table 3 <mrs_08_00101__td05a58b8249240a58b063a9ccb1f780c>` lists each component of Region described in :ref:`Figure 3 <mrs_08_00101__fd8c05b438f4e419a845ac4086068129e>`.

   .. _mrs_08_00101__td05a58b8249240a58b063a9ccb1f780c:

   .. table:: **Table 3** Region structure description

      +-----------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Module    | Description                                                                                                                                                                                                                                                     |
      +===========+=================================================================================================================================================================================================================================================================+
      | Store     | A Region consists of one or multiple Stores. Each Store maps a column family in :ref:`Figure 2 <mrs_08_00101__fig29501314327>`.                                                                                                                                 |
      +-----------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | MemStore  | A Store contains one MemStore. The MemStore caches data inserted to a Region by the client. When the MemStore capacity reaches the upper limit, RegionServer flushes data in MemStore to the HDFS.                                                              |
      +-----------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | StoreFile | The data flushed to the HDFS is stored as a StoreFile in the HDFS. As more data is inserted, multiple StoreFiles are generated in a Store. When the number of StoreFiles reaches the upper limit, RegionServer merges multiple StoreFiles into a big StoreFile. |
      +-----------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | HFile     | HFile defines the storage format of StoreFiles in a file system. HFile is the underlying implementation of StoreFile.                                                                                                                                           |
      +-----------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | HLog      | HLogs prevent data loss when RegionServer is faulty. Multiple Regions in a RegionServer share the same HLog.                                                                                                                                                    |
      +-----------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  **Metadata Table**

   The metadata table is a special HBase table, which is used by the client to locate a region. Metadata table includes **hbase:meta** table to record region information of user tables, such as the region location and start and end RowKey.

   :ref:`Figure 4 <mrs_08_00101__f1dd74070230f4fd99e391a49363263c2>` shows the mapping relationship between metadata tables and user tables.

   .. _mrs_08_00101__f1dd74070230f4fd99e391a49363263c2:

   .. figure:: /_static/images/en-us_image_0000001349309941.png
      :alt: **Figure 4** Mapping relationships between metadata tables and user tables

      **Figure 4** Mapping relationships between metadata tables and user tables

-  **Data Operation Process**

   :ref:`Figure 5 <mrs_08_00101__fa04dc85032574524af4fa8ab21b5642b>` shows the HBase data operation process.

   .. _mrs_08_00101__fa04dc85032574524af4fa8ab21b5642b:

   .. figure:: /_static/images/en-us_image_0000001296430786.png
      :alt: **Figure 5** Data processing

      **Figure 5** Data processing

   #. When you add, delete, modify, and query HBase data, the HBase client first connects to ZooKeeper to obtain information about the RegionServer where the **hbase:meta** table is located. If you modify the namespace, such as creating and deleting a table, you need to access HMaster to update the meta information.
   #. The HBase client connects to the RegionServer where the region of the **hbase:meta** table is located and obtains the RegionServer location where the region of the user table resides.
   #. Then the HBase client connects to the RegionServer where the region of the user table is located and issues a data operation command to the RegionServer. The RegionServer executes the command.

   To improve data processing efficiency, the HBase client caches region information of the **hbase:meta** table and user table. When an application initiates a second data operation, the HBase client queries the region information from the memory. If no match is found in the memory, the HBase client performs the preceding operations to obtain region information.
