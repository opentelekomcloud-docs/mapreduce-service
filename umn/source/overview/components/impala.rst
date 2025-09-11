:original_name: mrs_08_0038.html

.. _mrs_08_0038:

Impala
======


Impala
------

Impala provides fast, interactive SQL queries directly on your Apache Hadoop data stored in HDFS, HBase, or the Object Storage Service (OBS). In addition to using the same unified storage platform, Impala also uses the same metadata, SQL syntax (Hive SQL), ODBC driver, and user interface (Impala query UI in Hue) as Apache Hive. This provides a familiar and unified platform for real-time or batch-oriented queries. Impala is an addition to tools available for querying big data. Impala does not replace the batch processing frameworks built on MapReduce such as Hive. Hive and other frameworks built on MapReduce are best suited for long running batch jobs.

Impala provides the following features:

-  Most common SQL-92 features of Hive Query Language (HiveQL) including SELECT, JOIN, and aggregate functions
-  HDFS, HBase, and OBS storage, including:

   -  HDFS file formats: delimited text files, Parquet, Avro, SequenceFile, and RCFile
   -  Compression codecs: Snappy, GZIP, Deflate, BZIP

-  Common data access interfaces including:

   -  JDBC driver
   -  ODBC driver
   -  Hue Beeswax and the Impala query UI

-  **impala-shell** command line interface
-  Kerberos authentication

Impala applies to offline analysis (such as log and cluster status analysis) of real-time data queries, large-scale data mining (such as user behavior analysis, interest region analysis, and region display), and other scenarios.

Impala consists of three roles: Impala Daemon (Impalad), Impala StateStore, and Impala Catalog Service.

Impala Daemon
-------------

The core Impala component is the Impala daemon, physically represented by the **impalad** process.

A few of the key functions that an Impala daemon performs are:

-  Runs on all data nodes.
-  Reads and writes to data files.
-  Accepts queries transmitted from the **impala-shell** command, Hue, JDBC, or ODBC.
-  Parallelizes the queries and transmits intermediate query results back to the central coordinator.
-  Invokes a node to return the query results to the client.

The Impala daemons are in constant communication with StateStore, to confirm which daemons are healthy and can accept new work.

Impala StateStore
-----------------

The Impala component known as the StateStore checks on the health of all Impala daemons in a cluster, and continuously relays its findings to each of those daemons. It is physically represented by a daemon process named **statestored**. You only need such a process on one host in a cluster. If an Impala daemon goes offline due to hardware failure, network error, software issue, or other reason, the StateStore informs all the other Impala daemons so that future queries can avoid making requests to the unreachable Impala daemon.

Impala Catalog Service
----------------------

The Impala component known as the Catalog Service relays the metadata changes from Impala SQL statements to all the Impala daemons in a cluster. It is physically represented by a daemon process named **catalogd**. When you create a table, load data, and so on through Hive, you do need to issue REFRESH or INVALIDATE METADATA on an Impala daemon before executing a query there. The catalog service avoids the need to issue REFRESH and INVALIDATE METADATA statements when the metadata changes are performed by statements issued through Impala.
