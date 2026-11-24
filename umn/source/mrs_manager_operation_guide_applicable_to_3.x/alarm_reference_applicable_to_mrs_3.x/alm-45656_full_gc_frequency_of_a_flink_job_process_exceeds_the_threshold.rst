:original_name: ALM-45656.html

.. _ALM-45656:

ALM-45656 Full GC Frequency of a Flink Job Process Exceeds the Threshold
========================================================================

Alarm Description
-----------------

The system checks the number of full GCs for each job process at the interval defined by **metrics.reporter.alarm.interval** (default: 30s). An alarm is triggered when the full GC frequency of a Flink job process exceeds the threshold. The alarm is cleared after the job is successfully restarted or when the job is deleted. Otherwise, you need to manually clear this alarm.

The alarm threshold is calculated as: (Increment in full GC count)/(Time interval of the change in full GC count). The default threshold is 5 times/min.

-  The increment in full GC count is controlled by the **metrics.reporter.alarm.job.alarm.fullGC.count.delta** parameter. The default value is **5**.
-  The time interval of the change in full GC count is controlled by the **metrics.reporter.alarm.job.alarm.fullGC.interval** parameter. The default value is 1 min, and the unit can be **s**, **min**, **h**, or **d**.

This alarm involves only the frequency of full GCs, not the duration of any single full GC.

-  If the full GC frequency for any process of the same job exceeds the threshold, an alarm is generated. While alarms are auto-cleared, they are recorded in historical events.
-  If the full GC frequency for the same process of the same job keeps exceeding the threshold, alarms are generated continuously. While alarms are auto-cleared, they are recorded in historical events.

Alarm Attributes
----------------

======== ============== ================== ============ ============
Alarm ID Alarm Severity Alarm Type         Service Type Auto Cleared
======== ============== ================== ============ ============
45656    Major          Quality of service Flink        No
======== ============== ================== ============ ============

Alarm Parameters
----------------

+------------------------+-----------------+--------------------------------------------------------------------------+
| Type                   | Parameter       | Description                                                              |
+========================+=================+==========================================================================+
| Location Information   | Source          | Specifies the cluster for which the alarm was generated.                 |
+------------------------+-----------------+--------------------------------------------------------------------------+
|                        | ServiceName     | Specifies the service for which the alarm was generated.                 |
+------------------------+-----------------+--------------------------------------------------------------------------+
|                        | ApplicationName | Specifies the name of the application for which the alarm was generated. |
+------------------------+-----------------+--------------------------------------------------------------------------+
|                        | JobName         | Specifies the job for which the alarm was generated.                     |
+------------------------+-----------------+--------------------------------------------------------------------------+
|                        | UserName        | Specifies the username for which the alarm was generated.                |
+------------------------+-----------------+--------------------------------------------------------------------------+
| Additional Information | ProcessName     | Specifies the name of the process for which the alarm was generated.     |
+------------------------+-----------------+--------------------------------------------------------------------------+
|                        | AlarmCount      | Specifies the number of times the alarm was generated for the process.   |
+------------------------+-----------------+--------------------------------------------------------------------------+

Impact on the System
--------------------

Frequent full GCs in a Flink job process typically indicate improper memory management or high resource pressure. This can cause performance degradation and may even result in OOM exceptions. Check whether the Flink job's memory allocation and program design are appropriate.

This alarm applies only to the Flink jobs and has no impact on FlinkServer.

Possible Causes
---------------

-  Heap memory is overused or improperly configured, resulting in frequent full GCs in the process.
-  The alarm threshold is improperly configured. For example, the threshold may be lower than the recommended value or below the appropriate full GC frequency.

Handling Procedure
------------------

**Adjust the memory configuration of Flink jobs.**

#. Log in to MRS Manager as a user with FlinkServer administrator permissions.
#. Choose **O&M** > **Alarm** > **Alarms**, locate **ALM-45656 Full GC Frequency of a Flink Job Process Exceeds the Threshold**, and check and record the **ProcessName** value in **Additional Information** of the alarm to determine whether the alarm is generated for the JobManager or TaskManager.
#. Choose **Cluster** > **Services** > **Flink** and click the link next to **Flink Web UI**. On the displayed page, choose **Job Management**, and click **Develop** in the **Operation** column of the target job to switch to the job editing page.
#. On the **Basic Parameter** tab page, adjust the value of **JobManager Memory(MB)** or the value of **Memory(MB)** under **taskManager**, restart the job, and check whether the alarm persists.

   -  If yes, go to :ref:`5 <alm-45656__en-us_topic_0000002521725194_en-us_topic_0000002523611423_li455515512914>`.
   -  If no, no further action is required.

**Adjust the Full GC alarm threshold.**

5. .. _alm-45656__en-us_topic_0000002521725194_en-us_topic_0000002523611423_li455515512914:

   Adjust the full GC alarm threshold in either of the following ways.

   -  Jobs submitted through FlinkServer: Choose **Cluster** > **Services** > **Flink**, click **Configurations** and then **All Configurations**, and choose **FlinkServer(Role)** > **ALARM**. Increase the full GC alarm threshold based on the alarm threshold calculation formula, and click **Save**. Click the **Instances** tab, synchronize the configuration, and restart FlinkServer instances.
   -  Jobs submitted through the client: Choose **Cluster** > **Services** > **Flink**, click **Configurations** and then **All Configurations**, and choose **FlinkResource(Role)** > **ALARM**. Increase the full GC alarm threshold based on the alarm threshold calculation formula, and click **Save**. Click the **Instances** tab, synchronize the configuration, and restart FlinkResource instances. Apply the configuration to the client.

6. Restart the job and check whether the alarm persists.

   -  If yes, go to :ref:`7 <alm-45656__en-us_topic_0000002521725194_en-us_topic_0000002523611423_li5131512717158>`.
   -  If no, no further action is required.

**Collect fault information.**

7. .. _alm-45656__en-us_topic_0000002521725194_en-us_topic_0000002523611423_li5131512717158:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8. Expand the **Service** drop-down list, and select **Flink** for the target cluster.

9. Click |image1| in the upper right corner, and select a time span starting 10 minutes before and ending 10 minutes after when the alarm was generated. Then, click **Download** to collect the logs.

10. Check the logs of the job process for which the alarm was reported to identify and fix the issue, or contact O&M personnel and provide the collected fault logs. No further action is required.

Alarm Clearance
---------------

The alarm is cleared after the Flink job is successfully restarted or when the job is deleted. Otherwise, the system will not automatically clear the alarm, and you must clear it manually.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000002525540373.png
