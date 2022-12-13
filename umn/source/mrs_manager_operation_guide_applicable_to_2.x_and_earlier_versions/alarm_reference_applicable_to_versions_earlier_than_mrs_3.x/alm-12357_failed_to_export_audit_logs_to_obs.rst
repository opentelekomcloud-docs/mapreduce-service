:original_name: alm_12357.html

.. _alm_12357:

ALM-12357 Failed to Export Audit Logs to OBS
============================================

Description
-----------

If the user has configured audit log export to the OBS on MRS Manager, the system regularly exports audit logs to the OBS. This alarm is reported if the system fails to access the OBS.

This alarm is cleared after the system exports audit logs to the OBS successfully.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12357    Major          Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Parameter   Description
=========== =======================================================
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

The local system saves a maximum of seven compressed service audit log files. If this alarm persists, local service audit logs may be lost.

The local system saves a maximum of 50 management audit log files (each file contains 100,000 records). If this alarm persists, local management audit logs may be lost.

Possible Causes
---------------

-  Connection to the OBS server fails.
-  The specified OBS file system does not exist.
-  The user AK/SK information is invalid.
-  The local OBS configuration cannot be obtained.

Procedure
---------

#. Log in to the OBS server and check whether the OBS server can be properly accessed.

   -  If yes, go to :ref:`3 <alm_12357__en-us_topic_0191813876_li17073310143018>`.
   -  If no, go to :ref:`2 <alm_12357__en-us_topic_0191813876_li51875580143018>`.

#. .. _alm_12357__en-us_topic_0191813876_li51875580143018:

   Contact the maintenance personnel to repair OBS. Then check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm_12357__en-us_topic_0191813876_li17073310143018>`.

#. .. _alm_12357__en-us_topic_0191813876_li17073310143018:

   On MRS Manager, choose **System** > **Export Audit Log**. Check whether the AK/SK information, file system name, and path are correct.

   -  If yes, go to :ref:`5 <alm_12357__en-us_topic_0191813876_li572522141314>`.
   -  If no, go to :ref:`4 <alm_12357__en-us_topic_0191813876_li52527297143018>`.

#. .. _alm_12357__en-us_topic_0191813876_li52527297143018:

   Correct the information. Then check whether the alarm is cleared when the export task is executed again.

   .. note::

      To check alarm clearance quickly, you can set the start time of audit log collection to 10 or 30 minutes later than the current time. After checking the result, restore the original start time.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm_12357__en-us_topic_0191813876_li572522141314>`.

#. .. _alm_12357__en-us_topic_0191813876_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Related Information
-------------------

N/A
