:original_name: ALM-18020.html

.. _ALM-18020:

ALM-18020 Yarn Task Execution Timeout
=====================================

Description
-----------

The system checks MapReduce and Spark tasks (except for permanent JDBC tasks) submitted to Yarn every 15 minutes. This alarm is generated when the task execution time exceeds the timeout duration specified by the user. However, the task can be properly executed. The client timeout parameter of MapReduce is mapreduce.application.timeout.alarm and that of Spark is spark.application.timeout.alarm. The unit is ms.

This alarm is cleared when the task is finished or terminated.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
18020    Minor          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------------------+
| Name              | Meaning                                                                 |
+===================+=========================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                 |
+-------------------+-------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                 |
+-------------------+-------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                    |
+-------------------+-------------------------------------------------------------------------+
| ApplicationName   | Specifies the object (application ID) for which the alarm is generated. |
+-------------------+-------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.                       |
+-------------------+-------------------------------------------------------------------------+

Impact on the System
--------------------

The alarm persists after task execution times out. However, the task can still be properly executed, so this alarm does not exert any impact on the system.

Possible Causes
---------------

-  The specified timeout duration is shorter than the required execution time.
-  The queue resources for task running are insufficient.
-  Task data skew occurs. As a result, some tasks process a large amount of data and take a long time to execute.

Procedure
---------

**Check whether the timeout interval is correctly set.**

#. On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. The **Alarms** page is displayed.

#. Select the alarm whose ID is **18020**. In the alarm details, view **Location** to obtain the timeout task name and timeout duration.

#. Based on the task name and timeout interval, choose **Cluster** > *Name of the desired cluster* > **Services** > **Yarn** > **ResourceManager (Active)** to log in to the native Yarn page. Then find the task on the native page, check its **StartTime** and calculate the task execution time based on the current system time. Check whether the task execution time exceeds the timeout duration.

   -  If yes, go to :ref:`4 <alm-18020__li135821125144620>`.
   -  If no, go to :ref:`10 <alm-18020__li6394993485922>`.

#. .. _alm-18020__li135821125144620:

   Evaluate the expected task execution time based on the service and compare it with the task timeout interval. If the timeout interval is too short, set the timeout interval (**mapreduce.application.timeout.alarm** or **spark.application.timeout.alarm**) of the client to the task expected execution time. Run the task again and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-18020__li9996125375313>`.

**Check whether the queue resources are sufficient.**

5. .. _alm-18020__li9996125375313:

   Find the task on the native page and view the queue name of the task. Click **Scheduler** on the left of the native page. On the **Applications Queues** page, find the corresponding queue name and expand the queue details, as shown in the following figure.

   |image1|

6. Check whether the value of **Used Resources** in the queue details is approximately equal to the value of **Max Resources**, which indicates that the resources in the queue submitted by the task have been used up. If the queue resources are insufficient, choose **Tenant Resources** > **Dynamic Resource Plan** > **Resource Distribution Policy** on FusionInsight Manager and increase the value of **Max Resources** for the queue. Run the task again and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-18020__li5526143185420>`.

**Check whether data skew occurs.**

7. .. _alm-18020__li5526143185420:

   On the native Yarn page, click *task ID* (for example, **application_1565337919723_0002**) > **Tracking URL:ApplicationMaster** > **job_1565337919723_0002**. The following page is displayed.

   |image2|

8. Choose **Job** > **Map tasks** or **Job** > **Reduce tasks** on the left and check whether the execution time of each Map or Reduce task differs greatly. If yes, task data skew occurs. In this case, you need to balance the task data.

9. Rectify the fault based on the preceding causes and perform the tasks again. Then, check whether the alarm persists.

   -  If yes, go to :ref:`10 <alm-18020__li6394993485922>`.
   -  If no, no further action is required.

**Collect the fault information.**

10. .. _alm-18020__li6394993485922:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

11. Expand the **Service** drop-down list, and select **Yarn** for the target cluster.

12. Click |image3| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

13. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582927573.png
.. |image2| image:: /_static/images/en-us_image_0000001583127321.png
.. |image3| image:: /_static/images/en-us_image_0000001532448194.png
