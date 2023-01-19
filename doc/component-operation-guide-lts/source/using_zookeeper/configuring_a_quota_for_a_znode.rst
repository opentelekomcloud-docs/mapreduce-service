:original_name: mrs_01_2104.html

.. _mrs_01_2104:

Configuring a Quota for a Znode
===============================

Scenario
--------

Set a quota for Znodes in ZooKeeper of a security cluster in O&M scenarios or service scenarios to restrict the quantity and byte space of Znodes and subnodes.

Two modes are available:

-  On Manager, enable the automatic quota setting function and set related configuration items to enable the ZooKeeper service to automatically set the Znode quota. For details, see :ref:`1 <mrs_01_2104__en-us_topic_0000001219231125_li39081429191111>` to :ref:`8 <mrs_01_2104__en-us_topic_0000001219231125_li1991010290113>`.
-  On Manager, disable the automatic quota setting function and run commands on the client to manually set the Znode quota. For details, see :ref:`1 <mrs_01_2104__en-us_topic_0000001219231125_li39081429191111>` to :ref:`3 <mrs_01_2104__en-us_topic_0000001219231125_li1190922991115>`.

Impact on the System
--------------------

If the configured quantity or capacity quota is less than the quantity or capacity of directories required for normal service running, services may fail to run properly. Exercise cautions when setting the quota.

Prerequisites
-------------

The ZooKeeper client has been installed in a directory, for example, **/opt/client**.

Procedure
---------

**Use the automatic quota setting function.**

#. .. _mrs_01_2104__en-us_topic_0000001219231125_li39081429191111:

   Go to the **All Configurations** page of ZooKeeper. Click the **Quota** tab and set **quotas.auto.check.enable** to **true**, and click **Save**. For details, see :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.

#. Determine whether to set the quota of the top directory (for example, Yarn service) on ZooKeeper.

   -  If yes, go to :ref:`3 <mrs_01_2104__en-us_topic_0000001219231125_li1190922991115>`.
   -  If no, go to :ref:`5 <mrs_01_2104__en-us_topic_0000001219231125_li149104295112>`.

#. .. _mrs_01_2104__en-us_topic_0000001219231125_li1190922991115:

   Go to the **All Configurations** page of Yarn by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>` and search for **zk.quota**.

#. Set the following quotas properly and click Save. The ZooKeeper service periodically sets the quota of the Yarn service on the top directory of ZooKeeper.

   a. **zk.quota.number** indicates the directory quota of the service on ZooKeeper.
   b. **zk.quota.bytes** indicates the capacity quota of the service directory on ZooKeeper.

   .. note::

      If the configured quantity or capacity quota is less than the actual quantity or capacity quota of the current directory, the setting can be saved successfully. However, an alarm indicating that the setting is invalid is displayed on the page, prompting you to reset the quota.

      If the configured quantity or capacity quota is less than the quantity or capacity of directories required for normal service running, services may fail to run properly. Exercise cautions when setting the quota.

#. .. _mrs_01_2104__en-us_topic_0000001219231125_li149104295112:

   Check whether quotas of other custom top directories except service directories need to be configured.

   -  If yes, go to :ref:`6 <mrs_01_2104__en-us_topic_0000001219231125_li5910829141117>`.
   -  If no, no further action is required.

#. .. _mrs_01_2104__en-us_topic_0000001219231125_li5910829141117:

   Go to the **All Configurations** page of ZooKeeper and click the **Quota** tab.

#. Enter the top directory (for example, **/abc**) of ZooKeeper in the **Value** text box of **customized.quota**.

#. .. _mrs_01_2104__en-us_topic_0000001219231125_li1991010290113:

   In the **Value** text box, enter the quantity quota and capacity quota separated by a comma (,). (You can also set only the quantity quota). If you need to set quotas for multiple top directories, click **+** to add quotas. Click **Save**. The ZooKeeper service automatically sets the quota of the top directory periodically. No further action is required.

   .. note::

      The entered quantity quota cannot be greater than the value of **max.znode.count**. The entered capacity quota cannot be greater than the value of **max.data.size**.

      If the top directory on ZooKeeper is not the top directory of a service, and its quota is not specified using **customized.quota**, the ZooKeeper service sets the quota to the value of **defaultQuota**.

**Run commands on the client.**

9.  Go to the **All Configurations** page of ZooKeeper. Click the **Quota** tab and set **quotas.auto.check.enable** to **false**, and click **Save**.
10. Start the ZooKeeper client. For details, see :ref:`Using a ZooKeeper Client <mrs_01_2095>`.

    .. note::

       In security mode, user authentication is required to start the ZooKeeper client. The ZooKeeper user (system administrator of ZooKeeper) is used for authentication, and the **kinit zookeeper** command is executed.

11. Run the **setquota** /*znode* **-n** *number* **-b** *byte* command.

    -  *znode* indicates the node for which you want to set a quota.
    -  *number* indicates the maximum number of nodes and subnodes.
    -  *byte* indicates the maximum byte space for the node and subnodes.
