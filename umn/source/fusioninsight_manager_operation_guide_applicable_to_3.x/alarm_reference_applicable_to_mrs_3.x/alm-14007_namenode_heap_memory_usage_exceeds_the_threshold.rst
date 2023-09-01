:original_name: ALM-14007.html

.. _ALM-14007:

ALM-14007 NameNode Heap Memory Usage Exceeds the Threshold
==========================================================

Description
-----------

The system checks the HDFS NameNode Heap Memory usage every 30 seconds and compares the actual Heap memory usage with the threshold. The HDFS NameNode Heap Memory usage has a default threshold. This alarm is generated when the HDFS NameNode Heap Memory usage exceeds the threshold.

You can change the threshold in **O&M** > **Alarm >** **Thresholds** > *Name of the desired cluster* **>** **HDFS**.

When the **Trigger Count** is 1, this alarm is cleared when the HDFS NameNode Heap memory usage is less than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the HDFS NameNode Heap memory usage is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
14007    Major          Yes
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

The HDFS NameNode Heap Memory usage is too high, which affects the data read/write performance of the HDFS.

Possible Causes
---------------

The HDFS NameNode Heap Memory is insufficient.

Procedure
---------

**Delete unnecessary files.**

#. Log in to the HDFS client as user **root**. Run **cd** to switch to the client installation directory, and run **source bigdata_env**.

   If the cluster uses the security mode, perform security authentication.

   Run the **kinit hdfs** command and enter the password as prompted. Obtain the password from the administrator.

#. Run the **hdfs dfs -rm -r** *file or directory* command to delete unnecessary files.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-14007__li15187254165341>`.

**Check the NameNode JVM memory usage and configuration.**

4. .. _alm-14007__li15187254165341:

   On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS**.

5. In the **Basic Information** area, click **NameNode(Active)** to go to the HDFS WebUI.

   .. note::

      By default, the **admin** user does not have the permissions to manage other components. If the page cannot be opened or the displayed content is incomplete when you access the native UI of a component due to insufficient permissions, you can manually create a user with the permissions to manage that component.

6. .. _alm-14007__li13697230165341:

   On the HDFS WebUI, click the **Overview** tab. In **Summary**, check the numbers of files, directories, and blocks in the HDFS.

7. .. _alm-14007__li46442940165341:

   On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS** > **Configurations** > **All** **Configurations**. In **Search**, enter **GC_OPTS** to check the **GC_OPTS** memory parameter of **HDFS->NameNode**.

**Adjust the configuration in the system.**

8.  Check whether the memory is configured properly based on the number of files in :ref:`6 <alm-14007__li13697230165341>` and the NameNode Heap Memory parameters in :ref:`7 <alm-14007__li46442940165341>`.

    -  If yes, go to :ref:`9 <alm-14007__li14671769165341>`.
    -  If no, go to :ref:`11 <alm-14007__li58431113165341>`.

    .. note::

       The recommended mapping between the number of HDFS file objects (filesystem objects = files + blocks) and the JVM parameters configured for NameNode is as follows:

       -  If the number of file objects reaches 10,000,000, you are advised to set the JVM parameters as follows: -Xms6G -Xmx6G -XX:NewSize=512M -XX:MaxNewSize=512M
       -  If the number of file objects reaches 20,000,000, you are advised to set the JVM parameters as follows: -Xms12G -Xmx12G -XX:NewSize=1G -XX:MaxNewSize=1G
       -  If the number of file objects reaches 50,000,000, you are advised to set the JVM parameters as follows: -Xms32G -Xmx32G -XX:NewSize=3G -XX:MaxNewSize=3G
       -  If the number of file objects reaches 100,000,000, you are advised to set the JVM parameters as follows: -Xms64G -Xmx64G -XX:NewSize=6G -XX:MaxNewSize=6G
       -  If the number of file objects reaches 200,000,000, you are advised to set the JVM parameters as follows: -Xms96G -Xmx96G -XX:NewSize=9G -XX:MaxNewSize=9G
       -  If the number of file objects reaches 300,000,000, you are advised to set the JVM parameters as follows: -Xms164G -Xmx164G -XX:NewSize=12G -XX:MaxNewSize=12G

9.  .. _alm-14007__li14671769165341:

    Modify the heap memory parameters of the NameNode based on the mapping between the number of file objects and the memory. Click **Save** and choose **Dashboard** > **More** > **Restart Service**.

10. Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-14007__li58431113165341>`.

**Collect fault information.**

11. .. _alm-14007__li58431113165341:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

12. Select the following nodes in the required cluster from the **Service**:

    -  ZooKeeper
    -  HDFS

13. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532607958.png
