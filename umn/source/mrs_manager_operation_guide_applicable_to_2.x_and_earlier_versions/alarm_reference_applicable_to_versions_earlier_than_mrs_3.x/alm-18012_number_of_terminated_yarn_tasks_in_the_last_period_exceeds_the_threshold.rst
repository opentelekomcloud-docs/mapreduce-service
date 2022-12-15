:original_name: alm_18012.html

.. _alm_18012:

ALM-18012 Number of Terminated Yarn Tasks in the Last Period Exceeds the Threshold
==================================================================================

Description
-----------

The system checks the number of terminated Yarn tasks every 10 minutes. This alarm is generated when the number of terminated Yarn tasks in the last 10 minutes is greater than the threshold. This alarm is automatically cleared when the number of terminated Yarn tasks is less than the threshold in the next 10 minutes.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
18012    Major          Yes
======== ============== ==========

Parameter
---------

=========== =========================================
Parameter   Description
=========== =========================================
ServiceName Service for which the alarm is generated.
RoleName    Role for which the alarm is generated.
HostName    Host for which the alarm is generated.
=========== =========================================

Impact on the System
--------------------

None

Possible Causes
---------------

A user manually stops a running Yarn task.

Procedure
---------

Check the task termination operator in the Yarn logs and audit logs, and determine the cause of the task termination.

Reference
---------

None
