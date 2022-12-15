:original_name: alm_12014.html

.. _alm_12014:

ALM-12014 Device Partition Lost
===============================

Description
-----------

This alarm is generated when the system detects that a partition to which service directories are mounted is lost (because the device is removed or goes offline, or the partition is deleted). The system checks the partition status periodically.

This alarm needs to be cleared manually.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12014    Major          No
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

-  The disk is removed.
-  The disk is offline, or a bad sector exists on the disk.

Procedure
---------

#. Go to the MRS cluster details page and choose **Alarms**.

#. In the real-time alarm list, click the row that contains the alarm.

#. In the **Alarm Details** area, obtain the values of **HostName**, **PartitionName**, and **DirName** from **Location**.

#. Check whether the disk corresponding to **PartitionName** on **HostName** is inserted to the correct server slot.

   -  If yes, go to :ref:`5 <alm_12014__en-us_topic_0191813950_li1456274715359>`.
   -  If no, go to :ref:`6 <alm_12014__en-us_topic_0191813950_li6395586615359>`.

#. .. _alm_12014__en-us_topic_0191813950_li1456274715359:

   Contact hardware engineers to remove the faulty disk.

#. .. _alm_12014__en-us_topic_0191813950_li6395586615359:

   Use PuTTY to log in to the **HostName** node where an alarm is reported and check whether there is a line containing **DirName** in the **/etc/fstab** file.

   -  If yes, go to :ref:`7 <alm_12014__en-us_topic_0191813950_li921471615359>`.
   -  If no, go to :ref:`8 <alm_12014__en-us_topic_0191813950_li819455015359>`.

#. .. _alm_12014__en-us_topic_0191813950_li921471615359:

   Run the **vi /etc/fstab** command to edit the file and delete the line containing **DirName**.

#. .. _alm_12014__en-us_topic_0191813950_li819455015359:

   Contact hardware engineers to insert a new disk. For details, see the hardware product document of the relevant model. If the faulty disk is in a RAID group, configure the RAID group. For details, see the configuration methods of the relevant RAID controller card.

#. Wait 20 to 30 minutes (The disk size determines the waiting time), and run the **mount** command to check whether the disk has been mounted to the **DirName** directory.

   -  If yes, manually clear the alarm. No further operation is required.
   -  If no, go to :ref:`10 <alm_12014__en-us_topic_0191813950_li572522141314>`.

#. .. _alm_12014__en-us_topic_0191813950_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
