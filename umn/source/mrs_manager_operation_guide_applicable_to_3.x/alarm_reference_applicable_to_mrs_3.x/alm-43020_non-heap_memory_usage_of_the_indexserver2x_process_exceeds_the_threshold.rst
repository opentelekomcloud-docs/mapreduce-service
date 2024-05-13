:original_name: ALM-43020.html

.. _ALM-43020:

ALM-43020 Non-Heap Memory Usage of the IndexServer2x Process Exceeds the Threshold
==================================================================================

Description
-----------

The system checks the IndexServer2x process status every 30 seconds. The alarm is generated when the non-heap memory usage of the IndexServer2x process exceeds the threshold (95% of the maximum memory).

Attribute
---------

======== ======== ==========
Alarm ID Severity Auto Clear
======== ======== ==========
43020    Major    Yes
======== ======== ==========

Parameters
----------

+-------------------+---------------------------------------------------------+
| Parameter         | Description                                             |
+===================+=========================================================+
| Source            | Specifies the cluster for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.       |
+-------------------+---------------------------------------------------------+

Impact on the System
--------------------

If the available IndexServer2x process non-heap memory is insufficient, a memory overflow occurs and the service breaks down.

Possible Causes
---------------

The non-heap memory of the IndexServer2x process is overused or the non-heap memory is inappropriately allocated.

Procedure
---------

**Check non-heap memory usage.**

#. On MRS Manager, choose **O&M** > **Alarm** **> Alarms**. In the displayed alarm list, choose the alarm for which the ID is **43020**, and check the **RoleName** in **Location** and confirm the IP address of **HostName**.

#. On MRS Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Spark2x** > **Instance**. Click the IndexServer2x that reported the alarm to go to the **Dashboard** page. Click the drop-down list in the upper right corner of the chart area, and choose **Customize** > **Memory > IndexServer2x Memory Usage Statistics** > **OK**. Check whether the non-heap memory used by the IndexServer2x process reaches the maximum non-heap memory threshold (95% by default).

   -  If the threshold is reached, go to :ref:`3 <alm-43020__li311482053120>`.
   -  If the threshold is not reached, go to :ref:`7 <alm-43020__li141131720123116>`.

#. .. _alm-43020__li311482053120:

   On MRS Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Spark2x** > **Instance**. Click the IndexServer2x that reported the alarm to go to the **Dashboard** page. Click the drop-down list in the upper right corner of the chart area, and choose **Customize** > **Memory** > **Statistics for the non-heap memory of the IndexServer2x Process** > **OK**. Based on the alarm generation time, check the values of the used non-heap memory of the IndexServer2x process in the corresponding period and obtain the maximum value.

#. On MRS Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Spark2x** > **Configurations** > **All Configurations** > **IndexServer2x**> **Tuning**. You can change the value of **XX:MaxMetaspaceSize** in the **spark.driver.extraJavaOptions** parameter based on the ratio of the maximum non-heap memory used by the IndexServer2x process to the threshold specified by **IndexServer2x Non-Heap Memory Usage Statistics (IndexServer2x)** in the alarm period.

   .. note::

      On MRS Manager, you can choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **Spark2x** > **Memory** > **IndexServer2x Non-Heap Memory Usage Statistics (IndexServer2x)** to view the threshold.

#. Restart all IndexServer2x instances.

#. After 10 minutes, check whether the alarm is cleared.

   -  If the alarm is cleared, no further action is required.
   -  If the alarm is not cleared, go to :ref:`7 <alm-43020__li141131720123116>`.

**Collect fault information**.

7.  .. _alm-43020__li141131720123116:

    On MRS Manager, choose **O&M** > **Log** > **Download**.

8.  Expand the **Service** drop-down list, and select **Spark2x** for the target cluster.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.

10. Contact the O&M personnel and provide the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Reference
---------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927518.png
