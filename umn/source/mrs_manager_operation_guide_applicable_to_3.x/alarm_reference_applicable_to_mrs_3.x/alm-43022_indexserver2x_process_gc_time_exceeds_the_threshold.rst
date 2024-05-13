:original_name: ALM-43022.html

.. _ALM-43022:

ALM-43022 IndexServer2x Process GC Time Exceeds the Threshold
=============================================================

Description
-----------

The system checks the GC time of the IndexServer2x process every 60 seconds. This alarm is generated when the detected GC time exceeds the threshold (12 seconds) for three consecutive times. To change the threshold, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **Spark2x** > **GC Time** > **Total GC time in milliseconds (IndexServer2x)**. This alarm is cleared when the IndexServer2x GC time is shorter than or equal to the threshold.

Attribute
---------

======== ======== ==========
Alarm ID Severity Auto Clear
======== ======== ==========
43022    Major    Yes
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

If the GC time exceeds the threshold, IndexServer2x may run in low performance or even unavailable.

Possible Causes
---------------

The heap memory of the IndexServer2x process is overused or the heap memory is inappropriately allocated. As a result, GC occurs frequently.

Procedure
---------

**Check the GC time.**

#. On MRS Manager, choose **O&M** > **Alarm** **> Alarms**. In the displayed alarm list, choose the alarm with ID **43022**, and check the **RoleName** in **Location** and confirm the IP address of **HostName**.

#. On MRS Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Spark2x** > **Instance** and click the IndexServer2x for which the alarm is generated to go to the **Dashboard** page. Click the drop-down menu in the Chart area and choose **Customize** > **GC Time** > **Garbage Collection (GC) Time of IndexServer2x** from the drop-down list box in the upper right corner and click **OK** to check whether the GC time is longer than the threshold (default value: 12 seconds).

   -  If the threshold is reached, go to :ref:`3 <alm-43022__li928810235414>`.
   -  If the threshold is not reached, go to :ref:`6 <alm-43022__li728614235411>`.

#. .. _alm-43022__li928810235414:

   On MRS Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Spark2x** > **Configurations** > **All Configurations** > **IndexServer2x** > **Default**. The default value of the **SPARK_DRIVER_MEMORY** is 4 GB. You can change the value according to the following rules: Increase the value of the **SPARK_DRIVER_MEMORY** parameter 1.5 times to its default value. If this alarm is still generated occasionally after the adjustment, increase the value by 0.5 times. Double the value if the alarm is reported frequently.

#. Restart all IndexServer2x instances.

#. After 10 minutes, check whether the alarm is cleared.

   -  If the alarm is cleared, no further action is required.
   -  If the alarm is not cleared, go to :ref:`6 <alm-43022__li728614235411>`.

**Collect fault information.**

6. .. _alm-43022__li728614235411:

   On MRS Manager, choose **O&M** > **Log** > **Download**.

7. Expand the **Service** drop-down list, and select **Spark2x** for the target cluster.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.

9. Contact the O&M personnel and provide the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Reference
---------

None

.. |image1| image:: /_static/images/en-us_image_0000001532607946.png
