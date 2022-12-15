:original_name: mrs_01_0842.html

.. _mrs_01_0842:

Introduction to MapReduce Logs
==============================

Log Description
---------------

**Log paths:**

-  JobhistoryServer: **/var/log/Bigdata/mapreduce/jobhistory** (run log) and **/var/log/Bigdata/audit/mapreduce/jobhistory** (audit log)
-  Container: **/srv/BigData/hadoop/data1/nm/containerlogs/application_${appid}/container_{$contid}**

.. note::

   The logs of running tasks are stored in the preceding paths. After the running is complete, the system determines whether to aggregate the logs to an HDFS directory based on the YARN configuration. For details, see :ref:`Common YARN Parameters <mrs_01_0852>`.

**Log archive rule**:

The automatic compression and archive function is enabled for MapReduce logs. By default, a log file is automatically compressed when the size of the log file is greater than 50 MB. The name of the compressed log file is in the following format: *<Name of the original log>-<yyyy-mm-dd_hh-mm-ss>.[NO.]*\ **.log.zip**. A maximum of 100 latest compressed files are reserved. The number of compressed files can be configured on the parameter configuration page.

In MapReduce, JobhistoryServer cleans the old log files stored in HDFS periodically. The default storage directory is **/mr-history/done**. **mapreduce.jobhistory.max-age-ms** is used to set the cleanup interval. The default value of this parameter is 1,296,000,000 ms, which indicates 15 days.

.. table:: **Table 1** MapReduce log list

   +-----------+-------------------------------------------------+-------------------------------------------------------------------------------------+
   | Type      | Name                                            | Description                                                                         |
   +===========+=================================================+=====================================================================================+
   | Run log   | jhs-daemon-start-stop.log                       | Startup log file of the daemon process                                              |
   +-----------+-------------------------------------------------+-------------------------------------------------------------------------------------+
   |           | hadoop-<SSH_USER>-jhshadaemon-<hostname>.log    | Run log file of the daemon process                                                  |
   +-----------+-------------------------------------------------+-------------------------------------------------------------------------------------+
   |           | hadoop-<SSH_USER>-<process_name>-<hostname>.out | Log that records the MapReduce running environment information                      |
   +-----------+-------------------------------------------------+-------------------------------------------------------------------------------------+
   |           | historyserver-<SSH_USER>-<DATE>-<PID>-gc.log    | Log that records the garbage collection of the MapReduce service                    |
   +-----------+-------------------------------------------------+-------------------------------------------------------------------------------------+
   |           | jhs-haCheck.log                                 | Log that records the active and standby status of MapReduce instances               |
   +-----------+-------------------------------------------------+-------------------------------------------------------------------------------------+
   |           | yarn-start-stop.log                             | Log that records the startup and stop of the MapReduce service                      |
   +-----------+-------------------------------------------------+-------------------------------------------------------------------------------------+
   |           | yarn-prestart.log                               | Log that records cluster operations before the MapReduce service startup            |
   +-----------+-------------------------------------------------+-------------------------------------------------------------------------------------+
   |           | yarn-postinstall.log                            | Work log before the MapReduce service startup and after the installation            |
   +-----------+-------------------------------------------------+-------------------------------------------------------------------------------------+
   |           | yarn-cleanup.log                                | Log that records the cleanup logs about the uninstallation of the MapReduce service |
   +-----------+-------------------------------------------------+-------------------------------------------------------------------------------------+
   |           | mapred-service-check.log                        | Log that records the health check details of the MapReduce service                  |
   +-----------+-------------------------------------------------+-------------------------------------------------------------------------------------+
   |           | container_{$contid}                             | Container log                                                                       |
   +-----------+-------------------------------------------------+-------------------------------------------------------------------------------------+
   |           | hadoop-<SSH_USER>-<process_name>-<hostname>.log | MR run log                                                                          |
   +-----------+-------------------------------------------------+-------------------------------------------------------------------------------------+
   |           | mapred-switch-jhs.log                           | MR active/standby switchover log                                                    |
   +-----------+-------------------------------------------------+-------------------------------------------------------------------------------------+
   |           | env.log                                         | Environment information log before the instance is started or stopped               |
   +-----------+-------------------------------------------------+-------------------------------------------------------------------------------------+
   | Audit log | mapred-audit-jobhistory.log                     | MapReduce operation audit log                                                       |
   +-----------+-------------------------------------------------+-------------------------------------------------------------------------------------+
   |           | SecurityAuth.audit                              | MapReduce security audit log                                                        |
   +-----------+-------------------------------------------------+-------------------------------------------------------------------------------------+

Log Level
---------

:ref:`Table 2 <mrs_01_0842__tefeb2aa164fe4238b59439b2b0dacf00>` describes the log levels supported by MapReduce The log levels are FATAL, ERROR, WARN, INFO, and DEBUG from high priority to low. Logs whose levels are higher than or equal to the specified level are printed. The number of printed logs decreases as the specified log level increases.

.. _mrs_01_0842__tefeb2aa164fe4238b59439b2b0dacf00:

.. table:: **Table 2** Log level

   +-------+--------------------------------------------------------------------------------------------+
   | Level | Description                                                                                |
   +=======+============================================================================================+
   | FATAL | Logs of this level record critical error information about the current event processing.   |
   +-------+--------------------------------------------------------------------------------------------+
   | ERROR | Logs of this level record error information about the current event processing.            |
   +-------+--------------------------------------------------------------------------------------------+
   | WARN  | Logs of this level record unexpected alarm information about the current event processing. |
   +-------+--------------------------------------------------------------------------------------------+
   | INFO  | Logs of this level record normal running status information about the system and events.   |
   +-------+--------------------------------------------------------------------------------------------+
   | DEBUG | Logs of this level record the system information and system debugging information.         |
   +-------+--------------------------------------------------------------------------------------------+

To modify log levels, perform the following operations:

#. Go to the **All Configurations** page of the MapReduce service. For details, see :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.
#. On the left menu bar, select the log menu of the target role.
#. Select a desired log level.
#. Save the configuration. In the displayed dialog box, click **OK** to make the configurations take effect.

   .. note::

      The configurations take effect immediately without restarting the service.

Log Format
----------

The following table lists the MapReduce log formats.

.. table:: **Table 3** Log format

   +-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type      | Format                                                                                                                                                 | Example                                                                                                                                                                                                                                 |
   +===========+========================================================================================================================================================+=========================================================================================================================================================================================================================================+
   | Run log   | <*yyyy-MM-dd HH:mm:ss,SSS*>|<*Log level*>|<*Name of the thread that generates the log*>|<*Message in the log*>|<*Location where the log event occurs*> | 2020-01-26 14:18:59,109 \| INFO \| main \| Client environment:java.compiler=<NA> \| org.apache.zookeeper.Environment.logEnv(Environment.java:100)                                                                                       |
   +-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Audit log | <*yyyy-MM-dd HH:mm:ss,SSS*>|<*Log level*>|<*Name of the thread that generates the log*>|<*Message in the log*>|<*Location where the log event occurs*> | 2020-01-26 14:24:43,605 \| INFO \| main-EventThread \| USER=omm OPERATION=refreshAdminAcls TARGET=AdminService RESULT=SUCCESS \| org.apache.hadoop.yarn.server.resourcemanager.RMAuditLogger$LogLevel$6.printLog(RMAuditLogger.java:91) |
   +-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
