:original_name: ALM-45451.html

.. _ALM-45451:

ALM-45451 ClickHouse Failed to Access OBS
=========================================

.. note::

   This section is available for MRS 3.3.1-LTS or later version only.

Alarm Description
-----------------

When cold-hot separation is enabled, the system checks the OBS access every minute. This alarm is generated when the system detects that OBS cannot be accessed for three consecutive times.

This alarm is automatically cleared when the system successfully accesses OBS.

Alarm Attributes
----------------

======== ============== ================== ============ ============
Alarm ID Alarm Severity Alarm Type         Service Type Auto Cleared
======== ============== ================== ============ ============
45451    Critical       Quality of service ClickHouse   Yes
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

For tables configured with the cold-hot separation policy, cold data on OBS cannot be read or written. Hot data on local disks cannot be moved to OBS.

Possible Causes
---------------

-  Parameters such as the endpoint used by ClickHouse to access OBS are incorrect.
-  OBS is abnormal.

Handling Procedure
------------------

#. Check whether the cold and hot separation configuration is correct. If the configuration is incorrect, modify the configuration and restart the ClickHouse instance. Wait for 3 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`2 <alm-45451__li1314322683817>`.

**Collect fault information.**

2. .. _alm-45451__li1314322683817:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

3. Expand the **Service** drop-down list, and select **ClickHouse** for the target cluster.

4. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the abnormal host, and click **OK**.

5. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

6. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
