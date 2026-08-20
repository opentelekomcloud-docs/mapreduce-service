:original_name: ALM-45453.html

.. _ALM-45453:

ALM-45453 Keeper Disconnected
=============================

.. note::

   This section applies only to MRS 3.6.0 and later versions.

Alarm Description
-----------------

The system checks the connection between ClickHouse and Keeper every minute. This alarm is generated when the system detects that the connection fails due to a connection exception or the connection fails for three consecutive times due to Keeper disconnection.

This alarm is automatically cleared when the system detects that the connection is normal.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45453    Critical       Yes
======== ============== ============

Alarm Parameters
----------------

+----------------------+-------------+--------------------------------------------------------------------+
| Type                 | Parameter   | Description                                                        |
+======================+=============+====================================================================+
| Location Information | Source      | Specifies the cluster or system for which the alarm was generated. |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | ServiceName | Specifies the service for which the alarm was generated.           |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | RoleName    | Specifies the role for which the alarm was generated.              |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | HostName    | Specifies the host for which the alarm was generated.              |
+----------------------+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

If ClickHouse is disconnected from Keeper, the ClickHouse service cannot be used.

Possible Causes
---------------

-  Keeper is abnormal.
-  The ClickHouse service is overloaded.

Handling Procedure
------------------

**Check whether ClickHouseKeeper is normal.**

#. On MRS Manager, choose **Cluster** > **Services** > **ClickHouse** > **ClickHouseKeeper**.

#. Check whether ClickHouseKeeper instances are normal.

   -  If yes, go to :ref:`6 <alm-45453__en-us_topic_0000002481675136_en-us_topic_0000002176758178_li15319205119354>`.
   -  If no, go to :ref:`3 <alm-45453__en-us_topic_0000002481675136_en-us_topic_0000002176758178_li1395215202>`.

#. .. _alm-45453__en-us_topic_0000002481675136_en-us_topic_0000002176758178_li1395215202:

   Select the instances whose status is not **Normal**, click **More**, and select **Restart Instance**.

#. Check whether the instance status becomes normal after the restart.

   -  If yes, go to :ref:`5 <alm-45453__en-us_topic_0000002481675136_en-us_topic_0000002176758178_li6946141915104>`.
   -  If no, go to :ref:`10 <alm-45453__en-us_topic_0000002481675136_en-us_topic_0000002176758178_li6769733151816>`.

#. .. _alm-45453__en-us_topic_0000002481675136_en-us_topic_0000002176758178_li6946141915104:

   Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-45453__en-us_topic_0000002481675136_en-us_topic_0000002176758178_li15319205119354>`.

**Check whether the ClickHouse service is overloaded.**

6. .. _alm-45453__en-us_topic_0000002481675136_en-us_topic_0000002176758178_li15319205119354:

   Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and view the role name and the IP address for the hostname in **Location**.

7. Log in to the node where the client is installed as the client installation user and run the following commands:

   **cd** *{Client installation path}*

   **source bigdata_env**

   -  For a cluster with Kerberos authentication enabled (security mode):

      **kinit** *Component service user*

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm is reported* **--port** 9440 **--secure**

   -  For a cluster with Kerberos authentication disabled (normal mode):

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm is reported* **--user** *Username* **--password --port** 9440

8. Check whether data is frequently written to the system table. If yes, wait until the service execution is complete and check whether the alarm is cleared.

   **SELECT query_id, user, FQDN(), elapsed, query FROM system.processes ORDER BY query_id;**

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-45453__en-us_topic_0000002481675136_en-us_topic_0000002176758178_li195348914449>`.

9. .. _alm-45453__en-us_topic_0000002481675136_en-us_topic_0000002176758178_li195348914449:

   Check whether a large amount of data is written. If yes, wait until the task is complete and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-45453__en-us_topic_0000002481675136_en-us_topic_0000002176758178_li6769733151816>`.

**Collect fault information.**

10. .. _alm-45453__en-us_topic_0000002481675136_en-us_topic_0000002176758178_li6769733151816:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

11. Expand the **Service** drop-down list, and select **ClickHouse** for the target cluster.

12. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the abnormal host, and click **OK**.

13. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
