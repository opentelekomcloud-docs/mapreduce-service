:original_name: ALM-50228.html

.. _ALM-50228:

ALM-50228 Memory Usage of a Doris Tenant Exceeds the Threshold
==============================================================

Alarm Description
-----------------

The system checks the memory usage of BE nodes every 30 seconds. This alarm is generated when the memory usage of a tenant exceeds the threshold.

This alarm is cleared when the system detects that the memory usage of tenant's BE nodes is lower than the threshold.

This alarm applies only to MRS 3.3.1 or later.

Alarm Attributes
----------------

+-----------------------+-----------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                    | Auto Cleared          |
+=======================+===================================+=======================+
| 50228                 | Critical (default threshold: 90%) | Yes                   |
|                       |                                   |                       |
|                       | Major (default threshold: 85%)    |                       |
+-----------------------+-----------------------------------+-----------------------+

Alarm Parameters
----------------

+------------------------+-------------+--------------------------------------------------------------------+
| Type                   | Parameter   | Description                                                        |
+========================+=============+====================================================================+
| Location Information   | Source      | Specifies the cluster or system for which the alarm was generated. |
+------------------------+-------------+--------------------------------------------------------------------+
|                        | ServiceName | Specifies the service for which the alarm was generated.           |
+------------------------+-------------+--------------------------------------------------------------------+
|                        | RoleName    | Specifies the role for which the alarm was generated.              |
+------------------------+-------------+--------------------------------------------------------------------+
|                        | HostName    | Specifies the host for which the alarm was generated.              |
+------------------------+-------------+--------------------------------------------------------------------+
| Additional Information | Detail      | Specifies the alarm triggering condition.                          |
+------------------------+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

Processes respond slowly or do not work.

Possible Causes
---------------

The data queried by the tenant is too large, and memory soft limit is not enabled.

Handling Procedure
------------------

**Check the memory used by the BE nodes of the tenant.**

#. Log in to MRS Manager and choose **O&M** > **Alarm** > **Alarms**. In the alarm list, view the role name and obtain the IP address of the instance in **Location** of the alarm whose ID is **50228**.

#. .. _alm-50228__en-us_topic_0000001870498537_li368143145912:

   Click **Thresholds** and choose *Name of the desired cluster* > **Doris** > **Tenant Resources** > **Memory Usage Exceeds Threshold** to view and record the threshold.

#. .. _alm-50228__en-us_topic_0000001870498537_li2681431115919:

   Choose **Cluster** > **Services** > **Doris** > **Instances**, select the BE instance for which the alarm is generated, and click **Chart**. Select **Tenant Resource** from the **Chart Category** pane, check whether the actual memory usage in the **Memory Used by Tenants** chart is greater than the threshold obtained in :ref:`2 <alm-50228__en-us_topic_0000001870498537_li368143145912>`, and record the name of the tenant whose memory usage exceeds the threshold.

   -  If yes, go to :ref:`3 <alm-50228__en-us_topic_0000001870498537_li2681431115919>`.
   -  If no, go to :ref:`8 <alm-50228__en-us_topic_0000001870498537_li16671231185913>`.

#. Check whether a large amount of table data were being queried during the alarm period.

   -  If yes, go to :ref:`5 <alm-50228__en-us_topic_0000001870498537_li1368123145916>`.
   -  If no, go to :ref:`8 <alm-50228__en-us_topic_0000001870498537_li16671231185913>`.

#. .. _alm-50228__en-us_topic_0000001870498537_li1368123145916:

   Choose **Tenant Resources** > **Tenant Resources Management**. In the tenant list, click the tenant name in :ref:`2 <alm-50228__en-us_topic_0000001870498537_li368143145912>`, and then the **Resource** tab. Click the edit button on the right of **Resource Details**, and check whether **Memory Soft Limit** is enabled.

   -  If yes, go to :ref:`7 <alm-50228__en-us_topic_0000001870498537_li15691331155917>`.
   -  If no, go to :ref:`6 <alm-50228__en-us_topic_0000001870498537_li5691431175911>`.

#. .. _alm-50228__en-us_topic_0000001870498537_li5691431175911:

   Enable **Soft Memory Limit** and click **OK**. Check whether the alarm is cleared in the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-50228__en-us_topic_0000001870498537_li15691331155917>`.

#. .. _alm-50228__en-us_topic_0000001870498537_li15691331155917:

   Choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **Doris** > **Tenant Resources**. Increase the threshold value and trigger counts based on service requirements. Check whether the alarm is cleared in the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-50228__en-us_topic_0000001870498537_li16671231185913>`.

**Collect fault information.**

8.  .. _alm-50228__en-us_topic_0000001870498537_li16671231185913:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, and select **Doris** for the target cluster.

10. In the Host area, select the host to which the role belongs and click OK.

11. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
