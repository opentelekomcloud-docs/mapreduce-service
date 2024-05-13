:original_name: ALM-12014.html

.. _ALM-12014:

ALM-12014 Partition Lost
========================

Description
-----------

The system checks the partition status every 60 seconds. This alarm is generated when the system detects that a partition to which service directories are mounted is lost (because the device is removed or goes offline, or the partition is deleted). The system checks the partition status periodically.

This alarm must be manually cleared.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12014    Major          No
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

-  The hard disk is removed.
-  The hard disk is offline, or a bad sector exists on the hard disk.

Procedure
---------

#. On MRS Manager, click **O&M > Alarm > Alarms**, and click |image1| in the row where the alarm is located.

#. Obtain **HostName**, **PartitionName** and **DirName** from **Location**.

#. Check whether the disk of **PartitionName** on **HostName** is inserted to the correct server slot.

   -  If yes, go to :ref:`4 <alm-12014__li9631929173421>`.
   -  If no, go to :ref:`5 <alm-12014__li18162941173421>`.

#. .. _alm-12014__li9631929173421:

   Contact hardware engineers to remove the faulty disk.

#. .. _alm-12014__li18162941173421:

   Log in to the **HostName** node where an alarm is reported and check whether there is a line containing **DirName** in the **/etc/fstab** file as user **root**.

   -  If yes, go to :ref:`6 <alm-12014__li20338192173421>`.
   -  If no, go to :ref:`7 <alm-12014__li48826004173421>`.

#. .. _alm-12014__li20338192173421:

   Run the **vi /etc/fstab** command to edit the file and delete the line containing **DirName**.

#. .. _alm-12014__li48826004173421:

   Contact hardware engineers to insert a new disk. For details, see the hardware product document of the relevant model. If the faulty disk is in a RAID group, configure the RAID group. For details, see the configuration methods of the relevant RAID controller card.

#. Wait 20 to 30 minutes (The disk size determines the waiting time), and run the **mount** command to check whether the disk has been mounted to the **DirName** directory.

   -  If yes, manually clear the alarm. No further operation is required.
   -  If no, go to :ref:`9 <alm-12014__li1607193817587>`.

**Collect fault information.**

9.  .. _alm-12014__li1607193817587:

    On the MRS Manager, choose **O&M** > **Log > Download**.

10. Select the **OmmServer** from the Services drop-down list and click **OK**.

11. Set Start Date for log collection to 10 minutes ahead of the alarm generation time and End Date to 10 minutes behind the alarm generation time and click **Download**.

12. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system does not automatically clear this alarm, and you need to manually clear the alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532767638.png
