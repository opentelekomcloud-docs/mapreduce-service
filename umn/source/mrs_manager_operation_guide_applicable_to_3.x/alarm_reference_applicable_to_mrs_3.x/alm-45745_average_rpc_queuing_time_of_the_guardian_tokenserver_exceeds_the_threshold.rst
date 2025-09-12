:original_name: ALM-45745.html

.. _ALM-45745:

ALM-45745 Average RPC Queuing Time of the Guardian TokenServer Exceeds the Threshold
====================================================================================

Alarm Description
-----------------

The system checks the average RPC queuing time of the TokenServer service every 30 seconds. This alarm is generated when the average RPC queuing time of the TokenServer instance has exceeded the threshold for five consecutive times.

This alarm is cleared when the system detects that the average RPC queuing time falls below the threshold.

This alarm applies only to MRS 3.5.0 or later.

Alarm Attributes
----------------

+-----------------------+--------------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                       | Auto Cleared          |
+=======================+======================================+=======================+
| 45745                 | Critical (default threshold: 300 ms) | Yes                   |
|                       |                                      |                       |
|                       | Major (default threshold: 200 ms)    |                       |
+-----------------------+--------------------------------------+-----------------------+

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

If the average RPC queuing time of the Guardian TokenServer instance exceeds the threshold, service access to OBS may slow down or even OBS cannot be accessed.

Possible Causes
---------------

-  The alarm threshold is improperly configured.
-  The memory configured for the Guardian TokenServer instance is too small, and frame freezing occurs on the JVM due to frequent full garbage collection.

Handling Procedure
------------------

**Check whether the alarm threshold is set properly.**

#. .. _alm-45745__en-us_topic_0000002021205921_li441701812715:

   Log in to MRS Manager and choose **O&M** > **Alarm** > **Alarms**. In the **Location** field of the alarm details, view the host name of the TokenServer instance for which this alarm is generated.

#. On MRS Manager, choose **Cluster** > **Services** > **Guardian**. On the page that is displayed, click the **Instances** tab, click the TokenServer role for the host name obtained in :ref:`1 <alm-45745__en-us_topic_0000002021205921_li441701812715>`, click the drop-down list in the upper right corner of the **Chart** area, and select **Customize**. On the **Customize Statistics** page, choose **RPC** > **Average Time of TokenServer RPC Queuing**, and click **OK**.

#. Check whether the average RPC queuing time of TokenServer reaches the alarm threshold (300 ms for critical alarms and 200 ms for major alarms).

   -  If yes, go to :ref:`4 <alm-45745__en-us_topic_0000002021205921_li0418718182715>`.
   -  If no, go to :ref:`6 <alm-45745__en-us_topic_0000002021205921_li15417101818273>`.

#. .. _alm-45745__en-us_topic_0000002021205921_li0418718182715:

   On MRS Manager, choose **O&M** > **Alarm** > **Thresholds**, select the desired cluster, choose **Guardian** > **RPC**, and click **Average Time of TokenServer RPC Queuing**. In the right pane, locate the **default** rule, and click **Modify** in the **Operation** column. On the **Modify Rule** page, change the threshold for the **Critical** or **Major** alarm severity to 150% of the peak value within one day after the alarm is generated, and click **OK**.

#. Wait 5 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-45745__en-us_topic_0000002021205921_li15417101818273>`.

**Check whether the memory of the Guardian TokenServer is too small.**

6. .. _alm-45745__en-us_topic_0000002021205921_li15417101818273:

   On MRS Manager, choose **O&M** > **Alarm** > **Alarms** and check whether alarm **TokenServer Heap Memory Usage Exceeds the Threshold** is reported on the TokenServer instance.

   -  If yes, go to :ref:`7 <alm-45745__en-us_topic_0000002021205921_li641711816272>`.
   -  If no, go to :ref:`9 <alm-45745__en-us_topic_0000002021205921_li849415207819>`.

7. .. _alm-45745__en-us_topic_0000002021205921_li641711816272:

   Rectify the fault by following the handling procedure of **ALM-45737 TokenServer Heap Memory Usage Exceeds the Threshold**.

8. Wait 10 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-45745__en-us_topic_0000002021205921_li849415207819>`.

**Collect fault information.**

9.  .. _alm-45745__en-us_topic_0000002021205921_li849415207819:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

10. Expand the **Service** drop-down list, and select **Guardian** for the target cluster.

11. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
