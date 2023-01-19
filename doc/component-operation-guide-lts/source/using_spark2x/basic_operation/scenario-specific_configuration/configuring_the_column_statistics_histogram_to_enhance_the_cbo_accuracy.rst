:original_name: mrs_01_1967.html

.. _mrs_01_1967:

Configuring the Column Statistics Histogram to Enhance the CBO Accuracy
=======================================================================

Scenarios
---------

The execution plan for SQL statements is optimized in Spark. Common optimization rules are heuristic optimization rules. Heuristic optimization rules are provided based on the characteristics of logical plans, and the data characteristics and the execution costs of operators are not considered. Spark 2.20 introduces the Cost-Based Optimization (CBO). CBO collects statistics on tables and columns and estimates the number of output records and size of each operator in bytes based on the input data sets of operators, which is the cost of executing an operator.

CBO will adjust the execution plan to minimize the end-to-end query time. The main points are as follows:

-  Filter out irrelevant data as soon as possible.
-  Minimize the cost of each operator.

The CBO optimization process is divided into two steps:

#. Collect statistics.
#. Estimate the output data sets of a specific operator based on the input data sets.

Table-level statistics includes: number of records and the total size of a table data file.

Column-level statistics includes: number of unique values, maximum value, minimum value, number of null values, average length, maximum length, and the histogram.

After the statistics is obtained, the execution cost of operators can be estimated. Common operators include filter and join operators.

Histogram is a type of column statistics. It can clearly describe the distribution of column data. The column data is distributed to a specified number of bins that are displayed in ascending order by size. The upper and lower limits of each bin are calculated. The amount of data in all bins is the same (a contour histogram). After the data is distributed, the cost estimation of each operator is more accurate and the optimization effect is better.

This feature can be enabled by using the following parameter.

**spark.sql.statistics.histogram.enabled**: specifies whether to enable the histogram function. The default value is **false**.

Parameter Configuration
-----------------------

Log in to FusionInsight Manager, choose **Cluster >** *Name of the desired cluster* **> Services** > **Spark2x** > **Configurations**, click **All Configurations**, and search for the following parameters.

+----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+--------------+
| Parameter                                    | Description                                                                                                                                                                                                                                                          | Default Value | Value Range  |
+==============================================+======================================================================================================================================================================================================================================================================+===============+==============+
| spark.sql.cbo.enabled                        | Enables CBO to estimate the statistics for the execution plan.                                                                                                                                                                                                       | false         | [true,false] |
+----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+--------------+
| spark.sql.cbo.joinReorder.enabled            | Enables CBO join for reordering.                                                                                                                                                                                                                                     | false         | [true,false] |
+----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+--------------+
| spark.sql.cbo.joinReorder.dp.threshold       | Specifies the maximum number of nodes that can be joined in the dynamic planning algorithm.                                                                                                                                                                          | 12            | >=1          |
+----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+--------------+
| spark.sql.cbo.joinReorder.card.weight        | Specifies the proportion of dimension (number of rows) in the comparison of planned cost during reconnection: Number of rows x Proportion of dimension + File size x (1 - Proportion of dimension)                                                                   | 0.7           | 0-1          |
+----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+--------------+
| spark.sql.statistics.size.autoUpdate.enabled | Enables the function of automatically updating the table size when the table data volume changes. Note: If there are a large number of data files in a table, this operation is time consume, and the data processing speed is reduced.                              | false         | [true,false] |
+----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+--------------+
| spark.sql.statistics.histogram.enabled       | After this function is enabled, a histogram is generated when column statistics is collected. Histogram can improve the estimation accuracy, but collecting histogram information requires additional workload.                                                      | false         | [true,false] |
+----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+--------------+
| spark.sql.statistics.histogram.numBins       | Specifies the number of bins for the generated histogram.                                                                                                                                                                                                            | 254           | >=2          |
+----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+--------------+
| spark.sql.statistics.ndv.maxError            | Specifies the maximum estimation deviation allowed by the HyperLogLog++ algorithm when the column level statistics is generated.                                                                                                                                     | 0.05          | 0-1          |
+----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+--------------+
| spark.sql.statistics.percentile.accuracy     | Specifies the accuracy rate of the percentile estimation when the contour histogram is generated. The larger the value is, the more accurate the estimation is. The estimation error value can be obtained through (1.0/Accuracy rate of the percentile estimation). | 10000         | >=1          |
+----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+--------------+

.. note::

   -  If you want the histogram to take effect in CBO, the following conditions must be met:

      -  Set **spark.sql.statistics.histogram.enabled** to **true**. The default value is **false**. Change the value to **true** to enable the histogram function.
      -  Set **spark.sql.cbo.enabled** to **true**. The default value is **false**. Change the value to **true** to enable CBO.
      -  Set **spark.sql.cbo.joinReorder.enabled** to **true**. The default value is **false**. Change the value to **true** to enable connection reordering.

   -  If a client is used to submit a task, you need to download the client again after configuring the following parameters: **spark.sql.cbo.enabled**, **spark.sql.cbo.joinReorder.enabled**, **spark.sql.cbo.joinReorder.dp.threshold**, **spark.sql.cbo.joinReorder.card.weight**, **spark.sql.statistics.size.autoUpdate.enabled**, **spark.sql.statistics.histogram.enabled**, **spark.sql.statistics.histogram.numBins**, **spark.sql.statistics.ndv.maxError**, and **spark.sql.statistics.percentile.accuracy**.
