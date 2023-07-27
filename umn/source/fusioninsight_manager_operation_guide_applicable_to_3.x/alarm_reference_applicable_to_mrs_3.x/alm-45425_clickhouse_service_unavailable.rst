:original_name: ALM-45425.html

.. _ALM-45425:

ALM-45425 ClickHouse Service Unavailable
========================================

Description
-----------

The alarm module checks the ClickHouse instance status every 60 seconds. This alarm is generated when the alarm module detects that all ClickHouse instances are abnormal.

This alarm is cleared when the system detects that any ClickHouse instance is restored and the alarm is cleared.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45425    Critical       Yes
======== ============== ==========

Parameters
----------

+-------------+-------------------------------------------------------------------+
| Name        | Meaning                                                           |
+=============+===================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated. |
+-------------+-------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.           |
+-------------+-------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

The ClickHouse service is abnormal. You cannot use FusionInsight Manager to perform cluster operations on the ClickHouse service. The ClickHouse service function is unavailable.

Possible Causes
---------------

The configuration information in the **metrika.xml** file in the component configuration directory of the faulty ClickHouse instance node is inconsistent with that of the corresponding ClickHouse instance in the ZooKeeper.

Procedure
---------

**Check whether the configuration in metrika.xml of the ClickHouse instance is correct.**

#. Log in to FusionInsight Manager, choose **Cluster** > **Services** > **ClickHouse** > **Instance**, and locate the abnormal ClickHouse instance based on the alarm information.

   -  If yes, go to :ref:`2 <alm-45425__li237743710398>`.
   -  If no, go to :ref:`9 <alm-45425__li62779304563>`.

#. .. _alm-45425__li237743710398:

   Log in to the host where the ClickHouse service is abnormal and ping the IP address of another normal ClickHouse instance node to check whether the network connection is normal.

   -  If yes, go to :ref:`3 <alm-45425__li156597363713>`.
   -  If no, contact the network administrator to repair the network.

3. .. _alm-45425__li156597363713:

   Choose **Cluster** > **Services** > **ClickHouse** > **Instance**, click the abnormal instance name in the **Role** column, click **Configurations**, search for **macros.id** in the search box, and find the value of **macros.id** of the current instance.

4. Log in to the host where the ZooKeeper client is located and log in to the ZooKeeper client.

   Switch to the client installation directory.

   Example: **cd /opt/client**

   Run the following command to configure environment variables:

   **source bigdata_env**

   Run the following command to authenticate the user (skip this step in common mode):

   **kinit** *Component service user*

   Run the following command to log in to the client tool:

   **zkCli.sh -server** *service IP address of the node where the ZooKeeper role instance locates*\ **:**\ *client port*

5. .. _alm-45425__li1377133713911:

   Run the following command to check whether the ClickHouse cluster topology information can be obtained.

   **get /clickhouse/config/**\ *value of* **macros.id** *in* :ref:`3 <alm-45425__li156597363713>`/metrika.xml

   -  If yes, go to :ref:`6 <alm-45425__li1462431320505>`.
   -  If no, go to :ref:`9 <alm-45425__li62779304563>`.

6. .. _alm-45425__li1462431320505:

   Log in to the host where the ClickHouse instance is abnormal and go to the configuration directory of the ClickHouse instance.

   **cd** ${BIGDATA_HOME}\ **/FusionInsight_ClickHouse\_**\ *Version*\ **/**\ x_x\ **\_ClickHouseServer/etc**

   **cat metrika.xml**

7. Check whether the cluster topology information on ZooKeeper obtained in :ref:`5 <alm-45425__li1377133713911>` is the same as that in the **metrika.xml** file in the component configuration directory in :ref:`6 <alm-45425__li1462431320505>`.

   -  If yes, check whether the alarm is cleared. If the alarm persists, go to :ref:`9 <alm-45425__li62779304563>`.
   -  If no, go to :ref:`8 <alm-45425__li113661428132312>`.

8. .. _alm-45425__li113661428132312:

   On FusionInsight Manager, choose **Cluster** > **Services** > **ClickHouse**, click **More**, and select **Synchronize Configuration**. Then, check whether the service status is normal and whether the alarm is cleared 5 minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-45425__li62779304563>`.

**Collect the fault information.**

9.  .. _alm-45425__li62779304563:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

10. Expand the **Service** drop-down list, and select **ClickHouse** for the target cluster.

11. Choose the corresponding host form the host list.

12. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

13. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532448422.png
