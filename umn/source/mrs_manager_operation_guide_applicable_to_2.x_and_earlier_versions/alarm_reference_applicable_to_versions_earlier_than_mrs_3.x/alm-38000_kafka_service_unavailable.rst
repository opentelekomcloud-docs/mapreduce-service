:original_name: alm_38000.html

.. _alm_38000:

ALM-38000 Kafka Service Unavailable
===================================

Description
-----------

The system checks the Kafka service availability every 30 seconds. This alarm is generated if the Kafka service becomes unavailable.

This alarm is cleared after the Kafka service recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
38000    Critical       Yes
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

The cluster cannot provide the Kafka service and users cannot run new Kafka tasks.

Possible Causes
---------------

-  The KrbServer component is faulty.
-  The ZooKeeper component is faulty or fails to respond.
-  The Broker node in the Kafka cluster is abnormal.

Procedure
---------

#. Check the KrbServer component status. For clusters without Kerberos authentication, skip this step and go to :ref:`2 <alm_38000__en-us_topic_0191813970_li21507667181241>`.

   a. Go to the MRS cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. .. _alm_38000__en-us_topic_0191813970_li1071286918299:

      Check whether the health status of the KrbServer service is **Good**.

      -  If yes, go to :ref:`2.a <alm_38000__en-us_topic_0191813970_li22712539182948>`.
      -  If no, go to :ref:`1.c <alm_38000__en-us_topic_0191813970_li50060872182922>`.

   c. .. _alm_38000__en-us_topic_0191813970_li50060872182922:

      Rectify the fault by following instructions in ALM-25500 KrbServer Service Unavailable.

   d. Perform :ref:`1.b <alm_38000__en-us_topic_0191813970_li1071286918299>` again.

#. .. _alm_38000__en-us_topic_0191813970_li21507667181241:

   Check the ZooKeeper component status.

   a. .. _alm_38000__en-us_topic_0191813970_li22712539182948:

      Check whether the health status of the ZooKeeper service is **Good**.

      -  If yes, go to :ref:`3.a <alm_38000__en-us_topic_0191813970_li6551802183028>`.
      -  If no, go to :ref:`2.b <alm_38000__en-us_topic_0191813970_li35295745182948>`.

   b. .. _alm_38000__en-us_topic_0191813970_li35295745182948:

      If the ZooKeeper service is stopped, start it. For other problems, follow the instructions in ALM-13000 ZooKeeper Service Unavailable.

   c. Perform :ref:`2.a <alm_38000__en-us_topic_0191813970_li22712539182948>` again.

#. Check the Broker status.

   a. .. _alm_38000__en-us_topic_0191813970_li6551802183028:

      Choose **Components** > **Kafka** > **Broker**.

   b. In **Role**, check whether all instances are normal.

      -  If yes, go to :ref:`3.d <alm_38000__en-us_topic_0191813970_li54013684183028>`.
      -  If no, go to :ref:`3.c <alm_38000__en-us_topic_0191813970_li7614495183028>`.

   c. .. _alm_38000__en-us_topic_0191813970_li7614495183028:

      Select all instances of Broker and choose **More** > **Restart Instance**.

      -  If the restart is successful, go to :ref:`3.d <alm_38000__en-us_topic_0191813970_li54013684183028>`.
      -  If the restart fails, go to :ref:`4 <alm_38000__en-us_topic_0191813970_li572522141314>`.

   d. .. _alm_38000__en-us_topic_0191813970_li54013684183028:

      Choose **Components > Kafka**. Check whether the health status of Kafka is **Good**.

      -  If yes, go to :ref:`3.e <alm_38000__en-us_topic_0191813970_li11571314183028>`.
      -  If no, go to :ref:`4 <alm_38000__en-us_topic_0191813970_li572522141314>`.

   e. .. _alm_38000__en-us_topic_0191813970_li11571314183028:

      Wait 30 seconds and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_38000__en-us_topic_0191813970_li572522141314>`.

#. .. _alm_38000__en-us_topic_0191813970_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Related Information
-------------------

N/A
