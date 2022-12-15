:original_name: mrs_01_0055.html

.. _mrs_01_0055:

Viewing Job Configuration and Logs
==================================

This section describes how to view job configuration and logs.

Background
----------

-  You can view configuration information of all jobs.

-  You can only view logs of running jobs.

   Because logs of Spark SQL and DistCp jobs are not in the background, you cannot view logs of running Spark SQL and DistCp jobs.

Procedure
---------

#. Log in to the MRS management console.

#. Click |image1| in the upper-left corner on the management console and select a region and project.

#. Choose **Clusters** > **Active Clusters**, select a running cluster, and click its name to switch to the cluster details page.

#. Click **Jobs**.

#. In the **Operation** column of the job to be viewed, click **View Details**.

   In the **View Details** window that is displayed, configuration of the selected job is displayed.

#. Select a running job, and click **View Log** in the **Operation** column.

   In the new page that is displayed, real-time log information of the job is displayed.

   Each tenant can submit and view 10 jobs concurrently.

.. |image1| image:: /_static/images/en-us_image_0000001295738508.png
