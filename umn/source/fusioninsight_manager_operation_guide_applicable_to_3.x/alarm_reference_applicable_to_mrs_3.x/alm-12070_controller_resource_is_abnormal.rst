:original_name: ALM-12070.html

.. _ALM-12070:

ALM-12070 Controller Resource Is Abnormal
=========================================

Alarm Description
-----------------

HA checks the controller resources of Manager every 80 seconds. This alarm is generated when HA detects that the controller resources are abnormal for 2 consecutive times.

This alarm is cleared when the Controller resource is normal.

**Resource Type** of Controller is **Single-active**. Active/standby will be triggered upon resource exceptions. When this alarm is generated, the active/standby switchover is complete and new Controller resources have been enabled on the new active FusionInsight Manager. In this case, this alarm is cleared. This alarm is used to notify users of the cause of the active/standby switchover.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12070    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+---------------------------------------------------------------------+
| Parameter   | Description                                                         |
+=============+=====================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated.   |
+-------------+---------------------------------------------------------------------+
| ServiceName | Specifies the name of the service for which the alarm is generated. |
+-------------+---------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.                |
+-------------+---------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.                |
+-------------+---------------------------------------------------------------------+

Impact on the System
--------------------

-  The active/standby FusionInsight Manager switchover occurs.
-  The Controller process repeatedly restarts, which may cause the FusionInsight Manager login failure.

Possible Causes
---------------

The Controller process is abnormal.

Procedure
---------

**Check whether the controller process is normal.**

#. In the alarm list on FusionInsight Manager, locate the row that contains the alarm, and view the name of the host for which the alarm is generated.

#. Log in to the host for which the alarm is generated as user **root**.

#. Run the **su - omm** command to switch to user **omm**.Run the **sh ${BIGDATA_HOME}/om-server/OMS/workspace0/ha/module/hacom/script/status_ha.sh** command to check whether the status of the Controller resources managed by the HA is normal. In the single-node system, the Controller resource is in the normal state. In the dual-node system, the Controller resource is in the normal state on the active node and in the stopped state on the standby node.

   -  If it is, go to :ref:`6 <alm-12070__li69038231234>`.
   -  If it is not, go to :ref:`4 <alm-12070__li6903202312318>`.

#. .. _alm-12070__li6903202312318:

   Run the **vi $BIGDATA_LOG_HOME/omm/oms/ha/scriptlog/controller.log** command to view the Controller resource logs, and run the **vi $BIGDATA_LOG_HOME/controller/controller.log** command to view the Controller running logs, check whether the keyword **ERROR** exists. Analyze the logs to locate and rectify the fault.

#. Five minutes later, check whether this alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`6 <alm-12070__li69038231234>`.

**Collect fault information.**

6. .. _alm-12070__li69038231234:

   On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

7. Select **Controller** and **OmmServe** for **Service** and click **OK**.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour before and after the alarm generation time, respectively. Then, click **Download**.

9. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582927629.png
