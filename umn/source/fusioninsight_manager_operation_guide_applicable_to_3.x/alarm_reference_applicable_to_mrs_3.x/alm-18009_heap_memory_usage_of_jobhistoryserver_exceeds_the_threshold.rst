:original_name: ALM-18009.html

.. _ALM-18009:

ALM-18009 Heap Memory Usage of JobHistoryServer Exceeds the Threshold
=====================================================================

Description
-----------

The system checks the heap memory usage of Mapreduce JobHistoryServer every 30 seconds and compares the actual usage with the threshold. The alarm is generated when the heap memory usage of Mapreduce JobHistoryServer exceeds the threshold (95% of the maximum memory by default).

Users can choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **Mapreduce** to change the threshold.

When the **Trigger Count** is 1, this alarm is cleared when the heap memory usage of MapReduce JobHistoryServer is less than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the heap memory usage of MapReduce JobHistoryServer is less than or equal to 95% of the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
18009    Major          Yes
======== ============== =====================

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service name for which the alarm is generated.                                                                 |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role name for which the alarm is generated.                                                                    |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the object (host ID) for which the alarm is generated.                                                             |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

When the heap memory usage of Mapreduce JobHistoryServer is overhigh, the performance of Mapreduce log archiving is affected. In addition, a memory overflow may occur so that the Yarn service is unavailable.

Possible Causes
---------------

The heap memory of the Mapreduce JobHistoryServer instance on the node is overused or the heap memory is inappropriately allocated. As a result, the usage exceeds the threshold.

Procedure
---------

**Check the memory usage.**

#. On the FusionInsight Manager portal, choose **O&M > Alarm > Alarms** > **ALM-18009 Heap Memory Usage of MapReduce JobHistoryServer Exceeds the Threshold** > **Location**. Check the HostName of the instance for which the alarm is generated.

#. On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* **> Services** > **Mapreduce** > **Instance** > **JobHistoryServer.** Click the drop-down menu in the upper right corner of **Chart**, choose **Customize** > **JobHistoryServer heap memory usage statistics**. JobHistoryServer indicates the corresponding HostName of the instance for which the alarm is generated. Check the heap memory usage.

#. Check whether the used heap memory of JobHistoryServer reaches 95% of the maximum heap memory specified for JobHistoryServer.

   -  If yes, go to :ref:`4 <alm-18009__li4972156185337>`.
   -  If no, go to :ref:`6 <alm-18009__li30977950185337>`.

#. .. _alm-18009__li4972156185337:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* **> Services** > **Mapreduce** > **Configurations** > **All** **Configurations** > **JobHistoryServer** > **System**. Increase the value of **GC_OPTS** parameter as required, click **Save**. Click **OK** and restart the role instance.

   .. note::

      The mapping between the number of historical tasks (10000) and the memory of JobHistoryServer is as follows:

      -Xms30G -Xmx30G -XX:NewSize=1G -XX:MaxNewSize=2G

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-18009__li30977950185337>`.

**Collect fault information.**

6. .. _alm-18009__li30977950185337:

   On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

7. Select the following node in the required cluster from the **Service**.

   -  NodeAgent
   -  Mapreduce

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582927825.png
