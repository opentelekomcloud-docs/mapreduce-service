:original_name: ALM-50227.html

.. _ALM-50227:

ALM-50227 Concurrent Doris Tenant Queries Exceeds the Threshold
===============================================================

Alarm Description
-----------------

The system checks concurrent tenant queries on FE nodes every 30 seconds. This alarm is generated when the number exceeds the threshold (90% by default).

This alarm is cleared when the number of concurrent queries from the FE nodes falls below the threshold.

This alarm applies only to MRS 3.3.1 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50227    Major          Yes
======== ============== ============

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

Too many concurrent queries consume a large number of system resources. This leads to slow response and even request rejection.

Possible Causes
---------------

There is a large number of service requests.

Handling Procedure
------------------

**Check the actual number of concurrent tenant queries on FE nodes.**

#. Log in to MRS Manager and choose **O&M** > **Alarm** > **Alarms**. In the alarm list, view the role name and obtain the IP address of the instance in **Location** of the alarm whose ID is **50227**.

#. Choose **Cluster** > **Services** > **Doris** > **Instances**, select the FE instance for which the alarm is generated, and click **Chart**. Click **Tenant Resource** in the **Chart Category** pane, and check whether the actual number of concurrent queries in the **Number of Concurrent Tenant Queries** chart is greater than the threshold. The default value is 90%.

   -  If yes, go to :ref:`3 <alm-50227__en-us_topic_0000001823818764_li167041918143416>`.
   -  If no, go to :ref:`5 <alm-50227__en-us_topic_0000001823818764_li1770316189347>`.

#. .. _alm-50227__en-us_topic_0000001823818764_li167041918143416:

   Check whether a large number of tasks were being executed during the alarm period.

   -  If yes, go to :ref:`4 <alm-50227__en-us_topic_0000001823818764_li1704518193417>`.
   -  If no, go to :ref:`5 <alm-50227__en-us_topic_0000001823818764_li1770316189347>`.

#. .. _alm-50227__en-us_topic_0000001823818764_li1704518193417:

   On MRS Manager, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **Doris** > **Tenant Resources**. Increase the threshold value and trigger counts based on service requirements. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-50227__en-us_topic_0000001823818764_li1770316189347>`.

**Collect fault information.**

5. .. _alm-50227__en-us_topic_0000001823818764_li1770316189347:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Expand the **Service** drop-down list, and select **Doris** for the target cluster.

7. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the abnormal host, and click **OK**.

8. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
