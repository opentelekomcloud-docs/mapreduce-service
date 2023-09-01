:original_name: ALM-12039.html

.. _ALM-12039:

ALM-12039 Active/Standby OMS Databases Not Synchronized
=======================================================

Description
-----------

The system checks the data synchronization status between the active and standby OMS Databases every 10 seconds. This alarm is generated when the synchronization status cannot be queried for 30 consecutive times or when the synchronization status is abnormal.

This alarm is cleared when the data synchronization status becomes normal.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12039    Critical       Yes
======== ============== ==========

Parameters
----------

+---------------------+-------------------------------------------------------------------+
| Name                | Meaning                                                           |
+=====================+===================================================================+
| Source              | Specifies the cluster or system for which the alarm is generated. |
+---------------------+-------------------------------------------------------------------+
| ServiceName         | Specifies the service for which the alarm is generated.           |
+---------------------+-------------------------------------------------------------------+
| RoleName            | Specifies the role for which the alarm is generated.              |
+---------------------+-------------------------------------------------------------------+
| HostName            | Specifies the host for which the alarm is generated.              |
+---------------------+-------------------------------------------------------------------+
| Local GaussDB HA IP | Specifies the HA IP address of the local GaussDB.                 |
+---------------------+-------------------------------------------------------------------+
| Peer GaussDB HA IP  | Specifies the HA IP address of the peer GaussDB.                  |
+---------------------+-------------------------------------------------------------------+
| SYNC_PERCENT        | Specifies the synchronization percentage.                         |
+---------------------+-------------------------------------------------------------------+

Impact on the System
--------------------

When data is not synchronized between the active and standby OMS Databases, data may be lost or abnormal if the active instance becomes abnormal.

Possible Causes
---------------

-  The network between the active and standby nodes is unstable.
-  The standby OMS Database is abnormal.
-  The standby node disk space is full.

Procedure
---------

**Check whether the network between the active and standby nodes is normal.**

#. Log in to FusionInsight Manager, click **O&M > Alarm > Alarms**, click |image1| in the row where the alarm is located, and query the standby OMS Database IP address.

#. Log in to the active OMS Database node as user **root**.

#. Run the **ping** *Standby OMS Database heartbeat IP address* command to check whether the standby OMS Database node is reachable.

   -  If yes, go to :ref:`6 <alm-12039__li19362442104950>`.
   -  If no, go to :ref:`4 <alm-12039__li36080609104950>`.

#. .. _alm-12039__li36080609104950:

   Contact the network administrator to check whether the network is faulty.

   -  If yes, go to :ref:`5 <alm-12039__li35036231104950>`.
   -  If no, go to :ref:`6 <alm-12039__li19362442104950>`.

#. .. _alm-12039__li35036231104950:

   Rectify the network fault and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12039__li19362442104950>`.

**Check whether the standby OMS Database is normal.**

6. .. _alm-12039__li19362442104950:

   Log in to the standby OMS Database node as user **root**.

7. Run the **su - omm** command to switch to user **omm**.

8. Go to the **${BIGDATA_HOME}/om-server/om/sbin/** directory and run the **./status-oms.sh** command to check whether the OMS Database resource status of the standby DBService is normal. In the command output, check whether the following information is displayed in the row where **ResName** is **gaussDB**:

   For example:

   .. code-block::

      10_10_10_231 gaussDB Standby_normal Normal Active_standby

   -  If yes, go to :ref:`9 <alm-12039__li14387074104950>`.
   -  If no, go to :ref:`16 <alm-12039__li64121842104950>`.

**Check whether the standby node disk space is full.**

9.  .. _alm-12039__li14387074104950:

    Log in to the standby OMS Database node as user **root**.

10. Run the **su - omm** command to switch to user **omm**.

11. Run the **echo ${BIGDATA_DATA_HOME}/dbdata_om** command to obtain the OMS Database data directory.

12. Run the **df -h** command to view the system disk partition usage information.

13. Check whether the disk where the OMS Database data directory is mounted is full.

    -  If yes, go to :ref:`14 <alm-12039__li27597409104950>`.
    -  If no, go to :ref:`16 <alm-12039__li64121842104950>`.

14. .. _alm-12039__li27597409104950:

    Expand the disk capacity.

15. After the disk capacity is expanded, wait 2 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`16 <alm-12039__li64121842104950>`.

**Collect fault information.**

16. .. _alm-12039__li64121842104950:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

17. Select **OMMServer** from the **Service** and click **OK**.

18. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

19. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582927757.png
.. |image2| image:: /_static/images/en-us_image_0000001532448378.png
