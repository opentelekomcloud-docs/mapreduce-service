:original_name: ALM-12191.html

.. _ALM-12191:

ALM-12191 Disk I/O Usage Exceeds the Threshold
==============================================

Alarm Description
-----------------

The system checks the disk I/O usage every 30 seconds and compares the actual disk I/O usage with the threshold. This alarm is generated when the disk I/O usage exceeds the threshold for multiple consecutive times (**3** by default).

If the **hit number** is **1**, this alarm is cleared when the disk I/O usage is less than or equal to the threshold. If the **hit number** is greater than **1**, this alarm is cleared when the disk I/O usage is less than or equal to 90% of the threshold.

.. note::

   This alarm applies only to MRS 3.3.1 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
12191    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------------+--------------------------------------------------------------------+
| Type                   | Parameter         | Description                                                        |
+========================+===================+====================================================================+
| Location Information   | Source            | Specifies the cluster or system for which the alarm was generated. |
+------------------------+-------------------+--------------------------------------------------------------------+
|                        | ServiceName       | Specifies the service for which the alarm was generated.           |
+------------------------+-------------------+--------------------------------------------------------------------+
|                        | RoleName          | Specifies the role for which the alarm was generated.              |
+------------------------+-------------------+--------------------------------------------------------------------+
|                        | HostName          | Specifies the host for which the alarm was generated.              |
+------------------------+-------------------+--------------------------------------------------------------------+
| Additional Information | Trigger Condition | Specifies the alarm triggering condition.                          |
+------------------------+-------------------+--------------------------------------------------------------------+

Impact on the System
--------------------

-  Latency: Service processes may run slowly and there is a latency.
-  Service failure: Service processing may be slow, time out, or fail. As a result, jobs may fail to run.

Possible Causes
---------------

-  The alarm threshold or alarm trigger count is improperly configured.
-  The disk configuration cannot meet service requirements. The disk I/O usage reaches the upper limit. Alternatively, services are in peak hours. The disk I/O usage reaches the upper limit in a short period.

Handling Procedure
------------------

**Check whether the alarm threshold or alarm trigger count is properly configured.**

#. Modify the alarm threshold and alarm trigger count based on the actual disk I/O usage.

   a. Log in to MRS Manager and choose **O&M** > **Alarm** > **Thresholds**, click the name of the desired cluster, and choose **Host** > **Disk** > **Disk IO Utilization**.
   b. Click the edit button next to **Trigger Count** to change it to a proper value based on the actual service usage.

      .. note::

         **Trigger Count** indicates how many consecutive times the threshold is reached when the alarm is triggered.

   c. Click **Modify** in the **Operation** column of the row that contains the rule and change the alarm threshold.

#. Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-12191__li15891424513>`.

**Check whether the disk I/O usage reaches the upper limit.**

3. .. _alm-12191__li15891424513:

   On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the alarm list, expand the alarm details and click the name of the host for which the alarm is generated in **Location** area.

4. On the overview page of the host, observe the real-time data of the disk I/O usage for about 5 minutes. If the disk I/O usage exceeds the threshold for multiple times, contact the MRS cluster administrator to improve the disk specification.

   If **Disk IO Utilization** chart is not displayed, click the drop-down arrow on the right, select **Customize**, select the desired item, and click **OK**.

5. Check whether it was the peak hour. If this alarm was generated during peak hours, expand the node capacity or contact the MRS cluster administrator to improve the disk specification.

6. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-12191__li289102416117>`.

**Collect fault information.**

7.  .. _alm-12191__li289102416117:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Expand the **Service** drop-down list, select **NodeAgent** for the target cluster, and click **OK**.

9.  Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
