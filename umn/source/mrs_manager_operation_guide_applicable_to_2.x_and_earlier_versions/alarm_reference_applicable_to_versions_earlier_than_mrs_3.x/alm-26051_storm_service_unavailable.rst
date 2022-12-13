:original_name: alm_26051.html

.. _alm_26051:

ALM-26051 Storm Service Unavailable
===================================

Description
-----------

The system checks the Storm service availability every 30 seconds. This alarm is generated if the Storm service becomes unavailable after all Nimbus nodes in a cluster become abnormal.

This alarm is cleared after the Storm service recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
26051    Critical       Yes
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

-  The cluster cannot provide the Storm service.
-  Users cannot run new Storm tasks.

Possible Causes
---------------

-  The Kerberos component is faulty.
-  ZooKeeper is faulty or suspended.
-  The active and standby Nimbus nodes in the Storm cluster are abnormal.

Procedure
---------

#. Check the Kerberos component status. For clusters without Kerberos authentication, skip this step and go to :ref:`2 <alm_26051__en-us_topic_0191813871_li59618494175936>`.

   a. Go to the MRS cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. .. _alm_26051__en-us_topic_0191813871_li4574896917592:

      Check whether the health status of the Kerberos service is **Good**.

      -  If yes, go to :ref:`2.a <alm_26051__en-us_topic_0191813871_li384738318010>`.
      -  If no, go to :ref:`1.c <alm_26051__en-us_topic_0191813871_li22276139175922>`.

   c. .. _alm_26051__en-us_topic_0191813871_li22276139175922:

      Rectify the fault by following instructions in ALM-25500 KrbServer Service Unavailable.

   d. Perform :ref:`1.b <alm_26051__en-us_topic_0191813871_li4574896917592>` again.

#. .. _alm_26051__en-us_topic_0191813871_li59618494175936:

   Check the ZooKeeper component status.

   a. .. _alm_26051__en-us_topic_0191813871_li384738318010:

      Check whether the health status of the ZooKeeper service is **Good**.

      -  If yes, go to :ref:`3.a <alm_26051__en-us_topic_0191813871_li2005716918338>`.
      -  If no, go to :ref:`2.b <alm_26051__en-us_topic_0191813871_li398384891819>`.

   b. .. _alm_26051__en-us_topic_0191813871_li398384891819:

      If the ZooKeeper service is stopped, start it. For other problems, follow the instructions in ALM-13000 ZooKeeper Service Unavailable.

   c. Perform :ref:`2.a <alm_26051__en-us_topic_0191813871_li384738318010>` again.

#. Check the status of the active and standby Nimbus nodes.

   a. .. _alm_26051__en-us_topic_0191813871_li2005716918338:

      Choose **Components** > **Storm** > **Nimbus**.

   b. In **Role**, check whether only one active Nimbus node exists.

      -  If yes, go to :ref:`4 <alm_26051__en-us_topic_0191813871_li572522141314>`.
      -  If no, go to :ref:`3.c <alm_26051__en-us_topic_0191813871_li4603773018356>`.

   c. .. _alm_26051__en-us_topic_0191813871_li4603773018356:

      Select the two Nimbus instances and choose **More** > **Restart Instance**. Check whether the restart is successful.

      -  If yes, go to :ref:`3.d <alm_26051__en-us_topic_0191813871_li632054418412>`.
      -  If no, go to :ref:`4 <alm_26051__en-us_topic_0191813871_li572522141314>`.

   d. .. _alm_26051__en-us_topic_0191813871_li632054418412:

      Log in to MRS Manager again and choose **Components** > **Storm** > **Nimbus**. Check whether the health status of Nimbus is **Good**.

      -  If yes, go to :ref:`3.e <alm_26051__en-us_topic_0191813871_li5966586218421>`.
      -  If no, go to :ref:`4 <alm_26051__en-us_topic_0191813871_li572522141314>`.

   e. .. _alm_26051__en-us_topic_0191813871_li5966586218421:

      Wait 30 seconds and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_26051__en-us_topic_0191813871_li572522141314>`.

#. .. _alm_26051__en-us_topic_0191813871_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Related Information
-------------------

N/A
