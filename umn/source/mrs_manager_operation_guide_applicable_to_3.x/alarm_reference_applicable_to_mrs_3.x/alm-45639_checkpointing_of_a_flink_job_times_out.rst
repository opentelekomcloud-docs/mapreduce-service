:original_name: ALM-45639.html

.. _ALM-45639:

ALM-45639 Checkpointing of a Flink Job Times Out
================================================

Description
-----------

The system checks the checkpointing timeout of Flink jobs every 30 seconds. This alarm is generated if the checkpointing timeout of a Flink job is longer than the threshold (600 seconds by default). This alarm is cleared when the checkpointing timeout of a job is less than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45639    Minor          Yes
======== ============== ==========

Parameters
----------

=========== ========================================================
Name        Meaning
=========== ========================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
JobName     Specifies the job for which the alarm is generated.
UserName    Specifies the username for which the alarm is generated.
=========== ========================================================

Impact on the System
--------------------

This alarm has no impact on the system.

Possible Causes
---------------

The job may be in the sub-healthy state. The possible causes are as follows:

-  The memory for the TaskManager of the job is insufficient.
-  The state memory is too large, making checkpointing time-consuming.

Procedure
---------

#. Log in to Manager as a user who has the FlinkServer management permission.

#. Choose **O&M** > **Alarm** > **Alarms** > **ALM-45639 Checkpointing of a Flink Job Times Out**, view **Location**, and obtain the name of the task for which the alarm is generated.

#. Choose **Cluster** > **Services** > **Yarn** and click the link next to **ResourceManager WebUI** to go to the native Yarn page.

#. Locate the failed task based on its name displayed in **Location**, search for and record the application ID of the job, and check whether the job logs are available on the Yarn page.


   .. figure:: /_static/images/en-us_image_0000001532448466.png
      :alt: **Figure 1** Application ID of a job

      **Figure 1** Application ID of a job

   -  If yes, go to :ref:`5 <alm-45639__en-us_topic_0000001150940918_li109051158191>`.
   -  If no, go to :ref:`7 <alm-45639__en-us_topic_0000001150940918_li5902415141913>`.

#. .. _alm-45639__en-us_topic_0000001150940918_li109051158191:

   Click the application ID of the failed job to go to the job page.

   a. Click **Logs** in the **Logs** column to view JobManager logs.


      .. figure:: /_static/images/en-us_image_0000001583127589.png
         :alt: **Figure 2** Clicking Logs

         **Figure 2** Clicking Logs

   b. Click the ID in the **Attempt ID** column and click **Logs** in the **Logs** column to view TaskManager logs.


      .. figure:: /_static/images/en-us_image_0000001582927845.png
         :alt: **Figure 3** Clicking the ID in the Attempt ID column

         **Figure 3** Clicking the ID in the Attempt ID column


      .. figure:: /_static/images/en-us_image_0000001583087613.png
         :alt: **Figure 4** Clicking Logs

         **Figure 4** Clicking Logs

      .. note::

         You can also log in to Manager as a user who has the FlinkServer management permission. Choose **Cluster** > **Services** > **Flink**, and click the link next to **Flink WebUI**. On the displayed Flink web UI, click **Job Management**, click **More** in the **Operation** column, and select **Job Monitoring** to view TaskManager logs.

#. View the logs of the failed job to rectify the fault, or contact the O&M personnel and send the collected fault logs. No further action is required.

**If logs are unavailable on the Yarn page, download logs from HDFS.**

7. .. _alm-45639__en-us_topic_0000001150940918_li5902415141913:

   On Manager, choose **Cluster** > **Services** > **HDFS**, click the link next to **NameNode WebUI** to go to the HDFS page, choose **Utilities** > **Browse the file system**, and download logs in the **/tmp/logs/**\ *Username*\ **/logs/**\ *Application ID of the failed job* directory.

8. View the logs of the failed job to rectify the fault, or contact the O&M personnel and send the collected fault logs.

Alarm Clearing
--------------

This alarm is cleared when the checkpointing timeout a Flink job is less than or equal to the threshold.

Related Information
-------------------

None
