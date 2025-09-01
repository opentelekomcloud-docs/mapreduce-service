:original_name: ALM-45452.html

.. _ALM-45452:

ALM-45452 ClickHouse's Local Disk Space Is Below the Cold-Hot Separation Threshold
==================================================================================

.. note::

   This section is available for MRS 3.3.1-LTS or later version only.

Alarm Description
-----------------

When cold-hot separation is enabled, the system checks the remaining space of the local disk specified in the cold-hot separation policy every 5 minutes. This alarm is generated if the remaining space is lower than the **move_factor** threshold.

This alarm is automatically cleared when the remaining space of the local disk is greater than the **move_factor** threshold.

Alarm Attributes
----------------

======== ============== ================== ============ ============
Alarm ID Alarm Severity Alarm Type         Service Type Auto Cleared
======== ============== ================== ============ ============
45452    Major          Quality of service ClickHouse   Yes
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

Some hot data on the local disk is moved to OBS, affecting the read and write performance of the system.

Possible Causes
---------------

The local disk capacity configured for cold-hot separation on the ClickHouseServer node is too small.

Handling Procedure
------------------

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and view the role name and the IP address of the hostname in **Location**.
#. Expand the disk capacity of the node for which the alarm is generated.
#. Check whether the alarm is cleared after disk expansion.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-45452__li1314322683817>`.

**Collect fault information.**

4. .. _alm-45452__li1314322683817:

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
