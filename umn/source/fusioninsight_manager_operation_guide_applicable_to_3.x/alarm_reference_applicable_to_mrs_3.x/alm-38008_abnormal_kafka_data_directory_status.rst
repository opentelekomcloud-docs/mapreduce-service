:original_name: ALM-38008.html

.. _ALM-38008:

ALM-38008 Abnormal Kafka Data Directory Status
==============================================

Description
-----------

The system checks the Kafka data directory status every 60 seconds. This alarm is generated when the system detects that the status of a data directory is abnormal.

**Trigger Count** is set to **1**. This alarm is cleared when the data directory status becomes normal.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
38008    Major          Yes
======== ============== =====================

Parameters
----------

+-------------------+---------------------------------------------------------------------------+
| Name              | Meaning                                                                   |
+===================+===========================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                   |
+-------------------+---------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                   |
+-------------------+---------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                      |
+-------------------+---------------------------------------------------------------------------+
| HostName          | Specifies the host name for which the alarm is generated.                 |
+-------------------+---------------------------------------------------------------------------+
| DirName           | Specifies the directory name for which the alarm is generated.            |
+-------------------+---------------------------------------------------------------------------+
| Trigger Condition | Specifies the condition that the Kafka data directory status is abnormal. |
+-------------------+---------------------------------------------------------------------------+

Impact on the System
--------------------

If the Kafka data directory status is abnormal, the current replicas of all partitions in the data directory are brought offline, and the data directory status of multiple nodes is abnormal at the same time. As a result, some partitions may become unavailable.

Possible Causes
---------------

-  The data directory permission is tampered with.
-  The disk where the data directory is located is faulty.

Procedure
---------

**Check the permission on the faulty data directory.**

#. Find the host information in the alarm information and log in to the host.

#. .. _alm-38008__li1654108315440:

   In the alarm information, check whether the data directory and its subdirectories belong to the omm:wheel group.

   -  If yes, record the host name of the node and go to :ref:`4 <alm-38008__li7931254192720>`.
   -  If no, go to :ref:`3 <alm-38008__li1465202115440>`.

#. .. _alm-38008__li1465202115440:

   Restore the owner group of the data directory and its subdirectories to omm:wheel.

   -  If yes, go to :ref:`6 <alm-38008__li1893217544278>`.
   -  If no, go to :ref:`5 <alm-38008__li4931105420275>`.

**Check whether the disk where the data directory is located is faulty.**

4. .. _alm-38008__li7931254192720:

   In the upper-level directory of the data directory, create and delete files as user **omm**. Check whether data read/write on the disk is normal.

5. .. _alm-38008__li4931105420275:

   Replace or repair the disk where the data directory is located to ensure that data read/write on the disk is normal.

6. .. _alm-38008__li1893217544278:

   On the FusionInsight Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** > **Instance**. On the Kafka instance page that is displayed, restart the Broker instance on the host recorded in :ref:`2 <alm-38008__li1654108315440>`.

7. After Broker is started, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-38008__li783366415440>`.

**Collect fault information.**

8.  .. _alm-38008__li783366415440:

    On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

9.  In the **Service** area, select **Kafka** in the required cluster.

10. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269417506.png
