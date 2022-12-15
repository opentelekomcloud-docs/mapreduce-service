:original_name: ALM-12068.html

.. _ALM-12068:

ALM-12068 ACS Resource Exception
================================

Description
-----------

HA checks the ACS resources of Manager every 80 seconds. This alarm is generated when HA detects that the ACS resources are abnormal for two consecutive times.

This alarm is cleared when HA detects that the ACS resources are normal.

**Resource Type** of ACS is **Single-active**. Active/standby will be triggered upon resource exceptions. When this alarm is generated, the active/standby switchover is complete and new ACS resources have been enabled on the new active Manager. In this case, this alarm is cleared. This alarm is used to notify users of the cause of the active/standby Manager switchover.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12068    Major          Yes
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
-  The ACS process repeatedly restarts, which may cause the FusionInsight Manager login failure.

Possible Causes
---------------

The ACS process is abnormal.

Procedure
---------

**Check whether the ACS process is normal.**

#. In the alarm list on FusionInsight Manager, locate the row that contains the alarm, and click |image1| to view the name of the host for which the alarm is generated.

#. Log in to the alarm host as user **root**.

#. Run the **su - omm** command and then **sh ${BIGDATA_HOME}/om-server/OMS/workspace0/ha/module/hacom/script/status_ha.sh** to check whether the status of the ACS resources managed by the HA is normal. In the single-node system, the ACS resource is in the normal state. In the dual-node system, the ACS resource is in the normal state on the active node and in the stopped state on the standby node.

   -  If yes, go to :ref:`6 <alm-12068__li6152360163635>`.
   -  If no, go to :ref:`4 <alm-12068__li139657016249>`.

#. .. _alm-12068__li139657016249:

   Run the **vi $BIGDATA_LOG_HOME/omm/oms/ha/scriptlog/acs.log** command to check whether the ACS resource log of HA contains the keyword **ERROR**. If yes, analyze the logs to locate the resource exception cause and fix the exception.

#. After 5 minutes, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12068__li6152360163635>`.

**Collect the fault information.**

6. .. _alm-12068__li6152360163635:

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

.. |image1| image:: /_static/images/en-us_image_0263895733.png
.. |image2| image:: /_static/images/en-us_image_0263895594.png
