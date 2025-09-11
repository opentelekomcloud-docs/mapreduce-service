:original_name: ALM-45448.html

.. _ALM-45448:

ALM-45448 Rapid Increase of Znodes Used by ClickHouse
=====================================================

.. note::

   This section is available for MRS 3.3.1-LTS or later version only.

Alarm Description
-----------------

Metadata in ClickHouse is stored on ZooKeeper Znodes. The number of occupied Znodes may increase sharply even if service requirements do not change greatly. This alarm is generated when the number of occupied Znodes in two hours exceeds the threshold. If a large amount of data is imported or services are migrated, ignore this alarm.

This alarm is cleared when the system detects that the increase in two hours is lower than the threshold.

Alarm Attributes
----------------

======== ============== ================== ============ ============
Alarm ID Alarm Severity Alarm Type         Service Type Auto Cleared
======== ============== ================== ============ ============
45448    Major          Quality of service ClickHouse   Yes
======== ============== ================== ============ ============

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

ZooKeeper server resources are occupied. The number of Znodes will reach the upper limit in a short period of time, affecting the ClickHouse service.

Possible Causes
---------------

-  If the ClickHouse service volume retains at large scale, increase the value of **ZNODE_GROWTH_LIMIT** on the ClickHouse configuration page.
-  Major service changes, migration, and data import have been performed in ClickHouse.

Handling Procedure
------------------

#. Choose **Cluster** > **ClickHouse** > **Instances** > **All Configurations**, and search for **ZNODE_GROWTH_LIMIT**, increase the value of **ZNODE_GROWTH_LIMIT**. The default value is **100000**, the maximum value is **200000**, and the value is configured based a step of 50000. Wait for 2 hours and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`2 <alm-45448__li1965411520>`.

#. .. _alm-45448__li1965411520:

   Confirm with the service party whether there are new service requests or a large amount of data is imported or migrated during the period when the alarm is reported.

   -  If yes, go to :ref:`3 <alm-45448__li176869482515>`.
   -  If no, go to :ref:`4 <alm-45448__li1461914620531>`.

#. .. _alm-45448__li176869482515:

   Wait for 2 hours and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-45448__li1461914620531>`.

**Collect fault information.**

4. .. _alm-45448__li1461914620531:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

5. Expand the **Service** drop-down list, and select **ClickHouse** for the target cluster.

6. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the abnormal host, and click **OK**.

7. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
