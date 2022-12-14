:original_name: mrs_01_1965.html

.. _mrs_01_1965:

Broaden Support for Hive Partition Pruning Predicate Pushdown
=============================================================

Scenario
--------

In earlier versions, the predicate for pruning Hive table partitions is pushed down. Only comparison expressions between column names and integers or character strings can be pushed down. In version 2.3, pushdown of the null, in, and, or expressions are supported.

Parameters
----------

Log in to FusionInsight Manager and choose **Cluster** > *Name of the desired cluster* > **Services** > **Spark2x**. On the page that is displayed, click the **Configurations** tab then the **All Configurations** sub-tab, and search for the following parameters:

+-----------------------------------------------------------+-----------------------------------------------------------------------------------------+---------------+--------------+
| Parameter                                                 | Description                                                                             | Default Value | Value Range  |
+===========================================================+=========================================================================================+===============+==============+
| spark.sql.hive.advancedPartitionPredicatePushdown.enabled | Specifies whether to broaden the support for Hive partition pruning predicate pushdown. | true          | [true,false] |
+-----------------------------------------------------------+-----------------------------------------------------------------------------------------+---------------+--------------+
