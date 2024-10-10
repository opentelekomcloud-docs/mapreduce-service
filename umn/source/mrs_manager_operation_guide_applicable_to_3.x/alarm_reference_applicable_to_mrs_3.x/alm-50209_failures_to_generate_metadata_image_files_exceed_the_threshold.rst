:original_name: ALM-50209.html

.. _ALM-50209:

ALM-50209 Failures to Generate Metadata Image Files Exceed the Threshold
========================================================================

Alarm Description
-----------------

The system checks the number of failures to generate metadata image files on the FE node every 30 seconds. This alarm is generated when the number of failures exceeds the threshold (**1** by default).

This alarm is cleared when the system detects that the number of failures is less than the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50209    Critical       Yes
======== ============== ============

Alarm Parameters
----------------

+-------------------+-------------------------------------------------------------------+
| Parameter         | Description                                                       |
+===================+===================================================================+
| Source            | Specifies the cluster or system for which the alarm is generated. |
+-------------------+-------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.           |
+-------------------+-------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.              |
+-------------------+-------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.              |
+-------------------+-------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.                 |
+-------------------+-------------------------------------------------------------------+

Impact on the System
--------------------

The non-master FE node cannot receive the latest metadata image file. As a result, the system reliability deteriorates.

Possible Causes
---------------

The Doris service is abnormal.

Handling Procedure
------------------

**Check the Doris service status.**

#. Log in to FusionInsight Manager and choose **Cluster** > **Services** > **Doris**.

#. Check whether **Running Status** of the Doris service is **Normal**.

   -  If yes, go to :ref:`4 <alm-50209__li141367308352>`.
   -  If no, go to :ref:`3 <alm-50209__li1265314513420>`.

#. .. _alm-50209__li1265314513420:

   If the service process is not started, start it first.

#. .. _alm-50209__li141367308352:

   Check whether other alarms are generated in the cluster. If yes, clear the alarms by referring to the alarm help. Then, check whether this alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-50209__li39839699173731>`.

**Collect fault information.**

5. .. _alm-50209__li39839699173731:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Expand the **Service** drop-down list, select **Doris** for the target cluster, and click **OK**.

7. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

You need to manually clear the alarm after the fault is rectified.

Related Information
-------------------

None.
