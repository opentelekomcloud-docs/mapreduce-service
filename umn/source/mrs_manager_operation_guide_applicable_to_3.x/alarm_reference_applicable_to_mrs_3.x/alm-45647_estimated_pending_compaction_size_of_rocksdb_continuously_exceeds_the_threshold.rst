:original_name: ALM-45647.html

.. _ALM-45647:

ALM-45647 Estimated Pending Compaction Size of RocksDB Continuously Exceeds the Threshold
=========================================================================================

This section applies to MRS 3.3.0 or later.

Alarm Description
-----------------

The system checks the RocksDB monitoring data of jobs at the user-specified alarm reporting interval (**metrics.reporter.alarm.job.alarm.rocksdb.metrics.duration**, 180s by default). This alarm is generated when the estimated pending compaction size of RocksDB for a job continuously exceeds the threshold. This alarm is cleared when the estimated pending compaction size of RocksDB for the job is less than or equal to the threshold.

The threshold of the estimated pending compaction size is the smaller value of the following two parameters:

-  **state.backend.rocksdb.soft-pending-compaction-bytes-limit**. The default value is **64GB**.
-  **state.backend.rocksdb.hard-pending-compaction-bytes-limit**. The default value is **256GB**.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45647    Minor          Yes
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

The estimated compaction data size of RocksDB is too large.

Handling Procedure
------------------

**Check TaskManager logs for the estimated compaction data size and collect logs.**

#. Log in to FusionInsight Manager as a user who has the FlinkServer management permission.
#. Choose **O&M** > **Alarm** > **Alarms** > **ALM-45647 Estimated Pending Compaction Size of RocksDB Continuously Exceeds the Threshold**, view **Location**, and obtain the name of the task for which the alarm is generated.
#. Choose **Cluster** > **Services** > **Yarn** and click the link next to **ResourceManager WebUI** to go to the native Yarn page.

4. Locate the abnormal task based on its name displayed in **Location**, search for and record the application ID of the job, and check whether the job logs are available on the Yarn page.


   .. figure:: /_static/images/en-us_image_0000001971808574.png
      :alt: **Figure 1** Application ID of a job

      **Figure 1** Application ID of a job

   -  If yes, go to :ref:`5 <alm-45647__li192082249500>`.
   -  If no, go to :ref:`6 <alm-45647__li15924173318501>`.

5. .. _alm-45647__li192082249500:

   Click the application ID of the failed job to go to the job page.

   a. Click **Logs** in the **Logs** column to view JobManager logs.


      .. figure:: /_static/images/en-us_image_0000001971648822.png
         :alt: **Figure 2** Clicking Logs

         **Figure 2** Clicking Logs

   b. Click the ID in the **Attempt ID** column and click **Logs** in the **Logs** column to view and save TaskManager logs. Then go to :ref:`7 <alm-45647__li1157118941310>`.


      .. figure:: /_static/images/en-us_image_0000002008129137.png
         :alt: **Figure 3** Clicking the ID in the Attempt ID column

         **Figure 3** Clicking the ID in the Attempt ID column


      .. figure:: /_static/images/en-us_image_0000001971808582.png
         :alt: **Figure 4** Clicking Logs

         **Figure 4** Clicking Logs

      .. note::

         You can also log in to Manager as a user who has the management permission for the current Flink job. Choose **Cluster** > **Services** > **Flink**, and click the link next to **Flink WebUI**. On the displayed Flink web UI, click **Job Management**, click **More** in the **Operation** column, and select **Job Monitoring** to view TaskManager logs.

**If logs are unavailable on the Yarn page, download logs from HDFS.**

6. .. _alm-45647__li15924173318501:

   On Manager, choose **Cluster** > **Services** > **HDFS**, click the link next to **NameNode WebUI** to go to the HDFS page, choose **Utilities** > **Browse the file system**, and download logs in the **/tmp/logs/**\ *Username*\ **/bucket-logs-tfile/**\ *Last four digits of the task application ID/Application ID of the task* directory.

**Check whether the estimated compaction data size of RocksDB is too large.**

7. .. _alm-45647__li1157118941310:

   Check whether the value of **rocksdb.estimate-pending-compaction-bytes** (unit: byte) in TaskManager monitoring logs (keyword **RocksDBMetricPrint**) is greater than or equal to the **soft/hard-pending-compaction** size (values of **state.backend.rocksdb.soft-pending-compaction-bytes-limit** and **state.backend.rocksdb.hard-pending-compaction-bytes-limit**).

   -  If yes, adjust the values of the following custom parameters on the job development page of the Flink web UI, save the settings, and go to :ref:`8 <alm-45647__li4736164255016>`.

      .. table:: **Table 1** Custom parameters

         +-----------------------------------------------------------+-----------------------+------------------------------------------------------------------------------------------+
         | Parameter                                                 | Default Value         | Description                                                                              |
         +===========================================================+=======================+==========================================================================================+
         | state.backend.rocksdb.soft-pending-compaction-bytes-limit | 64GB                  | -  When the pending compaction size exceeds the threshold, the write traffic is limited. |
         |                                                           |                       | -  **64GB** to **512GB** are recommended.                                                |
         +-----------------------------------------------------------+-----------------------+------------------------------------------------------------------------------------------+
         | state.backend.rocksdb.hard-pending-compaction-bytes-limit | 256GB                 | -  When the pending compaction size exceeds the threshold, write operations are stopped. |
         |                                                           |                       | -  **64GB** to **512GB** are recommended.                                                |
         +-----------------------------------------------------------+-----------------------+------------------------------------------------------------------------------------------+

   -  If no, go to :ref:`9 <alm-45647__li573684212503>`.

8. .. _alm-45647__li4736164255016:

   Restart the job and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-45647__li573684212503>`.

9. .. _alm-45647__li573684212503:

   Contact O&M personnel and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
