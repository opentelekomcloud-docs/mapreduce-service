:original_name: ALM-43018.html

.. _ALM-43018:

ALM-43018 JobHistory2x Process Full GC Number Exceeds the Threshold
===================================================================

Description
-----------

The system checks the number of Full garbage collection (GC) times of the JobHistory2x process every 60 seconds. This alarm is generated when the detected Full GC number exceeds the threshold (exceeds 12 for three consecutive checks.) You can change the threshold by choosing **O&M** > **Alarm > Thresholds** > *Name of the desired cluster* > **Spark2x** > **GC number** > **Full GC Number of JobHistory2x**. This alarm is cleared when the Full GC number of the JobHistory2x process is less than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
43018    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+---------------------------------------------------------+
| Name              | Description                                             |
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

The performance of the JobHistory2x process is affected, or even the JobHistory2x process is unavailable.

Possible Causes
---------------

The heap memory usage of the JobHistory2x process is excessively large, or the heap memory is inappropriately allocated. As a result, Full GC occurs frequently.

Procedure
---------

**Check the number of Full GCs.**

#. Log in to MRS Manager, choose **O&M** > **Alarm** **> Alarms**, select this alarm, and check the **RoleName** in **Location** and confirm the IP address of **HostName**.

#. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Spark2x** > **Instance**. On the displayed page, click the JobHistory2x for which the alarm is reported. On the **Dashboard** page that is displayed, click the drop-down menu in the Chart area and choose **Customize** > **GC Number** > **Full GC Number of JobHistory2x** in the upper right corner and click **OK**. Check whether the number of Full GCs of the JobHistory2x process is greater than the threshold(default value: 12).

   -  If it is, go to :ref:`3 <alm-43018__li15899121475>`.
   -  If it is not, go to :ref:`6 <alm-43018__li159003211673>`.

#. .. _alm-43018__li15899121475:

   Choose **Cluster** > *Name of the desired cluster* > **Services** > **Spark2x** > **Configurations** > **All Configurations**. On the displayed page, choose **JobHistory2x** > **Default.** The default value of **SPARK_DAEMON_MEMORY** is 4GB. You can change the value according to the following rules: If this alarm is generated occasionally, increase the value by 0.5 times. If the alarm is frequently reported, increase the value by 1 time.

#. Restart all JobHistory2x instances.

#. After 10 minutes, check whether the alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`6 <alm-43018__li159003211673>`.

   **Collect fault information.**

#. .. _alm-43018__li159003211673:

   Log in to MRS Manager, and choose **O&M** > **Log** > **Download**.

#. Select **Spark2x** in the required cluster from the **Service**.

#. Click |image1| in the upper right corner. In the displayed dialog box, set **Start Date** and **End Date** to 10 minutes before and after the alarm generation time respectively and click **OK**. Then, click **Download**.

#. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

This alarm will be automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001782496978.png
