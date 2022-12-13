:original_name: alm_12002.html

.. _alm_12002:

ALM-12002 HA Resource Is Abnormal
=================================

Description
-----------

The high availability (HA) software periodically checks the WebService floating IP addresses and databases of Manager. This alarm is generated when the HA software detects that the WebService floating IP addresses or databases are abnormal.

This alarm is cleared when the HA software detects that the floating IP addresses or databases are normal.

**Attribute**
-------------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12002    Major          Yes
======== ============== ==========

Parameter
---------

=========== ========================================================
Parameter   Description
=========== ========================================================
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
RESName     Specifies the resource for which the alarm is generated.
=========== ========================================================

Impact on the System
--------------------

If the WebService floating IP addresses of Manager are abnormal, users cannot log in to or use Manager. If databases of Manager are abnormal, all core services and related service processes, such as alarms and monitoring functions, are affected.

Possible Causes
---------------

-  The floating IP address is abnormal.
-  The database is abnormal.

Procedure
---------

#. Check the floating IP address status of the active management node.

   a. Go to the MRS cluster details page. In the alarm list on the alarm management tab page, click the row that contains the alarm. In the alarm details, view the host address and resource name of the alarm.

   b. Log in to the active management node. Run the following commands to switch the user:

      **sudo su - root**

      **su - omm**

   c. Go to the **${BIGDATA_HOME}/om-0.0.1/sbin/** directory, run the **status-oms.sh** script to check whether the floating IP address of the active Manager is normal. View the command output, locate the row where **ResName** is **floatip**, and check whether the following information is displayed.

      Example:

      .. code-block::

         10-10-10-160 floatip Normal Normal Single_active

      -  If yes, go to :ref:`2 <alm_12002__en-us_topic_0191813914_li50663096131636>`.
      -  If no, go to :ref:`1.d <alm_12002__en-us_topic_0191813914_li41799423131631>`.

   d. .. _alm_12002__en-us_topic_0191813914_li41799423131631:

      Contact the O&M personnel to check whether the floating IP NIC exists.

      -  If yes, go to :ref:`2 <alm_12002__en-us_topic_0191813914_li50663096131636>`.
      -  If no, go to :ref:`1.e <alm_12002__en-us_topic_0191813914_li6978622131725>`.

   e. .. _alm_12002__en-us_topic_0191813914_li6978622131725:

      Contact O&M personnel to rectify the NIC fault.

      Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_12002__en-us_topic_0191813914_li50663096131636>`.

#. .. _alm_12002__en-us_topic_0191813914_li50663096131636:

   Check the database status of the active and standby management nodes.

   a. Log in to the active and standby management nodes, run the **sudo su - root** and **su - ommdba** commands to switch to user **ommdba**, and run the **gs_ctl query** command to check whether the following information is displayed in the command output.

      Command output of the active management node:

      .. code-block::

         Ha state:
         LOCAL_ROLE: Primary
         STATIC_CONNECTIONS: 1
         DB_STATE: Normal
         DETAIL_INFORMATION: user/password invalid
          Senders info:
         No information
          Receiver info:
         No information

      Command output of the standby management node:

      .. code-block::

         Ha state:
         LOCAL_ROLE: Standby
         STATIC_CONNECTIONS: 1
         DB_STATE : Normal
         DETAIL_INFORMATION: user/password invalid
          Senders info:
         No information
          Receiver info:
         No information

      -  If yes, go to :ref:`2.c <alm_12002__en-us_topic_0191813914_li55696398142240>`.
      -  If no, go to :ref:`2.b <alm_12002__en-us_topic_0191813914_li40232703142216>`.

   b. .. _alm_12002__en-us_topic_0191813914_li40232703142216:

      Contact the O&M personnel to check whether a network fault occurs and rectify the fault.

      -  If yes, go to :ref:`2.c <alm_12002__en-us_topic_0191813914_li55696398142240>`.
      -  If no, go to :ref:`3 <alm_12002__en-us_topic_0191813935_li2924012813025>`.

   c. .. _alm_12002__en-us_topic_0191813914_li55696398142240:

      Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_12002__en-us_topic_0191813935_li2924012813025>`.

#. .. _alm_12002__en-us_topic_0191813935_li2924012813025:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
