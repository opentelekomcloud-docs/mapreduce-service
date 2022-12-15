:original_name: alm_12001.html

.. _alm_12001:

ALM-12001 Audit Log Dump Failure
================================

Description
-----------

Cluster audit logs need to be dumped on a third-party server due to the local historical data backup policy. Audit logs can be successfully dumped if the dump server meets the configuration conditions. This alarm is generated when the audit log dump fails because the disk space of the dump directory on the third-party server is insufficient or a user changes the username, password, or dump directory of the dump server.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12001    Minor          Yes
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

The system can only store a maximum of 50 dump files locally. If the fault persists on the dump server, the local audit log may be lost.

Possible Causes
---------------

-  The network connection is abnormal.
-  The username, password, or dump directory of the dump server does not meet the configuration conditions.
-  The disk space of the dump directory is insufficient.

Procedure
---------

#. Check whether the username, password, and dump directory are correct.

   a. Check on the dump configuration page of MRS Manager to see if they are correct.

      -  If yes, go to :ref:`3 <alm_12001__en-us_topic_0191813935_li2924012813025>`.
      -  If no, go to :ref:`1.b <alm_12001__en-us_topic_0191813935_li56668375121446>`.

   b. .. _alm_12001__en-us_topic_0191813935_li56668375121446:

      Change the username, password, or dump directory, and click **OK**.

   c. Wait 2 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_12001__en-us_topic_0191813935_li5748176314415>`.

#. .. _alm_12001__en-us_topic_0191813935_li5748176314415:

   Reset the dump rule.

   a. On MRS Manager, choose **System** > **Dump Audit Log**.
   b. Reset dump rules, set the parameters properly, and click **OK**.
   c. Wait 2 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_12001__en-us_topic_0191813935_li2924012813025>`.

#. .. _alm_12001__en-us_topic_0191813935_li2924012813025:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

N/A
