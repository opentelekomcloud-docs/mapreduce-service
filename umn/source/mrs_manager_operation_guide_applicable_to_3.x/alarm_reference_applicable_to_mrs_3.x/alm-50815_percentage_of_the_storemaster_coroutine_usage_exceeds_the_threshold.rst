:original_name: ALM-50815.html

.. _ALM-50815:

ALM-50815 Percentage of the StoreMaster Coroutine Usage Exceeds the Threshold
=============================================================================

Alarm Description
-----------------

The system checks the percentage of the StoreMaster coroutine usage to the total coroutine usage every 30 seconds. This alarm is generated when the percentage exceeds the threshold.

This alarm is cleared when the percentage of the StoreMaster coroutine usage to the total coroutine usage falls below the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50815    Critical       Yes
======== ============== ============

Alarm Parameters
----------------

+-------------+--------------------------------------------------------------------+
| Parameter   | Description                                                        |
+=============+====================================================================+
| Source      | Specifies the cluster or system for which the alarm was generated. |
+-------------+--------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm was generated.           |
+-------------+--------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm was generated.              |
+-------------+--------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm was generated.              |
+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

The coroutine usage is high, which may cause task failures.

Possible Causes
---------------

-  The load pressure is too high.
-  The alarm threshold or alarm trigger count is improperly configured.

Handling Procedure
------------------

**Check the coroutine usage.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the alarm list, view the role name and obtain the IP address of the instance in **Location** of the alarm whose ID is **50815**.

#. Choose **Cluster** > **Services** > **MemArtsStore** > **Instances**, click the StoreMaster instance for which the alarm is generated, and click the **Chart** tab of the instance.

   Select **Resources** from **Chart Category** on the left and check whether the coroutine usage of the StoreMaster process is greater than 99%.

   -  If yes, go to :ref:`3 <alm-50815__en-us_topic_0000002520267245_en-us_topic_0000002157418372_li13806855181412>`.
   -  If no, go to :ref:`5 <alm-50815__en-us_topic_0000002520267245_en-us_topic_0000002157418372_li11805175541418>`.

#. .. _alm-50815__en-us_topic_0000002520267245_en-us_topic_0000002157418372_li13806855181412:

   Restart the instance.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-50815__en-us_topic_0000002520267245_en-us_topic_0000002157418372_li11805175541418>`.

**Check whether the alarm threshold or alarm trigger count is properly configured.**

5. .. _alm-50815__en-us_topic_0000002520267245_en-us_topic_0000002157418372_li11805175541418:

   Log in to MRS Manager and choose **O&M** > **Alarm** > **Thresholds** > **MemArtsStore** > **Resources** > **StoreMaster process coroutine usage (StoreMaster)**.

6. Click the edit button next to **Trigger Count**, change the number based on site requirements, and click **OK**.

   .. note::

      **Trigger Count** specifies how many times the threshold can be hit before an alarm is generated.

7. Click **Modify** in the **Operation** column, change the alarm threshold based on site requirements, and click **OK**.

8. Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-50815__en-us_topic_0000002520267245_en-us_topic_0000002157418372_li10360155511379>`.

**Collect fault information.**

9.  .. _alm-50815__en-us_topic_0000002520267245_en-us_topic_0000002157418372_li10360155511379:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

10. Expand the **Service** drop-down list, and select **MemArtsStore** for the target cluster.

11. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact O&M engineers and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
