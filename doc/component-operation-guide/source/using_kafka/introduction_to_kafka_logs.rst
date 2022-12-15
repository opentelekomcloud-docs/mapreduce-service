:original_name: mrs_01_1042.html

.. _mrs_01_1042:

Introduction to Kafka Logs
==========================

This section applies to MRS 3.\ *x* or later.

Log Description
---------------

**Log paths**: The default storage path of Kafka logs is **/var/log/Bigdata/kafka**. The default storage path of audit logs is **/var/log/Bigdata/audit/kafka**.

-  Broker: **/var/log/Bigdata/kafka/broker** (run logs)

Log archive rule: The automatic Kafka log compression function is enabled. By default, when the size of logs exceeds 30 MB, logs are automatically compressed into a log file named in the following format: *<Original log file name>-<yyyy-mm-dd_hh-mm-ss>.[ID].*\ **log.zip**. A maximum of 20 latest compressed files are retained by default. You can configure the number of compressed files and the compression threshold.

.. table:: **Table 1** Broker log list

   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | Type    | Log File Name                              | Description                                                                                                                      |
   +=========+============================================+==================================================================================================================================+
   | Run log | server.log                                 | Server run log of the broker process                                                                                             |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | controller.log                             | Controller run log of the broker process                                                                                         |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | kafka-request.log                          | Request run log of the broker process                                                                                            |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | log-cleaner.log                            | Cleaner run log of the broker process                                                                                            |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | state-change.log                           | State-change run log of the broker process                                                                                       |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | kafkaServer-<SSH_USER>-<DATE>-<PID>-gc.log | GC log of the broker process                                                                                                     |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | postinstall.log                            | Work log after broker installation                                                                                               |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | prestart.log                               | Work log before broker startup                                                                                                   |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | checkService.log                           | Log that records whether broker starts successfully                                                                              |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | start.log                                  | Startup log of the broker process                                                                                                |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | stop.log                                   | Stop log of the broker process                                                                                                   |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | checkavailable.log                         | Log that records the health check details of the Kafka service                                                                   |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | checkInstanceHealth.log                    | Log that records the health check details of broker instances                                                                    |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | kafka-authorizer.log                       | Broker authorization log                                                                                                         |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | kafka-root.log                             | Broker basic log                                                                                                                 |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | cleanup.log                                | Cleanup log of broker uninstallation                                                                                             |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | metadata-backup-recovery.log               | Broker backup and recovery log                                                                                                   |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | ranger-kafka-plugin-enable.log             | Log that records the Ranger plug-ins enabled by brokers                                                                          |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | server.out                                 | Broker JVM log                                                                                                                   |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   |         | audit.log                                  | Authentication log of the Ranger authentication plug-in. This log is archived in the **/var/log/Bigdata/audit/kafka** directory. |
   +---------+--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+

Log Level
---------

:ref:`Table 2 <mrs_01_1042__tdd8d04c16fc9471c90e233547cf6579c>` describes the log levels supported by Kafka.

Levels of run logs are ERROR, WARN, INFO, and DEBUG from the highest to the lowest priority. Run logs of equal or higher levels are recorded. The higher the specified log level, the fewer the logs recorded.

.. _mrs_01_1042__tdd8d04c16fc9471c90e233547cf6579c:

.. table:: **Table 2** Log levels

   +-------+------------------------------------------------------------------------------------------+
   | Level | Description                                                                              |
   +=======+==========================================================================================+
   | ERROR | Logs of this level record error information about system running.                        |
   +-------+------------------------------------------------------------------------------------------+
   | WARN  | Logs of this level record exception information about the current event processing.      |
   +-------+------------------------------------------------------------------------------------------+
   | INFO  | Logs of this level record normal running status information about the system and events. |
   +-------+------------------------------------------------------------------------------------------+
   | DEBUG | Logs of this level record the system information and system debugging information.       |
   +-------+------------------------------------------------------------------------------------------+

To modify log levels, perform the following operations:

#. Go to the **All Configurations** page. See :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.
#. On the menu bar on the left, select the log menu of the target role.
#. Select a desired log level.
#. Save the configuration. In the displayed dialog box, click **OK** to make the configurations take effect.

Log Format
----------

The following table describes the Kafka log format.

.. table:: **Table 3** Log formats

   +---------+------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
   | Type    | Format                                                                                                                                                     | Example                                                                                               |
   +=========+============================================================================================================================================================+=======================================================================================================+
   | Run log | <yyyy-MM-dd HH:mm:ss,SSS>|<Log Level>|<Thread that generates the log>|<Message in the log>|<Full name of the log event invocation class>(<Log file>:<Row>) | 2015-08-08 11:09:53,483 \| INFO \| [main] \| Loading logs. \| kafka.log.LogManager (Logging.scala:68) |
   +---------+------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
   |         | <yyyy-MM-dd HH:mm:ss><HostName><Component name><logLevel><Message>                                                                                         | 2015-08-08 11:09:51 10-165-0-83 Kafka INFO Running kafka-start.sh.                                    |
   +---------+------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
