:original_name: ALM-12104.html

.. _ALM-12104:

ALM-12104 Abnormal Knox Resources
=================================

Description
-----------

HA checks the Knox resources of Manager every 70 seconds. This alarm is generated when HA detects that the Knox resources are abnormal for three consecutive times.

This alarm is cleared when HA detects that the Knox resources are normal.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12104    Major          Yes
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

Requests sent by upper-layer services by using Knox cannot be properly processed.

Possible Causes
---------------

The Knox process is abnormal.

Procedure
---------

Check whether the Knox process is normal.

#. Log in to FusionInsight Manager. In the alarm list, locate the row that contains the alarm and view the name of the host for which the alarm is generated.

#. Use PuTTY to log in to the host for which the alarm is generated as user **root**.

#. Run the **su - omm** command to switch to user **omm**.

#. Run the **sh ${BIGDATA_HOME}/om-server/om/sbin/status-oms.sh** command to check whether the status of the Knox resources managed by HA is normal. If the status is normal, the Knox resources are normal. Otherwise, the Knox resources are abnormal.

   -  If yes, go to :ref:`7 <alm-12104__li3394198162>`.
   -  If no, go to :ref:`5 <alm-12104__li193959911619>`.

#. .. _alm-12104__li193959911619:

   Run the **vi $BIGDATA_LOG_HOME/omm/oms/ha/scriptlog/knox.log** command to check whether the Knox resource log of HA contains the keyword **ERROR**. If yes, analyze the log to locate the resource exception cause and fix the exception.

#. After 5 minutes, check whether this alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-12104__li3394198162>`.

Collect the fault information.

7.  .. _alm-12104__li3394198162:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  In the **Services** area, select **Controller** and **OmmServer**, and click **OK**.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact O&M personnel and provide the collected logs.

.. |image1| image:: /_static/images/en-us_image_0000001532767542.png
