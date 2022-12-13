:original_name: alm_12039.html

.. _alm_12039:

ALM-12039 GaussDB Data Is Not Synchronized
==========================================

Description
-----------

The system checks the data synchronization status between the active and standby GaussDB nodes every 10 seconds. This alarm is generated when the synchronization status cannot be queried for six consecutive times or when the synchronization status is abnormal.

This alarm is cleared when the data synchronization status is normal.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12039    Critical       Yes
======== ============== ==========

Parameter
---------

=================== =========================================
Parameter           Description
=================== =========================================
ServiceName         Service for which the alarm is generated.
RoleName            Role for which the alarm is generated.
HostName            Host for which the alarm is generated.
Local GaussDB HA IP HA IP address of the local GaussDB.
Peer GaussDB HA IP  HA IP address of the peer GaussDB.
SYNC_PERSENT        Synchronization percentage.
=================== =========================================

Impact on the System
--------------------

When data is not synchronized between the active and standby GaussDBs, the data may be lost or abnormal if the active instance becomes abnormal.

Possible Causes
---------------

-  The network between the active and standby nodes is unstable.
-  The standby GaussDB is abnormal.
-  The disk space of the standby node is full.

Procedure
---------

#. Go to the MRS cluster details page. In the alarm list on the alarm management tab page, click the row that contains the alarm. In the alarm details, view the IP address of the standby GaussDB node.

#. Log in to the active management node.

#. Run the following command to check whether the standby GaussDB is reachable:

   **ping** *heartbeat IP address of the standby GaussDB*

   If yes, go to :ref:`6 <alm_12039__en-us_topic_0191813916_li39909275144355>`.

   If no, go to :ref:`4 <alm_12039__en-us_topic_0191813916_li1095691144355>`.

#. .. _alm_12039__en-us_topic_0191813916_li1095691144355:

   Contact the O&M personnel to check whether the network is faulty.

   -  If yes, go to :ref:`5 <alm_12039__en-us_topic_0191813916_li8186264144355>`.
   -  If no, go to :ref:`6 <alm_12039__en-us_topic_0191813916_li39909275144355>`.

#. .. _alm_12039__en-us_topic_0191813916_li8186264144355:

   Rectify the network fault and check whether the alarm is cleared from the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm_12039__en-us_topic_0191813916_li39909275144355>`.

#. .. _alm_12039__en-us_topic_0191813916_li39909275144355:

   Log in to the standby GaussDB node.

#. Run the following commands to switch the user:

   **sudo su - root**

   **su - omm**

#. Go to the **${BIGDATA_HOME}/om-0.0.1/sbin/** directory.

   Run the following command to check whether the resource status of the standby GaussDB is normal:

   **sh status-oms.sh**

   In the command output, check whether the following information is displayed in the row where **ResName** is **gaussDB**:

   .. code-block::

      10_10_10_231 gaussDB Standby_normal Normal Active_standby

   -  If yes, go to :ref:`9 <alm_12039__en-us_topic_0191813916_li58535127144355>`.
   -  If no, go to :ref:`15 <alm_12039__en-us_topic_0191813916_li572522141314>`.

9.  .. _alm_12039__en-us_topic_0191813916_li58535127144355:

    Log in to the standby GaussDB node.

10. Run the following commands to switch the user:

    **sudo su - root**

    **su - omm**

11. Run the **echo ${BIGDATA_DATA_HOME}/dbdata_om** command to obtain the GaussDB data directory.

12. Run the **df -h** command to check the system disk partition usage.

13. Check whether the disk where the GaussDB data directory is mounted is full.

    -  If yes, go to :ref:`14 <alm_12039__en-us_topic_0191813916_li31581498144355>`.
    -  If no, go to :ref:`15 <alm_12039__en-us_topic_0191813916_li572522141314>`.

14. .. _alm_12039__en-us_topic_0191813916_li31581498144355:

    Contact the O&M personnel to expand the disk capacity. After capacity expansion, wait 2 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`15 <alm_12039__en-us_topic_0191813916_li572522141314>`.

15. .. _alm_12039__en-us_topic_0191813916_li572522141314:

    Collect fault information.

    a. On MRS Manager, choose **System** > **Export Log**.
    b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
