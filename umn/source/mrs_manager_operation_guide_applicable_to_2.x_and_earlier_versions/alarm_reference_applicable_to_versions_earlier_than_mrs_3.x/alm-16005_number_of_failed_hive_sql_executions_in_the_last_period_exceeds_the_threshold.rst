:original_name: alm_16005.html

.. _alm_16005:

ALM-16005 Number of Failed Hive SQL Executions in the Last Period Exceeds the Threshold
=======================================================================================

Description
-----------

The system checks whether the number of Hive SQL statements that fail to be executed has exceeded the threshold in the last 10-minute period. This alarm is generated when the number of failed Hive SQL statement executions in the last 10 minutes is greater than the threshold. In the next 10 minutes, if the number of failed Hive SQL statement executions is less than the threshold, the alarm is automatically cleared.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
16005    Major          Yes
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

The Hive SQL syntax is incorrect. As a result, the Hive SQL statements fail to be executed.

Procedure
---------

Check the Hive SQL statements that fail to be executed, correct the syntax, and execute the SQL statements again.

Reference
---------

None
