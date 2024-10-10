:original_name: ALM-45649.html

.. _ALM-45649:

ALM-45649 P95 Latency of RocksDB Get Requests Continuously Exceeds the Threshold
================================================================================

This section applies to MRS 3.3.0 or later.

Alarm Description
-----------------

The system checks the RocksDB monitoring data of jobs at the user-specified alarm reporting interval (**metrics.reporter.alarm.job.alarm.rocksdb.metrics.duration**, 180s by default). This alarm is generated when the P95 latency of RocksDB Get requests exceeds the threshold (**metrics.reporter.alarm.job.alarm.rocksdb.get.micros.threshold**, 50000 microseconds by default). This alarm is cleared when the P95 latency of RocksDB Get requests is less than or equal to the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45649    Minor          Yes
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

-  There are too many SST files at level 0, causing slow queries. In addition, **ALM-45644 Number of SST Files at Level 0 of RocksDB Continuously Exceeds the Threshold** is generated.
-  The cache hit ratio is lower than 60%, causing frequent swap-ins and swap-outs of the block cache.

Handling Procedure
------------------

**Check whether the number of SST files at level 0 is too large.**

#. On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**.

#. In the alarm list, check whether **ALM-45644 Number of SST Files at Level 0 of RocksDB Continuously Exceeds the Threshold** exists.

   -  If yes, go to :ref:`3 <alm-45649__li19933375403>`.
   -  If no, go to :ref:`5 <alm-45649__li2091153718402>`.

#. .. _alm-45649__li19933375403:

   Handle the alarm by following the instructions provided in section **ALM-45644 Number of SST Files at Level 0 of RocksDB Continuously Exceeds the Threshold**.

#. After ALM-45644 is cleared, wait a few minutes and check whether this alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-45649__li2091153718402>`.

**Check the cache hit ratio in TaskManager logs and collect logs.**

5. .. _alm-45649__li2091153718402:

   Log in to FusionInsight Manager as a user who has the FlinkServer management permission.

6. Choose **O&M** > **Alarm** > **Alarms** > **ALM-45649 P95 Latency of RocksDB Get Requests Continuously Exceeds the Threshold**, view **Location**, and obtain the name of the task for which the alarm is generated.

7. Choose **Cluster** > **Services** > **Yarn** and click the link next to **ResourceManager WebUI** to go to the native Yarn page.

8. Locate the abnormal task based on its name displayed in **Location**, search for and record the application ID of the job, and check whether the job logs are available on the Yarn page.


   .. figure:: /_static/images/en-us_image_0000002008248597.png
      :alt: **Figure 1** Application ID of a job

      **Figure 1** Application ID of a job

   -  If yes, go to :ref:`9 <alm-45649__li192082249500>`.
   -  If no, go to :ref:`10 <alm-45649__li15924173318501>`.

9. .. _alm-45649__li192082249500:

   Click the application ID of the failed job to go to the job page.

   a. Click **Logs** in the **Logs** column to view JobManager logs.


      .. figure:: /_static/images/en-us_image_0000001971648838.png
         :alt: **Figure 2** Clicking Logs

         **Figure 2** Clicking Logs

   b. Click the ID in the **Attempt ID** column and click **Logs** in the **Logs** column to view and save TaskManager logs. Then go to :ref:`11 <alm-45649__li133768138478>`.


      .. figure:: /_static/images/en-us_image_0000002008129145.png
         :alt: **Figure 3** Clicking the ID in the Attempt ID column

         **Figure 3** Clicking the ID in the Attempt ID column


      .. figure:: /_static/images/en-us_image_0000001971808602.png
         :alt: **Figure 4** Clicking Logs

         **Figure 4** Clicking Logs

      .. note::

         You can also log in to Manager as a user who has the management permission for the current Flink job. Choose **Cluster** > **Services** > **Flink**, and click the link next to **Flink WebUI**. On the displayed Flink web UI, click **Job Management**, click **More** in the **Operation** column, and select **Job Monitoring** to view TaskManager logs.

**If logs are unavailable on the Yarn page, download logs from HDFS.**

10. .. _alm-45649__li15924173318501:

    On Manager, choose **Cluster** > **Services** > **HDFS**, click the link next to **NameNode WebUI** to go to the HDFS page, choose **Utilities** > **Browse the file system**, and download logs in the **/tmp/logs/**\ *Username*\ **/bucket-logs-tfile/**\ *Last four digits of the task application ID/Application ID of the task* directory.

**Check whether the cache hit ratio is too low.**

11. .. _alm-45649__li133768138478:

    Check the values of **rocksdb.block.cache.hit** (cache hit) and **rocksdb.block.cache.miss** (cache miss) in TaskManager monitoring logs (keyword **RocksDBMetricPrint**). Calculate the hit ratio using the following formula and check whether it is less than 60%:

    **rocksdb.block.cache.hit/(rocksdb.block.cache.hit+rocksdb.block.cache.miss)**

    -  If yes, adjust the values of the following custom parameters on the job development page of the Flink web UI, save the settings, and go to :ref:`12 <alm-45649__li4736164255016>`.

       .. table:: **Table 1** Custom parameters

          +----------------------------------------+-------------------------------------------------------------+----------------------------------------------------------------------------------------------------+
          | Parameter                              | Default Value                                               | Description                                                                                        |
          +========================================+=============================================================+====================================================================================================+
          | state.backend.rocksdb.block.cache-size | -  **8MB**                                                  | -  Cache size                                                                                      |
          |                                        | -  **256MB**: enables **SPINNING_DISK_OPTIMIZED_HIGH_MEM**. | -  **8MB** to **1GB** are recommended.                                                             |
          +----------------------------------------+-------------------------------------------------------------+----------------------------------------------------------------------------------------------------+
          | state.backend.rocksdb.block.blocksize  | -  **4KB**                                                  | -  Block size                                                                                      |
          |                                        | -  **128KB**: enables **SPINNING_DISK_OPTIMIZED_HIGH_MEM**. | -  **4KB** to **256KB** are recommended.                                                           |
          +----------------------------------------+-------------------------------------------------------------+----------------------------------------------------------------------------------------------------+
          | state.backend.rocksdb.use-bloom-filter | **false**                                                   | -  Whether to speed up indexing. If it is **true**, each new SST file will contain a Bloom filter. |
          |                                        |                                                             | -  **true** is recommended.                                                                        |
          +----------------------------------------+-------------------------------------------------------------+----------------------------------------------------------------------------------------------------+

    -  If no, go to :ref:`13 <alm-45649__li573684212503>`.

12. .. _alm-45649__li4736164255016:

    Restart the job and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`13 <alm-45649__li573684212503>`.

13. .. _alm-45649__li573684212503:

    Contact O&M personnel and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
