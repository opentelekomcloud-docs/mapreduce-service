:original_name: mrs_01_24170.html

.. _mrs_01_24170:

Configuring Event Log Rollover
==============================

Scenario
--------

When the event log mode is enabled for Spark, that is, **spark.eventLog.enabled** is set to **true**, events are written to a configured log file to record the program running process. If a program, for example JDBCServer or Spark Streaming, runs for a long period of time and has run many jobs and tasks during this period, many events are recorded in the log file, significantly increasing the file size.

When log rollover is enabled, metadata events are written into the log file and job events are written into a new log file (whether a job event is written to the new log file depends on the file size). Metadata events include EnviromentUpdate, BlockManagerAdded, BlockManagerRemoved, UnpersistRDD, ExecutorAdded, ExecutorRemoved, MetricsUpdate, ApplicationStart, ApplicationEnd, and LogStart. Job events include StageSubmitted, StageCompleted, TaskResubmit, TaskStart, TaskEnd, TaskGettingResult, JobStart, and JobEnd. For Spark SQL applications, job events also include ExecutionStart and ExecutionEnd.

The UI for the HistoryServer service of Spark is obtained by reading and parsing these log files. The memory size is preset before the HistoryServer process starts. Therefore, when the size of log files is large, loading and parsing these files may cause problems such as insufficient memory and driver GC.

To load large log files in small memory mode, you need to enable log rollover for large applications. Generally, it is recommended that this function be enabled for long-running applications.

Parameters
----------

Log in to FusionInsight Manager, choose **Cluster** > **Services** > **Spark2x** > **Configurations**, click **All Configurations**, and search for the following parameters.

+----------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
| Parameter                              | Description                                                                                                                                                                                 | Default Value |
+========================================+=============================================================================================================================================================================================+===============+
| spark.eventLog.rolling.enabled         | Whether to enable rollover for event log files. If this parameter is set to **true**, the size of each event log file is reduced to the configured size.                                    | true          |
+----------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
| spark.eventLog.rolling.maxFileSize     | Maximum size of the event log file to be rolled over when **spark.eventlog.rolling.enabled** is set to **true**.                                                                            | 128M          |
+----------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
| spark.eventLog.compression.codec       | Codec used to compress event logs. By default, Spark provides four types of codecs: LZ4, LZF, Snappy, and ZSTD. If this parameter is not specified, **spark.io.compression.codec** is used. | None          |
+----------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
| spark.eventLog.logStageExecutorMetrics | Whether to write each stage peak value (for each executor) of executor metrics to the event log.                                                                                            | false         |
+----------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
