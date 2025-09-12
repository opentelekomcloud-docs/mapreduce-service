:original_name: ALM-14039.html

.. _ALM-14039:

ALM-14039 Slow DataNodes Exist in the Cluster
=============================================

Alarm Description
-----------------

The system checks the number of slow operations per second on HDFS DataNode instances every 60 seconds and compares the number with the threshold. This alarm is generated when the number of slow operations per second of an HDFS DataNode instance has exceeded the threshold for three minutes.

This alarm is cleared when the number of slow operations per second of the HDFS DataNode instance is less than or equal to the threshold.

Alarm Attributes
----------------

======== ============================== ============
Alarm ID Alarm Severity                 Auto Cleared
======== ============================== ============
14039    Major (default threshold: 100) Yes
======== ============================== ============

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

Slow DataNodes on HDFS affect the data read and write performance of HDFS.

Possible Causes
---------------

-  The disk I/O rate of the HDFS DataNode instance is low, and the HDFS DataNode processing capability reaches the bottleneck.
-  The network transmission rate between HDFS DataNode instances is low.

Handling Procedure
------------------

**Check whether the disk I/O rate of the DataNode instance is low.**

#. .. _alm-14039__en-us_topic_0000001979201172_li23652015192818:

   Log in to MRS Manager and choose **O&M** > **Alarm** > **Alarms**. In the **Location** field of the alarm details, view the host name of the DataNode instance for which this alarm is generated.

#. Choose **Cluster** > **Services** > **HDFS**, click the **Instances** tab, and click the DataNode role based on the host name obtained in :ref:`1 <alm-14039__en-us_topic_0000001979201172_li23652015192818>`.

#. Click the **Chart** tab and select **Performance** from the **Chart Category** area. Check whether any data in **Slow Flush or Sync Occurrences Per Second**, **Slow SyncWriterOsCache Occurrences Per Second**, and **Slow WriteDataToDisk Occurrences Per Second** charts is high.

   -  If yes, go to :ref:`4 <alm-14039__en-us_topic_0000001979201172_li2941154513215>`.
   -  If no, go to :ref:`8 <alm-14039__en-us_topic_0000001979201172_li188546153148>`.

#. .. _alm-14039__en-us_topic_0000001979201172_li2941154513215:

   On MRS Manager, choose **O&M** > **Alarm** > **Alarms** and check whether **ALM-12033 Slow Disk Fault** exists.

   -  If yes, record the disk information in the alarm details and go to :ref:`6 <alm-14039__en-us_topic_0000001979201172_li178785122417>`.
   -  If no, go to :ref:`5 <alm-14039__en-us_topic_0000001979201172_li48311375375>`.

#. .. _alm-14039__en-us_topic_0000001979201172_li48311375375:

   Obtain information about the disk where slow operations occur.

   a. Log in to the DataNode using the IP address obtained in :ref:`1 <alm-14039__en-us_topic_0000001979201172_li23652015192818>` as user **omm** and run the following commands to view the run log:

      **cd /var/log/Bigdata/hdfs/dn/**

      **vim hadoop-omm-datanode-**\ *Hostname*\ **.log**

   b. Search for keyword **slow** in the log to identify the disk where slow operations occur.

      |image1|

#. .. _alm-14039__en-us_topic_0000001979201172_li178785122417:

   Rectify the fault based on the obtained disk information by following the handling procedure of **ALM-12033 Slow Disk Fault**.

#. Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-14039__en-us_topic_0000001979201172_li188546153148>`.

**Check whether the network transmission rate between HDFS DataNode instances is low.**

8.  .. _alm-14039__en-us_topic_0000001979201172_li188546153148:

    On MRS Manager, choose **Cluster** > **Services** > **HDFS**, click the **Chart** tab, select **Performance** in the **Chart Category** area, and check whether any data in the **Slow Write Packet To DownStream Count Per Second** and **Slow Ack To Upstream Count Per Second** charts is high.

    -  If yes, go to :ref:`9 <alm-14039__en-us_topic_0000001979201172_li6854915131419>`.
    -  If no, go to :ref:`13 <alm-14039__en-us_topic_0000001979201172_li42224042151734>`.

9.  .. _alm-14039__en-us_topic_0000001979201172_li6854915131419:

    Log in to the DataNode using the IP address obtained in :ref:`1 <alm-14039__en-us_topic_0000001979201172_li23652015192818>` as user **omm** and run the following commands to view the run log:

    **cd /var/log/Bigdata/hdfs/dn/**

    **vim hadoop-omm-datanode-**\ *Hostname*\ **.log**

10. .. _alm-14039__en-us_topic_0000001979201172_li168554154148:

    Search for keyword **slow** in the log to identify the upstream and downstream nodes where slow operations occur.

    |image2|

11. Check whether the network communication between the current node and the nodes obtained in :ref:`10 <alm-14039__en-us_topic_0000001979201172_li168554154148>` is normal.

    -  If yes, go to :ref:`13 <alm-14039__en-us_topic_0000001979201172_li42224042151734>`.
    -  If no, contact the network administrator to repair the network.

12. Wait 5 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`13 <alm-14039__en-us_topic_0000001979201172_li42224042151734>`.

**Collect fault information.**

13. .. _alm-14039__en-us_topic_0000001979201172_li42224042151734:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

14. Expand the **Service** drop-down list, and select **HDFS** for the target cluster.

15. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

16. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000002380470068.png
.. |image2| image:: /_static/images/en-us_image_0000002414069433.png
