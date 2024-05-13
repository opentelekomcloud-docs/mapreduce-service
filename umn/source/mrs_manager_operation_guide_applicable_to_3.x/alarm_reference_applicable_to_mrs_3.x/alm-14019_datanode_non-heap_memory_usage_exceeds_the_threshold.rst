:original_name: ALM-14019.html

.. _ALM-14019:

ALM-14019 DataNode Non-heap Memory Usage Exceeds the Threshold
==============================================================

Description
-----------

The system checks the non-heap memory usage of the HDFS DataNode every 30 seconds and compares the actual usage with the threshold. The non-heap memory usage of the HDFS DataNode has a default threshold. This alarm is generated when the non-heap memory usage of the HDFS DataNode exceeds the threshold.

Users can choose **O&M > Alarm > Thresholds>** *Name of the desired cluster* **>** **HDFS** to change the threshold.

This alarm is cleared when the no-heap memory usage of the HDFS DataNode is less than or equal to the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
14019    Major          Yes
======== ============== =====================

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

If the memory usage of the HDFS DataNode is too high, data read/write performance of HDFS will be affected.

Possible Causes
---------------

Non-heap memory of the HDFS DataNode is insufficient.

Procedure
---------

**Delete unnecessary files.**

#. Log in to the HDFS client as user **root**. Run the **cd** command to go to the client installation directory, and run the **source bigdata_env** command.

   If the cluster adopts the security mode, perform security authentication.

   Run the **kinit hdfs** command and enter the password as prompted. Obtain the password from the administrator.

#. Run the **hdfs dfs -rm -r** *file or directory path* command to delete unnecessary files.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-14019__li4596028395356>`.

**Check the DataNode JVM non-heap memory usage and configuration.**

4. .. _alm-14019__li4596028395356:

   On the MRS Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS**.

5. In the **Basic Information** area, click **NameNode(Active)**. The HDFS WebUI is displayed.

   .. note::

      By default, the **admin** user does not have the permissions to manage other components. If the page cannot be opened or the displayed content is incomplete when you access the native UI of a component due to insufficient permissions, you can manually create a user with the permissions to manage that component.

6. .. _alm-14019__li3578073195356:

   On the HDFS WebUI, click the **Datanodes** tab to view the number of blocks of all DataNodes that report alarms.

7. .. _alm-14019__li4116310695356:

   On the MRS Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS** > **Configurations** > **All** **Configurations**. In **Search**, enter **GC_OPTS** to check the **GC_OPTS** non-heap memory parameter of **HDFS->DataNode**.

**Adjust system configurations.**

8.  Check whether the memory is properly configured based on the number of blocks in :ref:`6 <alm-14019__li3578073195356>` and the memory parameters configured for DataNode in :ref:`7 <alm-14019__li4116310695356>`.

    -  If yes, go to :ref:`9 <alm-14019__li3591807095356>`.
    -  If no, go to :ref:`12 <alm-14019__li6341663395356>`.

    .. note::

       The mapping between the average number of blocks of a DataNode instance and the DataNode memory is as follows:

       -  If the average number of blocks of a DataNode instance reaches 2,000,000, the reference values of the JVM parameters of the DataNode are as follows: -Xms6G -Xmx6G -XX:NewSize=512M -XX:MaxNewSize=512M
       -  If the average number of blocks of a DataNode instance reaches 5,000,000, the reference values of the JVM parameters of the DataNode are as follows: -Xms12G -Xmx12G -XX:NewSize=1G -XX:MaxNewSize=1G

9.  .. _alm-14019__li3591807095356:

    Modify the **GC_OPTS** parameter of the DataNode based on the mapping between the number of blocks and memory.

10. Save the configuration and click **Dashboard** > **More** > **Restart Service**.

11. Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-14019__li6341663395356>`.

**Collect fault information.**

12. .. _alm-14019__li6341663395356:

    On the MRS Manager portal, choose **O&M** > **Log > Download**.

13. Select the following services in the required cluster from the **Service**.

    -  ZooKeeper
    -  HDFS

14. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

15. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532607902.png
