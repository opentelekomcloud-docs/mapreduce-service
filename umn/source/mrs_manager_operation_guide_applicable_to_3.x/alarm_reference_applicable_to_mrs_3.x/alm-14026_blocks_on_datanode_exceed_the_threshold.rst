:original_name: ALM-14026.html

.. _ALM-14026:

ALM-14026 Blocks on DataNode Exceed the Threshold
=================================================

Description
-----------

The system checks the number of blocks on each DataNode every 30 seconds. This alarm is generated when the number of blocks on the DataNode exceeds the threshold.

If **Trigger Count** is **1** and the number of blocks on the DataNode is less than or equal to the threshold, this alarm is cleared. If **Trigger Count** is greater than **1** and the number of blocks on the DataNode is less than or equal to 90% of the threshold, this alarm is cleared.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14026    Minor          Yes
======== ============== ==========

Parameters
----------

+-------------------+---------------------------------------------------------+
| Name              | Meaning                                                 |
+===================+=========================================================+
| Source            | Specifies the cluster for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| Trigger condition | Specifies the threshold for triggering the alarm.       |
+-------------------+---------------------------------------------------------+

Impact on the System
--------------------

If this alarm is reported, there are too many blocks on the DataNode. In this case, data writing into the HDFS may fail due to insufficient disk space.

Possible Causes
---------------

-  The alarm threshold is improperly configured.

-  Data skew occurs among DataNodes.
-  The disk space configured for the HDFS cluster is insufficient.

Procedure
---------

**Change the threshold.**

#. On MRS Manager, choose **Cluster**, click the name of the desired cluster, and choose **HDFS**. Then choose **Configurations** > **All Configurations**. On the displayed page, find the **GC_OPTS** parameter under **HDFS->DataNode**.
#. Set the threshold of the DataNode blocks. Specifically, change the value of **Xmx** of the **GC_OPTS** parameter. **Xmx** specifies the memory, and each GB memory supports a maximum of 500,000 DataNode blocks. Set the memory as required. Confirm that **GC_PROFILE** is set to **custom** and save the configuration.
#. Choose **Cluster**, click the name of the desired cluster, and choose **HDFS** > **Instance**. Select the DataNode instance whose status is **Expired**, click **More**, and select **Restart Instance** to make the **GC_OPTS** configuration take effect.
#. Check whether the alarm is cleared 5 minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-14026__li10750133111389>`.

**Check whether associated alarms are reported.**

5. .. _alm-14026__li10750133111389:

   On MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and check whether the **ALM-14002 DataNode Disk Usage Exceeds the Threshold** alarm exists.

   -  If yes, go to :ref:`6 <alm-14026__li5750123115384>`.
   -  If no, go to :ref:`8 <alm-14026__li4795431151710>`.

6. .. _alm-14026__li5750123115384:

   Handle the alarm by following the instructions in **ALM-14002 DataNode Disk Usage Exceeds the Threshold** and check whether the alarm is cleared.

   -  If yes, go to :ref:`7 <alm-14026__li10751231113815>`.
   -  If no, go to :ref:`8 <alm-14026__li4795431151710>`.

7. .. _alm-14026__li10751231113815:

   Check whether the alarm is cleared 5 minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-14026__li4795431151710>`.

**Expand the DataNode capacity.**

8. .. _alm-14026__li4795431151710:

   Expand the DataNode capacity.

9. On MRS Manager, wait for 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-14026__li10844183481711>`.

**Collect the fault information.**

10. .. _alm-14026__li10844183481711:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

11. Expand the drop-down list next to the **Service** field. In the **Services** dialog box that is displayed, select **HDFS** for the target cluster.

12. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 20 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

13. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

**Configuration rules of the DataNode JVM parameter.**

Default value of the DataNode JVM parameter **GC_OPTS**:

-Xms2G -Xmx4G -XX:NewSize=128M -XX:MaxNewSize=256M -XX:MetaspaceSize=128M -XX:MaxMetaspaceSize=128M -XX:+UseConcMarkSweepGC -XX:+CMSParallelRemarkEnabled -XX:CMSInitiatingOccupancyFraction=65 -XX:+PrintGCDetails -Dsun.rmi.dgc.client.gcInterval=0x7FFFFFFFFFFFFFE -Dsun.rmi.dgc.server.gcInterval=0x7FFFFFFFFFFFFFE -XX:-OmitStackTraceInFastThrow -XX:+PrintGCDateStamps -XX:+UseGCLogFileRotation -XX:NumberOfGCLogFiles=10 -XX:GCLogFileSize=1M -Djdk.tls.ephemeralDHKeySize=2048

The average number of blocks stored in each DataNode instance in the cluster is: Number of HDFS blocks x 3/Number of DataNodes. If the average number of blocks changes, you need to change **-Xms2G -Xmx4G -XX:NewSize=128M -XX:MaxNewSize=256M** in the default value. The following table lists the reference values.

.. table:: **Table 1** DataNode JVM configuration

   +-------------------------------------------------+----------------------------------------------------+
   | Average Number of Blocks in a DataNode Instance | Reference Value                                    |
   +=================================================+====================================================+
   | 2,000,000                                       | -Xms6G -Xmx6G -XX:NewSize=512M -XX:MaxNewSize=512M |
   +-------------------------------------------------+----------------------------------------------------+
   | 5,000,000                                       | -Xms12G -Xmx12G -XX:NewSize=1G -XX:MaxNewSize=1G   |
   +-------------------------------------------------+----------------------------------------------------+

**Xmx** specifies memory which corresponds to the threshold of the number of DataNode blocks, and each GB memory supports a maximum of 500,000 DataNode blocks. Set the memory as required.

.. |image1| image:: /_static/images/en-us_image_0000001532767582.png
