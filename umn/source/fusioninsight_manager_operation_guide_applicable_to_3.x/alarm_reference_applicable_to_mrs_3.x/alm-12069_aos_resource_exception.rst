:original_name: ALM-12069.html

.. _ALM-12069:

ALM-12069 AOS Resource Exception
================================

Description
-----------

HA checks the AOS resources of Manager every 81 seconds. This alarm is generated when HA detects that the AOS resources are abnormal for two consecutive times.

This alarm is cleared when HA detects that the AOS resources become normal.

**Resource Type** of AOS is **Single-active**. Active/standby will be triggered upon resource exceptions. When this alarm is generated, the active/standby switchover is complete and new AOS resources have been enabled on the new active Manager. In this case, this alarm is cleared. This alarm is used to notify users of the cause of the active/standby Manager switchover.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12069    Major          Yes
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

-  The active/standby Manager switchover occurs.
-  The AOS process repeatedly restarts, which may cause the FusionInsight Manager login failure.

Possible Causes
---------------

The AOS process is abnormal.

Procedure
---------

**Check whether the AOS process is normal.**

#. In the alarm list on FusionInsight Manager, locate the row that contains the alarm, and click |image1| to view the name of the host for which the alarm is generated.

#. Log in to the alarm host as user **root**.

#. Run the **sh ${BIGDATA_HOME}/om-server/OMS/workspace0/ha/module/hacom/script/status_ha.sh** command to check whether the status of the AOS resources managed by the HA is normal. In the single-node system, the AOS resource is in the normal state. In the dual-node system, the AOS resource is in the normal state on the active node and in the stopped state on the standby node.

   -  If yes, go to :ref:`6 <alm-12069__li6152360163635>`.
   -  If no, go to :ref:`4 <alm-12069__li139657016249>`.

#. .. _alm-12069__li139657016249:

   Run the **vi $BIGDATA_LOG_HOME/omm/oms/ha/scriptlog/aos.log** command to check whether the AOS resource log of HA contains the keyword **ERROR**. If yes, analyze the logs to locate the resource exception cause and fix the exception.

#. After 5 minutes, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12069__li6152360163635>`.

**Collect the fault information.**

6. .. _alm-12069__li6152360163635:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7. In the **Services** area, select **Controller** and **OmmServer**, and click **OK**.

8. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532448286.png
.. |image2| image:: /_static/images/en-us_image_0000001582927665.png
