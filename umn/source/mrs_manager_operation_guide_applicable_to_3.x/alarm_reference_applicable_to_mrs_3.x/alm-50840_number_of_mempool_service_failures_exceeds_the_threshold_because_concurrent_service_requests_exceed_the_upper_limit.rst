:original_name: ALM-50840.html

.. _ALM-50840:

ALM-50840 Number of Mempool Service Failures Exceeds the Threshold Because Concurrent Service Requests Exceed the Upper Limit
=============================================================================================================================

Alarm Description
-----------------

The system checks the number of Mempool service failures due to concurrent service requests exceeding the upper limit every 30 seconds. This alarm is generated when the number of Mempool service failures exceeds the threshold.

This alarm is cleared when the number of Mempool service failures falls below the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50840    Minor          Yes
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

The server efficiency decreases, and tasks may fail.

Possible Causes
---------------

-  The load tilt is too large, and the load pressure is too high.
-  The upper limit for concurrent Mempool service requests is too small.

Handling Procedure
------------------

**Check the pool I/O time.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the alarm list, view the role name and obtain the IP address of the instance in **Location** of the alarm whose ID is **50840**.

#. Choose **Cluster** > **Services** > **MemArtsStore** > **Instances**, click the StoreWorker instance for which the alarm is generated, and click the **Chart** tab of the instance.

   Select **KV** from **Chart Category** on the left, observe the KV SDK latency of the StoreWorker process, and check whether the latency decreases and the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-50840__en-us_topic_0000002488107412_en-us_topic_0000002192819541_li887113479397>`.

**Change the upper limit for concurrent Mempool service requests.**

3. .. _alm-50840__en-us_topic_0000002488107412_en-us_topic_0000002192819541_li887113479397:

   Log in to MRS Manager, navigate to the MemArtsStore service, choose **Configurations** > **All Configurations**, and search for **total_server_req_concurrent**.

4. Locate the value of **total_server_req_concurrent** for **MemArtsStore** > **StoreWorker**.

   .. note::

      **total_server_req_concurrent** indicates the upper limit for a single Mempool node to process concurrent service requests. This alarm is generated when the number of service failures exceeds the threshold because the concurrent requests exceed this upper limit within the monitoring period (30 seconds).

5. Check whether this value is too small based on the actual concurrent service request processing capability of Mempool. If it is too small, increase it and click **Save**. Then the system modifies the configuration of all nodes synchronously.

6. Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-50840__en-us_topic_0000002488107412_en-us_topic_0000002192819541_li10360155511379>`.

**Collect fault information.**

7.  .. _alm-50840__en-us_topic_0000002488107412_en-us_topic_0000002192819541_li10360155511379:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Expand the **Service** drop-down list, and select **MemArtsStore** for the target cluster.

9.  Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact O&M engineers and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
