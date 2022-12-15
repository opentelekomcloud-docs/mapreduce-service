:original_name: ALM-14027.html

.. _ALM-14027:

ALM-14027 DataNode Disk Fault
=============================

Description
-----------

The system checks the disk status on DataNodes every 60 seconds. This alarm is generated when a disk is faulty.

After all faulty disks on the DataNode are recovered, you need to manually clear the alarm and restart the DataNode.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14027    Major          No
======== ============== ==========

Parameters
----------

============== =======================================================
Name           Meaning
============== =======================================================
Source         Specifies the cluster for which the alarm is generated.
ServiceName    Specifies the service for which the alarm is generated.
RoleName       Specifies the role for which the alarm is generated.
HostName       Specifies the host for which the alarm is generated.
Failed Volumes Specifies the list of faulty disks.
============== =======================================================

Impact on the System
--------------------

If this alarm is reported, there are abnormal disk partitions on the DataNode. This may cause the loss of written files.

Possible Causes
---------------

-  The hard disk is faulty.
-  The disk permissions are configured improperly.

Procedure
---------

**Check whether a disk alarm is generated.**

#. On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms** and check whether **ALM-12014 Partition Lost** or **ALM-12033 Slow Disk Fault** exists.

   -  If yes, go to :ref:`2 <alm-14027__li106705312711>`.
   -  If no, go to :ref:`4 <alm-14027__li76681531273>`.

#. .. _alm-14027__li106705312711:

   Rectify the fault by referring to the handling procedure of **ALM-12014 Partition Lost** or **ALM-12033 Slow Disk Fault**. Then, check whether the alarm is cleared.

   -  If yes, go to :ref:`3 <alm-14027__li1067073192717>`.
   -  If no, go to :ref:`4 <alm-14027__li76681531273>`.

#. .. _alm-14027__li1067073192717:

   Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-14027__li76681531273>`.

**Modify disk permissions.**

4. .. _alm-14027__li76681531273:

   Choose **O&M** > **Alarm** > **Alarms** and view **Location** and **Additional Information** of the alarm to obtain the location of the faulty disk.

5. Log in to the node for which the alarm is generated as user **root**. Go to the directory where the faulty disk is located, and run the **ll** command to check whether the permission of the faulty disk is **711** and whether the user is **omm**.

   -  If yes, go to :ref:`8 <alm-14027__li206502049133310>`.
   -  If no, go to :ref:`6 <alm-14027__li188961329122819>`.

6. .. _alm-14027__li188961329122819:

   Modify the permission of the faulty disk. For example, if the faulty disk is **data1**, run the following commands:

   **chown omm:wheel data1**

   **chmod 711 data1**

7. In the alarm list on Manager, click **Clear** in the **Operation** column of the alarm to manually clear the alarm. Choose **Cluster** > **Services** > **HDFS** > **Instance**, select the DataNode, choose **More** > **Restart Instance**, wait for 5 minutes, and check whether a new alarm is reported.

   -  If no, no further action is required.
   -  If yes, go to :ref:`8 <alm-14027__li206502049133310>`.

**Collect the fault information.**

8.  .. _alm-14027__li206502049133310:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, and select **HDFS** and **OMS** for the target cluster.

10. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 20 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system does not automatically clear this alarm and you need to manually clear the alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0263895589.png
