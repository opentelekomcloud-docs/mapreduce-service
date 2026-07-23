:original_name: ALM-50842.html

.. _ALM-50842:

ALM-50842 Percentage of Concurrent StoreWorker Writes Exceeds the Threshold
===========================================================================

Alarm Description
-----------------

The system checks the percentage of concurrent writes on StoreWorker instances every 30 seconds. This alarm is generated when the percentage exceeds the threshold.

This alarm is cleared when the percentage of concurrent writes on StoreWorker instances falls below the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50842    Minor          Yes
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

Too many partitions on a node are executing shuffle writes. As a result, the server efficiency decreases.

Possible Causes
---------------

-  The load tilt is too large, and the load pressure is too high.
-  The number of nodes is too small, causing high pressure on each node.

Handling Procedure
------------------

**Check the percentage of nodes for which the alarm is generated.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the alarm list, view the role name and obtain the IP address of the instance in **Location** of the alarm whose ID is **50842**.
#. Choose **Cluster** > **Services** > **MemArtsStore** > **Instances**, and calculate the percentage of the StoreWorker instances for which the alarm is generated in all StoreWorker instances.

   -  If the percentage is greater than or equal to 5%, go to :ref:`3 <alm-50842__en-us_topic_0000002520347237_en-us_topic_0000002192665181_li849319546319>`.
   -  If the percentage is less than 5%, go to :ref:`6 <alm-50842__en-us_topic_0000002520347237_en-us_topic_0000002192665181_li1028611121143>`.

**Add nodes.**

3. .. _alm-50842__en-us_topic_0000002520347237_en-us_topic_0000002192665181_li849319546319:

   Choose **Cluster** > **Services** > **MemArtsStore** and click **Instances**.

4. Click **Add Instance** to add StoreWorker instances.

5. Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-50842__en-us_topic_0000002520347237_en-us_topic_0000002192665181_li10360155511379>`.

**Change the Spark parameter value to the native setting.**

6. .. _alm-50842__en-us_topic_0000002520347237_en-us_topic_0000002192665181_li1028611121143:

   Log in to the Spark client node, go to the **/opt/client/Spark/spark/conf** directory, change the value of **spark.shuffle.manager** in the **spark-defaults.conf** file to **sort**, save the modification, exit, and run the task again.

   .. code-block::

      spark.shuffle.manager = sort

7. Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-50842__en-us_topic_0000002520347237_en-us_topic_0000002192665181_li10360155511379>`.

**Collect fault information.**

8.  .. _alm-50842__en-us_topic_0000002520347237_en-us_topic_0000002192665181_li10360155511379:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, and select **MemArtsStore** for the target cluster.

10. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact O&M engineers and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
