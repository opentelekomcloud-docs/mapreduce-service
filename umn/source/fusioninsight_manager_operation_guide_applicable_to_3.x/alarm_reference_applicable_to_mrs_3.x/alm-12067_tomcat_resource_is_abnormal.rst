:original_name: ALM-12067.html

.. _ALM-12067:

ALM-12067 Tomcat Resource Is Abnormal
=====================================

Description
-----------

HA checks the Tomcat resources of Manager every 85 seconds. This alarm is generated when HA detects that the Tomcat resources are abnormal for two consecutive times.

This alarm is cleared when HA detects that the Tomcat resources become normal.

**Resource Type** of Tomcat is **Single-active**. Active/standby will be triggered upon resource exceptions. When this alarm is generated, the active/standby switchover is complete and new Tomcat resources have been enabled on the new active Manager. In this case, this alarm is cleared. This alarm is used to notify users of the cause of the active/standby Manager switchover.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12067    Major          Yes
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
-  The Tomcat process repeatedly restarts.

Possible Causes
---------------

-  The Tomcat directory permission is abnormal, and the Tomcat process is abnormal.

Procedure
---------

**Check whether the permission on the Tomcat directory is normal.**

#. In the alarm list on FusionInsight Manager, locate the row that contains the alarm, and click |image1| to view the IP address of the host for which the alarm is generated.
#. Log in to the alarm host as user **root**.
#. Run the **su - omm** command to switch to user **omm**.
#. Run the **vi $BIGDATA_LOG_HOME/omm/oms/ha/scriptlog/tomcat.log** command to check whether the Tomcat resource log contains keyword **Cannot find XXX** and rectify the file permission based on the keyword.
#. After 5 minutes, check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12067__li711211264288>`.

**Collect the fault information.**

6. .. _alm-12067__li711211264288:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7. In the **Services** area, select **OmmServer** and **Tomcat**, and click **OK**.

8. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583127457.png
.. |image2| image:: /_static/images/en-us_image_0000001532767558.png
