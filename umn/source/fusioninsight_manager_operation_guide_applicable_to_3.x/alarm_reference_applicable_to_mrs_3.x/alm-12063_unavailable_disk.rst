:original_name: ALM-12063.html

.. _ALM-12063:

ALM-12063 Unavailable Disk
==========================

Description
-----------

The system checks whether the data disk of the current host is available at the top of each hour. The system creates files, writes files, and deletes files in the mount directory of the disk. If the operations fail, the alarm is generated. If the operations succeed, the disk is available, and the alarm is cleared.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12063    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+---------------------------------------------------------------------+
| Parameter   | Description                                                         |
+=============+=====================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated.   |
+-------------+---------------------------------------------------------------------+
| ServiceName | Specifies the name of the service for which the alarm is generated. |
+-------------+---------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.                |
+-------------+---------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.                |
+-------------+---------------------------------------------------------------------+
| DiskName    | Specifies the disk for which the alarm is generated.                |
+-------------+---------------------------------------------------------------------+

Impact on the System
--------------------

Data read or write on the data disk fails, and services are abnormal.

Possible Causes
---------------

-  The permission of the disk mount directory is abnormal.
-  There are disk bad sectors.

Procedure
---------

**Check whether the permission of the disk mount directory is normal.**

#. In the alarm list on FusionInsight Manager, locate the row that contains the alarm, and view the IP address of the host and **DiskName** for the disk for which the alarm is generated.
#. Log in to the host where the alarm is generated as user **root**.
#. Run the **df -h \|grep DiskName** command to obtain the mount point and check whether the permission of the mount directory is unwritable or unreadable.

   -  If it is, go to :ref:`4 <alm-12063__li1053537184512>`.
   -  If it is not, go to :ref:`8 <alm-12063__li8140111212587>`.

      .. note::

         If the permission of the mount directory is 000 or the owner is **root**, the mount directory is unreadable and unwritable.

4. .. _alm-12063__li1053537184512:

   Modify the directory permission.

5. One hour later, check whether this alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`6 <alm-12063__li4535871458>`.

6. .. _alm-12063__li4535871458:

   Contact hardware engineers to rectify the disk.

7. One hour later, check whether this alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`8 <alm-12063__li8140111212587>`.

**Collect fault information.**

8.  .. _alm-12063__li8140111212587:

    On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

9.  Select **NodeAgent** from the **Service** and click **OK**.

10. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583087405.png
