:original_name: ALM-50811.html

.. _ALM-50811:

ALM-50811 Number of StoreWorker Write Failures Due to Flow Control Exceeds the Threshold
========================================================================================

Alarm Description
-----------------

The system checks the number of StoreWorker write failures due to flow control every 30 seconds. This alarm is generated when the number of write failures exceeds the threshold.

This alarm is cleared when the number of StoreWorker write failures due to flow control falls below the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50811    Major          Yes
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

The server efficiency decreases, and tasks may fail.

Possible Causes
---------------

-  The load tilt is too large, and the load pressure is too high.
-  The alarm threshold or alarm trigger count is improperly configured.

Handling Procedure
------------------

**Check the pool I/O time.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the alarm list, view the role name and obtain the IP address of the instance in **Location** of the alarm whose ID is **50811**.

#. Choose **Cluster** > **Services** > **MemArtsStore** > **Instances**, click the StoreWorker instance for which the alarm is generated, and click the **Chart** tab of the instance.

   Select **Pool I/O** from **Chart Category** on the left, observe the Pool I/O time of the StoreWorker process, and check whether the latency decreases and the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-50811__en-us_topic_0000002488267378_en-us_topic_0000002157258604_li887113479397>`.

**Check whether the alarm threshold or alarm trigger count is properly configured.**

3. .. _alm-50811__en-us_topic_0000002488267378_en-us_topic_0000002157258604_li887113479397:

   Log in to MRS Manager and choose **O&M** > **Alarm** > **Thresholds** > **MemArtsStore** > **Service** > **Number of StoreWorker write failures due to flow control (StoreWorker)**.

4. Click the edit button next to **Trigger Count**, change the number based on site requirements, and click **OK**.

   .. note::

      **Trigger Count** specifies how many times the threshold can be hit before an alarm is generated.

5. Click **Modify** in the **Operation** column, change the alarm threshold based on site requirements, and click **OK**.

6. Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-50811__en-us_topic_0000002488267378_en-us_topic_0000002157258604_li10360155511379>`.

**Collect fault information.**

7.  .. _alm-50811__en-us_topic_0000002488267378_en-us_topic_0000002157258604_li10360155511379:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Expand the **Service** drop-down list, and select **MemArtsStore** for the target cluster.

9.  Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact O&M engineers and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
