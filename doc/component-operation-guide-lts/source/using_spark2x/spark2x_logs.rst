:original_name: mrs_01_1971.html

.. _mrs_01_1971:

Spark2x Logs
============

Log Description
---------------

**Log paths:**

-  Executor run log: **${BIGDATA_DATA_HOME}/hadoop/data${i}/nm/containerlogs/application_${appid}/container_{$contid}**

   .. note::

      The logs of running tasks are stored in the preceding path. After the running is complete, the system determines whether to aggregate the logs to an HDFS directory based on the Yarn configuration. For details, see :ref:`Common Yarn Parameters <mrs_01_0852>`.

-  Other logs: **/var/log/Bigdata/spark2x**

**Log archiving rule**:

-  When tasks are submitted in **yarn-client** or **yarn-cluster** mode, executor log files are stored each time when the size of the log files reaches 50 MB. A maximum of 10 log files can be reserved without being compressed.
-  The JobHistory2x log file is backed up each time when the size of the log file reaches 100 MB. A maximum of 100 log files can be reserved without being compressed.
-  The JDBCServer2x log file is backed up each time when the size of the log file reaches 100 MB. A maximum of 100 log files can be reserved without being compressed.
-  The IndexServer2x log file is backed up each time when the size of the log file reaches 100 MB. A maximum of 100 log files can be reserved without being compressed.
-  The JDBCServer2x audit log file is backed up each time when the size of the log file reaches 20 MB by default. A maximum of 20 log files can be reserved without being compressed.
-  The log file size and the number of compressed files to be reserved can be configured on FusionInsight Manager.

.. table:: **Table 1** Spark2x log list

   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   | Log Type              | Name                                                                                  | Description                                                                                     |
   +=======================+=======================================================================================+=================================================================================================+
   | SparkResource2x logs  | spark.log                                                                             | Spark2x service initialization log                                                              |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | prestart.log                                                                          | Prestart script log                                                                             |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | cleanup.log                                                                           | Cleanup log file for instance installation and uninstallation                                   |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | spark-availability-check.log                                                          | Spark2x service health check log                                                                |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | spark-service-check.log                                                               | Spark2x service check log                                                                       |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   | JDBCServer2x logs     | JDBCServer-start.log                                                                  | JDBCServer2x startup log                                                                        |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | JDBCServer-stop.log                                                                   | JDBCServer2x stop log                                                                           |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | JDBCServer.log                                                                        | JDBCServer2x run log on the server                                                              |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | jdbc-state-check.log                                                                  | JDBCServer2x health check log                                                                   |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | jdbcserver-omm-pid***-gc.log.*.current                                                | IJDBCServer2x process GC log                                                                    |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | spark-omm-org.apache.spark.sql.hive.thriftserver.HiveThriftProxyServer2-``***``.out\* | JDBCServer2x process startup log. If the process stops, the **jstack** information is printed.  |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   | JobHistory2x logs     | jobHistory-start.log                                                                  | JobHistory2x startup log                                                                        |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | jobHistory-stop.log                                                                   | JobHistory2x stop log                                                                           |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | JobHistory.log                                                                        | JobHistory2x running process log                                                                |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | jobhistory-omm-pid***-gc.log.*.current                                                | JobHistory2x process GC log                                                                     |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | spark-omm-org.apache.spark.deploy.history.HistoryServer-``***``.out\*                 | JobHistory2x process startup log. If the process stops, the **jstack** information is printed.  |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   | IndexServer2x logs    | IndexServer-start.log                                                                 | IndexServer2x startup log                                                                       |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | IndexServer-stop.log                                                                  | IndexServer2x stop log                                                                          |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | IndexServer.log                                                                       | IndexServer2x run log on the server                                                             |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | indexserver-state-check.log                                                           | IndexServer2x health check log                                                                  |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | indexserver-omm-pid***-gc.log.*.current                                               | IndexServer2x process GC log                                                                    |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | spark-omm-org.apache.spark.sql.hive.thriftserver.IndexServerProxy-``***``.out\*       | IndexServer2x process startup log. If the process stops, the **jstack** information is printed. |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   | Audit Log             | jdbcserver-audit.log                                                                  | JDBCServer2x audit log                                                                          |
   |                       |                                                                                       |                                                                                                 |
   |                       | ranger-audit.log                                                                      |                                                                                                 |
   +-----------------------+---------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+

Log levels
----------

:ref:`Table 2 <mrs_01_1971__en-us_topic_0000001173470966_tcc4372c0e4d742299effd8668554ac30>` describes the log levels supported by Spark2x. The priorities of log levels are ERROR, WARN, INFO, and DEBUG in descending order. Logs whose levels are higher than or equal to the specified level are printed. The number of printed logs decreases as the specified log level increases.

.. _mrs_01_1971__en-us_topic_0000001173470966_tcc4372c0e4d742299effd8668554ac30:

.. table:: **Table 2** Log levels

   +-------+------------------------------------------------------------------------------------------+
   | Level | Description                                                                              |
   +=======+==========================================================================================+
   | ERROR | Error information about the current event processing                                     |
   +-------+------------------------------------------------------------------------------------------+
   | WARN  | Exception information about the current event processing                                 |
   +-------+------------------------------------------------------------------------------------------+
   | INFO  | Logs of this level record normal running status information about the system and events. |
   +-------+------------------------------------------------------------------------------------------+
   | DEBUG | Logs of this level record the system information and system debugging information.       |
   +-------+------------------------------------------------------------------------------------------+

To modify log levels, perform the following operations:

.. note::

   By default, the service does not need to be restarted after the Spark2x log levels are configured.

#. Log in to FusionInsight Manager.
#. Choose **Cluster** > *Name of the desired cluster* > **Service** > **Spark2x** > **Configuration**.
#. Select **All Configurations**.
#. On the menu bar on the left, select the log menu of the target role.
#. Select a desired log level.
#. Click **Save**. Then, click **OK**.

Log Format
----------

.. table:: **Table 3** Log Format

   +---------+--------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
   | Type    | Format                                                                                                                                                 | Example                                                                                     |
   +=========+========================================================================================================================================================+=============================================================================================+
   | Run log | <*yyyy-MM-dd HH:mm:ss,SSS*>|<*Log level*>|<*Name of the thread that generates the log*>|<*Message in the log*>|<*Location where the log event occurs*> | 2014-09-22 11:16:23,980 INFO DAGScheduler: Final stage: Stage 0(reduce at SparkPi.scala:35) |
   +---------+--------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
