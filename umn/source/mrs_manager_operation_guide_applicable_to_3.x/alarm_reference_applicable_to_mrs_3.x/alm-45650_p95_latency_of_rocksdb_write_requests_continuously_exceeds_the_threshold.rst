:original_name: ALM-45650.html

.. _ALM-45650:

ALM-45650 P95 Latency of RocksDB Write Requests Continuously Exceeds the Threshold
==================================================================================

This section applies to MRS 3.3.0 or later.

Alarm Description
-----------------

The system checks the RocksDB monitoring data of jobs at the user-specified alarm reporting interval (**metrics.reporter.alarm.job.alarm.rocksdb.metrics.duration**, 180s by default). This alarm is generated when the P95 latency of RocksDB write requests exceeds the threshold (**metrics.reporter.alarm.job.alarm.rocksdb.write.micros.threshold**, 50000 microseconds by default). This alarm is cleared when the P95 latency of RocksDB write requests is less than or equal to the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45650    Minor          Yes
======== ============== ============

Alarm Parameters
----------------

+-----------------+-------------------------------------------------------------------------+
| Parameter       | Description                                                             |
+=================+=========================================================================+
| Source          | Specifies the cluster for which the alarm is generated.                 |
+-----------------+-------------------------------------------------------------------------+
| ServiceName     | Specifies the service for which the alarm is generated.                 |
+-----------------+-------------------------------------------------------------------------+
| ApplicationName | Specifies the name of the application for which the alarm is generated. |
+-----------------+-------------------------------------------------------------------------+
| RoleName        | Specifies the role for which the alarm is generated.                    |
+-----------------+-------------------------------------------------------------------------+
| JobName         | Specifies the job for which the alarm is generated.                     |
+-----------------+-------------------------------------------------------------------------+

Impact on the System
--------------------

This alarm has no adverse impact on the system.

Possible Causes
---------------

The possible causes are as follows:

-  There are too many MemTables. As a result, write traffic is limited or write stops, and **ALM-45643 MemTable Size of RocksDB Continuously Exceeds the Threshold** is generated.

-  There are too many SST files at level 0, and **ALM-45644 Number of SST Files at Level 0 of RocksDB Continuously Exceeds the Threshold** is generated.

-  The estimated compaction size exceeds the threshold, and **ALM-45647 Estimated Pending Compaction Size of RocksDB Continuously Exceeds the Threshold** is generated.

Handling Procedure
------------------

**Check whether write traffic limiting or write stop is caused due to too many MemTables.**

#. On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**.

#. In the alarm list, check whether **ALM-45643 MemTable Size of RocksDB Continuously Exceeds the Threshold** exists.

   -  If yes, go to :ref:`3 <alm-45650__li6823133191818>`.
   -  If no, go to :ref:`5 <alm-45650__li88241531181819>`.

#. .. _alm-45650__li6823133191818:

   Handle the alarm by following the instructions provided in section **ALM-45643 MemTable Size of RocksDB Continuously Exceeds the Threshold**.

#. After ALM-45643 is cleared, wait a few minutes and check whether this alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-45650__li88241531181819>`.

**Check whether the number of SST files at level 0 is too large.**

5. .. _alm-45650__li88241531181819:

   On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**.

6. In the alarm list, check whether **ALM-45644 Number of SST Files at Level 0 of RocksDB Continuously Exceeds the Threshold** exists.

   -  If yes, go to :ref:`7 <alm-45650__li1982483112189>`.
   -  If no, go to :ref:`9 <alm-45650__li1485215516483>`.

7. .. _alm-45650__li1982483112189:

   Handle the alarm by following the instructions provided in section **ALM-45644 Number of SST Files at Level 0 of RocksDB Continuously Exceeds the Threshold**.

8. After ALM-45644 is cleared, wait a few minutes and check whether this alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-45650__li1485215516483>`.

**Check whether the estimated compaction size exceeds the threshold.**

9.  .. _alm-45650__li1485215516483:

    In the alarm list, check whether **ALM-45647 Estimated Pending Compaction Size of RocksDB Continuously Exceeds the Threshold** exists.

    -  If yes, go to :ref:`10 <alm-45650__li1285312554818>`.
    -  If no, go to :ref:`12 <alm-45650__li1826072651812>`.

10. .. _alm-45650__li1285312554818:

    Handle the alarm by following the instructions provided in section **ALM-45647 Estimated Pending Compaction Size of RocksDB Continuously Exceeds the Threshold**.

11. After ALM-45647 is cleared, wait a few minutes and check whether this alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-45650__li1826072651812>`.

**Collect fault information.**

12. .. _alm-45650__li1826072651812:

    Log in to FusionInsight Manager as a user who has the FlinkServer management permission.

13. Choose **O&M** > **Alarm** > **Alarms** > **ALM-45650 P95 Latency of RocksDB Write Requests Continuously Exceeds the Threshold**, view **Location**, and obtain the name of the task for which the alarm is generated.

14. Choose **Cluster** > **Services** > **Yarn** and click the link next to **ResourceManager WebUI** to go to the native Yarn page.

15. Locate the abnormal task based on its name displayed in **Location**, search for and record the application ID of the job, and check whether the job logs are available on the Yarn page.


    .. figure:: /_static/images/en-us_image_0000002008248601.png
       :alt: **Figure 1** Application ID of a job

       **Figure 1** Application ID of a job

    -  If yes, go to :ref:`16 <alm-45650__li14941184217233>`.
    -  If no, go to :ref:`18 <alm-45650__li42141433171631>`.

16. .. _alm-45650__li14941184217233:

    Click the application ID of the failed job to go to the job page.

    a. Click **Logs** in the **Logs** column to view JobManager logs.


       .. figure:: /_static/images/en-us_image_0000001971648850.png
          :alt: **Figure 2** Clicking Logs

          **Figure 2** Clicking Logs

    b. Click the ID in the **Attempt ID** column and click **Logs** in the **Logs** column to view and save TaskManager logs.


       .. figure:: /_static/images/en-us_image_0000002008129157.png
          :alt: **Figure 3** Clicking the ID in the Attempt ID column

          **Figure 3** Clicking the ID in the Attempt ID column


       .. figure:: /_static/images/en-us_image_0000001971808618.png
          :alt: **Figure 4** Clicking Logs

          **Figure 4** Clicking Logs

       .. note::

          You can also log in to Manager as a user who has the FlinkServer management permission. Choose **Cluster** > **Services** > **Flink**, and click the link next to **Flink WebUI**. On the displayed Flink web UI, click **Job Management**, click **More** in the **Operation** column, and select **Job Monitoring** to view TaskManager logs.

17. View the job logs to rectify the fault, or contact the O&M personnel and send the collected fault logs. No further action is required.

**If logs are unavailable on the Yarn page, download logs from HDFS.**

18. .. _alm-45650__li42141433171631:

    On Manager, choose **Cluster** > **Services** > **HDFS**, click the link next to **NameNode WebUI** to go to the HDFS page, choose **Utilities** > **Browse the file system**, and download logs in the **/tmp/logs/**\ *Username*\ **/bucket-logs-tfile/**\ *Last four digits of the task application ID/Application ID of the task* directory.

19. View the logs of the failed job to rectify the fault, or contact the O&M personnel and send the collected fault logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
