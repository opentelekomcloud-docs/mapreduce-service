:original_name: mrs_03_1090.html

.. _mrs_03_1090:

How Do I Improve the Resource Utilization of Core Nodes in a Cluster?
=====================================================================

#. Go to the Yarn service configuration page.

   -  For versions earlier than 1.9.2,

      log in to MRS Manager, choose **Services** > **Yarn** > **Service Configuration**, and select **All** from the **Basic** drop-down list.

   -  For MRS 1.9.2 or later, click the cluster name on the MRS console, choose **Components** > **Yarn** > **Service Configuration**, and select **All** from the **Basic** drop-down list.

      .. note::

         If the **Components** tab is unavailable, complete IAM user synchronization first. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

   -  MRS 3.\ *x* or later: Log in to FusionInsight Manager. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Yarn** > **Configurations** > **All Configurations**.

#. Search for **yarn.nodemanager.resource.memory-mb**, and increase the value based on the actual memory of the cluster nodes.
#. Save the change and restart the affected services or instances.
