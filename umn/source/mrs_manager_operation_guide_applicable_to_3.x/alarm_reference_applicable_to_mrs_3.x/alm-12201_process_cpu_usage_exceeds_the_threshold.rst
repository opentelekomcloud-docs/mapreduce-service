:original_name: ALM-12201.html

.. _ALM-12201:

ALM-12201 Process CPU Usage Exceeds the Threshold
=================================================

Alarm Description
-----------------

The system checks the CPU usage every 30 seconds and compares the check result with the default threshold. This alarm is generated when the CPU usage exceeds the threshold for multiple consecutive times (**10** by default).

This alarm is cleared when **Trigger Count** is **1** and the CPU usage is less than or equal to the threshold. This alarm is cleared when **Trigger Count** is greater than 1 and the CPU usage is less than or equal to 90% of the threshold.

.. note::

   This alarm applies only to MRS 3.3.1 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
12201    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------------+--------------------------------------------------------------------+
| Type                   | Parameter         | Description                                                        |
+========================+===================+====================================================================+
| Location Information   | Source            | Specifies the cluster or system for which the alarm was generated. |
+------------------------+-------------------+--------------------------------------------------------------------+
|                        | ServiceName       | Specifies the service for which the alarm was generated.           |
+------------------------+-------------------+--------------------------------------------------------------------+
|                        | RoleName          | Specifies the role for which the alarm was generated.              |
+------------------------+-------------------+--------------------------------------------------------------------+
|                        | HostName          | Specifies the host for which the alarm was generated.              |
+------------------------+-------------------+--------------------------------------------------------------------+
| Additional Information | Trigger Condition | Specifies the alarm triggering condition.                          |
+------------------------+-------------------+--------------------------------------------------------------------+

Impact on the System
--------------------

-  Latency: Service processes may run slowly and there is a latency.
-  Service failure: Service processing may be slow, time out, or fail. As a result, jobs may fail to run.

Possible Causes
---------------

-  The alarm threshold or alarm trigger count is improperly configured.
-  The CPU configuration cannot meet service requirements, and the CPU usage reaches the upper limit. Alternatively, services are in peak hours. The CPU usage reaches the upper limit in a short period.

Handling Procedure
------------------

**Check whether the alarm threshold or alarm trigger count is properly configured.**

#. Modify the alarm threshold and alarm trigger count based on the actual CPU usage.

   a. Log in to MRS Manager and choose **O&M** > **Alarm** > **Thresholds** > **OMS** > **OMSServices** > **CPU** > **Process Used CPU (OMS)**.
   b. Click the edit button next to **Trigger Count** to set it a proper value based on the actual service usage.

      .. note::

         **Trigger Count** indicates how many consecutive times the threshold is reached when the alarm is triggered.

   c. Click **Modify** in the **Operation** column of the row that contains the rule and change the alarm threshold.

#. Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-12201__li64287686173731>`.

**Check whether the CPU usage reaches the upper limit.**

3. .. _alm-12201__li64287686173731:

   On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the alarm list, expand the alarm details and click the name of the host for which the alarm is generated in **Location** area.

4. On the overview page of the host, observe the real-time data of the host CPU usage for about 5 minutes. If the CPU usage exceeds the threshold for multiple times, contact the MRS cluster administrator to increase the CPU.

   If no chart is available, click the drop-down arrow on the right, select **Customize**, select the desired item, and click **OK**.

5. Check whether it was the peak hour. If this alarm was generated during peak hours, expand the node capacity or contact the MRS cluster administrator to improve the CPU specification.

6. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-12201__li39839699173731>`.

**Collect fault information.**

7.  .. _alm-12201__li39839699173731:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Expand the **Service** drop-down list, select **OmmServer** for the target cluster, and click **OK**.

9.  Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
