:original_name: mrs_08_0108.html

.. _mrs_08_0108:

ClickHouse
==========

Introduction to ClickHouse
--------------------------

ClickHouse is an open-source columnar database oriented to online analysis and processing. It is independent of the Hadoop big data system and features ultimate compression rate and fast query performance. In addition, ClickHouse supports SQL query and provides good query performance, especially the aggregation analysis and query performance based on large and wide tables. The query speed is one order of magnitude faster than that of other analytical databases.

The core functions of ClickHouse are as follows:

**Comprehensive DBMS functions**

ClickHouse has comprehensive database management functions, including the basic functions of a Database Management System (DBMS):

-  Data Definition Language (DDL): allows databases, tables, and views to be dynamically created, modified, or deleted without restarting services.
-  Data Manipulation Language (DML): allows data to be queried, inserted, modified, or deleted dynamically.
-  Permission control: supports user-based database or table operation permission settings to ensure data security.
-  Data backup and restoration: supports data backup, export, import, and restoration to meet the requirements of the production environment.
-  Distributed management: provides the cluster mode to automatically manage multiple database nodes.

**Column-based storage and data compression**

ClickHouse is a database that uses column-based storage. Data is organized by column. Data in the same column is stored together, and data in different columns is stored in different files.

During data query, columnar storage can reduce the data scanning range and data transmission size, thereby improving data query efficiency.

In a traditional row-based database system, data is stored in the sequence in :ref:`Table 1 <mrs_08_0108__table149821347311>`:

.. _mrs_08_0108__table149821347311:

.. table:: **Table 1** Row-based database

   === =========== ==== ===== ===== ===============
   row ID          Flag Name  Event Time
   === =========== ==== ===== ===== ===============
   0   12345678901 0    name1 1     2020/1/11 15:19
   1   32345678901 1    name2 1     2020/5/12 18:10
   2   42345678901 1    name3 1     2020/6/13 17:38
   N   ...         ...  ...   ...   ...
   === =========== ==== ===== ===== ===============

In a row-based database, data in the same row is physically stored together. In a column-based database system, data is stored in the sequence in :ref:`Table 2 <mrs_08_0108__table1835171820320>`:

.. _mrs_08_0108__table1835171820320:

.. table:: **Table 2** Columnar database

   ====== =============== =============== =============== ===
   row:   0               1               2               N
   ID:    12345678901     32345678901     42345678901     ...
   Flag:  0               1               1               ...
   Name:  name1           name2           name3           ...
   Event: 1               1               1               ...
   Time:  2020/1/11 15:19 2020/5/12 18:10 2020/6/13 17:38 ...
   ====== =============== =============== =============== ===

This example shows only the arrangement of data in a columnar database. Columnar databases store data in the same column together and data in different columns separately. Columnar databases are more suitable for online analytical processing (OLAP) scenarios.

**Vectorized executor**

ClickHouse uses CPU's Single Instruction Multiple Data (SIMD) to implement vectorized execution. SIMD is an implementation mode that uses a single instruction to operate multiple pieces of data and improves performance with data parallelism (other methods include instruction-level parallelism and thread-level parallelism). The principle of SIMD is to implement parallel data operations at the CPU register level.

**Relational model and SQL query**

ClickHouse uses SQL as the query language and provides standard SQL query APIs for existing third-party analysis visualization systems to easily integrate with ClickHouse.

In addition, ClickHouse uses a relational model. Therefore, the cost of migrating the system built on a traditional relational database or data warehouse to ClickHouse is lower.

**Data sharding and distributed query**

The ClickHouse cluster consists of one or more shards, and each shard corresponds to one ClickHouse service node. The maximum number of shards depends on the number of nodes (one shard corresponds to only one service node).

ClickHouse introduces the concepts of local table and distributed table. A local table is equivalent to a data shard. A distributed table itself does not store any data. It is an access proxy of the local table and functions as the sharding middleware. With the help of distributed tables, multiple data shards can be accessed by using the proxy, thereby implementing distributed query.

ClickHouse Applications
-----------------------

ClickHouse is short for Click Stream and Data Warehouse. It is initially applied to a web traffic analysis tool to perform OLAP analysis for data warehouses based on page click event flows. Currently, ClickHouse is widely used in Internet advertising, app and web traffic analysis, telecommunications, finance, and Internet of Things (IoT) fields. It is applicable to business intelligence application scenarios and has a large number of applications and practices worldwide. For details, visit https://clickhouse.tech/docs/en/introduction/adopters/.

ClickHouse Enhanced Open Source Features
----------------------------------------

MRS ClickHouse has advantages such as automatic cluster mode, HA deployment, and smooth and elastic scaling.

-  Automatic Cluster Mode

   As shown in :ref:`Figure 1 <mrs_08_0108__fig79238920553>`, a cluster consists of multiple ClickHouse nodes, which has no central node. It is more of a static resource pool. If the ClickHouse cluster mode is used for services, you need to pre-define the cluster information in the configuration file of each node. Only in this way, services can be correctly accessed.

   .. _mrs_08_0108__fig79238920553:

   .. figure:: /_static/images/en-us_image_0000001349110441.png
      :alt: **Figure 1** ClickHouse cluster

      **Figure 1** ClickHouse cluster

   Users are unaware of data partitions and replica storage in common database systems. However, ClickHouse allows you to proactively plan and define detailed configurations such as shards, partitions, and replica locations. The ClickHouse instance of MRS packs the work in a unified manner and adapts it to the automatic mode, implementing unified management, which is flexible and easy to use. A ClickHouse instance consists of three ZooKeeper nodes and multiple ClickHouse nodes. The Dedicated Replica mode is used to ensure high reliability of dual data copies.


   .. figure:: /_static/images/en-us_image_0000001349390609.png
      :alt: **Figure 2** ClickHouse cluster structure

      **Figure 2** ClickHouse cluster structure

-  Smooth and Elastic Scaling

   As business grows rapidly, MRS provides ClickHouse, a data migration tool, for scenarios such as the cluster's storage capacity or CPU compute resources approaching the limit. This tool is used to migrate some partitions of one or multiple MergeTree tables on several ClickHouseServer nodes to the same tables on other ClickHouseServer nodes. In this way, service availability is ensured and smooth capacity expansion is implemented.

   When you add ClickHouse nodes to a cluster, use this tool to migrate some data from the existing nodes to the new ones for data balancing after the expansion.

   |image1|

-  HA Deployment Architecture

   MRS uses the ELB-based high availability (HA) deployment architecture to automatically distribute user access traffic to multiple backend nodes, expanding service capabilities to external systems and improving fault tolerance. As shown in :ref:`Figure 3 <mrs_08_0108__fig15273873411>`, when a client application requests a cluster, Elastic Load Balance (ELB) is used to distribute traffic. With the ELB polling mechanism, data is written to local tables and read from distributed tables on different nodes. In this way, data read/write load and high availability of application access are guaranteed.

   After the ClickHouse cluster is provisioned, each ClickHouse instance node in the cluster corresponds to a replica, and two replicas form a logical shard. For example, when creating a ReplicatedMergeTree table, you can specify shards so that data can be automatically synchronized between two replicas in the same shard.

   .. _mrs_08_0108__fig15273873411:

   .. figure:: /_static/images/en-us_image_0000001296590598.png
      :alt: **Figure 3** HA deployment architecture

      **Figure 3** HA deployment architecture

.. |image1| image:: /_static/images/en-us_image_0000001296270774.png
