:original_name: ALM-12208.html

.. _ALM-12208:

ALM-12208 Too Many Full GCs for NodeAgent Process
=================================================

Alarm Description
-----------------

The system checks the full GC count of the NodeAgent process every 60 seconds. This alarm is generated when the number of full GCs exceeds the threshold.

The statistical method is Full GC count = Full GC count in the next period - Full GC count in the previous period. By default, an alarm is reported when the Full GC count exceeds 1 for three consecutive checks. You can adjust this threshold via **O&M** > **Alarm** > **Thresholds** > *Cluster name* > **Host** > **Process**.

This alarm is cleared when the full GC count of the NodeAgent process is less than or equal to the threshold.

.. note::

   This alarm applies only to MRS 3.6.0 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
12208    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------------+----------------------------------------------------------+
| Type                   | Parameter         | Description                                              |
+========================+===================+==========================================================+
| Location Information   | Source            | Specifies the cluster for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------+
|                        | ServiceName       | Specifies the service for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------+
|                        | RoleName          | Specifies the role for which the alarm was generated.    |
+------------------------+-------------------+----------------------------------------------------------+
|                        | HostName          | Specifies the host for which the alarm was generated.    |
+------------------------+-------------------+----------------------------------------------------------+
| Additional Information | Trigger condition | Specifies the alarm triggering condition.                |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

The monitoring data on the node cannot be properly reported. Frequent full GCs can cause slow command execution response on this node. In severe cases, it will lead to the restart of the node agent and the loss of heartbeat response from the controller.

Possible Causes
---------------

The memory usage of the NodeAgent process on the node is too high or the memory is inappropriately configured, resulting in frequent full GCs.

Handling Procedure
------------------

**Check the NodeAgent Full GC count**.

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the alarm list, expand the alarm details and click the name of the host generating the alarm in **Location** information.

#. On the **Dashboard** page of the host, check the "NodeAgent Full GC Counts" indicator in the **Charts** area, and verify if the Full GC count exceeds 1 (default).

   If no corresponding chart is available, click the drop-down arrow on the right side of the **Chart** area, click **Customize**, check the corresponding item, and click **OK**.

   -  If yes, go to :ref:`3 <alm-12208__en-us_topic_0000002149427148_en-us_topic_0000002165474553_li17254173220575>`.
   -  If no, go to :ref:`5 <alm-12208__en-us_topic_0000002149427148_en-us_topic_0000002165474553_li24184344163548>`.

3. .. _alm-12208__en-us_topic_0000002149427148_en-us_topic_0000002165474553_li17254173220575:

   Contact O&M personnel to modify the memory usage configuration of the process and restart it.

4. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-12208__en-us_topic_0000002149427148_en-us_topic_0000002165474553_li24184344163548>`.

**Collect fault information.**

5. .. _alm-12208__en-us_topic_0000002149427148_en-us_topic_0000002165474553_li24184344163548:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Select the **NodeAgent** of the target cluster for **Service**. For **Hosts**, select the host for which the alarm is reported.

7. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
