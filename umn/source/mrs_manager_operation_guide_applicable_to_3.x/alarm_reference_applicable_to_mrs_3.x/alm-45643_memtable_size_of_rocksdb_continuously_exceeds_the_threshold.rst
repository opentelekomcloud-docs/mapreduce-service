:original_name: ALM-45643.html

.. _ALM-45643:

ALM-45643 MemTable Size of RocksDB Continuously Exceeds the Threshold
=====================================================================

This section applies to MRS 3.3.0 or later.

Alarm Description
-----------------

The system checks the RocksDB monitoring data of jobs at the user-specified alarm reporting interval (**metrics.reporter.alarm.job.alarm.rocksdb.metrics.duration**, 180s by default). This alarm is generated when the MemTable size of RocksDB for a job continuously exceeds the threshold (**metrics.reporter.alarm.job.alarm.rocksdb.get.micros.threshold**, 50000 microseconds by default). This alarm is cleared when the MemTable size of RocksDB for the job is less than or equal to the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45643    Minor          Yes
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

The write pressure of RocksDB is high.

Handling Procedure
------------------

**Check TaskManager logs for the write pressure of RocksDB and collect logs.**

#. Log in to FusionInsight Manager as a user who has the FlinkServer management permission.
#. Choose **O&M** > **Alarm** > **Alarms** > **ALM-45643 MemTable Size of RocksDB Continuously Exceeds the Threshold**, view **Location**, and obtain the name of the task for which the alarm is generated.
#. Choose **Cluster** > **Services** > **Yarn** and click the link next to **ResourceManager WebUI** to go to the native Yarn page.

4. Locate the abnormal task based on its name displayed in **Location**, search for and record the application ID of the job, and check whether the job logs are available on the Yarn page.


   .. figure:: /_static/images/en-us_image_0000001971808442.png
      :alt: **Figure 1** Application ID of a job

      **Figure 1** Application ID of a job

   -  If yes, go to :ref:`5 <alm-45643__li14941184217233>`.
   -  If no, go to :ref:`6 <alm-45643__li382131054218>`.

5. .. _alm-45643__li14941184217233:

   Click the application ID of the failed job to go to the job page.

   a. Click **Logs** in the **Logs** column to view JobManager logs.


      .. figure:: /_static/images/en-us_image_0000002008248449.png
         :alt: **Figure 2** Clicking Logs

         **Figure 2** Clicking Logs

   b. Click the ID in the **Attempt ID** column and click **Logs** in the **Logs** column to view and save TaskManager logs. Then go to :ref:`7 <alm-45643__li9907135324219>`.


      .. figure:: /_static/images/en-us_image_0000001971648702.png
         :alt: **Figure 3** Clicking the ID in the Attempt ID column

         **Figure 3** Clicking the ID in the Attempt ID column


      .. figure:: /_static/images/en-us_image_0000002008129021.png
         :alt: **Figure 4** Clicking Logs

         **Figure 4** Clicking Logs

      .. note::

         You can also log in to Manager as a user who has the management permission for the current Flink job. Choose **Cluster** > **Services** > **Flink**, and click the link next to **Flink WebUI**. On the displayed Flink web UI, click **Job Management**, click **More** in the **Operation** column, and select **Job Monitoring** to view TaskManager logs.

**If logs are unavailable on the Yarn page, download logs from HDFS.**

6. .. _alm-45643__li382131054218:

   On Manager, choose **Cluster** > **Services** > **HDFS**, click the link next to **NameNode WebUI** to go to the HDFS page, choose **Utilities** > **Browse the file system**, and download logs in the **/tmp/logs/**\ *Username*\ **/bucket-logs-tfile/**\ *Last four digits of the task application ID/Application ID of the task* directory.

**Check whether the write pressure of RocksDB is high.**

7. .. _alm-45643__li9907135324219:

   Check whether the value of **rocksdb.size-all-mem-tables** (unit: byte) in the TaskManager monitoring logs (keyword **RocksDBMetricPrint**) is greater than or equal to the total write buffer size (Total write buffer = **write_buffer_size** x **max_write_buffer_number**).

   -  If yes, adjust the values of the following custom parameters on the job development page of the Flink web UI, save the settings, and go to :ref:`8 <alm-45643__li490825314219>`.

      .. table:: **Table 1** Custom parameters

         +-----------------------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------+
         | Parameter                               | Default Value                                           | Description                                                                                       |
         +=========================================+=========================================================+===================================================================================================+
         | state.backend.rocksdb.writebuffer.count | -  **2**                                                | -  Number of buffers                                                                              |
         |                                         | -  **4**: enables **SPINNING_DISK_OPTIMIZED_HIGH_MEM**. | -  **2** to **10** are recommended. Adjust the value based on service requirements.               |
         +-----------------------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------+
         | state.backend.rocksdb.writebuffer.size  | **64MB**                                                | -  Buffer size                                                                                    |
         |                                         |                                                         | -  **64MB** to **256MB** are recommended.                                                         |
         +-----------------------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------+
         | state.backend.rocksdb.thread.num        | -  **2**                                                | -  Number of flush threads. Increase the number of threads to quickly flush memory data to disks. |
         |                                         | -  **4**: enables **SPINNING_DISK_OPTIMIZED_HIGH_MEM**. | -  When the number of threads is increased, the number of vCores also needs to be increased.      |
         |                                         |                                                         | -  **2** to **10** are recommended.                                                               |
         +-----------------------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------+

   -  If no, go to :ref:`9 <alm-45643__li390818530424>`.

8. .. _alm-45643__li490825314219:

   Restart the job and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-45643__li390818530424>`.

9. .. _alm-45643__li390818530424:

   Contact O&M personnel and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
