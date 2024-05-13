:original_name: ALM-19000.html

.. _ALM-19000:

ALM-19000 HBase Service Unavailable
===================================

Description
-----------

This alarm is generated when the HBase service is unavailable. The alarm module checks the HBase service status every 120 seconds.

This alarm is cleared when the HBase service recovers.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
19000    Critical       Yes
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

Operations, such as reading or writing data and creating tables, cannot be performed.

Possible Causes
---------------

-  The ZooKeeper service is abnormal.
-  The HDFS service is abnormal.
-  The HBase service is abnormal.
-  The network is abnormal.

Procedure
---------

**Check the ZooKeeper service status.**

#. On the MRS Manager, check whether the running status of ZooKeeper is **Normal** on service list.

   -  If yes, go to :ref:`5 <alm-19000__li31549687192610>`.
   -  If no, go to :ref:`2 <alm-19000__li42710393192610>`.

#. .. _alm-19000__li42710393192610:

   In the alarm list, check whether **ALM-13000 ZooKeeper Service Unavailable** exists.

   -  If yes, go to :ref:`3 <alm-19000__li36989843192610>`.
   -  If no, go to :ref:`5 <alm-19000__li31549687192610>`.

#. .. _alm-19000__li36989843192610:

   Rectify the fault by following the steps provided in **ALM-13000 ZooKeeper Service Unavailable**.

#. Wait several minutes, and check whether alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-19000__li31549687192610>`.

**Check the HDFS service status.**

5.  .. _alm-19000__li31549687192610:

    In the alarm list, check whether **ALM-14000 HDFS Service Unavailable** exists.

    -  If yes, go to :ref:`6 <alm-19000__li5387888192610>`.
    -  If no, go to :ref:`8 <alm-19000__li7395880192610>`.

6.  .. _alm-19000__li5387888192610:

    Rectify the fault by following the steps provided in **ALM-14000 HDFS Service Unavailable**.

7.  Wait several minutes, and check whether alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`8 <alm-19000__li7395880192610>`.

8.  .. _alm-19000__li7395880192610:

    On the MRS Manager portal, choose **Cluster** *> Name of the desired cluster* > **Services** > **HDFS**. Check whether **Safe Mode** is **ON**.

    -  If yes, go to :ref:`9 <alm-19000__li42432199192610>`.
    -  If no, go to :ref:`12 <alm-19000__li3109192610>`.

9.  .. _alm-19000__li42432199192610:

    Log in to the HDFS client as user **root**. Run **cd** to switch to the client installation directory, and run **source bigdata_env**.

    If the cluster uses the security mode, perform security authentication. Obtain the password of user hdfs from the administrator, run the **kinit hdfs** command and enter the password as prompted.

10. Run the following command to manually exit the safe mode:

    **hdfs dfsadmin -safemode leave**

