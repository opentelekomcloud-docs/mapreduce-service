:original_name: alm_12035.html

.. _alm_12035:

ALM-12035 Unknown Data Status After Recovery Task Failure
=========================================================

Description
-----------

If a recovery task fails, the system attempts to automatically roll back. If the rollback fails, data may be lost. If this occurs, an alarm is reported. This alarm is cleared when the recovery task is successfully executed later.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12035    Critical       Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Parameter   Description
=========== =======================================================
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
TaskName    Specifies the task name.
=========== =======================================================

Impact on the System
--------------------

The data may be lost or the data status may be unknown, which may affect services.

Possible Causes
---------------

The possible cause of this alarm is that the component status does not meet the requirements before the restoration task is executed or an error occurs in a step during the restoration task. The error depends on the task details. You can obtain logs and task details to handle the alarm.

Procedure
---------

**Checking the component status**

#. Log in to MRS Manager and choose **Services**. On the page that is displayed, check whether the running status of the components meets the requirements. (OMS and DBService must be in the normal status, and other components must be stopped.)

   -  If yes, go to :ref:`7 <alm_12035__li449212126111>`.
   -  If no, go to :ref:`2 <alm_12035__li124931122116>`.

#. .. _alm_12035__li124931122116:

   Restore the component status as required and start the recovery task again.

#. Log in to MRS Manager and choose **Alarms**. In the alarm list, click the row containing the alarm and obtain the task name from the **Location** area.

#. Choose **System** > **Recovery Management**. Search for the restoration task based on the task name and view the task details.

#. Start the restoration task and check whether the task is executed.

   -  If yes, go to :ref:`6 <alm_12035__li106313102516>`.
   -  If no, go to :ref:`7 <alm_12035__li449212126111>`.

#. .. _alm_12035__li106313102516:

   After 2 minutes, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm_12035__li449212126111>`.

**Collecting fault information**

7. .. _alm_12035__li449212126111:

   On MRS Manager, choose **System** > **Export Log**.

8. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Reference
---------

None
