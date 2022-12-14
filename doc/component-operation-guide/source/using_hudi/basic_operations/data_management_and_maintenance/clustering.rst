:original_name: mrs_01_24088.html

.. _mrs_01_24088:

Clustering
==========

Introduction
------------

Clustering reorganizes data layout to improve query performance without affecting the ingestion speed.

Architecture
------------

Hudi provides different operations, such as **insert**, **upsert**, and **bulk_insert**, through its write client API to write data to a Hudi table. To weight between file size and speed of importing data into the data lake, Hudi provides **hoodie.parquet.small.file.limit** to configure the minimum file size. You can set it to **0** to force new data to be written to new file groups, or to a higher value to ensure that new data is "padded" to existing small file groups until it reaches the specified size, but this increases ingestion latency.

To support fast ingestion without affecting query performance, the clustering service is introduced to rewrite data to optimize the layout of Hudi data lake files.

The clustering service can run asynchronously or synchronously. It adds a new operation type called **REPLACE**, which will mark the clustering operation in the Hudi metadata timeline.

Clustering service is based on the MVCC design of Hudi to allow new data to be inserted. Clustering operations run in the background to reformat data layout, ensuring snapshot isolation between concurrent readers and writers.

|image1|

Clustering is divided into two parts:

-  Scheduling clustering: Create a clustering plan using a pluggable clustering strategy.

   #. Identify files that are eligible for clustering: Depending on the selected clustering strategy, the scheduling logic will identify the files eligible for clustering.
   #. Group files that are eligible for clustering based on specific criteria. The data size of each group must be a multiple of **targetFileSize**. Grouping is a part of the strategy defined in the plan. Additionally, there is an option to control group size to improve parallelism and avoid shuffling large volumes of data.
   #. Save the clustering plan to the timeline in Avro metadata format.

-  Execute clustering: Process the plan using an execution strategy to create new files and replace old files.

   #. Read the clustering plan and get **clusteringGroups** that marks the file groups to be clustered.
   #. Instantiate appropriate strategy class for each group using **strategyParams** (for example, **sortColumns**) and apply the strategy to rewrite data.
   #. Create a **REPLACE** commit and update the metadata in HoodieReplaceCommitMetadata.

How to Execute Clustering
-------------------------

#. Executing clustering synchronously

   Add the following configuration parameters when the data write operation is performed:

   **option("hoodie.clustering.inline", "true").**

   **option("hoodie.clustering.inline.max.commits", "4").**

   **option("hoodie.clustering.plan.strategy.target.file.max.bytes", "1073741824").**

   **option("hoodie.clustering.plan.strategy.small.file.limit", "629145600").**

   **option("hoodie.clustering.plan.strategy.sort.columns", "column1,column2").**

#. Executing clustering asynchronously

   **spark-submit --master yarn --class org.apache.hudi.utilities.HoodieClusteringJob /opt/client/Hudi/hudi/lib/hudi-utilities*.jar --schedule --base-path <table_path> --table-name <table_name> --props /tmp/clusteringjob.properties --spark-memory 1g**

   **spark-submit --master yarn --driver-memory 16G --executor-memory 12G --executor-cores 4 --num-executors 4 --class org.apache.hudi.utilities.HoodieClusteringJob /opt/client/Hudi/hudi/lib/hudi-utilities*.jar --base-path <table_path> --instant-time 20210605112954 --table-name <table_name> --props /tmp/clusteringjob.properties --spark-memory 12g**

   .. note::

      **clusteringjob.properties** contains custom clustering configurations.

      Example:

      hoodie.clustering.plan.strategy.target.file.max.bytes=1073741824

      hoodie.clustering.inline.max.commits=4

For details, see :ref:`Configuration Reference <mrs_01_24032>`.

.. caution::

   #. By default, only the two partitions with the largest size are clustered. The clustering of other partitions depends on the custom strategy.
   #. The sorting column of clustering cannot be null. This is restricted by Spark RDD.
   #. If the value of **target.file.max.bytes** is large, increase the value of **--spark-memory** to execute clustering. Otherwise, the executor memory overflow occurs.
   #. Currently, the clean mechanism cannot be used to delete junk files generated after the clustering fails.
   #. After the clustering, sizes of new files may be different, causing data skew.
   #. Clustering and upsert operations cannot be performed at the same time.

.. |image1| image:: /_static/images/en-us_image_0000001296090428.png
