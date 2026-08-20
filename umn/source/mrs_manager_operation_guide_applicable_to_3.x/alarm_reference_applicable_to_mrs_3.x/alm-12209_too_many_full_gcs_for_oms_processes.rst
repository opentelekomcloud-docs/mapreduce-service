:original_name: ALM-12209.html

.. _ALM-12209:

ALM-12209 Too Many Full GCs for OMS Processes
=============================================

Alarm Description
-----------------

The system checks the full GC count of OMS processes every 60 seconds. This alarm is generated when the number of full GCs exceeds the threshold.

The statistical method is Full GC count = Full GC count in the next period - Full GC count in the previous period. By default, an alarm is reported when the Full GC count exceeds 1 for three consecutive checks. You can adjust this threshold via **O&M** > **Alarm** > **Thresholds** > **OMS** > **OMSServices** > **GC**.

This alarm is cleared when the full GC count of the OMS processes is less than or equal to the threshold.

.. note::

   This alarm applies only to MRS 3.6.0 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
12209    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------------+----------------------------------------------------------------------+
| Type                   | Parameter         | Description                                                          |
+========================+===================+======================================================================+
| Location Information   | Source            | Specifies the cluster for which the alarm was generated.             |
+------------------------+-------------------+----------------------------------------------------------------------+
|                        | ServiceName       | Specifies the service for which the alarm was generated.             |
+------------------------+-------------------+----------------------------------------------------------------------+
|                        | RoleName          | Specifies the role for which the alarm was generated.                |
+------------------------+-------------------+----------------------------------------------------------------------+
|                        | HostName          | Specifies the host for which the alarm was generated.                |
+------------------------+-------------------+----------------------------------------------------------------------+
|                        | ProcessName       | Specifies the name of the process for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------------------+
| Additional Information | Trigger condition | Specifies the threshold for triggering the alarm.                    |
+------------------------+-------------------+----------------------------------------------------------------------+

Impact on the System
--------------------

The read and write operations of OMS processes are affected, which may lead to slowed task execution, unexpected service restarts, and false reporting of other alarms.

Possible Causes
---------------

The memory of main OMS processes is too high or inappropriately allocated, causing frequent occurrence of the full GC.

Handling Procedure
------------------

**Check the Full GC count of the OMS process**.

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the alarm list, expand the alarm details, record the process name in **Location**, click the reported host name, and record the service IP address of the host.

#. Choose **System** > **OMS**, view the **Full GCs of an OMS Process** - *Process Name* chart, and check whether the GC count is more than 1 (default value).

   If no corresponding chart is available, click the drop-down arrow on the right of the **Chart** area, choose **Customize**, select the corresponding indicator, and click **OK**.

   -  If yes, go to :ref:`3 <alm-12209__en-us_topic_0000002149269068_en-us_topic_0000002130115070_li17254173220575>`.
   -  If no, go to :ref:`5 <alm-12209__en-us_topic_0000002149269068_en-us_topic_0000002130115070_li24184344163548>`.

3. .. _alm-12209__en-us_topic_0000002149269068_en-us_topic_0000002130115070_li17254173220575:

   Contact O&M personnel to modify the memory usage configuration of the processes and restart it.

4. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-12209__en-us_topic_0000002149269068_en-us_topic_0000002130115070_li24184344163548>`.

**Collect fault information.**

5. .. _alm-12209__en-us_topic_0000002149269068_en-us_topic_0000002130115070_li24184344163548:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Expand the **Service** drop-down list, and select **OmmServer** for the target cluster.

7. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
