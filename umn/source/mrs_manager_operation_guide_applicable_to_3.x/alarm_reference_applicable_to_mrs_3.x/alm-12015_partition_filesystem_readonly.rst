:original_name: ALM-12015.html

.. _ALM-12015:

ALM-12015 Partition Filesystem Readonly
=======================================

Description
-----------

The system checks the partition status every 60 seconds. This alarm is generated when the system detects that a partition to which service directories are mounted enters the read-only mode (due to a bad sector or a faulty file system). The system checks the partition status periodically.

This alarm is cleared when the system detects that the partition to which service directories are mounted exits from the read-only mode (because the file system is restored to read/write mode, the device is removed, or the device is formatted).

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12015    Major          Yes
======== ============== ==========

Parameters
----------

+---------------+-------------------------------------------------------------------+
| Name          | Meaning                                                           |
+===============+===================================================================+
| Source        | Specifies the cluster or system for which the alarm is generated. |
+---------------+-------------------------------------------------------------------+
| ServiceName   | Specifies the service for which the alarm is generated.           |
+---------------+-------------------------------------------------------------------+
| RoleName      | Specifies the role for which the alarm is generated.              |
+---------------+-------------------------------------------------------------------+
| HostName      | Specifies the host for which the alarm is generated.              |
+---------------+-------------------------------------------------------------------+
| DirName       | Specifies the directory for which the alarm is generated.         |
+---------------+-------------------------------------------------------------------+
| PartitionName | Specifies the device partition for which the alarm is generated.  |
+---------------+-------------------------------------------------------------------+

Impact on the System
--------------------

Service data fails to be written into the partition, and the service system runs abnormally.

Possible Causes
---------------

The hard disk is faulty, for example, a bad sector exists.

Procedure
---------

#. On MRS Manager, choose **O&M** > **Alarm > Alarms**, click |image1| in the row where the alarm is located.
#. Obtain **HostName** and **PartitionName** from **Location**. **HostName** is the node where the alarm is reported, and **PartitionName** is the partition of the faulty disk.
#. Contact hardware engineers to check whether the disk is faulty. If the disk is faulty, remove it from the server.
#. After the disk is removed, alarm **ALM-12014 Partition Lost** is reported. Handle the alarm. For details, see :ref:`ALM-12014 Partition Lost <alm-12014>`. After the alarm **ALM-12014 Partition Lost** is cleared, alarm **ALM-12015 Partition Filesystem Readonly** is automatically cleared.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582807717.png
