:original_name: en-us_topic_0000002686018465.html

.. _en-us_topic_0000002686018465:

Paimon
======

Apache Paimon is a data lake format that enables building a real-time lakehouse architecture with Flink and Spark for both streaming and batch workloads. Apache Paimon combines the data lake format with a Log-Structured Merge-tree (LSM) structure, bringing real-time streaming updates to lake architectures. Its advantages include low latency, strong consistency, and high scalability.

-  **Read/Write:** Paimon supports multiple data read/write modes and OLAP queries. For read operations, data can be read from historical snapshots (batch mode), the latest offset (streaming mode), or incremental snapshots (hybrid mode). For write operations, Paimon supports streaming synchronization from database change data capture (CDC) or batch insertion/overwriting from offline data.
-  **Ecosystem:** In addition to Apache Flink, Paimon supports other compute engines like Apache Hive, Apache Spark, and Trino for reading data.
-  **Internal:** At the storage layer, Paimon stores columnar files in file systems or object storage. File metadata is stored in manifest files, which provide large-scale storage and data skipping capabilities. For primary key tables, the LSM-tree structure supports large-scale data updates and high-performance queries.

Paimon Key Technologies
-----------------------

-  Efficient storage: Paimon supports cost-effective object and distributed storage (HDFS, or OBS), uses columnar file formats, and enables data skipping to improve query performance.
-  Comprehensive data lake management: Apache Paimon provides full data lake capabilities, including ACID transactions, schema evolution, version backtracking, tagging, and branching.
-  Efficient write and query: LSM-tree technology supports high-throughput writing and low-latency querying.
-  Multi-engine support: In addition to deep integration with Apache Flink, Apache Paimon supports compute engines like Spark, Hive, and HetuEngine, offering flexible data read and write capabilities.
