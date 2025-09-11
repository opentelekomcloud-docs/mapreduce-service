:original_name: ALM-12207.html

.. _ALM-12207:

ALM-12207 Slow Disk Processing Timeout
======================================

Alarm Description
-----------------

When slow disk detection is enabled, the system checks the slow disk processing status every 10 minutes by default. This alarm is generated when the following disk or node status does not change within 10 hours.

Disk: Automatic isolation aborted, isolated, isolation failed, and de-isolation failed.

Node: Isolated, Isolation failed, Isolation cancellation failed, Node startup failed, and De-isolated.

This alarm is automatically cleared when the status of the node or disk that is in the processing timeout state changes.

.. note::

   This alarm applies only to MRS 3.3.1 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
12207    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------+--------------------------------------------------------------------+
| Type                   | Parameter   | Description                                                        |
+========================+=============+====================================================================+
| Location Information   | Source      | Specifies the cluster or system for which the alarm was generated. |
+------------------------+-------------+--------------------------------------------------------------------+
|                        | ServiceName | Specifies the service for which the alarm was generated.           |
+------------------------+-------------+--------------------------------------------------------------------+
|                        | RoleName    | Specifies the role for which the alarm was generated.              |
+------------------------+-------------+--------------------------------------------------------------------+
|                        | HostName    | Specifies the host for which the alarm was generated.              |
+------------------------+-------------+--------------------------------------------------------------------+
|                        | DiskName    | Specifies the disk for which the alarm was generated.              |
+------------------------+-------------+--------------------------------------------------------------------+
| Additional Information | HostName    | Specifies the host for which the alarm was generated.              |
+------------------------+-------------+--------------------------------------------------------------------+
|                        | DiskName    | Specifies the disk for which the alarm was generated.              |
+------------------------+-------------+--------------------------------------------------------------------+
|                        | Details     | Specifies that the description of slow disk isolation.             |
+------------------------+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

If an isolated disk or node cannot be restored in a timely manner, the running of components may be affected, which further affects user services.

Possible Causes
---------------

The isolation status of the disk or node exceeds the configured timeout period for processing slow disks.

Handling Procedure
------------------

**Check the cause of the slow disk processing timeout.**

#. Log in to MRS Manager and choose **O&M** > **Alarm** > **Alarms**. In the alarm list, expand the alarm details, and view and record the host or disk for which the alarm is generated.

#. Log in to the active OMS node as user **root** and run the following command to check the cause of slow disk processing timeout in the controller log and check whether there is obvious error information:

   **vi /var/log/Bigdata/controller/controller.log**

   -  If yes, go to :ref:`4 <alm-12207__li3891246115>`.
   -  If no, go to :ref:`3 <alm-12207__li11884227144712>`.

#. .. _alm-12207__li11884227144712:

   Log in to the node for which the alarm is generated as user **root** and run the following command to check the cause of slow disk processing timeout in the agent log and check whether any error information is displayed:

   **vi /var/log/Bigdata/nodeagent/agentlog/agent.log**

   -  If yes, go to :ref:`4 <alm-12207__li3891246115>`.
   -  If no, go to :ref:`5 <alm-12207__li39839699173731>`.

#. .. _alm-12207__li3891246115:

   Contact O&M personnel to rectify the fault and manually run the command for the slow disk or node. After the command is executed, observe for 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-12207__li39839699173731>`.

**Collect fault information.**

5. .. _alm-12207__li39839699173731:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Select **Controller** and **NodeAgent** for **Service**, select the active/standby OMS node and the node for which the alarm is generated in the **Host** area, and click **OK**.

7. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
