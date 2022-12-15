:original_name: ALM-43006.html

.. _ALM-43006:

ALM-43006 Heap Memory Usage of the JobHistory2x Process Exceeds the Threshold
=============================================================================

Description
-----------

The system checks the JobHistory2x Process status every 30 seconds. The alarm is generated when the heap memory usage of a JobHistory2x Process exceeds the threshold (95% of the maximum memory).

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
43006    Major          Yes
======== ============== ==========

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

If the available JobHistory2x Process heap memory is insufficient, a memory overflow occurs and the service breaks down.

Possible Causes
---------------

The heap memory of the JobHistory2x Process is overused or the heap memory is inappropriately allocated.

Procedure
---------

**Check heap memory usage.**

#. On the FusionInsight Manager portal, choose **O&M > Alarm** **> Alarms** and select the alarm whose **ID** is **43006**. Check the **RoleName** in **Location** and confirm the IP address of **HostName**.

#. On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **Spark2x** > **Instance** and click the JobHistory2x for which the alarm is generated to go to the **Dashboard** page. Click the drop-down menu in the Chart area and choose **Customize** > **Memory > JobHistory2x Memory Usage Statistics** from the drop-down list box in the upper right corner and click **OK**. Check whether the used heap memory of the JobHistory2x Process reaches the threshold(default value is 95%) of the maximum heap memory specified for JobHistory2x.

   -  If yes, go to :ref:`3 <alm-43006__li11885161253>`.
   -  If no, go to :ref:`7 <alm-43006__li113872433153>`.

#. .. _alm-43006__li11885161253:

   On the FusionInsight Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services** > **Spark2x** > **Instance**. Click **JobHistory2x** by which the alarm is reported to go to the **Dashboard** page, click the drop-down list in the upper right corner of the chart area, choose **Customize** > **Memory > Statistics for the heap memory of the JobHistory2x Process**, and click **OK**. Based on the alarm generation time, check the values of the used heap memory of the JobHistory2x process in the corresponding period and obtain the maximum value.

#. On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **Spark2x** > **Configurations**, and click **All Configurations**. Choose **JobHistory2x** > **Default**. The default value of **SPARK_DAEMON_MEMORY** is 4GB. You can change the value according to the following rules: Ratio of the maximum heap memory usage of the JobHistory2x to the **Threshold** of the **JobHistory2x Heap Memory Usage Statistics (JobHistory2x)** in the alarm period. If this alarm is generated occasionally after the parameter value is adjusted, increase the value by 0.5 times. If the alarm is frequently reported after the parameter value is adjusted, increase the value by 1 time.

   .. note::

      On the FusionInsight Manager home page, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* **>** **Spark2x** > **Memory** >\ **JobHistory2x Heap Memory Usage Statistics (JobHistory2x)** to view **Threshold**.

#. Restart all JobHistory2x instances.

#. After 10 minutes, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-43006__li113872433153>`.

**Collect fault information.**

7.  .. _alm-43006__li113872433153:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

8.  Select **Spark2x** in the required cluster from the **Service**.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269417534.png
