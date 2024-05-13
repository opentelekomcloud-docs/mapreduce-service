:original_name: ALM-12035.html

.. _ALM-12035:

ALM-12035 Unknown Data Status After Recovery Task Failure
=========================================================

Description
-----------

After the recovery task fails, the system automatically rolls back every 60 minutes. If the rollback fails, data may be lost. If this occurs, an alarm is reported. This alarm is cleared when the next recovery task execution is successful.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12035    Critical       Yes
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
| TaskName    | Specifies the task.                                               |
+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

After the recovery task fails, the system automatically rolls back. If the rollback fails, data may be lost or the data status may be unknown, which may affect services.

Possible Causes
---------------

The alarm cause depends on the task details. Handle the alarm according to the logs and alarm details.

Procedure
---------

**Collect fault information.**

#. In the MRS Manager, choose **Cluster >** *Name of the desired cluster* **> Services**, and check whether the running status of the component meets the requirements. (The OMS and DBService must be in the normal state, and other components must be stopped.)

   -  If yes, go to :ref:`9 <alm-12035__li18912172820165>`.
   -  If no, go to :ref:`2 <alm-12035__li16912228111613>`.

#. .. _alm-12035__li16912228111613:

   Restore the component status as required and start the recovery task again.

#. Log in to the MRS Manager portal and click **O&M > Alarm > Alarms**.

#. In the alarm list, click |image1| in the row where the alarm is located to obtain **TaskName** from **Location**.

#. Choose **O&M** > **Backup and Restoration > Restoration Management**.

#. Find the restoration task by **Task Name** and view the task details.

#. Perform the recovery task again and check whether the recovery task execution is successful.

   -  If yes, go to :ref:`8 <alm-12035__li691272812168>`.
   -  If no, go to :ref:`9 <alm-12035__li18912172820165>`.

#. .. _alm-12035__li691272812168:

   After 2 minutes, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-12035__li18912172820165>`.

**Collect fault information.**

9.  .. _alm-12035__li18912172820165:

    On the MRS Manager portal, choose **O&M** > **Log > Download**.

10. Select **Controller** from the **Service** and click **OK**.

11. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532448366.png
.. |image2| image:: /_static/images/en-us_image_0000001583127489.png
