:original_name: ALM-12103.html

.. _ALM-12103:

ALM-12103 Executor Resource Exception
=====================================

Description
-----------

HA checks the Executor resources of Manager every 30 seconds. This alarm is generated when HA detects that the Executor resources are abnormal for two consecutive times.

This alarm is cleared when the Executor resources are normal.

**Resource Type** of Executor is **Single-active**. Active/standby will be triggered upon resource exceptions. When this alarm is generated, the active/standby switchover is complete and new Executor resources have been enabled on the new active Manager. In this case, this alarm is cleared. This alarm is used to notify users of the cause of the active/standby Manager switchover.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12103    Major          Yes
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
-  The Executor process keeps restarting. As a result, the cluster page may fail to be accessed.

Possible Causes
---------------

The Executor process is abnormal.

Procedure
---------

**Check whether the Executor process is abnormal.**

#. In the alarm list on MRS Manager, locate the row that contains the alarm, and click |image1| to view the name of the host for which the alarm is generated.

#. Log in to the host for which the alarm is generated as user **root**.

#. Run the **su - omm** command to switch to user **omm**.

#. Run the **sh ${BIGDATA_HOME}/om-server/OMS/workspace0/ha/module/hacom/script/status_ha.sh** command to check whether the status of the Executor resources managed by the HA is normal. In the single-node system, the Executor resource is in the normal state. In the dual-node system, the Executor resource is in the normal state on the active node and in the stopped state on the standby node.

   -  If yes, go to :ref:`7 <alm-12103__li6152360163635>`.
   -  If no, go to :ref:`5 <alm-12103__li139657016249>`.

#. .. _alm-12103__li139657016249:

   Run the **vi $BIGDATA_LOG_HOME/omm/oms/ha/scriptlog/executor.log** command to check whether the Executor resource log of HA contains the keyword **ERROR**. If yes, analyze the log to locate the resource exception cause and fix the exception.

#. After 5 minutes, check whether this alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-12103__li6152360163635>`.

**Collect the fault information.**

7.  .. _alm-12103__li6152360163635:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  In the **Services** area, select **Controller** and **OmmServer**, and click **OK**.

9.  Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact O&M personnel and provide the collected logs.

.. |image1| image:: /_static/images/en-us_image_0000001582927809.png
.. |image2| image:: /_static/images/en-us_image_0000001582807861.png
