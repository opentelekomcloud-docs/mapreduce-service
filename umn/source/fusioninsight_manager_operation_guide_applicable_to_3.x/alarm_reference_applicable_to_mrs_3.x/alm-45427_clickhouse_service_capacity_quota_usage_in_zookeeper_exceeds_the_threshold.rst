:original_name: ALM-45427.html

.. _ALM-45427:

ALM-45427 ClickHouse Service Capacity Quota Usage in ZooKeeper Exceeds the Threshold
====================================================================================

Description
-----------

The alarm module checks the quota usage of the ClickHouse service in the ZooKeeper every 60 seconds. This alarm is generated when the alarm module detects that the usage exceeds the threshold (90%).

This alarm is cleared when the system detects that the usage is lower than the threshold and the alarm is cleared.

Attribute
---------

======== =============== ==========
Alarm ID Alarm Severity  Auto Clear
======== =============== ==========
45427    Major (default) Yes
======== =============== ==========

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

After the ZooKeeper quantity quota of the ClickHouse service exceeds the threshold, you cannot perform cluster operations on the ClickHouse service on FusionInsight Manager. As a result, the ClickHouse service cannot be used.

Possible Causes
---------------

-  When table data is created, inserted, or deleted, the ClickHouse creates znodes on ZooKeeper nodes. As the service volume increases, the capacity of znodes may exceed the configured threshold.
-  No quota limit is set for the metadata directory **/clickhouse** of ClickHouse in ZooKeeper.

Procedure
---------

**Check the znode capacity of the ClickHouse in the ZooKeeper.**

#. .. _alm-45427__li19429132053415:

   Log in to the host where the ZooKeeper client is located and log in to the ZooKeeper client.

   Switch to the client installation directory.

   Example: **cd /opt/client**

   Run the following command to configure environment variables:

   **source bigdata_env**

   Run the following command to authenticate the user (skip this step in common mode):

   **kinit** *Component service user*

   Run the following command to log in to the client tool:

   **zkCli.sh -server** *service IP address of the node where the ZooKeeper role instance locates*\ **:**\ *client port*

#. Run the following command to check the quota used by the ClickHouse in the ZooKeeper and check whether the quota information is correctly set:

   **listquota /clickhouse**

   .. code-block::

      absolute path is /zookeeper/quota/clickhouse
      Quota for path /clickhouse does not exist.

   -  If the preceding information indicates that the quota configuration is incorrect, go to :ref:`3 <alm-45427__li17669171018349>`.
   -  If not, go to :ref:`5 <alm-45427__li10833143016438>`.

#. .. _alm-45427__li17669171018349:

   Log in to FusionInsight Manager and choose **Cluster** > **Services** > **ZooKeeper**. On the displayed page, click **Configurations** and click **All Configurations**. On this sub-tab page, search for **quotas.auto.check.enable** to check whether its value is **true**.

   If the value is not **true**, change the value to **true** and click **Save**.

#. On FusionInsight Manager, choose **Cluster** > **Services** > **ClickHouse**, click **More**, and select **Synchronize Configuration**. After the synchronization is successful, go to :ref:`1 <alm-45427__li19429132053415>`.

#. .. _alm-45427__li10833143016438:

   Run the following command and check whether the ratio of the **bytes** value of **Output stat** to the **bytes** value of **Output quota** in the command output is greater than **0.9**:

   **listquota /clickhouse**

   .. code-block::

      absolute path is /zookeeper/quota/clickhouse
      Output quota for /clickhouse count=200000,bytes=1000000000
      Output stat for /clickhouse count=2667,bytes=60063

   In the preceding information, the **bytes** value of **Output stat** is **60063**, and the **bytes** value of **Output quota** is **1000000000**.

   -  If yes, go to :ref:`6 <alm-45427__li157515124315>`.
   -  If no, check whether the alarm is cleared 5 minutes later. If the alarm persists, go to :ref:`8 <alm-45427__li1460181994211>`.

#. .. _alm-45427__li157515124315:

   On FusionInsight Manager, choose **Cluster** > **Services** > **ClickHouse** > **Configurations** > **All Configurations**, search for the **clickhouse.zookeeper.quota.size** parameter, and change the value of this parameter to twice the **bytes** value of **Output stat** in :ref:`5 <alm-45427__li10833143016438>`.

#. Restart the ClickHouse instance for which the alarm is generated, and check whether the alarm is cleared 5 minutes later.

   -  If yes, no further action is required.
   -  If no, perform :ref:`6 <alm-45427__li157515124315>` again, and check whether the alarm is cleared 5 minutes later. If the alarm persists, go to :ref:`8 <alm-45427__li1460181994211>`.

**Collect the fault information.**

8.  .. _alm-45427__li1460181994211:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, and select **ClickHouse** for the target cluster.

10. Choose the corresponding host form the host list.

11. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0295706662.png
