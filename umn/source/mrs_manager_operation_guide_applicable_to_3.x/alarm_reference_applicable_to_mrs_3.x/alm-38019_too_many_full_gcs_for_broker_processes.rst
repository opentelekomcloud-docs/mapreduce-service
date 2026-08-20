:original_name: ALM-38019.html

.. _ALM-38019:

ALM-38019 Too Many Full GCs for Broker Processes
================================================

Alarm Description
-----------------

The system monitors the number of full garbage collection (GC) events for Broker processes every 60 seconds. A major alarm is generated if the count exceeds 12 for three consecutive times. A minor alarm is generated if the count exceeds 9 (80% of 12, rounded down) for three consecutive times.

You can log in to MRS Manager and change the threshold by choosing **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **Kafka** > **Process** > **Broker Full GCs**. This alarm is cleared when the number of full GC events for the Broker process is less than or equal to the threshold.

.. note::

   This alarm applies only to MRS 3.6.0 or later.

Alarm Attributes
----------------

+-----------------------+-----------------------------------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                                            | Auto Cleared          |
+=======================+===========================================================+=======================+
| 38019                 | Minor (default threshold: 9 for three consecutive times)  | Yes                   |
|                       |                                                           |                       |
|                       | Major (default threshold: 12 for three consecutive times) |                       |
+-----------------------+-----------------------------------------------------------+-----------------------+

Alarm Parameters
----------------

+------------------------+----------------+----------------------------------------------------------+
| Type                   | Parameter      | Description                                              |
+========================+================+==========================================================+
| Location Information   | Source         | Specifies the cluster for which the alarm was generated. |
+------------------------+----------------+----------------------------------------------------------+
|                        | ServiceName    | Specifies the service for which the alarm was generated. |
+------------------------+----------------+----------------------------------------------------------+
|                        | RoleName       | Specifies the role for which the alarm was generated.    |
+------------------------+----------------+----------------------------------------------------------+
|                        | HostName       | Specifies the host for which the alarm was generated.    |
+------------------------+----------------+----------------------------------------------------------+
| Additional Information | ThresholdValue | Specifies the threshold value for triggering the alarm.  |
+------------------------+----------------+----------------------------------------------------------+
|                        | CurrentValue   | Specifies the value that triggered the alarm.            |
+------------------------+----------------+----------------------------------------------------------+

Impact on the System
--------------------

The Broker process is unable to perform read and write operations properly.

Possible Causes
---------------

The Broker process is experiencing excessive heap memory usage or improper memory allocation, leading to frequent Full GC events.

Handling Procedure
------------------

**Check the GC time of the Broker process.**

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and check details about the current alarm in the alarm list. Check the host name of the instance for which the alarm is generated in **Location**.
#. Choose **Cluster** > **Services** > **Kafka** > **Instances**, and click the role corresponding to the host name of the instance for which the alarm is generated. On the displayed page, click the drop-down list in the upper right corner of the chart area, and choose **Customize**. In the displayed window, choose **Process**, select **Broker Full GCs**, and click **OK**.
#. Check whether the number of Full GC events for the Broker process, collected per minute, exceeds the defined alarm thresholds: 9 events for a minor alarm and 12 events for a major alarm.

   -  If yes, go to :ref:`4 <alm-38019__en-us_topic_0000002487840008_en-us_topic_0000002476074585_li14463514014>`.
   -  If no, go to :ref:`7 <alm-38019__en-us_topic_0000002487840008_en-us_topic_0000002476074585_li1922084015466>`.

**Check the heap memory size configured for Kafka.**

4. .. _alm-38019__en-us_topic_0000002487840008_en-us_topic_0000002476074585_li14463514014:

   On the MRS Manager homepage, choose **Cluster** > **Services** > **Kafka**. Click **Configurations** and then **All Configurations**, and choose **Broker(Role)** > **Environment**. Increase the value of **-Xmx** in the **KAFKA_HEAP_OPTS** parameter.

   -  It is recommended that **-Xmx** and **-Xms** be set to the same value.
   -  It is recommended that you set the value of **KAFKA_HEAP_OPTS** to twice the value of **Heap Memory Usage of Kafka** based on Kafka heap memory data. To check the Kafka heap memory data, choose **Cluster** > **Services** > **Kafka** on the MRS Manager homepage, click **Instances**, and select the role corresponding to the host name of the instance for which the alarm is generated. Click the drop-down list in the upper right corner of the chart area and choose **Customize**. In the displayed window, choose **Process**, and select **Heap Memory Utilization of Kafka** to check its data.

5. Save the configuration and restart the Kafka service.

6. Check whether the alarm is cleared after about five minutes.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-38019__en-us_topic_0000002487840008_en-us_topic_0000002476074585_li1922084015466>`.

**Collect fault information.**

7.  .. _alm-38019__en-us_topic_0000002487840008_en-us_topic_0000002476074585_li1922084015466:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Expand the **Service** drop-down list, and select **Kafka** for the target cluster.

9.  Click the edit icon in the upper right corner, and select a time span starting 10 minutes before and ending 10 minutes after when the alarm was generated. Then, click **Download** to collect the logs.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
