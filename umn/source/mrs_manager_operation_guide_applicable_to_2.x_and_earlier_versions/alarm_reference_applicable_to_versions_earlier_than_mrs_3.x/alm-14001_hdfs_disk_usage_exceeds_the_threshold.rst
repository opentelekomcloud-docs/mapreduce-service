:original_name: alm_14001.html

.. _alm_14001:

ALM-14001 HDFS Disk Usage Exceeds the Threshold
===============================================

Description
-----------

The system checks the disk usage of the HDFS cluster every 30 seconds and compares the actual disk usage with the threshold. The HDFS cluster disk usage indicator has a default threshold. This alarm is generated when the HDFS disk usage exceeds the threshold.

This alarm is cleared when the disk usage of the HDFS cluster is less than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14001    Major          Yes
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

The performance of writing data to HDFS is affected.

Possible Causes
---------------

The disk space configured for the HDFS cluster is insufficient.

Procedure
---------

#. Check the disk capacity and delete unnecessary files.

   a. On the MRS cluster details page, choose **Components** > **HDFS**. The **Service Status** page is displayed.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and choose **Services** > **HDFS**.

   b. In the **Charts** area, view the value of the monitoring indicator **Percentage of HDFS Capacity** to check whether the HDFS disk usage exceeds the threshold (80% by default).

      -  If yes, go to :ref:`1.c <alm_14001__en-us_topic_0191813969_cn_58_42_000001_5_mmccppss_step5>`.
      -  If no, go to :ref:`3 <alm_14001__en-us_topic_0191813969_li572522141314>`.

   c. .. _alm_14001__en-us_topic_0191813969_cn_58_42_000001_5_mmccppss_step5:

      Use the client on the cluster node and run the **hdfs dfsadmin -report** command to check whether the value of **DFS Used%** is less than 100% minus the threshold.

      -  If yes, go to :ref:`1.e <alm_14001__en-us_topic_0191813969_li39567352>`.
      -  If no, go to :ref:`3 <alm_14001__en-us_topic_0191813969_li572522141314>`.

   d. Use the client on the cluster node and run the **hdfs dfs -rm -r** *file or directory path* command to delete unnecessary files.

   e. .. _alm_14001__en-us_topic_0191813969_li39567352:

      Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2.a <alm_14001__en-us_topic_0191813969_cn_58_42_000001_5_mmccppss_step13>`.

#. Expand the system.

   a. .. _alm_14001__en-us_topic_0191813969_cn_58_42_000001_5_mmccppss_step13:

      Expand the disk capacity.

   b. Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_14001__en-us_topic_0191813969_li572522141314>`.

#. .. _alm_14001__en-us_topic_0191813969_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
