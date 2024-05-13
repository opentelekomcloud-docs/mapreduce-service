:original_name: ALM-14006.html

.. _ALM-14006:

ALM-14006 Number of HDFS Files Exceeds the Threshold
====================================================

Description
-----------

The system periodically checks the number of HDFS files every 30 seconds and compares the number of HDFS files with the threshold. This alarm is generated when the system detects that the number of HDFS files exceeds the threshold.

If **Trigger Count** is **1**, this alarm is cleared when the number of HDFS files is less than or equal to the threshold. If **Trigger Count** is greater than **1**, this alarm is cleared when the number of HDFS files is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14006    Minor          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------+
| Name              | Meaning                                                     |
+===================+=============================================================+
| Source            | Specifies the cluster for which the alarm is generated.     |
+-------------------+-------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.     |
+-------------------+-------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.        |
+-------------------+-------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.        |
+-------------------+-------------------------------------------------------------+
| NameServiceName   | Specifies the NameService for which the alarm is generated. |
+-------------------+-------------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.           |
+-------------------+-------------------------------------------------------------+

Impact on the System
--------------------

Disk storage space is insufficient, which may result in data import failure. The performance of the HDFS system is affected.

Possible Causes
---------------

The number of HDFS files exceeds the threshold.

Procedure
---------

**Check the number of files in the system.**

#. On MRS Manager, check the number of HDFS files. Specifically, choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS**. Click the drop-down menu in the upper right corner of **Chart**, choose **Customize** > **File and Block**, and select **HDFS File** and **Total Blocks**.
#. Choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS** > **Configurations** > **All Configurations**, and search for the **GC_OPTS** parameter under **NameNode**.
#. Configure the threshold of the number of configuration file objects. Specifically, change the value of **Xmx** (GB) in the **GC_OPTS** parameter. The threshold (specified by y) is calculated as follows: y = 0.2007 x Xmx - 0.6312, where x indicates the memory capacity Xmx (GB) and y indicates the number of files (unit: kW). Adjust the memory size as required.
#. Confirm that the value of **GC_PROFILE** is **custom** so that the **GC_OPTS** configuration takes effect. Click **Save** and choose **More** > **Restart Instance** to restart the service.
#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-14006__li57477018164725>`.

**Check whether needless files exist in the system.**

6. .. _alm-14006__li57477018164725:

   Log in to the HDFS client as user **root**. Run **cd** to switch to the client installation directory, and run **source bigdata_env** to configure the environment variables.

   If the cluster uses the security mode, perform security authentication.

   Run the **kinit hdfs** command and enter the password as prompted. Obtain the password from the MRS cluster administrator.

7. Run **hdfs dfs -ls** *file or directory* to check whether the files in the directory can be deleted.

   -  If yes, go to :ref:`8 <alm-14006__li46417503164725>`.
   -  If no, go to :ref:`9 <alm-14006__li15104347164725>`.

8. .. _alm-14006__li46417503164725:

   Run the **hdfs dfs -rm -r** *file or directory path* command. After deleting unnecessary files, wait until the files are retained in the recycle bin for a period longer than the value of **fs.trash.interval** on the NameNode. Then check whether the alarm is cleared.

   .. note::

      Deleting a file or folder is a high-risk operation. Ensure that the file or folder is no longer required before performing this operation.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-14006__li15104347164725>`.

**Collect the fault information.**

9.  .. _alm-14006__li15104347164725:

    On MRS Manager, choose **O&M** > **Log** > **Download**.

10. Expand the drop-down list next to the **Service** field. In the **Services** dialog box that is displayed, select **HDFS** for the target cluster.

11. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

**Configuration rules of the NameNode JVM parameter**

Default value of the NameNode JVM parameter **GC_OPTS**:

-Xms2G -Xmx4G -XX:NewSize=128M -XX:MaxNewSize=256M -XX:MetaspaceSize=128M -XX:MaxMetaspaceSize=128M -XX:+UseConcMarkSweepGC -XX:+CMSParallelRemarkEnabled -XX:CMSInitiatingOccupancyFraction=65 -XX:+PrintGCDetails -Dsun.rmi.dgc.client.gcInterval=0x7FFFFFFFFFFFFFE -Dsun.rmi.dgc.server.gcInterval=0x7FFFFFFFFFFFFFE -XX:-OmitStackTraceInFastThrow -XX:+PrintGCDateStamps -XX:+UseGCLogFileRotation -XX:NumberOfGCLogFiles=10 -XX:GCLogFileSize=1M -Djdk.tls.ephemeralDHKeySize=3072 -Djdk.tls.rejectClientInitiatedRenegotiation=true -Djava.io.tmpdir=${Bigdata_tmp_dir}

The number of NameNode files is proportional to the used memory size of the NameNode. When file objects change, you need to change **-Xms2G -Xmx4G -XX:NewSize=128M -XX:MaxNewSize=256M** in the default value. The following table lists the reference values.

.. table:: **Table 1** NameNode JVM configuration

   +------------------------+------------------------------------------------------+
   | Number of File Objects | Reference Value                                      |
   +========================+======================================================+
   | 10,000,000             | -Xms6G -Xmx6G -XX:NewSize=512M -XX:MaxNewSize=512M   |
   +------------------------+------------------------------------------------------+
   | 20,000,000             | -Xms12G -Xmx12G -XX:NewSize=1G -XX:MaxNewSize=1G     |
   +------------------------+------------------------------------------------------+
   | 50,000,000             | -Xms32G -Xmx32G -XX:NewSize=3G -XX:MaxNewSize=3G     |
   +------------------------+------------------------------------------------------+
   | 100,000,000            | -Xms64G -Xmx64G -XX:NewSize=6G -XX:MaxNewSize=6G     |
   +------------------------+------------------------------------------------------+
   | 200,000,000            | -Xms96G -Xmx96G -XX:NewSize=9G -XX:MaxNewSize=9G     |
   +------------------------+------------------------------------------------------+
   | 300,000,000            | -Xms164G -Xmx164G -XX:NewSize=12G -XX:MaxNewSize=12G |
   +------------------------+------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001532927350.png
