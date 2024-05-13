:original_name: ALM-12033.html

.. _ALM-12033:

ALM-12033 Slow Disk Fault
=========================

Description
-----------

-  For HDDs, the alarm is triggered when any of the following conditions is met:

   -  The system runs the **iostat** command every 3 seconds, and detects that the **svctm** value exceeds 1000 ms for 7 consecutive periods within 30 seconds.
   -  The system runs the **iostat** command every 3 seconds, and detects that more than 50% of I/Os take more than 150 ms within 300s.

-  For SSDs, the alarm is triggered when any of the following conditions is met:

   -  The system runs the **iostat** command every 3 seconds, and detects that the **svctm** value exceeds 1000 ms for 10 consecutive periods within 30 seconds.
   -  The system runs the **iostat** command every 3 seconds, and detects that more than 60% of I/Os take more than 20 ms within 300 seconds.

This alarm is automatically cleared when the preceding conditions have not been met for 15 minutes.

.. note::

   The **svctm** value can be obtained as follows:

   -  MRS 3.1.0:

      Run the **iostat -x -t** command in the OS.

      |image1|

   -  Versions later than MRS 3.1.0:

   svctm = (tot_ticks_new - tot_ticks_old)/(rd_ios_new + wr_ios_new - rd_ios_old - wr_ios_old)

   If **rd_ios_new + wr_ios_new - rd_ios_old - wr_ios_old** is **0**, then **svctm** is **0**.

   The parameters can be obtained as follows:

   The system runs the **cat /proc/diskstats** command every 3 seconds to collect data. For example:

   |image2|

   In these two commands:

   In the data collected for the first time, the number in the fourth column is the **rd_ios_old** value, the number in the eighth column is the **wr_ios_old** value, and the number in the thirteenth column is the **tot_ticks_old** value.

   In the data collected for the second time, the number in the fourth column is the **rd_ios_new** value, the number in the eighth column is the **wr_ios_new** value, and the number in the thirteenth column is the **tot_ticks_new** value.

   In this case, the value of **svctm** is as follows:

   (19571460 - 19569526)/(1101553 + 28747977 - 1101553 - 28744856) = 0.6197

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12033    Minor          Yes
======== ============== ==========

Parameters
----------

+-------------+-------------------------------------------------------------------+
| Name        | Meaning                                                           |
+=============+===================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated. |
+-------------+-------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.           |
+-------------+-------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+
| DiskName    | Specifies the disk for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

Service performance deteriorates, service processing capabilities become poor, and services may be unavailable.

Possible Causes
---------------

The disk is aged or has bad sectors.

Procedure
---------

**Check the disk status.**

#. On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**.

#. .. _alm-12033__li3788291791458:

   View the detailed information about the alarm. Check the values of **HostName** and **DiskName** in the location information to obtain the information about the faulty disk for which the alarm is generated.

#. Check whether the node for which the alarm is generated is in a virtualization environment.

   -  If yes, go to :ref:`4 <alm-12033__li2831628891458>`.
   -  If no, go to :ref:`7 <alm-12033__li2583597491458>`.

#. .. _alm-12033__li2831628891458:

   Check whether the storage performance provided by the virtualization environment meets the hardware requirements. Then, go to :ref:`5 <alm-12033__li1205527419227>`.

#. .. _alm-12033__li1205527419227:

   Log in to the alarm node as user **root**, run the **df -h** command, and check whether the command output contains the value of the **DiskName** field.

   -  If yes, go to :ref:`7 <alm-12033__li2583597491458>`.
   -  If no, go to :ref:`6 <alm-12033__li2325719119312>`.

#. .. _alm-12033__li2325719119312:

   Run the **lsblk** command to check whether the mapping between the value of **DiskName** and the disk has been created.

   |image3|

   -  If yes, go to :ref:`7 <alm-12033__li2583597491458>`. .
   -  If no, go to :ref:`22 <alm-12033__li4518231891458>`.

