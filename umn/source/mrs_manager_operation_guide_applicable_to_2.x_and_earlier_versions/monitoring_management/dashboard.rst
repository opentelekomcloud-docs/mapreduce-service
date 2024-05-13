:original_name: mrs_01_0107.html

.. _mrs_01_0107:

Dashboard
=========

On MRS Manager, nodes in a cluster can be classified into management nodes, control nodes, and data nodes. The change trends of key host monitoring metrics on each type of node can be calculated and displayed as curve charts in reports based on the customized periods. If a host belongs to multiple node types, the metric statistics will be repeatedly collected.

This section provides overview of MRS clusters and describes how to view, customize, and export node monitoring metrics on MRS Manager.

Procedure
---------

#. Log in to MRS Manager. For details, see :ref:`Accessing MRS Manager (MRS 2.x or Earlier) <mrs_01_0102>`.

#. Choose **Dashboard** on MRS Manager.

#. In **Period**, you can specify a period to view monitoring data. The options are as follows:

   -  Real time
   -  Last 3 hours
   -  Last 6 hours
   -  Last 24 hours
   -  Last week
   -  Last month
   -  Last 3 months
   -  Last 6 months
   -  Customize. If you select this option, you can customize the period for viewing monitoring data.

#. Click **View** to view monitoring data in a period.

   -  You can view **Health Status** and **Roles** of each service on the **Service Summary** page of MRS Manager.
   -  Click |image1| above the curve chart to view details about a metric.

#. Customize a monitoring report.

   a. Click **Customize** and select monitoring metrics to be displayed on MRS Manager.

      MRS Manager supports a maximum of 14 monitoring metrics, but at most 12 customized monitoring metrics can be displayed on the page.

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

#. Set an automatic refresh interval or click |image2| for an immediate refresh.

   The following refresh interval options are supported:

   -  Refresh every 30 seconds
   -  Refresh every 60 seconds
   -  Stop refreshing

      .. note::

         If you select **Full Screen**, the **Dashboard** window will be maximized.

#. Export a monitoring report.

   a. Select a period. The options are as follows:

      -  Real time
      -  Last 3 hours
      -  Last 6 hours
      -  Last 24 hours
      -  Last week
      -  Last month
      -  Last 3 months
      -  Last 6 months
      -  Customize. If you select this option, you can customize a time of period to export a report.

   b. Click **Export**. MRS Manager will generate a report about the selected monitoring metrics in a specified time of period. Save the report.

      .. note::

         To view the curve charts of monitoring metrics in a specified period, click **View**.

For MRS 1.7.2 or earlier, the real-time monitoring page and historical report page are separated. The procedure is as follows.

-  Real-time monitoring

   #. Log in to MRS Manager. For details, see :ref:`Accessing MRS Manager (MRS 2.x or Earlier) <mrs_01_0102>`.

   #. On MRS Manager, choose **Dashboard** > **Real time**.

      -  You can view **Health Status** and **Roles** of each service on the **Service Summary** page of MRS Manager.

      -  The following are some of host monitoring metrics displayed on MRS Manager.

         -  Cluster Host Health Status
         -  Host Network Read Speed Distribution
         -  Host Network Write Speed Distribution
         -  Cluster Disk Information
         -  Host Disk Usage Distribution
         -  Cluster Memory Usage
         -  Host Memory Usage Distribution
         -  Host CPU Usage Distribution
         -  Average Cluster CPU Usage

         You can click **Customize** to display the specified monitoring metrics.

   #. Set an automatic refresh interval or click |image3| for an immediate refresh.

      The following refresh interval options are supported:

      -  Refresh every 30 seconds
      -  Refresh every 60 seconds
      -  Stop refreshing

         .. note::

            If you select **Full Screen**, the **Real-time Monitoring** window will be maximized.

-  Historical reports

   #. View a monitoring report.

      a. Log in to MRS Manager. For details, see :ref:`Accessing MRS Manager (MRS 2.x or Earlier) <mrs_01_0102>`.

      b. On MRS Manager, click **Dashboard**.

      c. Click **Historical Report** to view a report.

         By default, the report displays the monitoring metric statistics of the previous day.

         .. note::

            If you select **Full Screen**, the **Historical Report** window will be maximized.

   #. Customize a monitoring report.

      a. Click **Customize** and select monitoring metrics to be displayed on MRS Manager.

         MRS Manager supports a maximum of 8 monitoring metrics, but at most 6 customized monitoring metrics can be displayed on the page.

         -  Cluster Network Read Speed Statistics
         -  Cluster Disk Write Speed Statistics
         -  Cluster Disk Usage Statistics
         -  Cluster Disk Information
         -  Cluster Disk Read Speed Statistics
         -  Cluster Memory Usage Statistics
         -  Cluster Network Write Speed Statistics
         -  Cluster CPU Usage Statistics

      b. Click **OK** to save the selected monitoring metrics for display.

         .. note::

            Click **Clear** to cancel all the selected monitoring metrics in a batch.

   #. Export a monitoring report.

      a. Select a period.

         The following options are available: **Last day**, **Last week**, **Last month**, **Last quarter**, and **Last half year**

         In **Time Range**, you can also specify exact start and end time.

      b. Click **Export**. MRS Manager will generate a report about the selected monitoring metrics in a specified time of period. Save the report.

         .. note::

            To view the curve charts of monitoring metrics in a specified period, click **View**.

.. |image1| image:: /_static/images/en-us_image_0000001296058400.png
.. |image2| image:: /_static/images/en-us_image_0000001348737865.png
.. |image3| image:: /_static/images/en-us_image_0000001348737865.png
