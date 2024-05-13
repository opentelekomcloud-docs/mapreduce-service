:original_name: ALM-45175.html

.. _ALM-45175:

ALM-45175 Average Time for Calling OBS Metadata APIs Is Greater than the Threshold
==================================================================================

Description
-----------

The system checks whether the average duration for calling OBS metadata APIs is greater than the threshold every 30 seconds. This alarm is generated when the number of consecutive times that the average time exceeds the specified threshold is greater than the number of smoothing times.

This alarm is automatically cleared when the average duration for calling the OBS metadata APIs is lower than the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45175    Minor          Yes
======== ============== ==========

Parameters
----------

+-------------------+---------------------------------------------------------+
| Name              | Meaning                                                 |
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

If the average time for calling the OBS metadata APIs exceeds the threshold, the upper-layer big data computing services may be affected. To be more specific, the execution time of some computing tasks will exceed the threshold.

Possible Causes
---------------

Frame freezing occurs on the OBS server, or the network between the OBS client and the OBS server is unstable.

Procedure
---------

**Check the heap memory usage.**

#. On the **MRS Manager** homepage, choose **O&M** > **Alarm** > **Alarms** > **Average Time for Calling the OBS Metadata API Exceeds the Threshold**, view the role name in **Location**, and check the instance IP address.

#. Choose **Cluster** > *Name of the desired cluster* > **Services** > **meta** > **Instance** > **meta** (IP address of the instance for which the alarm is generated). Click the drop-down list in the upper right corner of the chart area and choose **Customize**. In the dialog box that is displayed, select **Average time of OBS interface calls** from **OBS Meta data Operations**, and click **OK**. Check whether the average time of OBS metadata API calls exceeds the threshold.

   -  If yes, go to :ref:`3 <alm-45175__li5868113155910>`.
   -  If no, go to :ref:`5 <alm-45175__li4749473185459>`.

#. .. _alm-45175__li5868113155910:

   Choose **Cluster** > *Name of the desired cluster* > **O&M** > **Alarm** > **Thresholds** > **meta** > **Average Time for Calling the OBS Metadata API**. Increase the threshold or smoothing times as required.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-45175__li4749473185459>`.

**Collect the fault information.**

5. .. _alm-45175__li4749473185459:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. In the **Services** area, select **NodeAgent**, **NodeMetricAgent**, **OmmServer**, and **OmmAgent** under OMS.

7. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582807905.png