#. .. _alm-12033__li2583597491458:

   Log in to the alarm node as user **root**, run the **lsscsi \| grep "/dev/sd[x]"** command to view the disk information, and check whether RAID has been set up.

   .. note::

      In the command, **/dev/sd[x]** indicates the disk name obtained in :ref:`2 <alm-12033__li3788291791458>`.

   Example:

   **lsscsi \| grep "/dev/sda"**

   In the command output, if **ATA**, **SATA**, or **SAS** is displayed in the third line, the disk has not been organized into a RAID group. If other information is displayed, RAID has been set up.

   -  If yes, go to :ref:`12 <alm-12033__li1471607091458>`.
   -  If no, go to :ref:`8 <alm-12033__li523387391458>`.

#. .. _alm-12033__li523387391458:

   Run the **smartctl -i /dev/sd[x]** command to check whether the hardware supports the SMART tool.

   Example:

   **smartctl -i /dev/sda**

   In the command output, if "SMART support is: Enabled" is displayed, the hardware supports SMART. If "Device does not support SMART" or other information is displayed, the hardware does not support SMART.

   -  If yes, go to :ref:`9 <alm-12033__li3483730991458>`.
   -  If no, go to :ref:`17 <alm-12033__li3381567991458>`.

#. .. _alm-12033__li3483730991458:

   Run the **smartctl -H --all /dev/sd[x]** command to check basic SMART information and determine whether the disk is working properly.

   Example:

   **smartctl -H --all /dev/sda**

   Check the value of **SMART overall-health self-assessment test result** in the command output. If the value is **FAILED**, the disk is faulty and needs to be replaced. If the value is **PASSED**, check the value of **Reallocated_Sector_Ct** or **Elements in grown defect list**. If the value is greater than 100, the disk is faulty and needs to be replaced.

   -  If yes, go to :ref:`10 <alm-12033__li1145378391458>`.
   -  If no, go to :ref:`18 <alm-12033__li6235920691458>`.

#. .. _alm-12033__li1145378391458:

   Run the **smartctl -l error -H /dev/sd[x]** command to check the Glist of the disk and determine whether the disk is normal.

   Example:

   **smartctl -l error -H /dev/sda**

   Check the **Command/Feature_name** column in the command output. If **READ SECTOR(S)** or **WRITE SECTOR(S)** is displayed, the disk has bad sectors. If other errors occur, the disk circuit board is faulty. Both errors indicate that the disk is abnormal and needs to be replaced.

   If "No Errors Logged" is displayed, no error log exists. You can trigger the disk SMART self-check.

   -  If yes, go to :ref:`11 <alm-12033__li2167780691458>`.
   -  If no, go to :ref:`18 <alm-12033__li6235920691458>`.

#. .. _alm-12033__li2167780691458:

   Run the **smartctl -t long /dev/sd[x]** command to trigger the disk SMART self-check. After the command is executed, the time when the self-check is to be completed is displayed. After the self-check is completed, repeat :ref:`9 <alm-12033__li3483730991458>` and :ref:`10 <alm-12033__li1145378391458>` to check whether the disk is working properly.

   Example:

   **smartctl -t long /dev/sda**

   -  If yes, go to :ref:`17 <alm-12033__li3381567991458>`.
   -  If no, go to :ref:`18 <alm-12033__li6235920691458>`.

#. .. _alm-12033__li1471607091458:

   Run the **smartctl -d [sat|scsi]+megaraid,[DID] -H --all /dev/sd[x]** command to check whether the hardware supports SMART.

   .. note::

      -  In the command, **[sat|scsi]** indicates the disk type. Both types need to be used.
      -  **[DID]** indicates the slot information. Slots 0 to 15 need to be used.

   For example, run the following commands in sequence:

   **smartctl -d sat+megaraid,0 -H --all /dev/sda**

   **smartctl -d sat+megaraid,1 -H --all /dev/sda**

   **smartctl -d sat+megaraid,2 -H --all /dev/sda**

   ...

   Try the command combinations of different disk types and slot information. If "SMART support is: Enabled" is displayed in the command output, the disk supports SMART. Record the parameters of the disk type and slot information when a command is successfully executed. If "SMART support is: Enabled" is not displayed in the command output, the disk does not support SMART.

   -  If yes, go to :ref:`13 <alm-12033__li4568369291458>`.
   -  If no, go to :ref:`16 <alm-12033__li1606413991458>`.

