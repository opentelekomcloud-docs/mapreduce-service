:original_name: ALM-16053.html

.. _ALM-16053:

ALM-16053 Average HQL Submission Time of Hive in the Last 5 Minutes Exceeds the Threshold
=========================================================================================

Alarm Description
-----------------

The system periodically checks the average HQL submission time, which is the time for calling the MapReduce/Spark/Tez APIs to submit Yarn jobs, including the time for uploading dependent temporary JAR packages and splitting files. This alarm is generated when the average HQL submission time exceeds the threshold.

This alarm is cleared when the HQL submission time falls below the threshold.

This alarm applies to MRS 3.5.0 or later.

Alarm Attributes
----------------

+-----------------------+-------------------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                            | Auto Cleared          |
+=======================+===========================================+=======================+
| 16053                 | Critical (default threshold: 240 seconds) | Yes                   |
|                       |                                           |                       |
|                       | Major (default threshold: 120 seconds)    |                       |
+-----------------------+-------------------------------------------+-----------------------+

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

If this alarm is generated, the average HQL submission time in the last 5 minutes exceeds the threshold. As a result, the HQL running time is prolonged. Errors may occur in Hive On Spark jobs.

Possible Causes
---------------

The HiveServer GC time is too long or the HDFS NameNode/Router RPC latency is too long.

Handling Procedure
------------------

**Check whether the GC time of HiveServer is too long.**

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and check whether alarm **Heap Memory Usage of the Hive Process Exceeds the Threshold** exists in the alarm list.

   -  If yes, go to :ref:`2 <alm-16053__en-us_topic_0000001982875596_li12822145813344>`.
   -  If no, go to :ref:`4 <alm-16053__en-us_topic_0000001982875596_li7821358163411>`.

#. .. _alm-16053__en-us_topic_0000001982875596_li12822145813344:

   Rectify the fault by following the handling procedure of **ALM-16005 Heap Memory Usage of the Hive Process Exceeds the Threshold**.

#. Check whether the alarm is cleared in the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-16053__en-us_topic_0000001982875596_li7821358163411>`.

**Check whether the HDFS RPC latency is too long.**

4. .. _alm-16053__en-us_topic_0000001982875596_li7821358163411:

   Check whether alarm **Average NameNode RPC Processing Time Exceeds the Threshold** exists in the alarm list.

   -  If yes, go to :ref:`5 <alm-16053__en-us_topic_0000001982875596_li1882125813417>`.
   -  If no, go to :ref:`7 <alm-16053__en-us_topic_0000001982875596_li598725474015>`.

5. .. _alm-16053__en-us_topic_0000001982875596_li1882125813417:

   Rectify the fault by following the handling procedure of **ALM-14021 Average NameNode RPC Processing Time Exceeds the Threshold**.

6. Check whether the alarm is cleared in the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-16053__en-us_topic_0000001982875596_li598725474015>`.

**Collect fault information.**

7.  .. _alm-16053__en-us_topic_0000001982875596_li598725474015:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Expand the **Service** drop-down list, and select **Hive** for the target cluster.

9.  Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. On MRS Manager, choose **Cluster** > **Services** > **Hive**. On the displayed **Dashboard** page, click **More** and select **Collect Stack Information**. On the displayed page, set the following parameters:

    -  Select **HiveServer** for the role where you want to collect data.
    -  Select **jstack** and **Enable continuous collection of jstack and jmap -histo information**.
    -  Set the collection interval to 10 seconds and the duration to 2 minutes.

11. Click **OK**. After the collection is complete, click **Download**.

12. Contact O&M personnel and provide the collected logs and stack information.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
