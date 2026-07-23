:original_name: ALM-18031.html

.. _ALM-18031:

ALM-18031 TimelineServer Active Node Promotion Failed
=====================================================

Alarm Description
-----------------

This alarm is generated when the TimelineHaDaemon process fails to start the TimelineServer during the promotion of an active TimelineServer instance.

This alarm is cleared when the TimelineServer on the node either starts successfully or transitions to the standby state.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
18031    Critical       Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------------+----------------------------------------------------------+
| Type                   | Parameter         | Description                                              |
+========================+===================+==========================================================+
| Location Information   | Source            | Specifies the cluster for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------+
|                        | ServiceName       | Specifies the service for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------+
|                        | RoleName          | Specifies the role for which the alarm was generated.    |
+------------------------+-------------------+----------------------------------------------------------+
|                        | HostName          | Specifies the host for which the alarm was generated.    |
+------------------------+-------------------+----------------------------------------------------------+
| Additional Information | Trigger Condition | Specifies the alarm triggering condition.                |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

Historical records cannot be viewed on the Tez page.

Possible Causes
---------------

-  The ZooKeeper service is abnormal.
-  The HDFS service is abnormal.
-  The floating IP address is abnormal.

Handling Procedure
------------------

**Check the ZooKeeper service status.**

#. Log in to MRS Manager, and choose **Cluster** > **Services**. In the service list, check whether **Running Status** of ZooKeeper is **Normal**.

   -  If yes, go to :ref:`5 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li620900869259>`.
   -  If no, go to :ref:`2 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li257033669259>`.

#. .. _alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li257033669259:

   Choose **O&M** > **Alarm** > **Alarms**. In the alarm list, check whether alarm **ALM-13000 ZooKeeper Service Unavailable** exists.

   -  If yes, go to :ref:`3 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li15979369259>`.
   -  If no, go to :ref:`5 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li620900869259>`.

#. .. _alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li15979369259:

   Rectify the fault by performing the operations provided for **ALM-13000 ZooKeeper Service Unavailable**.

#. Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li620900869259>`.

**Check the HDFS service status.**

5.  .. _alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li620900869259:

    Choose **O&M** > **Alarm** > **Alarms**. In the alarm list, check whether alarm **ALM-14000 HDFS Service Unavailable** exists.

    -  If yes, go to :ref:`6 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li632410929259>`.
    -  If no, go to :ref:`8 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li660818889259>`.

6.  .. _alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li632410929259:

    Rectify the fault by performing the operations provided for **ALM-14000 HDFS Service Unavailable**.

7.  Wait 5 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`8 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li660818889259>`.

8.  .. _alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li660818889259:

    Choose **Cluster** > **Services** > **HDFS**. On the **Dashboard** page, check whether **Safe Mode** of HDFS is **ON**.

    -  If yes, go to :ref:`9 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li209194441242>`.
    -  If no, go to :ref:`12 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li18710104910430>`.

9.  .. _alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li209194441242:

    Log in to the node where the HDFS client is installed as user **root**, configure environment variables, and authenticate the user.

    **cd** *Client installation directory*

    **source bigdata_env**

    **kinit hdfs** (Skip this step if Kerberos authentication is disabled for the cluster (the cluster is in normal mode).)

    Obtain the password of the **hdfs** user from the cluster administrator.

10. Run the following command to manually exit the safe mode:

    **hdfs dfsadmin -safemode leave**

11. Wait 5 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li18710104910430>`.

**Check whether the floating IP address is abnormal.**

12. .. _alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li18710104910430:

    On MRS Manager, choose **Cluster** > **Services** > **Yarn**, click **Configurations** and then **All Configurations**, and check and record the value of **TLS_FLOAT_IP**.

13. On the **Instances** tab page of the YARN service, check and record the service IP address of the TimelineServer instance. Log in to the node where TimelineServer is installed as user **root** and run the following command to check whether the IP address in :ref:`12 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li18710104910430>` is accessible:

    **ping** *IP address in* :ref:`12 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li18710104910430>`

    -  If yes, go to :ref:`14 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li1671014917435>`.
    -  If no, go to :ref:`18 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li240314599259>`.

14. .. _alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li1671014917435:

    Run the following command to check whether the floating IP address is the TimelineServer floating IP address obtained in :ref:`12 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li18710104910430>`:

    **ip addr**

    -  If yes, go to :ref:`15 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li18711114919437>`.
    -  If no, change the floating IP address of **TLS_FLOAT_IP** in :ref:`12 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li18710104910430>` to the IP address that cannot be pinged and go to :ref:`16 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li14711164910437>`.

15. .. _alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li18711114919437:

    Run the following command to delete the floating IP address:

    **ip** **addr del** *IP address* **dev** *NIC name*

16. .. _alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li14711164910437:

    On MRS Manager, choose **Cluster** > **Services** > **Yarn** > **Instances**, select all TimelineServer instances, and choose **More** > **Restart Instance**.

17. Wait 5 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`18 <alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li240314599259>`.

**Collect fault information.**

18. .. _alm-18031__en-us_topic_0000002487959986_en-us_topic_0000002456600906_li240314599259:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

19. Expand the **Service** drop-down list, and select the following services for the target cluster:

    -  ZooKeeper
    -  HDFS
    -  Mapreduce

20. Click the edit icon in the upper right corner, and select a time span starting 10 minutes before and ending 10 minutes after when the alarm was generated. Then, click **Download** to collect the logs.

21. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
