:original_name: mrs_01_0056.html

.. _mrs_01_0056:

Stopping a Job
==============

This section describes how to stop running MRS jobs.

Background
----------

You cannot stop Spark SQL jobs. After a job is stopped, its status changes to **Terminated** and the job cannot be executed again.

Procedure
---------

#. Log in to the MRS management console.

#. Choose **Clusters** > **Active Clusters**, select a running cluster, and click its name.

   The cluster details page is displayed.

#. Click **Jobs**.

#. Select a running job, and choose **More > Stop** in the **Operation** column.

   The job status changes from **Running** to **Terminated**.
