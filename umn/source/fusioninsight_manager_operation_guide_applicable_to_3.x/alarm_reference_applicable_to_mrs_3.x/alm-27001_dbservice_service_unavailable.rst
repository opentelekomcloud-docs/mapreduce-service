:original_name: ALM-27001.html

.. _ALM-27001:

ALM-27001 DBService Service Unavailable
=======================================

Description
-----------

The alarm module checks the DBService service status every 30 seconds. This alarm is generated when the system detects that DBService service is unavailable.

This alarm is cleared when DBService service recovers.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
27001    Critical       Yes
======== ============== =====================

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

The database service is unavailable and cannot provide data import and query functions for upper-layer services, which results in some services exceptions.

Possible Causes
---------------

-  The floating IP address does not exist.
-  There is no active DBServer instance.
-  The active and standby DBServer processes are abnormal.

Procedure
---------

**Check whether the floating IP address exists in the cluster environment.**

#. On the FusionInsight Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services** > **DBService** > **Instance**.

#. Check whether the active instance exists.

   -  If yes, go to :ref:`3 <alm-27001__li35546035195610>`.
   -  If no, go to :ref:`9 <alm-27001__li20066855195610>`.

#. .. _alm-27001__li35546035195610:

   Select the active DBServer instance and record the IP address.

#. Log in to the host that corresponds to the preceding IP address as user **root**, and run the **ifconfig** command to check whether the DBService floating IP address exists on the node.

   -  If yes, go to :ref:`5 <alm-27001__li43040801195610>`.
   -  If no, go to :ref:`9 <alm-27001__li20066855195610>`.

#. .. _alm-27001__li43040801195610:

   Run the **ping** *floatip* command to check whether the DBService floating IP address can be pinged successfully.

   -  If yes, go to :ref:`6 <alm-27001__li121041629131211>`.
   -  If no, go to :ref:`9 <alm-27001__li20066855195610>`.

#. .. _alm-27001__li121041629131211:

   Log in to the host that corresponds to the DBService floating IP address as user **root**, and run the command to delete the floating IP address.

   **ifconfig** *interface* **down**

#. On the FusionInsight Manager home page, choose **Cluster >** *Name of the desired cluster* > **Services** > **DBService** > **More** > **Restart Service** to restart DBService, and check whether DBService is restarted successfully.

   -  If yes, go to :ref:`8 <alm-27001__li17142731195610>`.
   -  If no, go to :ref:`9 <alm-27001__li20066855195610>`.

#. .. _alm-27001__li17142731195610:

   Wait for about 2 minutes and check whether the alarm is cleared in the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`14 <alm-27001__li6055948195610>`.

**Check the status of the active DBServer instance.**

9.  .. _alm-27001__li20066855195610:

    Select the DBServer instance whose role status is abnormal and record the IP address.

10. On the **Alarm** page, check whether **Process Fault** occurs in the DBServer instance on the host that corresponds to the IP address.

    -  If yes, go to :ref:`11 <alm-27001__li26594651195610>`.
    -  If no, go to :ref:`14 <alm-27001__li6055948195610>`.

11. .. _alm-27001__li26594651195610:

    Handle the alarm according to "ALM-12007 Process Fault".

12. Wait for about 5 minutes and check whether the alarm is cleared in the alarm list.

    -  If yes, no further action is required.
    -  If no, go to :ref:`19 <alm-27001__li10820419195610>`.

**Check the status of the active and standby DBServers.**

13. Log in to the host that corresponds to the preceding IP address as user **root**, and run the **su - omm** command to switch to user **omm**.

14. .. _alm-27001__li6055948195610:

    Run the **cd ${DBSERVER_HOME}** command to go to the installation directory of the DBService.

15. Run the **sh sbin/status-dbserver.sh** command to view the status of the active and standby HA processes of DBService. Determine whether the status can be viewed successfully.

    .. code-block::

       HAMode
       double

       NodeName                  HostName               HAVersion                StartTime                HAActive             HAAllResOK           HARunPhase
       10_5_89_12                host01                 V100R001C01              2019-06-13 21:33:09      active               normal               Actived
       10_5_89_66                host03                 V100R001C01              2019-06-13 21:33:09      standby              normal               Deactived

       NodeName                  ResName                ResStatus                ResHAStatus              ResType
       10_5_89_12                floatip                Normal                   Normal                   Single_active
       10_5_89_12                gaussDB                Active_normal            Normal                   Active_standby
       10_5_89_66                floatip                Stopped                  Normal                   Single_active
       10_5_89_66                gaussDB                Standby_normal           Normal                   Active_standby

    -  If yes, go to :ref:`16 <alm-27001__li56882203195610>`.
    -  If no, go to :ref:`19 <alm-27001__li10820419195610>`.

16. .. _alm-27001__li56882203195610:

    Check whether the active and standby HA processes are in the abnormal state.

    -  If yes, go to :ref:`17 <alm-27001__li30245369195610>`.
    -  If no, go to :ref:`19 <alm-27001__li10820419195610>`.

17. .. _alm-27001__li30245369195610:

    On FusionInsight Manager, choose **Cluster >** *Name of the desired cluster* > **Services** > **DBService** > **More** > **Restart Service** to restart DBService, and check whether the system displays a message indicating that the restart is successful.

    -  If yes, go to :ref:`18 <alm-27001__li50093336195610>`.
    -  If no, go to :ref:`19 <alm-27001__li10820419195610>`.

18. .. _alm-27001__li50093336195610:

    Wait for about 2 minutes and check whether the alarm is cleared in the alarm list.

    -  If yes, no further action is required.
    -  If no, go to :ref:`19 <alm-27001__li10820419195610>`.

**Collect fault information.**

19. .. _alm-27001__li10820419195610:

    On FusionInsight Manager, choose **O&M** > **Log > Download**.

20. Select **DBService** in the required cluster and **NodeAgent** from the **Service**.

21. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

22. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269417464.png
