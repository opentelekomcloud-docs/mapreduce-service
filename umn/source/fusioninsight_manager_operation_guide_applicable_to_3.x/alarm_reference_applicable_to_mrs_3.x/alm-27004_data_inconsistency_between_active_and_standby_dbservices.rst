:original_name: ALM-27004.html

.. _ALM-27004:

ALM-27004 Data Inconsistency Between Active and Standby DBServices
==================================================================

Description
-----------

The system checks the data synchronization status between the active and standby DBService every 10 seconds. This alarm is generated when the synchronization status cannot be queried for six consecutive times or when the synchronization status is abnormal.

This alarm is cleared when the synchronization status becomes normal.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
27004    Critical       Yes
======== ============== =====================

Parameters
----------

+-------------------------+---------------------------------------------------------+
| Name                    | Meaning                                                 |
+=========================+=========================================================+
| Source                  | Specifies the cluster for which the alarm is generated. |
+-------------------------+---------------------------------------------------------+
| ServiceName             | Specifies the service for which the alarm is generated. |
+-------------------------+---------------------------------------------------------+
| RoleName                | Specifies the role for which the alarm is generated.    |
+-------------------------+---------------------------------------------------------+
| HostName                | Specifies the host for which the alarm is generated.    |
+-------------------------+---------------------------------------------------------+
| Local DBService HA Name | Specifies the HA name of the local DBService.           |
+-------------------------+---------------------------------------------------------+
| Peer DBService HA Name  | Specifies the HA name of the peer DBService.            |
+-------------------------+---------------------------------------------------------+
| SYNC_PERCENT            | Specifies the synchronization percentage.               |
+-------------------------+---------------------------------------------------------+

Impact on the System
--------------------

When data is not synchronized between the active and standby DBServices, data may be lost or abnormal if the active instance becomes abnormal.

Possible Causes
---------------

-  The network between the active and standby nodes is unstable.
-  The standby DBService is abnormal.
-  The standby node disk space is full.
-  The CPU usage of the GaussDB process on the active DBService node is high. You need to locate the failure cause based on logs.

Procedure
---------

**Check whether the network between the active and standby nodes is normal.**

#. On FusionInsight Manager, choose **Cluster > Services > DBService > Instance**, check the service IP address of the standby DBServer instance.

#. Log in to the active DBService node as user **root**.

#. Run the **ping** *Standby DBService heartbeat IP address* command to check whether the standby DBService node is reachable.

   -  If yes, go to :ref:`6 <alm-27004__li53069850195034>`.
   -  If no, go to :ref:`4 <alm-27004__li40047077195034>`.

#. .. _alm-27004__li40047077195034:

   Contact the network administrator to check whether the network is faulty.

   -  If yes, go to :ref:`5 <alm-27004__li22196300195034>`.
   -  If no, go to :ref:`6 <alm-27004__li53069850195034>`.

#. .. _alm-27004__li22196300195034:

   Rectify the network fault and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-27004__li53069850195034>`.

**Check whether the standby DBService is normal.**

6. .. _alm-27004__li53069850195034:

   Log in to the standby DBService node as user **root**.

7. Run the **su - omm** command to switch to user **omm**.

8. Go to the **${DBSERVER_HOME}/sbin** directory and run the **./status-dbserver.sh** command to check whether the GaussDB resource status of the standby DBService is normal. In the command output, check whether the following information is displayed in the row where **ResName** is **gaussDB**:

   For example:

   .. code-block::

      10_10_10_231 gaussDB Standby_normal Normal Active_standby

   -  If yes, go to :ref:`9 <alm-27004__li13084069195034>`.
   -  If no, go to :ref:`16 <alm-27004__li45928829195034>`.

**Check whether the standby node disk space is full.**

9.  .. _alm-27004__li13084069195034:

    Log in to the standby DBService node as user **root**.

10. Run the **su - omm** command to switch to user **omm**.

11. Go to the **${DBSERVER_HOME}** directory, and run the following commands to obtain the DBService data directory:

    **cd ${DBSERVER_HOME}**

    **source .dbservice_profile**

    **echo ${DBSERVICE_DATA_DIR}**

12. Run the **df -h** command to view the system disk partition usage information.

13. Check whether the DBService data directory space is full.

    -  If yes, go to :ref:`14 <alm-27004__li255547195034>`.
    -  If no, go to :ref:`16 <alm-27004__li45928829195034>`.

14. .. _alm-27004__li255547195034:

    Expand the disk capacity.

15. After the disk capacity is expanded, wait 2 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`16 <alm-27004__li45928829195034>`.

**Collect fault information.**

16. .. _alm-27004__li45928829195034:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

17. In the **Service** area, select **DBService** of the target cluster and **OS**, **OS Statistics**, and **OS Performance** under **OMS**, and click **OK**.

18. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

19. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927470.png
