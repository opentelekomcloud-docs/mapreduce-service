:original_name: alm_14006.html

.. _alm_14006:

ALM-14006 Number of HDFS Files Exceeds the Threshold
====================================================

Description
-----------

The system periodically checks the number of HDFS files every 30 seconds and compares the number of HDFS files with the threshold. This alarm is generated when the system detects that the number of HDFS files exceeds the threshold.

This alarm is cleared when the number of HDFS files is less than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14006    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------------------------------+
| Parameter         | Description                                                                         |
+===================+=====================================================================================+
| ServiceName       | Specifies the service for which the alarm is generated.                             |
+-------------------+-------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| NSName            | Specifies the NameService service for which the alarm is generated.                 |
+-------------------+-------------------------------------------------------------------------------------+
| Trigger condition | Generates an alarm when the actual indicator value exceeds the specified threshold. |
+-------------------+-------------------------------------------------------------------------------------+

Impact on the System
--------------------

Disk storage space is insufficient, which may result in data import failure. The performance of the HDFS system is affected.

Possible Causes
---------------

The number of HDFS files exceeds the threshold.

Procedure
---------

#. Check whether unnecessary files exist in the system.

   a. Use the client on the cluster node and run the **hdfs dfs -ls** *file or directory path* command to check whether the file or directory can be deleted.

      -  If yes, go to :ref:`1.b <alm_14006__en-us_topic_0191813952_alm-14006_mmccppss_step4>`.
      -  If no, go to :ref:`2.a <alm_14006__en-us_topic_0191813952_yt16>`.

   b. .. _alm_14006__en-us_topic_0191813952_alm-14006_mmccppss_step4:

      Run the **hdfs dfs -rm -r** *file or directory path* command. Delete unnecessary files, wait 5 minutes, and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2.a <alm_14006__en-us_topic_0191813952_yt16>`.

#. Check the number of files in the system.

   a. .. _alm_14006__en-us_topic_0191813952_yt16:

      On MRS Manager, choose **System** > **Threshold Configuration**.

   b. In the navigation tree on the left, choose **Services** > **HDFS** > **HDFS File** > **Total Number of Files**.

   c. In the right pane, modify the threshold in the rule based on the number of current HDFS files.

      To check the number of HDFS files, choose **Services** > **HDFS**, click **Customize** in the **Real-Time Statistics** area on the right, and select the **HDFS File** monitoring item.

   d. Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_14006__en-us_topic_0191813952_li572522141314>`.

#. .. _alm_14006__en-us_topic_0191813952_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
