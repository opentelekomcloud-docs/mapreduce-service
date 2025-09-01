:original_name: ALM-12203.html

.. _ALM-12203:

ALM-12203 Process Full GC Duration Exceeds the Threshold
========================================================

Alarm Description
-----------------

The system checks the GC duration of main OMS processes every 30 seconds. If the GC duration of an OMS process exceeds the threshold for three consecutive times, this alarm is generated. You can choose **O&M** > **Alarm** > **Thresholds** > **OMS** > **OMSServices** to change the threshold.

This alarm is cleared when the GC duration of the OMS process is shorter than or equal to the threshold.

.. note::

   This alarm applies only to MRS 3.3.1 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
12203    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------------+----------------------------------------------------------+
| Type                   | Parameter         | Description                                              |
+========================+===================+==========================================================+
| Location Information   | Source            | Specifies the cluster for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------+
|                        | ServiceName       | Specifies the service for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------+
|                        | RoleName          | Specifies the role for which the alarm was generated.    |
+------------------------+-------------------+----------------------------------------------------------+
|                        | HostName          | Specifies the host for which the alarm was generated.    |
+------------------------+-------------------+----------------------------------------------------------+
| Additional Information | Trigger condition | Specifies the alarm triggering condition.                |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

Read and write performance deteriorates. As a result, the task execution may slow down and even the service may restart unexpectedly.

Possible Causes
---------------

The memory of main OMS processes is too high or inappropriately allocated, causing frequent occurrence of the full GC.

Handling Procedure
------------------

**Check the GC duration.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the alarm list, expand the alarm details, record the process name in **Location**, click the reported host name, and record the service IP address of the host.

#. Choose **System** > **OMS**, view the Full GC Times of OMS Process chart, and check whether the GC time is longer than 12 seconds (default value).

   If no chart is available, click the drop-down arrow on the right, select **Customize**, select the desired item, and click **OK**.

   -  If yes, go to :ref:`3 <alm-12203__li17254173220575>`.
   -  If no, go to :ref:`6 <alm-12203__li24184344163548>`.

3. .. _alm-12203__li17254173220575:

   Contact O&M personnel to modify the memory configurations of the processes.

4. Restart the process.

5. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12203__li24184344163548>`.

**Collect fault information.**

6. .. _alm-12203__li24184344163548:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7. Expand the **Service** drop-down list, and select **OmmServer** for the target cluster.

8. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
