:original_name: mrs_08_0186.html

.. _mrs_08_0186:

Iceberg
=======

Principles
----------

Iceberg is an open table format for data lakes. You can quickly build your own data lake storage service on HDFS or OBS that stores data in Iceberg format.


.. figure:: /_static/images/en-us_image_0000002499008876.png
   :alt: **Figure 1** Architecture

   **Figure 1** Architecture

Iceberg Features
----------------

Iceberg has the following features:

-  Data organization based on storage formats
-  ACID and concurrency capabilities
-  Row-level modification
-  Schema evolution
-  Partition layout evolution
-  Hidden partitioning
-  Version rollback

Key Technologies and Advantages
-------------------------------

-  Key Technologies

   -  Strong transaction support to ensure data consistency

      The system implements ACID transactions and supports concurrent read, write, and delete operations, addressing the traditional data lake issue in which data cannot be read during writes or written during reads.

   -  Snapshot mechanism

      Each data change generates a new snapshot. With time travel, you can query any historical version of the data, making it easier to perform data backtracking, auditing, and fault recovery.

   -  Atomic partition evolution

      You can safely add, delete, or modify partition fields without rewriting the entire table, preventing data inconsistency.

-  High query performance

   -  Flexible partitioning and layout optimization to improve query performance

      -  Hidden partitioning: Partition fields are integrated into the table structure. You can filter them directly using SQL without knowing the partition path, which simplifies query logic.
      -  Partition evolution: Partition policies can be adjusted dynamically. For example, you can switch from daily to hourly partitions without requiring table rebuilding or data migration.
      -  Data layout optimization: Built-in bucketing and sorting optimize the physical storage layout of data files based on query patterns, reducing I/O overhead. Data files can be rewritten, small files merged, and large files split to prevent small-file storms.

   -  Open and compatible ecosystem, adaptable to multiple engines and platforms

      -  Support for multiple compute engines: Iceberg provides native compatibility with mainstream compute engines such as Spark, Flink, and HetuEngine. A single Iceberg table can be read and written concurrently by multiple engines, removing cross-engine barriers.
      -  Adaptable to multiple storage systems: Iceberg supports object storage and distributed file systems such as HDFS, OBS, and S3 without binding to any specific storage platform.
      -  Open standards and community: Iceberg, as an Apache top-level project, follows open table format specifications to avoid vendor lock-in. The community is highly active and consistently delivers new features and improvements.

   -  Fine-grained metadata management to simplify data governance

      -  Centralized metadata: Iceberg stores table metadata (such as schemas, partitions, snapshots, and file lists) as structured files, eliminating the need for external components like Hive Metastore. This design enables faster and more efficient metadata queries.
      -  Schema evolution: Iceberg supports flexible table structure changes, such as adding, deleting, renaming, or altering columns. These changes do not require full table scanning or rewriting and remain compatible with existing historical data.
      -  Data lifecycle management: Iceberg offers built-in features including expired snapshot cleanup and data file archiving. When used together with the snapshot mechanism, these features support automated data retention and cleanup policies.
