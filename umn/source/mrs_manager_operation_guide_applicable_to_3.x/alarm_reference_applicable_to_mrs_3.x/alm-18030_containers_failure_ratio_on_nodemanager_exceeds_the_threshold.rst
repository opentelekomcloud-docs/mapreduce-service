:original_name: ALM-18030.html

.. _ALM-18030:

ALM-18030 Container's Failure Ratio on NodeManager Exceeds the Threshold
========================================================================

Alarm Description
-----------------

NodeManager periodically checks the running status of the Container on an instance every 30 seconds. This alarm is triggered when Container's failure ratio exceeds the threshold for more than three consecutive occurrences.

The alarm is cleared when the Container's failure ratio on the NodeManager instance is lower than the threshold.

.. note::

   This alarm applies only to MRS 3.6.0 or later.

Alarm Attributes
----------------

+-----------------------+-----------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                    | Auto Cleared          |
+=======================+===================================+=======================+
| 18030                 | Critical (default threshold: 90%) | Yes                   |
|                       |                                   |                       |
|                       | Major (default threshold: 80%)    |                       |
+-----------------------+-----------------------------------+-----------------------+

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
| Additional Information | Trigger Condition | Specifies the alarm triggering condition.                |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

The tasks of upper-layer services (such as HBase and Spark) may fail, interrupting the upper-layer services.

Possible Causes
---------------

-  NodeManager's processing capability has reached the bottleneck.
-  The NodeManager instance configuration is improper or its key files may be damaged.

Handling Procedure
------------------

**Check whether the NodeManager's processing capability reaches a bottleneck.**

#. .. _alm-18030__en-us_topic_0000002204791261_en-us_topic_0000002199696401_li166717351206:

   Log in to MRS Manager, and choose **O&M** > **Alarm** > **Alarms**. View and record the NodeManager instance name reported in the alarm details.

#. In the alarm list, check if the alarm "ALM-18011 NodeManager GC Time Exceeds the Threshold" is reported and if the reported host name matches the one you obtained in :ref:`1 <alm-18030__en-us_topic_0000002204791261_en-us_topic_0000002199696401_li166717351206>`.

   -  If yes, go to :ref:`3 <alm-18030__en-us_topic_0000002204791261_en-us_topic_0000002199696401_li178785122417>`.
   -  If no, go to :ref:`5 <alm-18030__en-us_topic_0000002204791261_en-us_topic_0000002199696401_li7321724142718>`.

#. .. _alm-18030__en-us_topic_0000002204791261_en-us_topic_0000002199696401_li178785122417:

   Rectify the fault by following the handling procedure of "ALM-18011 NodeManager GC Time Exceeds the Threshold".

4. Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-18030__en-us_topic_0000002204791261_en-us_topic_0000002199696401_li7321724142718>`.

**Check whether the NodeManager configuration is improper.**

5. .. _alm-18030__en-us_topic_0000002204791261_en-us_topic_0000002199696401_li7321724142718:

   On MRS Manager, choose **Cluster** > **Services** > **Yarn** > **Instances**. Click the name of the NodeManager instance corresponding to the host obtained in :ref:`1 <alm-18030__en-us_topic_0000002204791261_en-us_topic_0000002199696401_li166717351206>`.

6. Choose **Configurations** > **All Configurations** > **System**. Check if the system parameters for the NodeManager instance are appropriately set. If not, adjust the settings, save the changes, and choose **More** > **Restart Instance** in the upper right corner. After passing password verification, restart the instance.

7. Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-18030__en-us_topic_0000002204791261_en-us_topic_0000002199696401_li7307174513810>`.

**Collect fault information.**

8.  .. _alm-18030__en-us_topic_0000002204791261_en-us_topic_0000002199696401_li7307174513810:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, select **Yarn** for the target cluster, and click **OK**.

10. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
