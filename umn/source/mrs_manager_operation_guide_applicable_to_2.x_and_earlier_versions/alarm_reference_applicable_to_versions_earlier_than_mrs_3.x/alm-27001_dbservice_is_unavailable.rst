:original_name: alm_27001.html

.. _alm_27001:

ALM-27001 DBService Is Unavailable
==================================

Description
-----------

The alarm module checks the DBService status every 30 seconds. This alarm is generated when the system detects that DBService is unavailable.

This alarm is cleared when DBService recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
27001    Critical       Yes
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

The database service is unavailable and cannot provide data import and query functions for upper-layer services, which results in service exceptions.

Possible Causes
---------------

-  The floating IP address does not exist.
-  There is no active DBServer instance.
-  The active and standby DBServer processes are abnormal.

Procedure
---------

#. Check whether the floating IP address exists in the cluster environment.

   a. Go to the MRS cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. Choose **DBService** > **Instances**.

   c. Check whether the active instance exists.

      -  If yes, go to :ref:`1.d <alm_27001__en-us_topic_0191813879_step111>`.
      -  If no, go to :ref:`2.a <alm_27001__en-us_topic_0191813879_step88>`.

   d. .. _alm_27001__en-us_topic_0191813879_step111:

      Select the active DBServer instance and record the IP address.

   e. Log in to the host with the preceding IP address and run the **ifconfig** command to check whether the DBService floating IP address exists on the node.

      -  If yes, go to :ref:`1.f <alm_27001__en-us_topic_0191813879_checkfloatip>`.
      -  If no, go to :ref:`2.a <alm_27001__en-us_topic_0191813879_step88>`.

   f. .. _alm_27001__en-us_topic_0191813879_checkfloatip:

      Run the **ping** *floating IP address* command to check whether the DBService floating IP address can be pinged.

      -  If yes, go to :ref:`1.g <alm_27001__en-us_topic_0191813879_findfloatip>`.
      -  If no, go to :ref:`2.a <alm_27001__en-us_topic_0191813879_step88>`.

   g. .. _alm_27001__en-us_topic_0191813879_findfloatip:

      Log in to the host where the DBService floating IP address is located and run the **ifconfig** *interface* **down** command to delete the floating IP address.

   h. Choose **Components** > **DBService** > **More** > **Restart Service** to restart DBService and check whether DBService is started successfully.

      -  If yes, go to :ref:`1.i <alm_27001__en-us_topic_0191813879_resumealarm1>`.
      -  If no, go to :ref:`2.a <alm_27001__en-us_topic_0191813879_step88>`.

   i. .. _alm_27001__en-us_topic_0191813879_resumealarm1:

      Wait about 2 minutes and check whether the alarm is cleared in the alarm list.

      -  If yes, no further action is required.
      -  If no, go to :ref:`Step 13 <alm_27001__en-us_topic_0191813879_loginact>`.

#. Check the status of the active DBServer instance.

   a. .. _alm_27001__en-us_topic_0191813879_step88:

      Select the DBServer instance whose role status is abnormal and record the IP address.

   b. On the **Alarms** page, check whether ALM-12007 Process Fault occurs in the DBServer instance on the host that corresponds to the IP address.

      -  If yes, go to :ref:`2.c <alm_27001__en-us_topic_0191813879_alarm27001>`.
      -  If no, go to :ref:`4 <alm_27001__en-us_topic_0191813879_li572522141314>`.

   c. .. _alm_27001__en-us_topic_0191813879_alarm27001:

      Rectify the fault by following steps provided in ALM-12007 Process Fault.

   d. Wait about 5 minutes and check whether the alarm is cleared in the alarm list.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_27001__en-us_topic_0191813879_li572522141314>`.

#. Check the status of the active and standby DBServers.

   a. .. _alm_27001__en-us_topic_0191813879_loginact:

      Log in to the host where the DBService floating IP address is located, run the **sudo su - root** and **su - omm** commands to switch to user **omm**, and run the **cd ${BIGDATA_HOME}/FusionInsight/dbservice/** command to go to the DBService installation directory.

   b. Run the **sh sbin/status-dbserver.sh** command to view the status of the active and standby HA processes of DBService. Determine whether the status can be viewed successfully.

      -  If yes, go to :ref:`3.c <alm_27001__en-us_topic_0191813879_loginactive>`.
      -  If no, go to :ref:`4 <alm_27001__en-us_topic_0191813879_li572522141314>`.

   c. .. _alm_27001__en-us_topic_0191813879_loginactive:

      Check whether the active and standby HA processes are abnormal.

      -  If yes, go to :ref:`3.d <alm_27001__en-us_topic_0191813879_recoverdb>`.
      -  If no, go to :ref:`4 <alm_27001__en-us_topic_0191813879_li572522141314>`.

   d. .. _alm_27001__en-us_topic_0191813879_recoverdb:

      Choose **Components** > **DBService** > **More** > **Restart Service** to restart DBService and check whether DBService is started successfully.

      -  If yes, go to :ref:`3.e <alm_27001__en-us_topic_0191813879_resumealarm>`.
      -  If no, go to :ref:`4 <alm_27001__en-us_topic_0191813879_li572522141314>`.

   e. .. _alm_27001__en-us_topic_0191813879_resumealarm:

      Wait about 2 minutes and check whether the alarm is cleared in the alarm list.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_27001__en-us_topic_0191813879_li572522141314>`.

#. .. _alm_27001__en-us_topic_0191813879_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
