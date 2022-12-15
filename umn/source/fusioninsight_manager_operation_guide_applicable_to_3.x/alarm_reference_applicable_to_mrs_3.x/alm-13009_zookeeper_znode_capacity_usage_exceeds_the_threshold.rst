:original_name: ALM-13009.html

.. _ALM-13009:

ALM-13009 ZooKeeper Znode Capacity Usage Exceeds the Threshold
==============================================================

Description
-----------

The system checks the level-2 ZNode status in the ZooKeeper data directory every hour. This alarm is generated when the system detects that the capacity usage exceeds the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
13009    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+-----------------------------------------------------------+
| Name              | Meaning                                                   |
+===================+===========================================================+
| Source            | Specifies the cluster for which the alarm is generated.   |
+-------------------+-----------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.   |
+-------------------+-----------------------------------------------------------+
| ServiceDirectory  | Specifies the directory for which the alarm is generated. |
+-------------------+-----------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.      |
+-------------------+-----------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.         |
+-------------------+-----------------------------------------------------------+

Impact on the System
--------------------

A large amount of data is written to the ZooKeeper data directory. As a result, ZooKeeper cannot provide services properly.

Possible Causes
---------------

-  A large volume of data has been written to the ZooKeeper data directory.
-  The threshold is improperly defined.

Procedure
---------

**Check whether a large volume of data is written to the alarm directory.**

#. On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. Click the drop-down list in the row containing **ALM-13009 ZooKeeper ZNode Capacity Usage Exceeds the Threshold**, and find the ZNode for which the alarm is generated in the **Location** area.

#. Choose **Cluster** > **Services** > **ZooKeeper**. On the page that is displayed, click the **Resource** tab. In the **Used Resources (By Second-Level ZNode)** area, click **By capacity** and check whether a large amount of data is written to the top-level ZNode directory.

   -  If yes, record the directory to which a large amount of data is written and go to :ref:`3 <alm-13009__li151971257113310>`.
   -  If no, go to :ref:`5 <alm-13009__li1932073512913>`.

#. .. _alm-13009__li151971257113310:

   Check whether data in the directory can be deleted.

   .. important::

      Deleting data from ZooKeeper is a high-risk operation. Exercise caution when performing this operation.

   -  If yes, go to :ref:`4 <alm-13009__li40737202161840>`.
   -  If no, go to :ref:`5 <alm-13009__li1932073512913>`.

#. .. _alm-13009__li40737202161840:

   Log in to the ZooKeeper client and delete unnecessary data from the directory to which a large amount of data is written.

   a. Log in to the ZooKeeper client installation directory, for example, **/opt/client**, and configure environment variables.

      **cd /opt/client**

      **source bigdata_env**

   b. Run the following command to authenticate the user (skip this step for a cluster in normal mode):

      **kinit** *Component service user*

   c. Run the following command to log in to the client tool:

      **zkCli.sh -server** **<**\ *Service IP address of the node where any ZooKeeper instance resides*\ **>:<**\ *Client port*\ **>**

   d. Run the following command to delete unnecessary data:

      **delete** *Path of the file to be deleted*

#. .. _alm-13009__li1932073512913:

   Log in to FusionInsight Manager and choose **Cluster** > **Services** > **ZooKeeper**. On the page that is displayed, click the **Configuration** tab then the **All Configurations** sub-tab, and search for **max.data.size**. The value of **max.data.size** is the maximum capacity quota of the ZooKeeper directory. The unit is byte. Search for the **GC_OPTS** configuration item and check the value of **Xmx**.

#. Compare the values of **max.data.size** and **Xmx*0.65**. The threshold is the smaller value multiplied by 80%. You can change the values of **max.data.size** and **Xmx*0.65** to increase the threshold.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-13009__li57092876161840>`.

**Collect the fault information.**

8.  .. _alm-13009__li57092876161840:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, and select **ZooKeeper** for the target cluster.

10. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0263895683.png
