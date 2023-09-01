:original_name: ALM-14020.html

.. _ALM-14020:

ALM-14020 Number of Entries in the HDFS Directory Exceeds the Threshold
=======================================================================

Description
-----------

The system obtains the number of subfiles and subdirectories in a specified directory every hour and checks whether it reaches the percentage of the threshold (the maximum number of subfiles and subdirectories in an HDFS directory, the threshold for triggering an alarm is **90%** by default). If it exceeds the percentage of the threshold, an alarm is triggered.

When the number of subfiles and subdirectories in the directory the alarm is lower than the percentage of the threshold, the alarm is automatically cleared. When the monitoring switch is disabled, alarms corresponding to all directories are cleared. If a directory is removed from the monitoring list, alarms corresponding to the directory are cleared.

.. note::

   -  The **dfs.namenode.fs-limits.max-directory-items** parameter specifies the maximum number of subfiles and subdirectories in the HDFS directory. Its default value is **1048576**. If the number of subfiles and subdirectories in a directory exceeds the parameter value, subfiles and subdirectories cannot be created in the directory.
   -  The **dfs.namenode.directory-items.monitor** parameter specifies the list of directories to be monitored. Its default value is **/tmp,/SparkJobHistory,/mr-history**.
   -  The **dfs.namenode.directory-items.monitor.enabled** parameter is used to enable or disable the monitoring switch. Its default value is **true**, which means the monitoring switch is enabled by default.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
14020    Major          Yes
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
| NameServiceName   | Specifies the NameService service for which the alarm is generated.                                                          |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Directory         | Specifies the directory for which the alarm is generated.                                                                    |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

If the number of entries in the monitored directory exceeds 90% of the threshold, an alarm is triggered, but entries can be added to the directory. Once the maximum threshold is exceeded, entries will fail to be added to the directory.

Possible Causes
---------------

The number of entries in the monitored directory exceeds 90% of the threshold.

Procedure
---------

**Check whether unnecessary files exist in the system.**

#. Log in to the HDFS client as user **root**. Run the **cd** command to go to the client installation directory, and run the **source bigdata_env** command to set the environment variables.

   If the cluster is in security mode, security authentication is required.

   Run the **kinit hdfs** command and enter the password as prompted. Obtain the password from the administrator.

#. Run the following command to check whether files and directories in the directory with the alarm can be deleted:

   **hdfs dfs -ls** *Directory with the alarm*

   -  If yes, go to :ref:`3 <alm-14020__li352493139594>`.
   -  If no, go to :ref:`5 <alm-14020__li564838279594>`.

#. .. _alm-14020__li352493139594:

   Run the following command to delete unnecessary files.

   **hdfs dfs -rm -r -f** *File or directory path*

   .. note::

      Deleting a file or folder is a high-risk operation. Ensure that the file or folder is no longer required before performing this operation.

#. Wait 1 hour and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-14020__li564838279594>`.

**Check whether the threshold is correctly configured.**

5. .. _alm-14020__li564838279594:

   On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS** > **Configurations** > **All** **Configurations**. Search for the **dfs.namenode.fs-limits.max-directory-items** parameter and check whether the parameter value is appropriate.

   -  If yes, go to :ref:`9 <alm-14020__li615368649594>`.
   -  If no, go to :ref:`6 <alm-14020__li152448229594>`.

6. .. _alm-14020__li152448229594:

   Increase the parameter value.

7. Save the configuration and click **Dashboard** > **More** > **Restart Service**.

8. Wait 1 hour and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-14020__li615368649594>`.

**Collect fault information.**

9.  .. _alm-14020__li615368649594:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

10. Select **HDFS** in the required cluster from the **Service**.

11. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582807729.png
