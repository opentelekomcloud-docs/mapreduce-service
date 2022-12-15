:original_name: alm_18013.html

.. _alm_18013:

ALM-18013 Number of Failed Yarn Tasks in the Last Period Exceeds the Threshold
==============================================================================

Description
-----------

The system checks the number of failed Yarn tasks every 10 minutes. This alarm is generated when the number of failed Yarn tasks in the last 10 minutes is greater than the threshold. This alarm is automatically cleared when the number of failed Yarn tasks is less than the threshold in the next 10 minutes.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
18013    Major          Yes
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

The submitted Yarn job program is incorrect. For example, the parameter for Spark to submit a job is incorrect.

Procedure
---------

Check the log of the failed job, locate the failure cause, modify the job, and submit the job again.

Reference
---------

None
