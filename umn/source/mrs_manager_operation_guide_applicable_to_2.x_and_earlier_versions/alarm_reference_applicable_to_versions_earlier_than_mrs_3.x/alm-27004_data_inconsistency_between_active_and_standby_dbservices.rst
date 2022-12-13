:original_name: alm_27004.html

.. _alm_27004:

ALM-27004 Data Inconsistency Between Active and Standby DBServices
==================================================================

Description
-----------

The system checks the data synchronization status between the active and standby DBServices every 10 seconds. This alarm is generated when the synchronization status cannot be queried for six consecutive times or when the synchronization status is abnormal.

This alarm is cleared when the synchronization is in normal state.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
27004    Critical       Yes
======== ============== ==========

Parameters
----------

+-------------------------+---------------------------------------------------------+
| Parameter               | Description                                             |
+=========================+=========================================================+
| ServiceName             | Specifies the service for which the alarm is generated. |
+-------------------------+---------------------------------------------------------+
| RoleName                | Specifies the role for which the alarm is generated.    |
+-------------------------+---------------------------------------------------------+
| HostName                | Specifies the host for which the alarm is generated.    |
+-------------------------+---------------------------------------------------------+
| Local DBService HA Name | Specifies a local DBService HA.                         |
+-------------------------+---------------------------------------------------------+
| Peer DBService HA Name  | Specifies a peer DBService HA.                          |
+-------------------------+---------------------------------------------------------+
| SYNC_PERSENT            | Synchronization percentage.                             |
+-------------------------+---------------------------------------------------------+

Impact on the System
--------------------

When data is not synchronized between the active and standby DBServices, the data may be lost or abnormal if the active instance becomes abnormal.

Possible Causes
---------------

-  The network between the active and standby nodes is unstable.
-  The standby DBService is abnormal.
-  The disk space of the standby node is full.

Procedure
---------

#. Check whether the network between the active and standby nodes is in normal state.

   a. Go to the cluster details page and choose **Alarms**.

   b. In the alarm list, locate the row that contains the alarm and view the IP address of the standby DBService node in the alarm details.

   c. Log in to the active DBService node.

   d. Run the **ping** *heartbeat IP address of the standby DBService* command to check whether the standby DBService node is reachable.

      -  If yes, go to :ref:`2.a <alm_27004__en-us_topic_0191813894_alm-27002_3_mmccppss_step6>`.
      -  If no, go to :ref:`1.e <alm_27004__en-us_topic_0191813894_alm-27002_3_mmccppss_step2>`.

   e. .. _alm_27004__en-us_topic_0191813894_alm-27002_3_mmccppss_step2:

      Contact the O&M personnel to check whether the network is faulty.

      -  If yes, go to :ref:`1.f <alm_27004__en-us_topic_0191813894_alm-27002_3_mmccppss_s4>`.
      -  If no, go to :ref:`2.a <alm_27004__en-us_topic_0191813894_alm-27002_3_mmccppss_step6>`.

   f. .. _alm_27004__en-us_topic_0191813894_alm-27002_3_mmccppss_s4:

      Rectify the network fault and check whether the alarm is cleared from the alarm list.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2.a <alm_27004__en-us_topic_0191813894_alm-27002_3_mmccppss_step6>`.

#. Check whether the standby DBService is in normal state.

   a. .. _alm_27004__en-us_topic_0191813894_alm-27002_3_mmccppss_step6:

      Log in to the standby DBService node.

   b. Run the following commands to switch the user:

      **sudo su - root**

      **su - omm**

   c. Go to the **${DBSERVER_HOME}/sbin** directory and run the **./status-dbserver.sh** command to check whether the GaussDB resource status of the standby DBService is in normal state. In the command output, check whether the following information is displayed in the row where **ResName** is **gaussDB**:

      Example:

      .. code-block::

         10_10_10_231 gaussDB Standby_normal Normal Active_standby

      -  If yes, go to :ref:`3.a <alm_27004__en-us_topic_0191813894_alm-27002_3_mmccppss_step9>`.
      -  If no, go to :ref:`4 <alm_27004__en-us_topic_0191813894_li572522141314>`.

#. Check whether the disk space of the standby node is insufficient.

   a. .. _alm_27004__en-us_topic_0191813894_alm-27002_3_mmccppss_step9:

      Log in to the standby DBService node.

   b. Run the following commands to switch the user:

      **sudo su - root**

      **su - omm**

   c. Go to the **${DBSERVER_HOME}** directory, and run the following commands to obtain the DBService data directory:

      **cd ${DBSERVER_HOME}**

      **source .dbservice_profile**

      **echo ${DBSERVICE_DATA_DIR}**

   d. Run the **df -h** command to check the system disk partition usage.

   e. Check whether the DBService data directory space is full.

      -  If yes, go to :ref:`3.f <alm_27004__en-us_topic_0191813894_alm-27002_3_mmccppss_step14>`.
      -  If no, go to :ref:`4 <alm_27004__en-us_topic_0191813894_li572522141314>`.

   f. .. _alm_27004__en-us_topic_0191813894_alm-27002_3_mmccppss_step14:

      Perform upgrade and expand capacity.

   g. After capacity expansion, wait 2 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_27004__en-us_topic_0191813894_li572522141314>`.

#. .. _alm_27004__en-us_topic_0191813894_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
