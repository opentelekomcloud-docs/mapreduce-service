:original_name: mrs_01_2091.html

.. _mrs_01_2091:

Why Does a MapReduce Job Fail to Run When a Non-ViewFS File System Is Configured as ViewFS?
===========================================================================================

Question
--------

Why does a MapReduce job fail to run when a non-ViewFS file system is configured as ViewFS?

Answer
------

When a non-ViewFS file system is configured as a ViewFS using cluster, the user permissions on folders in the ViewFS file system are different from those of non-ViewFS folders in the default NameService. The submitted MapReduce job fails to be executed because the directory permissions are inconsistent.

When configuring the ViewFS user in the cluster, you need to check and verify the directory permissions. Before submitting a job, change the ViewFS folder permissions based on the default NameService folder permissions.

The following table lists the default permission structure of directories configured in ViewFS. If the configured directory permissions are not included in the following table, you must change the directory permissions accordingly.

.. table:: **Table 1** Default permission structure of directories configured in ViewFS

   +---------------------------------------------+---------------------------------------------------------------------------------------------------+----------------------------------------------------------------+---------------------------------------------------------------+
   | Parameter                                   | Description                                                                                       | Default Value                                                  | Default value and default permissions on the parent directory |
   +=============================================+===================================================================================================+================================================================+===============================================================+
   | yarn.nodemanager.remote-app-log-dir         | On the default file system (usually HDFS), specify the directory to which the NM aggregates logs. | logs                                                           | 777                                                           |
   +---------------------------------------------+---------------------------------------------------------------------------------------------------+----------------------------------------------------------------+---------------------------------------------------------------+
   | yarn.nodemanager.remote-app-log-archive-dir | Directory for archiving logs                                                                      | ``-``                                                          | 777                                                           |
   +---------------------------------------------+---------------------------------------------------------------------------------------------------+----------------------------------------------------------------+---------------------------------------------------------------+
   | yarn.app.mapreduce.am.staging-dir           | Staging directory used when a job is submitted                                                    | /tmp/hadoop-yarn/staging                                       | 777                                                           |
   +---------------------------------------------+---------------------------------------------------------------------------------------------------+----------------------------------------------------------------+---------------------------------------------------------------+
   | mapreduce.jobhistory.intermediate-done-dir  | Directory for storing historical files of MapReduce jobs                                          | ${yarn.app.mapreduce.am.staging-dir}/history/done_intermediate | 777                                                           |
   +---------------------------------------------+---------------------------------------------------------------------------------------------------+----------------------------------------------------------------+---------------------------------------------------------------+
   | mapreduce.jobhistory.done-dir               | Directory of historical files managed by the MR JobHistory Server.                                | ${yarn.app.mapreduce.am.staging-dir}/history/done              | 777                                                           |
   +---------------------------------------------+---------------------------------------------------------------------------------------------------+----------------------------------------------------------------+---------------------------------------------------------------+
