:original_name: ALM-16004.html

.. _ALM-16004:

ALM-16004 Hive Service Unavailable
==================================

Description
-----------

This alarm is generated when the HiveServer service is unavailable. The system checks the HiveServer service status every 60 seconds.

This alarm is cleared when the HiveServer service is normal.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
16004    Critical       Yes
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

The system cannot provide data loading, query, and extraction services.

Possible Causes
---------------

-  Hive service unavailability may be related to the faults of the Hive process as well as basic services, such as ZooKeeper, Hadoop distributed file system (HDFS), Yarn, and DBService.

   -  The ZooKeeper service is abnormal.
   -  The HDFS service is abnormal.
   -  The Yarn service is abnormal.
   -  The DBService service is abnormal.
   -  The Hive service process is abnormal. If the alarm is caused by Hive process fault, the alarm report has a delay of about 5 minutes.

-  The network communication between the Hive and basic services is interrupted.

Procedure
---------

**Check the HiveServer/MetaStore process status.**

#. On the FusionInsight Manager portal, click **Cluster >** *Name of the desired cluster* **> Services** > **Hive** > **Instance**. In the Hive instance list, check whether the HiveServer or MetaStore instances are in the Unknown state.

   -  If yes, go to :ref:`2 <alm-16004__li45196532141457>`.
   -  If no, go to :ref:`4 <alm-16004__li31923589141457>`.

#. .. _alm-16004__li45196532141457:

   In the Hive instance list, choose **More** > **Restart Instance** to restart the HiveServer/MetaStore process.

#. In the alarm list, check whether **Hive Service Unavailable** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-16004__li31923589141457>`.

**Check the ZooKeeper service status.**

4. .. _alm-16004__li31923589141457:

   On the FusionInsight Manager, check whether the alarm list contains **Process Fault**.

   -  If yes, go to :ref:`5 <alm-16004__li58014365141457>`.
   -  If no, go to :ref:`8 <alm-16004__li41412512141457>`.

5. .. _alm-16004__li58014365141457:

   In the **Process Fault**, check whether **ServiceName** is **ZooKeeper**.

   -  If yes, go to :ref:`6 <alm-16004__li1543118141457>`.
   -  If no, go to :ref:`8 <alm-16004__li41412512141457>`.

6. .. _alm-16004__li1543118141457:

   Rectify the fault by following the steps provided in "ALM-12007 Process Fault".

7. In the alarm list, check whether **Hive Service Unavailable** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-16004__li41412512141457>`.

**Check the HDFS service status.**

8.  .. _alm-16004__li41412512141457:

    On the FusionInsight Manager, check whether the alarm list contains **HDFS Service Unavailable**.

    -  If yes, go to :ref:`9 <alm-16004__li66079189141457>`.
    -  If no, go to :ref:`11 <alm-16004__li26828739141457>`.

9.  .. _alm-16004__li66079189141457:

    Rectify the fault by following the steps provided in "ALM-14000 HDFS Service Unavailable".

10. In the alarm list, check whether **Hive Service Unavailable** is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-16004__li26828739141457>`.

**Check the Yarn service status.**

11. .. _alm-16004__li26828739141457:

    In FusionInsight Manager alarm list, check whether **Yarn Service Unavailable** is generated.

    -  If yes, go to :ref:`12 <alm-16004__li25644284141457>`.
    -  If no, go to :ref:`14 <alm-16004__li53539591141457>`.

12. .. _alm-16004__li25644284141457:

    Rectify the fault. For details, see "ALM-18000 Yarn Service Unavailable".

13. In the alarm list, check whether **Hive Service Unavailable** is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`14 <alm-16004__li53539591141457>`.

**Check the DBService service status.**

14. .. _alm-16004__li53539591141457:

    In FusionInsight Manager alarm list, check whether **DBService Service Unavailable** is generated.

    -  If yes, go to :ref:`15 <alm-16004__li41739587141457>`.
    -  If no, go to :ref:`17 <alm-16004__li44837990141457>`.

15. .. _alm-16004__li41739587141457:

    Rectify the fault. For details, see "ALM-27001 DBService Service Unavailable".

16. In the alarm list, check whether **Hive Service Unavailable** is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`17 <alm-16004__li44837990141457>`.

**Check the network connection between the Hive and ZooKeeper, HDFS, Yarn, and DBService.**

17. .. _alm-16004__li44837990141457:

    On the FusionInsight Manager, choose **Cluster >** *Name of the desired cluster* **> Services** > **Hive**.

18. Click **Instance**.

    The HiveServer instance list is displayed.

19. Click **Host Name** in the row of **HiveServer**.

    The active HiveServer host status page is displayed.

20. .. _alm-16004__li19527969141457:

    Record the IP address under **Basic Information**.

21. Use the IP address obtained in :ref:`20 <alm-16004__li19527969141457>` to log in to the host where the active HiveServer runs as user **omm**.

22. Run the **ping** command to check whether communication between the host that runs the active HiveServer and the hosts that run the ZooKeeper, HDFS, Yarn, and DBService services is normal. (Obtain the IP addresses of the hosts that run the ZooKeeper, HDFS, Yarn, and DBService services in the same way as that for obtaining the IP address of the active HiveServer.)

    -  If yes, go to :ref:`25 <alm-16004__li18695793141457>`.
    -  If no, go to :ref:`23 <alm-16004__li42271322141457>`.

23. .. _alm-16004__li42271322141457:

    Contact the administrator to restore the network.

24. In the alarm list, check whether **Hive Service Unavailable** is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`25 <alm-16004__li18695793141457>`.

**Collect fault information.**

25. .. _alm-16004__li18695793141457:

    On the FusionInsight Manager, choose **O&M** > **Log > Download**.

26. Select the following nodes in the required cluster from the **Service**:

    -  ZooKeeper
    -  HDFS
    -  Yarn
    -  DBService
    -  Hive

27. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

28. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927286.png
