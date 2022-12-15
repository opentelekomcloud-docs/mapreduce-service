:original_name: ALM-16047.html

.. _ALM-16047:

ALM-16047 HiveServer Has Been Deregistered from ZooKeeper
=========================================================

Description
-----------

The system checks the Hive service every 60 seconds. This alarm is generated when Hive registration information on ZooKeeper is lost or Hive cannot connect to ZooKeeper.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
16047    Major          Yes
======== ============== ==========

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

If the Hive configuration cannot be read from ZooKeeper, HiveServer will be unavailable.

Possible Causes
---------------

-  The network is disconnected.
-  The ZooKeeper instance is abnormal.

Procedure
---------

**Restart related instances.**

#. Log in to FusionInsight Manager. Choose **O&M** > **Alarm** > **Alarms**, click the drop-down list in the row that contains the alarm, and view role and the IP address of the node for which the alarm is generated in **Location**.
#. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Hive** > **Instance**, select the instance at the IP address for which the alarm is generated, and choose **More** > **Restart Instance**.
#. Wait for 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-16047__li57092876161840>`.

**Collect the fault information.**

4. .. _alm-16047__li57092876161840:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

5. Expand the **Service** drop-down list, and select **Hive** for the target cluster.

6. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

7. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0263895811.png
