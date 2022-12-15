:original_name: ALM-12051.html

.. _ALM-12051:

ALM-12051 Disk Inode Usage Exceeds the Threshold
================================================

Description
-----------

The system checks the disk Inode usage every 30 seconds and compares the actual Inode usage with the threshold (the default threshold is 80%). This alarm is generated when the Inode usage exceeds the threshold for several times (5 times by default) consecutively.

To change the threshold, choose **O&M > Alarm** > **Thresholds** > *Name of the desired cluster* > **Host** > **Disk** > **Disk Inode Usage**.

When the **Trigger Count** is 1, this alarm is cleared when the disk Inode usage is less than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the disk Inode usage is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12051    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster or system for which the alarm is generated.                                                            |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| PartitionName     | Specifies the disk partition for which the alarm is generated.                                                               |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

Data cannot be properly written to the file system.

Possible Causes
---------------

Massive small files are stored in the disk.

Procedure
---------

**Massive small files are stored in the disk.**

#. On FusionInsight Manager, choose **O&M > Alarm > Alarms** and click |image1| in the row where the alarm is located in the real-time alarm list and obtain the IP address of the host and the disk partition for which the alarm is generated.

#. Log in to the host for which the alarm is generated as user **root**.

#. Run the **df -i \| grep -iE "**\ *partition name\|*\ Filesystem" command to check the current disk Inode usage.

   .. code-block::

      # df -i | grep -iE "xvda2|Filesystem"
      Filesystem            Inodes   IUsed   IFree IUse% Mounted on
      /dev/xvda2           2359296  207420 2151876    9% /

#. If the Inode usage exceeds the threshold, manually check small files stored in the disk partition and confirm whether these small files can be deleted.

   .. note::

      Run the **for i in /*; do echo $i; find $i|wc -l;** **done** command to query the number of files in a partition. Replace **/\*** with the specified partition.

   .. code-block::

      # for i in /srv/*; do echo $i; find $i|wc -l; done
      /srv/BigData
      4284
      /srv/ftp
      1
      /srv/www
      13

   -  If yes, run the **rm -rf** *Path of the file or folder* to be deleted command to delete the file or folder and go to :ref:`5 <alm-12051__li52275864151050>`.

      .. note::

         Deleting a file or folder is a high-risk operation. Ensure that the file or folder is no longer required before performing this operation.

   -  If no, expand the capacity. Then, perform :ref:`5 <alm-12051__li52275864151050>`.

#. .. _alm-12051__li52275864151050:

   Wait for 5 minutes, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12051__li1819875814203>`.

**Collect fault information.**

6.  .. _alm-12051__li1819875814203:

    On the FusionInsight Manager home page of the active cluster, choose **O&M** > **Log > Download**.

7.  Select **OMS** from the **Service** and click **OK**.

8.  Set **Host** to the node for which the alarm is generated and the active OMS node.

9.  Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383877.png
.. |image2| image:: /_static/images/en-us_image_0269383878.png
