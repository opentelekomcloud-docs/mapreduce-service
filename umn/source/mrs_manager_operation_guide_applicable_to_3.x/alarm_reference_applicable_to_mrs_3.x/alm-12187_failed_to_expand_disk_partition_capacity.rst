:original_name: ALM-12187.html

.. _ALM-12187:

ALM-12187 Failed to Expand Disk Partition Capacity
==================================================

Alarm Description
-----------------

The system checks the disk space every 60 seconds. When detecting that the disk space is expanded, the system expands disk partition. This alarm is generated when the disk partition fails to be expanded.

This alarm is cleared when the system detects that the disk partition is successfully expanded.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
12187    Minor          Yes
======== ============== ============

Alarm Parameters
----------------

+--------------------+-------------------------------------------------------------------+
| Parameter          | Description                                                       |
+====================+===================================================================+
| Source             | Specifies the cluster or system for which the alarm is generated. |
+--------------------+-------------------------------------------------------------------+
| ServiceName        | Specifies the service for which the alarm is generated.           |
+--------------------+-------------------------------------------------------------------+
| RoleName           | Specifies the role for which the alarm is generated.              |
+--------------------+-------------------------------------------------------------------+
| HostName           | Specifies the host for which the alarm is generated.              |
+--------------------+-------------------------------------------------------------------+
| MountDirectoryName | Specifies the directory for which the alarm is generated.         |
+--------------------+-------------------------------------------------------------------+

Impact on the System
--------------------

The expanded data disk space cannot be used to store data.

Possible Causes
---------------

-  The growpart scale-out tool is not installed.
-  The system fails to execute the command for expanding disk partition.

Handling Procedure
------------------

**Check whether growpart is installed.**

#. Log in to FusionInsight Manager, click **O&M**, and choose **Alarm** > **Alarms** to view the alarm details. In the **Location** column, check the name of the host and mount directory for which the alarm is generated. Click the host name to view its IP address.

#. Log in to the node for which the alarm is generated as user **root**.

#. Run the following command to check whether growpart is installed:

   **which growpart**

   If information similar to the following is displayed, the growpart tool is installed. Otherwise, contact O&M personnel to install the growpart tool.

   .. code-block:: console

      [root@xxx ~]#which growpart
      /usr/bin/growpart

4. Wait for 5 minutes, then choose **O&M**, and choose **Alarm** > **Alarms** on FusionInsight Manager. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-12187__li88865011163>`.

**Run the disk partition expansion command.**

5. .. _alm-12187__li88865011163:

   Run the following command to view the disk and partition information:

   **lsblk**

   Search for the partition and the disk based on the mount directory name in the alarm location information, and check the disk and partition sizes.

   In the following example, the mount directory is **/srv/BigData/data1**, the used disk is **/dev/vdb**, and the disk partition is **/dev/vdb1**.

   |image1|

6. Run the following command to expand the partition using growpart:

   **growpart** *Data disk Partition number*

   Run the following command:

   **growpart /dev/vdb 1**

   If information similar to the following is displayed, the execution is successful. If the execution fails, contact O&M personnel.

   |image2|

7. Run the following command to expand the file system size of the disk partition:

   **resize2fs** *Disk partition*

   Run the following command:

   **resize2fs /dev/vdb1**

   If information similar to the following is displayed, the execution is successful:

   |image3|

8. Wait for 5 minutes, click **O&M**, and choose **Alarm** > **Alarms** on FusionInsight Manager. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, contact O&M personnel.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000002008258969.png
.. |image2| image:: /_static/images/en-us_image_0000001971659208.png
.. |image3| image:: /_static/images/en-us_image_0000001971818980.png
