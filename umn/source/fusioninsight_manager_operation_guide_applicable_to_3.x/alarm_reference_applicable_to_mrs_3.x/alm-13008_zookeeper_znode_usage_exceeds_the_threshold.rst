:original_name: ALM-13008.html

.. _ALM-13008:

ALM-13008 ZooKeeper Znode Usage Exceeds the Threshold
=====================================================

Description
-----------

The system checks the level-2 Znode status in the ZooKeeper data directory every hour. This alarm is generated when the system detects that the level-2 Znode usage exceeds the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
13008    Major          Yes
======== ============== =====================

Parameters
----------

+-------------------+--------------------------------------------------------------+
| Name              | Meaning                                                      |
+===================+==============================================================+
| Source            | Specifies the cluster for which the alarm is generated.      |
+-------------------+--------------------------------------------------------------+
| ServiceName       | Specifies the service name for which the alarm is generated. |
+-------------------+--------------------------------------------------------------+
| ServiceDirectory  | Specifies the directory for which the alarm is generated.    |
+-------------------+--------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.         |
+-------------------+--------------------------------------------------------------+
| Trigger Condition | Specifies the cause of the alarm.                            |
+-------------------+--------------------------------------------------------------+

Impact on the System
--------------------

A large amount of data is written to the ZooKeeper data directory. As a result, ZooKeeper cannot provide services properly.

Possible Causes
---------------

-  A large amount of data is written to the ZooKeeper data directory.
-  The user-defined threshold is inappropriate.

Procedure
---------

**Check whether a large amount of data is written into the directory for which the alarm is generated.**

#. Log in to FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **ZooKeeper**, and click **Resource**. Click **By Znode quantity** in **Used Resources (By Second-Level Znode)**, and check whether a large amount of data is written to the top Znode.

   -  If yes, go to :ref:`2 <alm-13008__li787172215383>`.
   -  If no, go to :ref:`4 <alm-13008__li10279134491613>`.

#. .. _alm-13008__li787172215383:

   Log in to FusionInsight Manager, choose **O&M > Alarm > Alarms**, select **Location** from the drop-down list box next to **ALM-13008 ZooKeeper Znode Quantity Usage Exceeds Threshold**, and obtain the Znode path in **ServiceDirectory**.

#. Log in to the ZooKeeper client as a cluster user and delete unnecessary data from the Znode corresponding to the alarm.

#. .. _alm-13008__li10279134491613:

   Log in to FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **ZooKeeper** > **Configurations** > **All Configurations**, and search for **max.znode.count**, which is the maximum number of ZooKeeper directories. The alarm threshold is 80% of this parameter. Increase the value of this parameter, click **Save**, and restart the service for the configuration to take effect.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-13008__li180651333416>`.

**Collect fault information.**

6. .. _alm-13008__li180651333416:

   On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

7. Select **ZooKeeper** in the required cluster from the **Service**.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383953.png
