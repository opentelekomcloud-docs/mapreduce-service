:original_name: mrs_01_24745.html

.. _mrs_01_24745:

Configuring the Drop Partition Command to Support Batch Deletion
================================================================

.. note::

   This section applies only to MRS 3.2.0 or later.

Scenario
--------

Currently, the **Drop Partition** command in Spark supports partition deletion using only the equal sign (=). This configuration allows multiple filter criteria to be used to delete partitions in batches, for example, **<**, **<=**, **>**, **>=**, **!>**, and **!<**.

Configuration
-------------

Log in to FusionInsight Manager and choose **Cluster**. Click the name of the desired cluster and choose **Services** > **Spark2x**. On the page that is displayed, click the **Configurations** tab then **All Configurations**, and search for the following parameters.

+-----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
| Parameter                               | Description                                                                                                                                                    | Default Value |
+=========================================+================================================================================================================================================================+===============+
| spark.sql.dropPartitionsInBatch.enabled | If this parameter is set to **true**, the **Drop Partition** command supports the following filter criteria: **<**, **<=**, **>**, **>=**, **!>**, and **!<**. | true          |
+-----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
| spark.sql.dropPartitionsInBatch.limit   | Indicates the maximum number of partitions that can be batch dropped.                                                                                          | 1000          |
+-----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
