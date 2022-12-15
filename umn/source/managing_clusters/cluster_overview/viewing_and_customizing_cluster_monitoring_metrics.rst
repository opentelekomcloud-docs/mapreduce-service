:original_name: mrs_01_0515.html

.. _mrs_01_0515:

Viewing and Customizing Cluster Monitoring Metrics
==================================================

MRS cluster nodes are classified into management nodes, control nodes, and data nodes. The change trends of key host monitoring metrics on each type of node can be calculated and displayed as curve charts in reports based on the customized periods. If a host belongs to multiple node types, the metric statistics will be repeatedly collected.

This section provides overview of MRS clusters and describes how to view, customize, and export node monitoring metrics on MRS Manager.

.. note::

   Cluster metrics are monitored periodically. The average historical monitoring interval is about 5 minutes.

**Method 1** **(applicable to clusters of versions earlier than MRS 3.x):**

#. Choose **Clusters** > **Active Clusters** and click a cluster name to go to the cluster details page.
#. Click the **Dashboard** tab, you can view the cluster host health status statistics on the lower part of the displayed tab page.
#. To view or export reports of other metrics, click **Access Manager** next to **MRS Manager** in the **Basic Information** area to access the Manager page. For details, see :ref:`Accessing Manager <mrs_01_0128>`.
#. On the Manager page, view, customize, and export the node monitoring metric report. For details, see :ref:`Dashboard <mrs_01_0107>`.

**Method 2 (applicable to clusters of MRS 1.9.2 to 2.1.0)**

#. Log in to the MRS console.
#. Choose **Clusters > Active Clusters** and click a cluster name to go to the cluster details page.
#. In the **Basic Information** area on the **Dashboard** tab page, click **Click to synchronize** on the right side of **IAM User Sync** to synchronize IAM users.
#. After the synchronization is complete, you can view the cluster monitoring metric report on the right of the page.
#. In time range area, specify a period to view monitoring data. The options are as follows:

   -  Last 1 hour
   -  Last 3 hours
   -  Last 12 hours
   -  Last 24 hours
   -  Recent 7 days
   -  Recent 30 days
   -  Customize: You can customize the period for viewing monitoring data.

#. Customize a monitoring metric report.

   a. Click **Customize** and select monitoring metrics to be displayed.

      MRS supports a maximum of 14 monitoring metrics, but at most 12 customized monitoring metrics can be displayed on the page.

      -  Cluster Host Health Status
      -  Cluster Network Read Speed Statistics
      -  Host Network Read Speed Distribution
      -  Host Network Write Speed Distribution
      -  Cluster Disk Write Speed Statistics
      -  Cluster Disk Usage Statistics
      -  Cluster Disk Information
      -  Host Disk Usage Statistics
      -  Cluster Disk Read Speed Statistics
      -  Cluster Memory Usage Statistics
      -  Host Memory Usage Distribution
      -  Cluster Network Write Speed Statistics
      -  Host CPU Usage Distribution
      -  Cluster CPU Usage Statistics

   b. Click **OK** to save the selected monitoring metrics for display.

      .. note::

         Click **Clear** to cancel all the selected monitoring metrics in a batch.

#. Export a monitoring report.

   a. Select a period. The options are as follows:

      -  Last 1 hour
      -  Last 3 hours
      -  Last 12 hours
      -  Last 24 hours
      -  Recent 7 days
      -  Recent 30 days
      -  Customize: You can customize the period for viewing monitoring data.

   b. Click **Export**. MRS will generate a report about the selected monitoring metrics in a specified time of period. Save the report.

**Method 3: (applicable to MRS 3.x clusters)**

#. Log in to the MRS console.
#. Choose **Clusters > Active Clusters** and click a cluster name to go to the cluster details page.
#. In the **Basic Information** area on the **Dashboard** tab page, click **Click to synchronize** on the right side of **IAM User Sync** to synchronize IAM users.
#. After the synchronization is complete, you can view the cluster monitoring metric report on the right of the page.
#. In time range area, specify a period to view monitoring data. The options are as follows:

   -  Last 1 hour
   -  Last 3 hours
   -  Last 12 hours
   -  Last 24 hours
   -  Recent 7 days
   -  Recent 30 days
   -  Customize: You can customize the period for viewing monitoring data.

#. Customize a monitoring metric report.

   a. Click **Customize** and select monitoring metrics to be displayed.

      At most 12 customized monitoring metrics can be displayed on the page.

   b. Click **OK** to save the selected monitoring metrics for display.

      .. note::

         Click **Clear** to cancel all the selected monitoring metrics in a batch.
