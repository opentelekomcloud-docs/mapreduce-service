:original_name: mrs_01_1759.html

.. _mrs_01_1759:

How Do I Prevent Key Directories from Data Loss Caused by Misoperations of the **insert overwrite** Statement?
==============================================================================================================

Question
--------

How do I prevent key directories from data loss caused by misoperations of the **insert overwrite** statement?

Answer
------

During monitoring of key Hive databases, tables, or directories, to prevent data loss caused by misoperations of the **insert overwrite** statement, configure **hive.local.dir.confblacklist** in Hive to protect directories.

This configuration item has been configured for directories such as **/opt/** and **/user/hive/warehouse** by default.

Prerequisites
-------------

The Hive and HDFS components are running properly.

Procedure
---------

#. Log in to FusionInsight Manager.
#. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Hive** > **Configurations** > **All Configurations**, and search for the **hive.local.dir.confblacklist** configuration item.

3. Add paths of databases, tables, or directories to be protected in the parameter value.
4. Click **Save** to save the settings.
