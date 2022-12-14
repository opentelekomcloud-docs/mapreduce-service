:original_name: mrs_01_1787.html

.. _mrs_01_1787:

Differences Among Connectors Used During the Process of Importing Data from the Oracle Database to HDFS
=======================================================================================================

Question
--------

Three types of connectors are available for importing data from the Oracle database to HDFS using Loader. That is, generic-jdbc-connector, oracle-connector, and oracle-partition-connector. Which one should I select? What are the differences between them?

Answers
-------

-  generic-jdbc-connector

   Reads data from the Oracle database in JDBC mode. It is applicable to databases that support JDBC.

   In this mode, data loading performance of Loader is subject to data distribution in a partition column. When data skew occurs (data has only one value or several values) in a partition column, a few Maps process a significant portion of data. As a result, the index becomes invalid, causing a sharp decline in SQL query performance.

   **generic-jdbc-connector** supports view import and export, but oracle-partition-connector and oracle-connector do not support. Therefore, only this connector can be used to import views.

-  Both **oracle-partition-connector** and **oracle-connector**

   can use the ROWID of Oracle for partitioning. oracle-partition-connector is self-developed and oracle-connector is an open-source edition. The two types of connectors share similar performance.

   **oracle-connector** requires more system table permissions. The following lists the read permissions required by the system tables of **oracle-connector** and **oracle-connector**.

   -  **oracle-connector**: dba_tab_partitions, dba_constraints, dba_tables t, dba_segments, v$version, dba_objects, v$instance, SYS_CONTEXT function, dba_extents, and dba_tab_subpartitions
   -  **oracle-partition-connector**: DBA_OBJECTS and DBA_EXTENTS

   Compared with **generic-jdbc-connector**, **oracle-partition-connector** and **oracle-connector** have the following advantages:

   #. Load balancing: Number and scope of data segments are determined by the storage structure (data blocks) of the source table rather than the data on the source table. In terms of granularity, a data block can occupy a partition.
   #. Stable performance: Invalid index faults caused by data skew and bound variable snooping can be completely eliminated.
   #. Fast query speed: Using data segmentation delivers a higher query speed than that of using index.
   #. Excellent horizontal scalability: The number of generated segments increases with the increase of data volume. In this case, ideal performance can be delivered when you increase the number of concurrent tasks. Contrarily, decreasing concurrent tasks saves resources.
   #. Simplified data segmentation logic: Problems like precision loss, type compatibility, and bound variables can be prevented.
   #. Enhanced usability: Users do not need to create partition columns and tables for Loader.
