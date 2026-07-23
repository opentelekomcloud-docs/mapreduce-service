:original_name: ALM-18032.html

.. _ALM-18032:

ALM-18032 JobHistoryServer Active Node Promotion Failed
=======================================================

Alarm Description
-----------------

This alarm is generated when the JhsHaDaemon process fails to start the JobHistoryServer during the promotion of an active JobHistoryServer instance.

This alarm is cleared when the JobHistoryServer on the node either starts successfully or transitions to the standby state.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
18032    Critical       Yes
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

-  You cannot view logs for completed jobs.
-  The Hive on MR job occasionally exhibits abnormal status.

Possible Causes
---------------

-  The ZooKeeper service is abnormal.
-  The HDFS service is abnormal.
-  The floating IP address is abnormal.

Handling Procedure
------------------

**Check the ZooKeeper service status.**

#. Log in to MRS Manager, and choose **Cluster** > **Services**. In the service list, check whether **Running Status** of ZooKeeper is **Normal**.

   -  If yes, go to :ref:`5 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li851630135816>`.
   -  If no, go to :ref:`2 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li18516100185814>`.

#. .. _alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li18516100185814:

   Choose **O&M** > **Alarm** > **Alarms**. In the alarm list, check whether alarm **ALM-13000 ZooKeeper Service Unavailable** exists.

   -  If yes, go to :ref:`3 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li05161204589>`.
   -  If no, go to :ref:`5 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li851630135816>`.

#. .. _alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li05161204589:

   Rectify the fault by performing the operations provided for **ALM-13000 ZooKeeper Service Unavailable**.

#. Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li851630135816>`.

**Check the HDFS service status.**

5.  .. _alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li851630135816:

    Choose **O&M** > **Alarm** > **Alarms**. In the alarm list, check whether alarm **ALM-14000 HDFS Service Unavailable** exists.

    -  If yes, go to :ref:`6 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li13516120105811>`.
    -  If no, go to :ref:`8 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li175161504581>`.

6.  .. _alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li13516120105811:

    Rectify the fault by performing the operations provided for **ALM-14000 HDFS Service Unavailable**.

7.  Wait 5 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`8 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li175161504581>`.

8.  .. _alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li175161504581:

    Choose **Cluster** > **Services** > **HDFS**. On the **Dashboard** page, check whether **Safe Mode** of HDFS is **ON**.

    -  If yes, go to :ref:`9 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li185162016581>`.
    -  If no, go to :ref:`12 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li18710104910430>`.

9.  .. _alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li185162016581:

    Log in to the node where the HDFS client is installed as user **root**, configure environment variables, and authenticate the user.

    **cd** *Client installation directory*

    **source bigdata_env**

    **kinit hdfs** (Skip this step if Kerberos authentication is disabled for the cluster (the cluster is in normal mode).)

    Obtain the password of the **hdfs** user from the cluster administrator.

10. Run the following command to manually exit the safe mode:

    **hdfs dfsadmin -safemode leave**

11. Wait 5 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li18710104910430>`.

**Check whether the floating IP address is abnormal.**

12. .. _alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li18710104910430:

    On MRS Manager, choose **Cluster** > **Services** > **Mapreduce**, click **Configurations** and then **All Configurations**, and check and record the value of **JHS_FLOAT_IP**.

13. On the **Instances** tab page of the MapReduce service, check and record the service IP address of the JobHistoryServer instance. Log in to the node where JobHistoryServer is installed as user **root** and run the following command to check whether the IP address in :ref:`12 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li18710104910430>` is accessible:

    **ping** *IP address in* *:ref:`12 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li18710104910430>`*

    -  If yes, go to :ref:`14 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li1671014917435>`.
    -  If no, go to :ref:`18 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li2517140145816>`.

14. .. _alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li1671014917435:

    Run the following command to check whether the floating IP address is the JobHistoryServer floating IP address obtained in :ref:`12 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li18710104910430>`:

    **ip addr**

    -  If yes, go to :ref:`15 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li18711114919437>`.
    -  If no, change the floating IP address of **JHS_FLOAT_IP** in :ref:`12 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li18710104910430>` to the IP address that cannot be pinged and go to :ref:`16 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li14711164910437>`.

15. .. _alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li18711114919437:

    Run the following command to delete the floating IP address:

    **ip** **addr del** *IP address* **dev** *NIC name*

16. .. _alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li14711164910437:

    On MRS Manager, choose **Cluster** > **Services** > **Yarn** > **Instances**, select all JobHistoryServer instances, and choose **More** > **Restart Instance**.

17. Wait 5 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`18 <alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li2517140145816>`.

**Collect fault information.**

18. .. _alm-18032__en-us_topic_0000002520079833_en-us_topic_0000002489560573_li2517140145816:

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
