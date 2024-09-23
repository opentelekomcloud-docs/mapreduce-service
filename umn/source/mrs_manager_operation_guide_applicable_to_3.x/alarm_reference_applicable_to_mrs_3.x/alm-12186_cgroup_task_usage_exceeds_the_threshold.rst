:original_name: ALM-12186.html

.. _ALM-12186:

ALM-12186 CGroup Task Usage Exceeds the Threshold
=================================================

Alarm Description
-----------------

The system checks the CGroup task usage of user **omm** every 5 minutes. This alarm is generated when the CGroup task usage exceeds 90%. This alarm is cleared when the CGroup task usage is less than or equal to 90%.

CGroup task usage = Number of used CGroup tasks/Maximum number of CGroup tasks

You can run the **systemctl status user-$(id -u).slice \| grep limit \| awk -F ' ' '{print $2}'** command as user **omm** to obtain the number of used CGroup tasks of this user and run the **echo $(systemctl status user-$(id -u).slice \| grep limit \| awk -F ' ' '{print $4}') \| sed -e 's/)//g'** command to obtain the maximum number of CGroup tasks allowed for this user.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
12186    Major          Yes
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

-  Failed to switch to user **omm**.
-  Failed to create new **omm** processes.

-  A faulty service or process cannot be restarted.

Possible Causes
---------------

The CGroup task usage exceeds 90%.

Handling Procedure
------------------

**Check the maximum number of threads that can be concurrently opened by user omm is properly set.**

#. Log in to FusionInsight Manager and choose **O&M** > **Alarm** > **Alarms**. On the page that is displayed, click |image1| in the row containing the alarm, and view the name of the host for which the alarm is generated in **Location**. Click the host name to view its IP address.

#. Log in to the host for which the alarm is generated as user **omm**.

#. Run the following command to obtain the maximum number of threads that can be concurrently opened by user **omm** and check whether this number is greater than or equal to **60000**:

   **systemctl status user-$(id -u).slice \| grep limit**

   -  If yes, go to :ref:`6 <alm-12186__li18602412348>`.
   -  If no, go to :ref:`4 <alm-12186__li9448150105813>`.

#. .. _alm-12186__li9448150105813:

   Switch to user **root** and run the following command to change the value for user **omm** to **60000**:

   **systemctl set-property user-2000.slice TasksMax=60000**

#. Change the value of **UserTasksMax** in the **/etc/systemd/logind.conf** file to **60000**. (If the parameter is commented out, uncomment it.) Save the file, wait 5 minutes, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12186__li18602412348>`.

**Collect fault information.**

6. .. _alm-12186__li18602412348:

   On FusionInsight Manager of the cluster, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7. Expand the **Service** drop-down list, select **OmmServer** and **NodeAgent** for the target cluster, and click **OK**.

8. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000001971659200.png
.. |image2| image:: /_static/images/en-us_image_0000001971818972.png