11. Wait several minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-19000__li3109192610>`.

**Check the HBase service status.**

12. .. _alm-19000__li3109192610:

    On the MRS Manager portal, click **Cluster** > *Name of the desired cluster* > **Services** > **HBase**.

13. Check whether there is one active HMaster and one standby HMaster.

    -  If yes, go to :ref:`15 <alm-19000__li26121173192610>`.
    -  If no, go to :ref:`14 <alm-19000__li51944053192610>`.

14. .. _alm-19000__li51944053192610:

    Click **Instances**, select the HMaster whose status is not **Active**, click **More**, and select **Restart Instance** to restart the HMaster. Check whether there is one active HMaster and one standby HMaster again.

    -  If yes, go to :ref:`15 <alm-19000__li26121173192610>`.
    -  If no, go to :ref:`21 <alm-19000__li23797537192610>`.

15. .. _alm-19000__li26121173192610:

    Choose **Cluster** >\ *Name of the desired cluster* > **Services** > **HBase** > **HMaster(Active)** to go to the HMaster WebUI.

    .. note::

       By default, the **admin** user does not have the permissions to manage other components. If the page cannot be opened or the displayed content is incomplete when you access the native UI of a component due to insufficient permissions, you can manually create a user with the permissions to manage that component.

16. Check whether at least one RegionServer exists under **Region Servers**.

    -  If yes, go to :ref:`17 <alm-19000__li52728456192610>`.
    -  If no, go to :ref:`21 <alm-19000__li23797537192610>`.

17. .. _alm-19000__li52728456192610:

    Check **Tables** > **System Tables**, as shown in :ref:`Figure 1 <alm-19000__fig13078536192610>`. Check whether **hbase:meta**, **hbase:namespace**, and **hbase:acl** exist in the **Table Name** column.

    -  If yes, go to :ref:`18 <alm-19000__li52774331192610>`.
    -  If no, go to :ref:`19 <alm-19000__li2123961192610>`.

    .. _alm-19000__fig13078536192610:

    .. figure:: /_static/images/en-us_image_0000001532448266.png
       :alt: **Figure 1** HBase system table

       **Figure 1** HBase system table

18. .. _alm-19000__li52774331192610:

    As shown in :ref:`Figure 1 <alm-19000__fig13078536192610>`, click the **hbase:meta**, **hbase:namespace**, and **hbase:acl** hyperlinks and check whether the pages are properly displayed. If the pages are properly displayed, the tables are normal.

    If they are, go to :ref:`19 <alm-19000__li2123961192610>`.

    If they are not, go to :ref:`23 <alm-19000__li52963882192610>`.

    .. note::

       In normal mode, **ACL** is enabled for HBase by default. The **hbase:acl** table is generated only when **ACL** is manually enabled. In this case, check this table. In other scenarios, this table does not need to be checked.

19. .. _alm-19000__li2123961192610:

    View the HMaster startup status.

    In :ref:`Figure 2 <alm-19000__fig2133867192610>`, if the **RUNNING** state exists in **Tasks**, HMaster is being started. In the **State** column, you can view the time when HMaster is in the **RUNNING** state. In :ref:`Figure 3 <alm-19000__fig41660353192610>`, if the state is **COMPLETE**, HMaster is started.

    Check whether HMaster is in the **RUNNING** state for a long time.

    .. _alm-19000__fig2133867192610:

    .. figure:: /_static/images/en-us_image_0000001532767490.png
       :alt: **Figure 2** HMaster is being started

       **Figure 2** HMaster is being started

    .. _alm-19000__fig41660353192610:

    .. figure:: /_static/images/en-us_image_0000001583087409.png
       :alt: **Figure 3** HMaster is started

       **Figure 3** HMaster is started

    -  If yes, go to :ref:`20 <alm-19000__li34107122192610>`.
    -  If no, go to :ref:`21 <alm-19000__li23797537192610>`.

20. .. _alm-19000__li34107122192610:

    On the HMaster WebUI, check whether any hbase:meta is in the **Region in Transition** state for a long time.


    .. figure:: /_static/images/en-us_image_0000001582927649.png
       :alt: **Figure 4** Region in Transition

       **Figure 4** Region in Transition

    -  If yes, go to :ref:`21 <alm-19000__li23797537192610>`.
    -  If no, go to :ref:`22 <alm-19000__li53096940192610>`.

21. .. _alm-19000__li23797537192610:

    In the precondition that services are not affected, log in to the MRS Manager portal and choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase** > **More** > **Restart Service**. Enter the administrator password and click **OK**.

    -  If yes, go to :ref:`22 <alm-19000__li53096940192610>`.
    -  If no, go to :ref:`23 <alm-19000__li52963882192610>`.

22. .. _alm-19000__li53096940192610:

    Wait several minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`23 <alm-19000__li52963882192610>`.

**Check the network connection between HMaster and dependent components.**

23. .. _alm-19000__li52963882192610:

    On the MRS Manager, choose **Cluster** >\ *Name of the desired cluster* > **Services** > **HBase**.

24. .. _alm-19000__li6333253192610:

    Click **Instance** and the HMaster instance list is displayed. Record the **management IP Address** in the row of **HMaster(Active)**.

25. Use the IP address obtained in :ref:`24 <alm-19000__li6333253192610>` to log in to the host where the active HMaster runs as user **omm** .

26. Run the **ping** command to check whether communication between the host that runs the active HMaster and the hosts that run the dependent components. (The dependent components include ZooKeeper, HDFS and Yarn. Obtain the IP addresses of the hosts that run these services in the same way as that for obtaining the IP address of the active HMaster.)

    -  If yes, go to :ref:`29 <alm-19000__li5658542192610>`.
    -  If no, go to :ref:`27 <alm-19000__li11937281192610>`.

27. .. _alm-19000__li11937281192610:

    Contact the administrator to restore the network.

28. In the alarm list, check whether **HBase Service Unavailable** is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`29 <alm-19000__li5658542192610>`.

**Collect fault information.**

29. .. _alm-19000__li5658542192610:

    On the MRS Manager, choose **O&M** > **Log** > **Download**.

30. Select the following nodes in the required cluster from the **Service** drop-down list:

    -  ZooKeeper
    -  HDFS
    -  HBase

31. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

32. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582807697.png
