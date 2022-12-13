:original_name: mrs_08_0083.html

.. _mrs_08_0083:

Hudi
====

Hudi is the file organization layer of the data lake. It manages Parquet files, provides the data lake capability, and supports multiple compute engines. It also provides insert, update, and deletion (IUD) interfaces and streaming primitives for inserting, updating, and incremental pulling on HDFS datasets.

.. note::

   To use Hudi, ensure that the Spark2x service has been installed in the MRS cluster.


.. figure:: /_static/images/en-us_image_0000001349190321.png
   :alt: **Figure 1** Basic architecture of Hudi

   **Figure 1** Basic architecture of Hudi

Feature
-------

-  The ACID transaction capability supports real-time data import to the lake and batch data import to the data lake.
-  Multiple view capabilities (read-optimized view/incremental view/real-time view) enable quick data analysis.
-  Multi-version concurrency control (MVCC) design supports data version backtracking.
-  Automatic management of file sizes and layouts optimizes query performance and provides quasi-real-time data for queries.
-  Concurrent read and write are supported. Data can be read when being written based on snapshot isolation.
-  Bootstrapping is supported to convert existing tables into Hudi datasets.

Key Technologies and Advantages
-------------------------------

-  Pluggable index mechanism: Hudi provides multiple index mechanisms to quickly update and delete massive data.
-  Ecosystem support: Hudi supports multiple data engines, including Hive, Spark, HetuEngine, and Flink.

Two Types of Tables Supported by Hudi
-------------------------------------

-  Copy On Write

   Copy-on-write tables are also called COW tables. Parquet files are used to store data, and internal update operations need to be performed by rewriting the original Parquet files.

   -  Advantage: It is efficient because only one data file in the corresponding partition needs to be read.
   -  Disadvantage: During data write, a previous copy needs to be copied and then a new data file is generated based on the previous copy. This process is time-consuming. Therefore, the data read by the read request lags behind.

-  Merge On Read

   Merge-on-read tables are also called MOR tables. The combination of columnar-based Parquet and row-based format Avro is used to store data. Parquet files are used to store base data, and Avro files (also called log files) are used to store incremental data.

   -  Advantage: Data is written to the delta log first, and the delta log size is small. Therefore, the write cost is low.
   -  Disadvantage: Files need to be compacted periodically. Otherwise, there are a large number of fragment files. The read performance is poor because delta logs and old data files need to be merged.

Hudi Supporting Three Types Of Views for Read Capabilities in Different Scenarios
---------------------------------------------------------------------------------

-  Snapshot View

   Provides the latest snapshot data of the current Hudi table. That is, once the latest data is written to the Hudi table, the newly written data can be queried through this view.

   Both COW and MOR tables support this view capability.

-  Incremental View

   Provides the incremental query capability. The incremental data after a specified commit can be queried. This view can be used to quickly pull incremental data.

   COW tables support this view capability. MOR tables also support this view capability, but the incremental view capability disappears once the compact operation is performed.

-  Read Optimized View

   Provides only the data stored in the latest Parquet file.

   This view is different for COW and MOR tables.

   For COW tables, the view capability is the same as the real-time view capability. (COW tables use only Parquet files to store data.)

   For MOR tables, only base files are accessed, and the data in the given file slices since the last compact operation is provided. It can be simply understood that this view provides only the data stored in Parquet files of MOR tables, and the data in log files is ignored. The data provided by this view may not be the latest. However, once the compact operation is performed on MOR tables, the incremental log data is merged into the base data. In this case, this view has the same capability as the real-time view.
