:original_name: ALM-50832.html

.. _ALM-50832:

ALM-50832 Number of StoreMaster Failures to Create Partitions Exceeds the Threshold
===================================================================================

Alarm Description
-----------------

The system checks the number of StoreMaster failures to create partitions every 30 seconds. This alarm is generated when the number exceeds the threshold.

This alarm is cleared when the number of failures falls below the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50832    Critical       Yes
======== ============== ============

Alarm Parameters
----------------

+-------------+--------------------------------------------------------------------+
| Parameter   | Description                                                        |
+=============+====================================================================+
| Source      | Specifies the cluster or system for which the alarm was generated. |
+-------------+--------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm was generated.           |
+-------------+--------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm was generated.              |
+-------------+--------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm was generated.              |
+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

The corresponding Spark task fails.

Possible Causes
---------------

Access to ZooKeeper is abnormal.

Handling Procedure
------------------

**Check the Spark client configurations.**

#. Log in to the node where the client is installed as the client installation user.

#. Go to the node directory where the Spark client is installed.

   **cd** *Client installation directory*\ **/Spark/spark/conf**

#. Check the **spark-defaults.conf** configuration file. Check whether the IP address and port number of the ZooKeeper configuration parameter **spark.rss.zookeeper.address** are correct.

#. Run the task again and check whether it is normal.

   -  If yes, go to :ref:`5 <alm-50832__en-us_topic_0000002488107410_en-us_topic_0000002192819537_li150034614718>`.
   -  If no, go to :ref:`6 <alm-50832__en-us_topic_0000002488107410_en-us_topic_0000002192819537_li10360155511379>`.

#. .. _alm-50832__en-us_topic_0000002488107410_en-us_topic_0000002192819537_li150034614718:

   Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-50832__en-us_topic_0000002488107410_en-us_topic_0000002192819537_li10360155511379>`.

**Collect fault information.**

6. .. _alm-50832__en-us_topic_0000002488107410_en-us_topic_0000002192819537_li10360155511379:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7. Expand the **Service** drop-down list, and select **MemArtsStore** for the target cluster.

8. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M engineers and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
