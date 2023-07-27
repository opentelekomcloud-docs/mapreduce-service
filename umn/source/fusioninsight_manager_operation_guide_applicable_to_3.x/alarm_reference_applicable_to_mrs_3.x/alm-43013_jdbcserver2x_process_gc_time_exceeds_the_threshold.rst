:original_name: ALM-43013.html

.. _ALM-43013:

ALM-43013 JDBCServer2x Process GC Time Exceeds the Threshold
============================================================

Description
-----------

The system checks the garbage collection (GC) time of the JDBCServer2x Process every 60 seconds. This alarm is generated when the detected GC time exceeds the threshold (exceeds 5 seconds for three consecutive checks.) To change the threshold, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **Spark2x** > **GC Time** > **Total GC time in milliseconds (JDBCServer2x)**. This alarm is cleared when the JDBCServer2x GC time is shorter than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
43013    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------------------------------+
| Name              | Meaning                                                                             |
+===================+=====================================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                             |
+-------------------+-------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service name for which the alarm is generated.                        |
+-------------------+-------------------------------------------------------------------------------------+
| RoleName          | Specifies the role name for which the alarm is generated.                           |
+-------------------+-------------------------------------------------------------------------------------+
| HostName          | Specifies the object (host ID) for which the alarm is generated.                    |
+-------------------+-------------------------------------------------------------------------------------+
| Trigger Condition | Generates an alarm when the actual indicator value exceeds the specified threshold. |
+-------------------+-------------------------------------------------------------------------------------+

Impact on the System
--------------------

If the GC time exceeds the threshold, JDBCServer2x maybe run in low performance.

Possible Causes
---------------

The memory of JDBCServer2x is overused, the heap memory is inappropriately allocated. As a result, GCs occur frequently.

Procedure
---------

**Check the GC time.**

#. On the FusionInsight Manager portal, choose **O&M** **> Alarm** **> Alarms** and select the alarm whose **ID** is **43013**. Check the **RoleName** in **Location** and confirm the IP address of **HostName**.

#. On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **Spark2x** > **Instance** and click the JDBCServer2x for which the alarm is generated to go to the **Dashboard** page. Click the drop-down menu in the Chart area and choose **Customize** > **GC Time** > **Garbage Collection (GC) Time of JDBCServer2x** from the drop-down list box in the upper right corner and click **OK** to check whether the GC time is longer than the threshold(default value: 12 seconds).

   -  If yes, go to :ref:`3 <alm-43013__li187231820103612>`.
   -  If no, go to :ref:`6 <alm-43013__li1560184215369>`.

#. .. _alm-43013__li187231820103612:

   On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **Spark2x** > **Configurations**, and click **All** **Configurations**. Choose **JDBCServer2x** > **Default**. The default value of **SPARK_DRIVER_MEMORY** is 4 GB. You can change the value according to the following rules: If this alarm is generated occasionally, increase the value by 0.5 times. If the alarm is frequently reported, increase the value by 1 time. In the case of large service volume and high service concurrency, you are advised to add instances.

#. Restart all JDBCServer2x instances.

#. After 10 minutes, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-43013__li1560184215369>`.

**Collect fault information.**

6. .. _alm-43013__li1560184215369:

   On the FusionInsight Manager interface of active and standby clusters, choose **O&M** > **Log > Download**.

7. Select **Spark2x** in the required cluster from the **Service**.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532767654.png
