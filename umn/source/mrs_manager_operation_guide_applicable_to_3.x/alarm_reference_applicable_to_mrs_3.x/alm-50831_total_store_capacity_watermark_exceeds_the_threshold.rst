:original_name: ALM-50831.html

.. _ALM-50831:

ALM-50831 Total Store Capacity Watermark Exceeds the Threshold
==============================================================

Alarm Description
-----------------

The system checks the total capacity watermark of Store every 30 seconds. This alarm is generated when the watermark exceeds the threshold.

This alarm is cleared when the watermark falls below the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50831    Major          Yes
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

If data is still written without being deleted, the cluster cannot provide services.

Possible Causes
---------------

-  Data is continuously written and is not deleted in a timely manner, which is close to the upper limit of the storage pool.
-  The alarm threshold or alarm trigger count is improperly configured.

Handling Procedure
------------------

**Check whether the alarm threshold or alarm trigger count is properly configured.**

#. Log in to MRS Manager and choose **O&M** > **Alarm** > **Thresholds** > **MemArtsStore** > **Disk** > **Percentage of Store disk usage to the total disk capacity (StoreMaster)**.
#. Click the edit button next to **Trigger Count**, change the number based on site requirements, and click **OK**.

   .. note::

      **Trigger Count** specifies how many times the threshold can be hit before an alarm is generated.

#. Click **Modify** in the **Operation** column, change the alarm threshold based on site requirements, and click **OK**.
#. Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-50831__en-us_topic_0000002520267255_en-us_topic_0000002157418388_li71831533164213>`.

**Collect fault information.**

5. .. _alm-50831__en-us_topic_0000002520267255_en-us_topic_0000002157418388_li71831533164213:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Expand the **Service** drop-down list, and select **MemArtsStore** for the target cluster.

7. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M engineers and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
