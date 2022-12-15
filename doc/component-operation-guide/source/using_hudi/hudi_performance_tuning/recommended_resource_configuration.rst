:original_name: mrs_01_24102.html

.. _mrs_01_24102:

Recommended Resource Configuration
==================================

-  For MOR tables:

   The essence of MOR tables is to write incremental files, so the tuning is based on the data size (dataSize) of Hudi.

   If dataSize is only several GBs, you are advised to run Spark in single-node mode or run Spark in Yarn mode with only one container allocated.

   Parallelism (**p**) of programs for importing data to the lake: **p** = dataSize/128 MB. The number of cores allocated to programs must be the same as the value of **p**. It is recommended that the ratio of the memory size to the number of cores be greater than 1.5:1. That is, a core is configured with 1.5 GB memory. For off-heap memory, it is recommended that the ratio of the memory size to the number of cores be greater than 0.5:1.

-  For COW tables:

   The principle of COW tables is to rewrite the original data. Therefore, dataSize and the number of rewritten files must be considered during tuning. Generally, more cores lead to better performance. The number of cores is directly related to the number of rewritten files. The settings of parallelism (**p**) and memory size are similar to those of MOR tables.
