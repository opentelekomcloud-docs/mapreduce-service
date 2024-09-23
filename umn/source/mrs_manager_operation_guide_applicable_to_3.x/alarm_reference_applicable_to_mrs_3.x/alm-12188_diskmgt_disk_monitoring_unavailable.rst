:original_name: ALM-12188.html

.. _ALM-12188:

ALM-12188 diskmgt Disk Monitoring Unavailable
=============================================

Alarm Description
-----------------

NodeAgent checks the status of the diskmgt disk monitoring service every 5 minutes. This alarm is generated when diskmgt disk monitoring is unavailable.

This alarm is cleared when the diskmgt disk monitoring service recovers.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
12188    Minor          Yes
======== ============== ============

Alarm Parameters
----------------

+-------------+-------------------------------------------------------------------+
| Parameter   | Description                                                       |
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

When diskmgt disk monitoring is unavailable, the read-only detection of the device partition file system, device partition loss detection, and disk partition scale-out detection cannot be performed.

Possible Causes
---------------

-  The diskmgt disk monitoring service does not exist.
-  The diskmgt disk monitoring service is not started.

Handling Procedure
------------------

**Check whether the diskmgt disk monitoring service exists.**

#. Log in to FusionInsight Manager, click **O&M**, and choose **Alarm** > **Alarms** to view the alarm details. In the **Location** column, check the name of the host for which the alarm is generated. Click the host name to view its IP address.

#. Log in to the node for which the alarm is generated as user **root**.

#. Run the following command to check whether the core service file exists:

   **stat /usr/local/diskmgt/inner/diskmgtd**

   If the file does not exist, contact O&M personnel.

**Start the diskmgt disk monitoring service.**

4. Run the following command to start the diskmgt disk monitoring service:

   **systemctl restart diskmgt**

5. Run the following command to check whether the diskmgt disk monitoring service is started:

   **systemctl status diskmgt**

   -  If information similar to the following is displayed, the service is started successfully. Go to :ref:`6 <alm-12188__li09010504164>`.

      |image1|

   -  If no, contact O&M personnel.

6. .. _alm-12188__li09010504164:

   Wait for 5 minutes, click **O&M**, and choose **Alarm** > **Alarms** on FusionInsight Manager. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, contact O&M personnel.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000002008258977.png
