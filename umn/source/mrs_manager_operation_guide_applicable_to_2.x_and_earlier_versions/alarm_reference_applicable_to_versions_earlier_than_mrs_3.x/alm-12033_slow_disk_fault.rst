:original_name: alm_12033.html

.. _alm_12033:

ALM-12033 Slow Disk Fault
=========================

Description
-----------

The system runs the **iostat** command every second to monitor the disk I/O indicator. If there are more than 30 times that the **svctm** value is greater than 100 ms in 60 seconds, the disk is faulty and the alarm is generated.

This alarm is automatically cleared after the disk is replaced.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12033    Major          Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Parameter   Description
=========== =======================================================
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
DiskName    Specifies the disk for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

Service performance deteriorates and service processing capabilities become poor. For example, DBService active/standby synchronization is affected and even the service is unavailable.

Possible Causes
---------------

The disk is aged or has bad sectors.

Procedure
---------

#. Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
