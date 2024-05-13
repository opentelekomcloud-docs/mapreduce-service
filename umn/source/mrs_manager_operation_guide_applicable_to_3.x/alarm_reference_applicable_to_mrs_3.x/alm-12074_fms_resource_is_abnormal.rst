:original_name: ALM-12074.html

.. _ALM-12074:

ALM-12074 FMS Resource Is Abnormal
==================================

Description
-----------

HA checks the fms resources of Manager every 60 seconds. This alarm is generated when HA detects that the fms resources are abnormal for 2 consecutive times.

This alarm is cleared when the FMS resource is normal.

**Resource Type** of FMS is **Single-active**. Active/standby will be triggered upon resource exceptions. When this alarm is generated, the active/standby switchover is complete and new FMS resources have been enabled on the new active MRS Manager. In this case, this alarm is cleared. This alarm is used to notify users of the cause of the active/standby switchover.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12074    Major          Yes
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

-  The active/standby MRS Manager switchover occurs.
-  The FMS process repeatedly restarts. As a result, alarm information may fail to be reported.

Possible Causes
---------------

The FMS process is abnormal.

Procedure
---------

**Check whether the FMS process is abnormal.**

#. In the alarm list on MRS Manager, locate the row that contains the alarm, and view the name of the host for which the alarm is generated.

#. Log in to the host for which the alarm is generated as user **root**.

#. Run the **su -omm** command and then the **sh ${BIGDATA_HOME}/om-server/OMS/workspace0/ha/module/hacom/script/status_ha.sh** command to check whether the status of the FMS resources managed by the HA is normal. In the single-node system, the FMS resource is in the normal state. In the dual-node system, the FMS resource is in the normal state on the active node and in the stopped state on the standby node.

   -  If it is, go to :ref:`6 <alm-12074__li5828173931412>`.
   -  If it is not, go to :ref:`4 <alm-12074__li1183383931416>`.

#. .. _alm-12074__li1183383931416:

   Run the **vi $BIGDATA_LOG_HOME/omm/oms/fms/fms.log** and **vi $BIGDATA_LOG_HOME/omm/oms/fms/scriptlog/fms_ha.log** commands to view the FMS resource logs, check whether the keyword **ERROR** exists. Analyze the logs to locate and rectify the fault.

#. 5 minutes later, check whether this alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`6 <alm-12074__li5828173931412>`.

**Collect fault information.**

6. .. _alm-12074__li5828173931412:

   On MRS Manager, choose **O&M**> **Log** > **Download**.

7. Select **Controller** and **OmmServer** for **Service** and click **OK**.

8. Click |image1| in the upper right corner. In the displayed dialog box, set **Start Date** and **End Date** to 1 hour before and after the alarm generation time respectively and click **OK**. Then, click **Download**.

9. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

This alarm will be automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532767442.png
