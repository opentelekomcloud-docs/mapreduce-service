:original_name: alm_18009.html

.. _alm_18009:

ALM-18009 Heap Memory Usage of MapReduce JobHistoryServer Exceeds the Threshold
===============================================================================

Description
-----------

The system checks the heap memory usage of MapReduce JobHistoryServer every 30 seconds and compares the actual usage with the threshold. The alarm is generated when the heap memory usage of MapReduce JobHistoryServer exceeds the threshold (80% of the maximum memory by default).

To change the threshold, choose **System** > **Threshold Configuration** > **Service** > **MapReduce**. The alarm is cleared when the heap memory usage is less than or equal to the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
18009    Major          Yes
======== ============== =====================

Parameters
----------

+-------------------+---------------------------------------------------------+
| Parameter         | Description                                             |
+===================+=========================================================+
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

When the heap memory usage of MapReduce JobHistoryServer is overhigh, the performance of MapReduce log archiving is affected. What is more, a memory overflow occurs so that the Yarn service is unavailable.

Possible Causes
---------------

The heap memory of the MapReduce JobHistoryServer instance on the node is overused or the heap memory is inappropriately allocated. As a result, the usage exceeds the threshold.

Procedure
---------

#. Check the heap memory usage.

   a. Go to the cluster details page and choose **Alarms**.

   b. Select the alarm whose **Alarm ID** is **18009** and view the IP address and role name of the instance in **Location**.

   c. Choose **Components** > **MapReduce** > **Instance** > **JobHistoryServer** (IP address of the instance for which the alarm is generated) > **Customize** > **JobHistoryServer Heap Memory Usage Statistics**. Check the heap memory usage.

   d. Check whether the heap memory usage of JobHistoryServer has reached the threshold (80% of the maximum heap memory).

      -  If yes, go to :ref:`1.e <alm_18009__en-us_topic_0191813867_li1011493181634>`.
      -  If no, go to :ref:`2 <alm_18009__en-us_topic_0191813867_li572522141314>`.

   e. .. _alm_18009__en-us_topic_0191813867_li1011493181634:

      Choose **Components** > **MapReduce** > **Service Configuration**. Set **Type** to **All** and choose **JobHistoryServer** > **System**. Increase the value of **-Xmx** in the **GC_OPTS** parameter as required, click **Save Configuration**, and select **Restart the affected services or instances.** Click **OK**.

   f. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_18009__en-us_topic_0191813867_li572522141314>`.

#. .. _alm_18009__en-us_topic_0191813867_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
