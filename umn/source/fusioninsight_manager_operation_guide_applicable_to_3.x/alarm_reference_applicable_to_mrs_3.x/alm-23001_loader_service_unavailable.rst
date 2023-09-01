:original_name: ALM-23001.html

.. _ALM-23001:

ALM-23001 Loader Service Unavailable
====================================

Description
-----------

The system checks the Loader service availability every 60 seconds. This alarm is generated when the system detects that the Loader service is unavailable. This alarm is cleared when the Loader service is available.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
23001    Critical       Yes
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

When the Loader service is unavailable, the data loading, import, and conversion functions are unavailable.

Possible Causes
---------------

-  The internal service on which the Loader service depends is abnormal.

   -  The ZooKeeper service is abnormal.
   -  The HDFS service is abnormal.
   -  The DBService service is abnormal.
   -  The Yarn service is abnormal.
   -  The Mapreduce service is abnormal.

-  Environment fault: The network is abnormal, which the Loader service cannot communicate with the depended internal services and cannot provide services.
-  Software fault: The Loader service cannot run properly.

Procedure
---------

**Check the ZooKeeper service status.**

#. On the FusionInsight Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services** > **ZooKeeper** to check whether the ZooKeeper running status is **Normal**.

   -  If yes, go to :ref:`3 <alm-23001__li796972081432>`.
   -  If no, go to :ref:`2 <alm-23001__li4762296581432>`.

#. .. _alm-23001__li4762296581432:

   Choose **More** > **Restart Service** to restart the ZooKeeper service. In the alarm list, check whether **LoaderService Unavailable** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-23001__li796972081432>`.

#. .. _alm-23001__li796972081432:

   On the FusionInsight Manager, check whether the alarm list contains **Process Fault**.

   -  If yes, go to :ref:`4 <alm-23001__li1999976981432>`.
   -  If no, go to :ref:`7 <alm-23001__li2767755181432>`.

#. .. _alm-23001__li1999976981432:

   In the **Location** area of **Process Fault**, check whether **ServiceName** is **ZooKeeper**.

   -  If yes, go to :ref:`5 <alm-23001__li936862281432>`.
   -  If no, go to :ref:`7 <alm-23001__li2767755181432>`.

#. .. _alm-23001__li936862281432:

   Rectify the fault by following the steps provided in **ALM-12007 Process Fault**.

#. In the alarm list, check whether **Loader Service Unavailable** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-23001__li2767755181432>`.

**Check the HDFS service status.**

7. .. _alm-23001__li2767755181432:

   On the FusionInsight Manager, check whether the alarm list contains **HDFS Service Unavailable**.

   -  If yes, go to :ref:`8 <alm-23001__li2728912881432>`.
   -  If no, go to :ref:`10 <alm-23001__li508775181432>`.

8. .. _alm-23001__li2728912881432:

   Rectify the fault by following the steps provided in **ALM-14000 HDFS Service Unavailable**.

9. In the alarm list, check whether **Loader Service Unavailable** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-23001__li508775181432>`.

**Check the DBService status.**

10. .. _alm-23001__li508775181432:

    On the FusionInsight Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services** > **DBService** to check whether the DBService running status is **Normal**.

    -  If yes, go to :ref:`12 <alm-23001__li1459212281432>`.
    -  If no, go to :ref:`11 <alm-23001__li600348181432>`.

11. .. _alm-23001__li600348181432:

    Choose **More** > **Restart Service** to restart the DBService service. In the alarm list, check whether **LoaderService Unavailable** is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-23001__li1459212281432>`.

**Check the Mapreduce status.**

12. .. _alm-23001__li1459212281432:

    On the FusionInsight Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services** > **Mapreduce** to check whether the Mapreduce running status is **Normal**.

    -  If yes, go to :ref:`16 <alm-23001__li3662318181432>`.
    -  If no, go to :ref:`13 <alm-23001__li3072601281432>`.

13. .. _alm-23001__li3072601281432:

    Choose **More** > **Restart Service** to restart the Mapreduce service. In the alarm list, check whether **LoaderService Unavailable** is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`16 <alm-23001__li3662318181432>`.

**Check the Yarn status.**

14. On the FusionInsight Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services** > **Yarn** to check whether the Yarn running status is **Normal**.

    -  If yes, go to :ref:`16 <alm-23001__li3662318181432>`.
    -  If no, go to :ref:`15 <alm-23001__li853150381432>`.

15. .. _alm-23001__li853150381432:

    Choose **More** > **Restart Service** to restart the Yarn service. In the alarm list, check whether **LoaderService Unavailable** is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`16 <alm-23001__li3662318181432>`.

16. .. _alm-23001__li3662318181432:

    On the FusionInsight Manager, check whether the alarm list contains **Yarn Service Unavailable**.

    -  If yes, go to :ref:`17 <alm-23001__li1368764681432>`.
    -  If no, go to :ref:`19 <alm-23001__li2284337281432>`.

17. .. _alm-23001__li1368764681432:

    Rectify the fault by following the steps provided in **ALM-18000 Yarn Service Unavailable**.

18. In the alarm list, check whether **Loader Service Unavailable** is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`19 <alm-23001__li2284337281432>`.

**Check the network connection between Loader and dependent components.**

19. .. _alm-23001__li2284337281432:

    On the FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Loader**.

20. Click **Instance** and the LoaderServer instance list is displayed.

21. .. _alm-23001__li5727208881432:

    Record the **Management IP Address** in the row of **LoaderServer(Active)**.

22. Log in to the host where the active LoaderServer runs as **omm** user using the IP address obtained in :ref:`21 <alm-23001__li5727208881432>`.

23. Run the **ping** command to check whether communication between the host that runs the active LoaderServer and the hosts that run the dependent components. (The dependent components include ZooKeeper, DBService, HDFS, Mapreduce and Yarn. Obtain the IP addresses of the hosts that run these services in the same way as that for obtaining the IP address of the active LoaderServer.)

    -  If yes, go to :ref:`26 <alm-23001__li2799521581432>`.
    -  If no, go to :ref:`24 <alm-23001__li904948781432>`.

24. .. _alm-23001__li904948781432:

    Contact the administrator to restore the network.

25. In the alarm list, check whether **Loader Service Unavailable** is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`26 <alm-23001__li2799521581432>`.

**Collect fault information.**

26. .. _alm-23001__li2799521581432:

    On the FusionInsight Manager, choose **O&M** > **Log** > **Download**.

27. Select the following nodes in the required cluster from the **Service** drop-down list:

    -  ZooKeeper
    -  HDFS
    -  DBService
    -  Yarn
    -  Mapreduce
    -  Loader

28. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

29. On the FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Loader**.

30. Choose **More** > **Restart Service**, and click **OK**.

31. Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`32 <alm-23001__li2579152581432>`.

32. .. _alm-23001__li2579152581432:

    Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583087489.png
