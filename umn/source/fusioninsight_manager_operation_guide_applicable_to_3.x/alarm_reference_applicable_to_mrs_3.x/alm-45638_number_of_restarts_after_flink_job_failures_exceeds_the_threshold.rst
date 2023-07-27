:original_name: ALM-45638-1.html

.. _ALM-45638-1:

ALM-45638 Number of Restarts After Flink Job Failures Exceeds the Threshold
===========================================================================

This section applies to MRS 3.2.0 or later.

Description
-----------

The system checks the number of Flink job restarts based on the alarm checking interval. This alarm is generated when the number exceeds the configured threshold. This alarm is cleared when the job is restarted.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45638    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+---------------------------------------------------------------------+
| Name        | Meaning                                                             |
+=============+=====================================================================+
| Source      | Specifies the cluster for which the alarm is generated.             |
+-------------+---------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.             |
+-------------+---------------------------------------------------------------------+
| JobName     | Specifies the job for which the alarm is generated.                 |
+-------------+---------------------------------------------------------------------+
| Username    | Specifies the username of the job for which the alarm is generated. |
+-------------+---------------------------------------------------------------------+

Impact on the System
--------------------

This alarm has no impact on the system.

Possible Causes
---------------

You can view the causes in the specific logs.

Procedure
---------

#. Log in to Manager as a user who has the FlinkServer management permission.

#. Choose **Cluster** > **Services** > **Yarn** and click the link next to **ResourceManager WebUI** to go to the Yarn page.

#. Locate the failed job based on its name displayed in **Location**, search for and record the application ID of the failed job, and check whether the job logs are available on the Yarn page.


   .. figure:: /_static/images/en-us_image_0000001532767354.png
      :alt: **Figure 1** Application ID of a job

      **Figure 1** Application ID of a job

   If yes, go to :ref:`4 <alm-45638-1__en-us_topic_0000001480898081_en-us_topic_0000001396557914_li109051158191>`.

   If no, go to :ref:`6 <alm-45638-1__en-us_topic_0000001480898081_en-us_topic_0000001396557914_li5902415141913>`.

#. .. _alm-45638-1__en-us_topic_0000001480898081_en-us_topic_0000001396557914_li109051158191:

   Click the application ID of the failed job to go to the job page.

   a. Click **Logs** in the **Logs** column to view JobManager logs.


      .. figure:: /_static/images/en-us_image_0000001532927290.png
         :alt: **Figure 2** Clicking Logs

         **Figure 2** Clicking Logs

   b. Click the ID in the **Attempt ID** column and click **Logs** in the **Logs** column to view TaskManager logs.


      .. figure:: /_static/images/en-us_image_0000001532607622.png
         :alt: **Figure 3** Clicking the ID in the Attempt ID column

         **Figure 3** Clicking the ID in the Attempt ID column


      .. figure:: /_static/images/en-us_image_0000001583087273.png
         :alt: **Figure 4** Clicking Logs

         **Figure 4** Clicking Logs

      .. note::

         You can also log in to Manager as a user who has the FlinkServer management permission, choose **Cluster** > **Services** > **Flink**, click the link next to **Flink WebUI**. On the displayed Flink web UI, click **Job Management** and choose **More** > **Job Monitoring** in the **Operation** column to view the TaskManager logs.

#. View the logs of the failed job to rectify the fault, or contact the O&M personnel personnel and send the collected fault logs. No further action is required.

**If logs are unavailable on the Yarn page, download logs from HDFS.**

6. .. _alm-45638-1__en-us_topic_0000001480898081_en-us_topic_0000001396557914_li5902415141913:

   On Manager, choose **Cluster** > **Services** > **HDFS**, click the link next to **NameNode WebUI** to go to the HDFS page, select **Utilities** > **Browse the file system**, and download logs in the **/tmp/logs/**\ *User name*\ **/logs/**\ *Application ID of the failed job* directory.

7. View the logs of the failed job to rectify the fault, or contact the O&M personnel personnel and send the collected fault logs.

Alarm Clearing
--------------

This alarm is cleared when the Flink job is successfully restarted.

Related Information
-------------------

None
