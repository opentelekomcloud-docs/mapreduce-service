:original_name: ALM-45430.html

.. _ALM-45430:

ALM-45430 Permission Metadata Synchronization Failed on the Added ClickHouse Node
=================================================================================

.. note::

   This section applies only to MRS 3.1.2-LTS.6 or later.

Description
-----------

This alarm is generated when user and permission information fails to be synchronized during ClickHouse capacity expansion.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45430    Major          No
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

The created user does not have operation permissions on the node.

Possible Causes
---------------

A node is stopped or faulty during capacity expansion.

Procedure
---------

#. On FusionInsight Manager, choose **Cluster** > **Services** > **ClickHouse** > **Instance**.

#. Check whether an instance is stopped, decommissioned, or faulty.

   -  If yes, go to :ref:`3 <alm-45430__li1857611153310>`.
   -  If no, go to :ref:`4 <alm-45430__li1457618110336>`.

#. .. _alm-45430__li1857611153310:

   Start the instance or rectify the instance fault until all instances are running properly.

#. .. _alm-45430__li1457618110336:

   On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**, locate this alarm and the faulty host based on the location information.

5. Log in to the faulty host as user **omm**.

6. Run the following commands to initialize environment variables:

   **source** *Cluster installation directory*\ **/FusionInsight_ClickHouse_*/*_*_ClickHouseServer/etc/ENV_VARS**

   **source** *Cluster installation directory*\ **/FusionInsight_ClickHouse_*/*_*_ClickHouseServer/etc/clickhouse-env.sh**

   **export CLICKHOUSE_CONF_DIR=${CLICKHOUSE_CONF_DIR}**

7. Run the following command to run the metadata synchronization tool to synchronize metadata from the existing node to the faulty node:

   **sh** *Cluster installation directory*\ **/FusionInsight_ClickHouse_*/install/FusionInsight-ClickHouse-*/clickhouse/sbin/clickhouse-create-meta.sh** **true**

8. Run the following command to view the log information and check whether the metadata has been synchronized:

   **vim /var/log/Bigdata/clickhouse/clickhouseServer/start.log**

   If the synchronization is complete, go to :ref:`9 <alm-45430__li185513552368>`.

   If the synchronization fails, go to :ref:`10 <alm-45430__li4749473185459>`.

9. .. _alm-45430__li185513552368:

   On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**. In the **Alarm ID** column, locate the corresponding alarm and click **Clear** in the **Operation** column. In the displayed dialog box, click **OK** to manually clear the alarm.

**Collect the fault information.**

10. .. _alm-45430__li4749473185459:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

11. Expand the **Service** drop-down list, select **ClickHouse** for the target cluster, and click **OK**.

12. Choose the corresponding host form the host list.

13. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.

14. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm needs to be manually cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532448154.png
