:original_name: ALM-50222.html

.. _ALM-50222:

ALM-50222 Disk Status of a Specified Data Directory on BE Is Abnormal
=====================================================================

Alarm Description
-----------------

The system checks the disk status of a specified data directory on BE every 30 seconds. This alarm is generated when the disk status is not **1** (**1** indicates the normal state and **0** indicates the abnormal state). This alarm is cleared when the disk status of the specified data directory on BE becomes normal.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50222    Critical       Yes
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

Service data may be unavailable.

Possible Causes
---------------

-  The hard disk is faulty.
-  The disk permissions are set incorrectly.

Handling Procedure
------------------

**Check whether a disk alarm is generated.**

#. On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms** and check whether **ALM-12014 Partition Lost** or **ALM-12033 Slow Disk Fault** exists.

   -  If yes, go to :ref:`2 <alm-50222__li106705312711>`.
   -  If no, go to :ref:`4 <alm-50222__li76681531273>`.

#. .. _alm-50222__li106705312711:

   Rectify the fault by referring to the handling procedure of **ALM-12014 Partition Lost** or **ALM-12033 Slow Disk Fault**. Then, check whether the alarm is cleared.

   -  If yes, go to :ref:`3 <alm-50222__li1067073192717>`.
   -  If no, go to :ref:`4 <alm-50222__li76681531273>`.

#. .. _alm-50222__li1067073192717:

   Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-50222__li76681531273>`.

**Modify disk permissions.**

4. .. _alm-50222__li76681531273:

   Choose **O&M** > **Alarm** > **Alarms** and view **Location** and **Additional Information** of the alarm to obtain the location of the faulty disk.

5. Log in to the node for which the alarm is generated as user **root**. Go to the directory where the faulty disk is located, and run the **ll** command to check whether the permission for the faulty disk is **711** and whether the user is **omm**.

   -  If yes, go to :ref:`7 <alm-50222__li3669433276>`.
   -  If no, go to :ref:`6 <alm-50222__li188961329122819>`.

6. .. _alm-50222__li188961329122819:

   Modify the permission of the faulty disk. For example, if the faulty disk is **data1**, run the following commands:

   **chown omm:wheel data1**

   **chmod 711 data1**

7. .. _alm-50222__li3669433276:

   Choose **Cluster** > **Services** > **Doris** > **Instances**, select this BE instance, click **More**, and select **Restart Instance**. Wait 5 minutes and check whether an alarm is generated.

   -  If no, no further action is required.
   -  If yes, go to :ref:`8 <alm-50222__li206502049133310>`.

   .. important::

      During BE instance restart, the tasks running on BE nodes will fail. The tasks on BE nodes that are not restarted are not affected.

**Collect fault information.**

8.  .. _alm-50222__li206502049133310:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, and select **Doris** and **OMS** for the target cluster.

10. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 20 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