#. .. _alm-12033__li4568369291458:

   Run the **smartctl -d [sat|scsi]+megaraid,[DID] -H --all /dev/sd[x]** command recorded in :ref:`12 <alm-12033__li1471607091458>` to check basic SMART information and determine whether the disk is normal.

   Example:

   **smartctl -d sat+megaraid,2 -H --all /dev/sda**

   Check the value of **SMART overall-health self-assessment test result** in the command output. If the value is **FAILED**, the disk is faulty and needs to be replaced. If the value is **PASSED**, check the value of **Reallocated_Sector_Ct** or **Elements in grown defect list**. If the value is greater than 100, the disk is faulty and needs to be replaced.

   -  If yes, go to :ref:`14 <alm-12033__li5027541391458>`.
   -  If no, go to :ref:`18 <alm-12033__li6235920691458>`.

#. .. _alm-12033__li5027541391458:

   Run the **smartctl -d [sat|scsi]+megaraid,[DID] -l error -H /dev/sd[x]** command to check the Glist of the disk and determine whether the hard disk is working properly.

   Example:

   **smartctl -d sat+megaraid,2 -l error -H /dev/sda**

   Check the **Command/Feature_name** column in the command output. If **READ SECTOR(S)** or **WRITE SECTOR(S)** is displayed, the disk has bad sectors. If other errors occur, the disk circuit board is faulty. Both errors indicate that the disk is abnormal and needs to be replaced.

   If "No Errors Logged" is displayed, no error log exists. You can trigger the disk SMART self-check.

   -  If yes, go to :ref:`15 <alm-12033__li1119862391458>`.
   -  If no, go to :ref:`18 <alm-12033__li6235920691458>`.

#. .. _alm-12033__li1119862391458:

   Run the **smartctl -d [sat|scsi]+megaraid,[DID] -t long /dev/sd[x]** command to trigger the disk SMART self-check. After the command is executed, the time when the self-check is to be completed is displayed. After the self-check is completed, repeat :ref:`13 <alm-12033__li4568369291458>` and :ref:`14 <alm-12033__li5027541391458>` to check whether the disk is working properly.

   Example:

   **smartctl -d sat+megaraid,2 -t long /dev/sda**

   -  If yes, go to :ref:`17 <alm-12033__li3381567991458>`.
   -  If no, go to :ref:`18 <alm-12033__li6235920691458>`.

#. .. _alm-12033__li1606413991458:

   If the configured RAID controller card does not support SMART, the disk does not support SMART. In this case, use the check tool provided by the corresponding RAID controller card vendor to rectify the fault. Then go to :ref:`17 <alm-12033__li3381567991458>`.

   For example, LSI is a MegaCLI tool.

#. .. _alm-12033__li3381567991458:

   On MRS Manager, choose **O&M** > **Alarm** > **Alarms**, click **Clear** in the **Operation** column of the alarm, and check whether the alarm is reported on the same disk again.

   If the alarm is reported for three times, replace the disk.

   -  If yes, go to :ref:`18 <alm-12033__li6235920691458>`.
   -  If no, no further action is required.

**Replace the disk.**

18. .. _alm-12033__li6235920691458:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**.

19. View the detailed information about the alarm. Check the values of **HostName** and **DiskName** in the location information to obtain the information about the faulty disk for which the alarm is reported.

20. Replace the disk.

21. Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`22 <alm-12033__li4518231891458>`.

**Collect the fault information.**

22. .. _alm-12033__li4518231891458:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

23. Select **OMS** for **Service** and click **OK**.

24. Click |image4| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

25. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583087321.png
.. |image2| image:: /_static/images/en-us_image_0000001582807613.png
.. |image3| image:: /_static/images/en-us_image_0000001583127305.jpg
.. |image4| image:: /_static/images/en-us_image_0000001532927338.png
