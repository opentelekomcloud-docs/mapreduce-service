:original_name: alm_12015.html

.. _alm_12015:

ALM-12015 Device Partition File System Read-Only
================================================

Description
-----------

This alarm is generated when the system detects that a partition to which service directories are mounted enters the read-only mode (due to a bad sector or a faulty file system). The system checks the partition status periodically.

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

+---------------+------------------------------------------------------------------+
| Parameter     | Description                                                      |
+===============+==================================================================+
| ServiceName   | Specifies the service for which the alarm is generated.          |
+---------------+------------------------------------------------------------------+
| RoleName      | Specifies the role for which the alarm is generated.             |
+---------------+------------------------------------------------------------------+
| HostName      | Specifies the host for which the alarm is generated.             |
+---------------+------------------------------------------------------------------+
| DirName       | Specifies the directory for which the alarm is generated.        |
+---------------+------------------------------------------------------------------+
| PartitionName | Specifies the device partition for which the alarm is generated. |
+---------------+------------------------------------------------------------------+

Impact on the System
--------------------

Service data fails to be written into the partition, and the service system runs abnormally.

Possible Causes
---------------

The disk is faulty, for example, a bad sector exists.

Procedure
---------

#. Go to the MRS cluster details page and choose **Alarms**.
#. In the real-time alarm list, click the row that contains the alarm.
#. In the **Alarm Details** area, obtain **HostName** and **PartitionName** from **Location**. **HostName** indicates the node for which the alarm is generated, and **PartitionName** indicates the partition of the faulty disk.
#. Contact hardware engineers to check whether the disk is faulty. If the disk is faulty, remove it from the server.
#. After the disk is removed, the system reports ALM-12014 Partition Lost. Handle the alarm by following the instructions in :ref:`ALM-12014 Device Partition Lost <alm_12014>`. After the handling, the alarm is automatically cleared.

Reference
---------

None
