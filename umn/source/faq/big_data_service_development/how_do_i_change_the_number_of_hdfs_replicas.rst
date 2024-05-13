:original_name: mrs_03_1061.html

.. _mrs_03_1061:

How Do I Change the Number of HDFS Replicas?
============================================

#. Go to the HDFS service configuration page.

   -  For MRS cluster versions earlier than 1.9.2:

      Log in to MRS Manager, choose **Services** > **HDFS** > **Service Configuration**, and select **All** from the **Basic** drop-down list.

   -  For MRS 1.9.2 or later, click the cluster name on the MRS console, choose **Components** > **HDFS** > **Service Configuration**, and select **All** from the **Basic** drop-down list.

      .. note::

         If the **Components** tab is unavailable, complete IAM user synchronization first. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

   -  MRS 3.\ *x* or later: Log in to MRS Manager. And choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS** > **Configurations** > **All Configurations**.

#. Search for **dfs.replication**, change the value (value range: 1 to 16), and restart the HDFS instance.
