:original_name: alm_24000.html

.. _alm_24000:

ALM-24000 Flume Service Unavailable
===================================

Description
-----------

The alarm module checks the Flume service status every 180 seconds. This alarm is generated if the Flume service is abnormal.

This alarm is cleared after the Flume service recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
24000    Critical       Yes
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

Flume cannot work and data transmission is interrupted.

Possible Causes
---------------

-  HDFS is unavailable.
-  LdapServer is unavailable.

Procedure
---------

#. Check the HDFS status.

   a. Go to the MRS cluster details page and choose **Alarms**.
   b. Check whether the ALM-14000 HDFS Service Unavailable alarm is generated.

      -  If yes, clear the alarm according to the handling suggestions of "ALM-14000 HDFS Service Unavailable".
      -  If no, go to :ref:`2 <alm_24000__en-us_topic_0191813917_li56731580163419>`.

#. .. _alm_24000__en-us_topic_0191813917_li56731580163419:

   Check the LdapServer status.

   Check whether the ALM-25000 LdapServer Service Unavailable alarm is generated.

   -  If yes, clear the alarm according to the handling suggestions of "ALM-25000 LdapServer Service Unavailable".
   -  If no, go to :ref:`3.b <alm_24000__en-us_topic_0191813917_li950355316374>`.

#. Check whether the HDFS and LdapServer services are stopped.

   a. Go to the MRS cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. .. _alm_24000__en-us_topic_0191813917_li950355316374:

      In the service list on MRS Manager, check whether the HDFS and LdapServer services are stopped.

      -  If yes, start the HDFS and LdapServer services and go to :ref:`3.c <alm_24000__en-us_topic_0191813917_li4163406916374>`.
      -  If no, go to :ref:`4 <alm_24000__en-us_topic_0191813917_li572522141314>`.

   c. .. _alm_24000__en-us_topic_0191813917_li4163406916374:

      Check whether the "ALM-24000 Flume Service Unavailable" alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_24000__en-us_topic_0191813917_li572522141314>`.

#. .. _alm_24000__en-us_topic_0191813917_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Related Information
-------------------

N/A
