:original_name: ALM-14018.html

.. _ALM-14018:

ALM-14018 NameNode Non-heap Memory Usage Exceeds the Threshold
==============================================================

Description
-----------

The system checks the non-heap memory usage of the HDFS NameNode every 30 seconds and compares the actual usage with the threshold. The non-heap memory usage of the HDFS NameNode has a default threshold. This alarm is generated when the non-heap memory usage of the HDFS NameNode exceeds the threshold.

Users can choose **O&M > Alarm > Thresholds >** *Name of the desired cluster* > **HDFS** to change the threshold.

This alarm is cleared when the no-heap memory usage of the HDFS NameNode is less than or equal to the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
14018    Major          Yes
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

If the memory usage of the HDFS NameNode is too high, data read/write performance of HDFS will be affected.

Possible Causes
---------------

Non-heap memory of the HDFS NameNode is insufficient.

Procedure
---------

**Delete unnecessary files.**

#. Log in to the HDFS client as user **root**. Run the **cd** command to go to the client installation directory, and run the **source bigdata_env** command.

   If the cluster adopts the security mode, perform security authentication.

   Run the **kinit hdfs** command and enter the password as prompted. Obtain the password from the administrator.

#. Run the **hdfs dfs -rm -r** *file or directory path* command to delete unnecessary files.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-14018__li6485487494622>`.

**Check the NameNode JVM non-heap memory usage and configuration.**

4. .. _alm-14018__li6485487494622:

   On the MRS Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS**. The HDFS status page is displayed.

5. In the **Basic Information** area, click **NameNode(Active)**. The HDFS WebUI is displayed.

   .. note::

      By default, the **admin** user does not have the permissions to manage other components. If the page cannot be opened or the displayed content is incomplete when you access the native UI of a component due to insufficient permissions, you can manually create a user with the permissions to manage that component.

6. .. _alm-14018__li3062349394622:

   On the HDFS WebUI, click the **Overview** tab. In **Summary**, check the numbers of files, directories, and blocks in HDFS.

7. .. _alm-14018__li4379666894622:

   On the MRS Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS** > **Configurations** > **All** **Configurations**. In **Search**, enter **GC_OPTS** to check the **GC_OPTS** non-heap memory parameter of **HDFS->NameNode**.

**Adjust system configurations.**

8.  Check whether the non-heap memory is properly configured based on the number of file objects in :ref:`6 <alm-14018__li3062349394622>` and the non-heap parameters configured for NameNode in :ref:`7 <alm-14018__li4379666894622>`.

    -  If yes, go to :ref:`9 <alm-14018__li1465143294622>`.
    -  If no, go to :ref:`12 <alm-14018__li6570062694622>`.

    .. note::

       The recommended mapping between the number of HDFS file objects (filesystem objects = files + blocks) and the JVM parameters configured for NameNode is as follows:

       -  If the number of file objects reaches 10,000,000, you are advised to set the JVM parameters as follows: -Xms6G -Xmx6G -XX:NewSize=512M -XX:MaxNewSize=512M
       -  If the number of file objects reaches 20,000,000, you are advised to set the JVM parameters as follows: -Xms12G -Xmx12G -XX:NewSize=1G -XX:MaxNewSize=1G
       -  If the number of file objects reaches 50,000,000, you are advised to set the JVM parameters as follows: -Xms32G -Xmx32G -XX:NewSize=3G -XX:MaxNewSize=3G
       -  If the number of file objects reaches 100,000,000, you are advised to set the JVM parameters as follows: -Xms64G -Xmx64G -XX:NewSize=6G -XX:MaxNewSize=6G
       -  If the number of file objects reaches 200,000,000, you are advised to set the JVM parameters as follows: -Xms96G -Xmx96G -XX:NewSize=9G -XX:MaxNewSize=9G
       -  If the number of file objects reaches 300,000,000, you are advised to set the JVM parameters as follows: -Xms164G -Xmx164G -XX:NewSize=12G -XX:MaxNewSize=12G

9.  .. _alm-14018__li1465143294622:

    Modify the **GC_OPTS** parameter of the NameNode based on the mapping between the number of file objects and non-heap memory.

10. Save the configuration and click **Dashboard** > **More** > **Restart Service**.

11. Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-14018__li6570062694622>`.

**Collect fault information.**

12. .. _alm-14018__li6570062694622:

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

.. |image1| image:: /_static/images/en-us_image_0000001583087625.png
