:original_name: ALM-45644.html

.. _ALM-45644:

ALM-45644 Number of SST Files at Level 0 of RocksDB Continuously Exceeds the Threshold
======================================================================================

This section applies to MRS 3.3.0 or later.

Alarm Description
-----------------

The system checks the RocksDB monitoring data of jobs at the user-specified alarm reporting interval (**metrics.reporter.alarm.job.alarm.rocksdb.metrics.duration**, 180s by default). This alarm is generated when the number of SST files at level 0 of RocksDB for a job continuously exceeds the threshold (**state.backend.rocksdb.level0_slowdown_writes_trigger**, 20 by default). This alarm is cleared when the number of SST files at level 0 of RocksDB for the job is less than or equal to the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45644    Minor          Yes
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

Possible causes are as follows:

-  The compaction pressure of RocksDB is too high, and **ALM-45646 Pending Compaction Size of RocksDB Continuously Exceeds the Threshold** and **ALM-45647 Estimated Pending Compaction Size of RocksDB Continuously Exceeds the Threshold** are generated.
-  There are too many SST files at level 0.

Handling Procedure
------------------

**Check whether the compaction pressure of RocksDB is too high and ALM-45646 is generated.**

#. On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**.

#. In the alarm list, check whether **ALM-45646 Pending Compaction Size of RocksDB Continuously Exceeds the Threshold** exists.

   -  If yes, go to :ref:`3 <alm-45644__li125749379316>`.
   -  If no, go to :ref:`5 <alm-45644__li95737371433>`.

#. .. _alm-45644__li125749379316:

   Handle the alarm by following the instructions provided in section **ALM-45646 Pending Compaction Size of RocksDB Continuously Exceeds the Threshold**.

#. After ALM-45646 is cleared, wait a few minutes and check whether this alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-45644__li95737371433>`.

**Check whether the compaction pressure of RocksDB is too high and ALM-45647 is generated.**

5. .. _alm-45644__li95737371433:

   In the alarm list, check whether **ALM-45647 Estimated Pending Compaction Size of RocksDB Continuously Exceeds the Threshold** exists.

   -  If yes, go to :ref:`6 <alm-45644__li1857319375312>`.
   -  If no, go to :ref:`8 <alm-45644__li168007412119>`.

6. .. _alm-45644__li1857319375312:

   Handle the alarm by following the instructions provided in section **ALM-45647 Estimated Pending Compaction Size of RocksDB Continuously Exceeds the Threshold**.

7. After ALM-45647 is cleared, wait a few minutes and check whether this alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-45644__li168007412119>`.

**Check TaskManager logs for the number of SST files at level 0 and collect logs.**

8.  .. _alm-45644__li168007412119:

    Log in to FusionInsight Manager as a user who has the FlinkServer management permission.

9.  Choose **O&M** > **Alarm** > **Alarms** > **ALM-45644 Number of SST Files at Level 0 of RocksDB Continuously Exceeds the Threshold**, view **Location**, and obtain the name of the task for which the alarm is generated.

10. Choose **Cluster** > **Services** > **Yarn** and click the link next to **ResourceManager WebUI** to go to the native Yarn page.

11. Locate the abnormal task based on its name displayed in **Location**, search for and record the application ID of the job, and check whether the job logs are available on the Yarn page.


    .. figure:: /_static/images/en-us_image_0000001971808474.png
       :alt: **Figure 1** Application ID of a job

       **Figure 1** Application ID of a job

    -  If yes, go to :ref:`12 <alm-45644__li14941184217233>`.
    -  If no, go to :ref:`13 <alm-45644__li0378678118>`.

12. .. _alm-45644__li14941184217233:

    Click the application ID of the failed job to go to the job page.

    a. Click **Logs** in the **Logs** column to view JobManager logs.


       .. figure:: /_static/images/en-us_image_0000002008248489.png
          :alt: **Figure 2** Clicking Logs

          **Figure 2** Clicking Logs

    b. Click the ID in the **Attempt ID** column and click **Logs** in the **Logs** column to view and save TaskManager logs. Then go to :ref:`14 <alm-45644__li1924461021119>`.


       .. figure:: /_static/images/en-us_image_0000001971648738.png
          :alt: **Figure 3** Clicking the ID in the Attempt ID column

          **Figure 3** Clicking the ID in the Attempt ID column


       .. figure:: /_static/images/en-us_image_0000002008129057.png
          :alt: **Figure 4** Clicking Logs

          **Figure 4** Clicking Logs

       .. note::

          You can also log in to Manager as a user who has the management permission for the current Flink job. Choose **Cluster** > **Services** > **Flink**, and click the link next to **Flink WebUI**. On the displayed Flink web UI, click **Job Management**, click **More** in the **Operation** column, and select **Job Monitoring** to view TaskManager logs.

**If logs are unavailable on the Yarn page, download logs from HDFS.**

13. .. _alm-45644__li0378678118:

    On Manager, choose **Cluster** > **Services** > **HDFS**, click the link next to **NameNode WebUI** to go to the HDFS page, choose **Utilities** > **Browse the file system**, and download logs in the **/tmp/logs/**\ *Username*\ **/bucket-logs-tfile/**\ *Last four digits of the task application ID/Application ID of the task* directory.

**Check whether the number of SST files at level 0 is too large.**

14. .. _alm-45644__li1924461021119:

    Check whether the value of **rocksdb.num-files-at-level0** in TaskManager monitoring logs (keyword **RocksDBMetricPrint**) is greater than or equal to the value of **state.backend.rocksdb.level0_slowdown_writes_trigger** or **state.backend.rocksdb.level0_stop_writes_trigger**.

    -  If yes, adjust the values of the following custom parameters on the job development page of the Flink web UI, save the settings, and go to :ref:`15 <alm-45644__li82441810181117>`.

       .. table:: **Table 1** Custom parameters

          +------------------------------------------------------+-----------------------+---------------------------------------------------------+
          | Parameter                                            | Default Value         | Description                                             |
          +======================================================+=======================+=========================================================+
          | state.backend.rocksdb.level0_slowdown_writes_trigger | 20                    | -  Number of files that trigger slowdown at level 0     |
          |                                                      |                       | -  **20** to **30** are recommended.                    |
          +------------------------------------------------------+-----------------------+---------------------------------------------------------+
          | state.backend.rocksdb.level0_stop_writes_trigger     | 36                    | -  Maximum number of files that trigger stop at level 0 |
          |                                                      |                       | -  **36** to **46** are recommended.                    |
          +------------------------------------------------------+-----------------------+---------------------------------------------------------+

    -  If no, go to :ref:`16 <alm-45644__li6245710111114>`.

15. .. _alm-45644__li82441810181117:

    Restart the job and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`16 <alm-45644__li6245710111114>`.

16. .. _alm-45644__li6245710111114:

    Contact O&M personnel and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
