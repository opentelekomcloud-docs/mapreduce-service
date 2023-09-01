:original_name: ALM-12071.html

.. _ALM-12071:

ALM-12071 Httpd Resource Is Abnormal
====================================

Description
-----------

HA checks the httpd resources of Manager every 120 seconds. This alarm is generated when HA detects that the httpd resources are abnormal for 10 consecutive times.

This alarm is cleared when the httpd resource is normal.

**Resource Type** of httpd is **Single-active**. Active/standby will be triggered upon resource exceptions. When this alarm is generated, the active/standby switchover is complete and new httpd resources have been enabled on the new active FusionInsight Manager. In this case, this alarm is cleared. This alarm is used to notify users of the cause of the active/standby switchover.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12071    Major          Yes
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

-  The active/standby FusionInsight Manager switchover occurs.
-  The httpd process is repeatedly restarts, which may lead to the failure to visit the native service UI.

Possible Causes
---------------

The httpd process is abnormal.

Procedure
---------

**Check whether the httpd process is abnormal.**

#. In the alarm list on FusionInsight Manager, locate the row that contains the alarm, and view the name of the host for which the alarm is generated.

#. Log in to the host for which the alarm is generated as user **root**.

#. Run the **su - omm** command to switch to user **omm**.

#. Run the **sh ${BIGDATA_HOME}/om-server/OMS/workspace0/ha/module/hacom/script/status_ha.sh** command to check whether the status of the httpd resources managed by the HA is normal. In the single-node system, the httpd resource is in the normal state. In the dual-node system, the httpd resource is in the normal state on the active node and in the stopped state on the standby node.

   -  If it is, go to :ref:`7 <alm-12071__li384145118188>`.
   -  If it is not, go to :ref:`5 <alm-12071__li584395101819>`.

#. .. _alm-12071__li584395101819:

   Run the **vi $BIGDATA_LOG_HOME/omm/oms/ha/scriptlog/httpd.log** command to view the httpd resource logs, check whether the keyword **ERROR** exists. Analyze the logs to locate and rectify the fault.

#. Five minutes later, check whether this alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`7 <alm-12071__li384145118188>`.

**Collect fault information.**

7.  .. _alm-12071__li384145118188:

    On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

8.  Select **Controller** and **OmmServer** for **Service** and click **OK**.

9.  Click |image1| in the upper right corner. In the displayed dialog box, set **Start Date** and **End Date** to 1 hour before and after the alarm generation time respectively and click **OK**. Then, click **Download**.

10. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

This alarm will be automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582927741.png
