:original_name: ALM-12202.html

.. _ALM-12202:

ALM-12202 Process Memory Usage Exceeds the Threshold
====================================================

Alarm Description
-----------------

The system checks the memory usage of main OMS processes every 30 seconds. This alarm is generated when the memory usage of main OMS processes is greater than 90% (default value) of the maximum memory.

This alarm is cleared when the memory usage of main OMS processes is less than or equal to 90% of the maximum memory.

.. note::

   This alarm applies only to MRS 3.3.1 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
12202    Major          Yes
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
| Additional Information | Trigger Condition | Specifies the alarm triggering condition.                |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

If the memory usage of main OMS processes is too high, the performance of these processes deteriorates, and even memory overflow occurs. As a result, main OMS processes are unavailable, and OMS tasks are slow or fail to run.

Possible Causes
---------------

The memory usage of main OMS processes is too high or the memory is inappropriately allocated.

Handling Procedure
------------------

**Check the memory usage of main OMS processes.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the alarm list, expand the alarm details, record the process name in **Location**, click the reported host name, and record the service IP address of the host.

#. Choose **System** > **OMS** to view the **OMS Process Memory Usage Ratio** chart. Check whether the memory usage of the processes reaches the threshold (90% by default) at the time when the alarm is generated.

   If no chart is available, click the drop-down arrow on the right, select **Customize**, select the desired item, and click **OK**.

   -  If yes, go to :ref:`3 <alm-12202__li17254173220575>`.
   -  If the threshold is not reached, go to :ref:`6 <alm-12202__li17840184055712>`.

#. .. _alm-12202__li17254173220575:

   Contact O&M personnel to modify the memory configurations of the processes.

#. Restart the processes for which the alarm is generated.

#. Check whether the alarm is cleared in 10 minutes.

   -  If yes, no further action is required.
   -  If the threshold is not reached, go to :ref:`6 <alm-12202__li17840184055712>`.

**Collect fault information.**

6. .. _alm-12202__li17840184055712:

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
