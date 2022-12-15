:original_name: alm_12051.html

.. _alm_12051:

ALM-12051 Disk Inode Usage Exceeds the Threshold
================================================

Description
-----------

The system checks the disk inode usage every 30 seconds. This alarm is generated when the disk inode usage exceeds the threshold (the default threshold is 80%) for multiple times (the default value is 5).

You can change the threshold by choosing **System** > **Threshold Configuration** > **Device** > **Host** > **Disk** > **Disk Inode Usage** > **Disk Inode Usage**.

If the **hit number** is **1**, this alarm is cleared when the disk inode usage is less than or equal to the threshold. If the **hit number** is greater than **1**, this alarm is cleared when the disk inode usage is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12051    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+----------------------------------------------------------------+
| Parameter         | Description                                                    |
+===================+================================================================+
| ServiceName       | Specifies the service for which the alarm is generated.        |
+-------------------+----------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.           |
+-------------------+----------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.           |
+-------------------+----------------------------------------------------------------+
| PartitionName     | Specifies the disk partition for which the alarm is generated. |
+-------------------+----------------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.              |
+-------------------+----------------------------------------------------------------+

Impact on the System
--------------------

Data cannot be written to the file system.

Possible Causes
---------------

-  There are too many small files on the disk.
-  The system is abnormal.

Procedure
---------

**There are too many small files on the disk.**

#. Go to the MRS cluster details page and choose **Alarms**.

#. In the real-time alarm list, click the alarm. In the **Alarm Details** area, obtain the IP address and disk partitions of the host for which the alarm is generated.

#. Use PuTTY to log in to the host for which the alarm is generated as user **root**.

#. Run the **df -i** *partition name* command to check the current inode usage of the disk.

#. If the inode usage exceeds the threshold, manually check whether the small files in the partition can be deleted.

   -  If yes, delete the files and go to :ref:`6 <alm_12051__en-us_topic_0191813886_en-us_topic_0087039294_li4609093115844>`.
   -  If no, adjust the capacity. Then go to :ref:`7 <alm_12051__en-us_topic_0191813886_en-us_topic_0087039294_li946980415844>`.

#. .. _alm_12051__en-us_topic_0191813886_en-us_topic_0087039294_li4609093115844:

   Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm_12051__en-us_topic_0191813886_en-us_topic_0087039294_li946980415844>`.

**Check whether the system environment is normal.**

7. .. _alm_12051__en-us_topic_0191813886_en-us_topic_0087039294_li946980415844:

   Contact the operating system maintenance personnel to check whether the system environment is abnormal.

   -  If yes, rectify the operating system fault and go to :ref:`8 <alm_12051__en-us_topic_0191813886_en-us_topic_0087039294_li1457809415844>`.
   -  If no, go to :ref:`9 <alm_12051__en-us_topic_0191813886_li572522141314>`.

8. .. _alm_12051__en-us_topic_0191813886_en-us_topic_0087039294_li1457809415844:

   Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm_12051__en-us_topic_0191813886_li572522141314>`.

9. .. _alm_12051__en-us_topic_0191813886_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
