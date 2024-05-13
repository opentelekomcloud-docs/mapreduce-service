:original_name: ALM-13010.html

.. _ALM-13010:

ALM-13010 Znode Usage of a Directory with Quota Configured Exceeds the Threshold
================================================================================

Description
-----------

The system checks the Znode usage of all service directories with quota configured every hour. This alarm is generated when the system detects that the level-2 Znode usage exceeds the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
13010    Major          Yes
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

#. On MRS Manager, choose **O&M** > **Alarm > Alarms**. Confirm the Znode for which the alarm is generated in **Location** of this alarm.

#. Choose **Cluster** > *Name of the desired cluster* > **Services** > **ZooKeeper** and click **Resource**. In **Used Resources (By Second-Level Znode)**, check whether a large amount of data is written into the top Znode.

   -  If yes, go to :ref:`3 <alm-13010__li19446131612914>`.
   -  If no, go to :ref:`5 <alm-13010__li598192363510>`.

#. .. _alm-13010__li19446131612914:

   Log in to MRS Manager, choose **O&M > Alarm > Alarms**, select Location from the drop-down list box next to **ALM-13010 Znode Usage of a Directory with Quota Configured Exceeds the Threshold**, and obtain the Znode path in ServiceDirectory.

#. Log in to the ZooKeeper client as a cluster user and delete unwanted data in the Znode for which the alarm is generated.

#. .. _alm-13010__li598192363510:

   Log in to MRS Manager, and choose **Cluster** > *Name of the desired cluster* > **Services** > *Component of the top Znode for which the alarm isgenerated*. Choose **Configurations** > **All Configurations**, search for **zk.quota.number**, increase its value, click **Save**.

   .. important::

      If the Component of the top Znode for which the alarm isgenerated is ClickHouse, change the value of **clickhouse.zookeeper.quota.node.count**.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-13010__li13978523123518>`.

**Collect fault information.**

7.  .. _alm-13010__li13978523123518:

    On the MRS Manager portal, choose **O&M** > **Log > Download**.

8.  Select **ZooKeeper** in the required cluster from the **Service**.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583087329.png
