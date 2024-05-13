:original_name: ALM-45428.html

.. _ALM-45428:

ALM-45428 ClickHouse Disk I/O Exception
=======================================

Description
-----------

This alarm is generated when the alarm module detects EIO or EROFS errors during ClickHouse read and write every 60 seconds.

Attribute
---------

======== =============== ==========
Alarm ID Alarm Severity  Auto Clear
======== =============== ==========
45428    Major (default) No
======== =============== ==========

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

-  ClickHouse fails to read and write data. The INSERT, SELECT, and CREATE operations on the local tables may be abnormal. Distributed tables are not affected.
-  Services are affected, and I/Os fail.

Possible Causes
---------------

The disk is aged or has bad sectors.

Procedure
---------

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms** > **ALM-45428 ClickHouse Disk I/O Exception**. Check the role name and the IP address of the host where the alarm is generated in **Location**.
#. Use PuTTY to log in to the node for which the fault is generated as user **root**.
#. Run the **df -h** command to check the mount directory and find the disk mounted to the faulty directory.
#. Run the **smartctl -a /dev/sd\*** command to check disks.

   -  If **SMART Health Status: OK** is displayed, as shown in the following figure, the disk is healthy. In this case, go to :ref:`6 <alm-45428__li186532017115614>`.

      |image1|

   -  If the number following **Elements in grown defect list** is not 0, as shown in the following figure, the disk may have bad sectors. If **SMART Health Status: FAILURE** is displayed, the disk is in the sub-health state. In this case, contact O&M personnel.

      |image2|

#. After the fault is rectified, manually clear the alarm on MRS Manager and check whether the alarm is generated again during the periodic check.

   -  If yes, go to :ref:`6 <alm-45428__li186532017115614>`.
   -  If no, no further action is required.

**Collect the fault information.**

6.  .. _alm-45428__li186532017115614:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7.  Expand the **Service** drop-down list, and select **ClickHouse** for the target cluster.

8.  Choose the corresponding host form the host list.

9.  Click |image3| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

If the alarm has no impact, manually clear the alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582807689.png
.. |image2| image:: /_static/images/en-us_image_0000001583127381.png
.. |image3| image:: /_static/images/en-us_image_0000001582927637.png
