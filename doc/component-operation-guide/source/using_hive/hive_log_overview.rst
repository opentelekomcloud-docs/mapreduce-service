:original_name: mrs_01_0976.html

.. _mrs_01_0976:

Hive Log Overview
=================

Log Description
---------------

**Log path**: The default save path of Hive logs is **/var/log/Bigdata/hive/**\ *role name*, the default save path of Hive1 logs is **/var/log/Bigdata/hive1/**\ *role name*, and the others follow the same rule.

-  HiveServer: **/var/log/Bigdata/hive/hiveserver** (run log) and **var/log/Bigdata/audit/hive/hiveserver** (audit log)
-  MetaStore: **/var/log/Bigdata/hive/metastore** (run log) and **/var/log/Bigdata/audit/hive/metastore** (audit log)
-  WebHCat: **/var/log/Bigdata/hive/webhcat** (run log) and **/var/log/Bigdata/audit/hive/webhcat** (audit log)

**Log archive rule**: The automatic compression and archiving function of Hive is enabled. By default, when the size of a log file exceeds 20 MB (which is adjustable), the log file is automatically compressed. The naming rule of a compressed log file is as follows: <*Original log name*>-<*yyyy-mm-dd_hh-mm-ss*>.[*ID*].\ **log.zip** A maximum of 20 latest compressed files are reserved. The number of compressed files and compression threshold can be configured.

.. table:: **Table 1** Hive log list

   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | Log Type              | Log File Name                                                              | Description                                                                         |
   +=======================+============================================================================+=====================================================================================+
   | Run log               | /hiveserver/hiveserver.out                                                 | Log file that records HiveServer running environment information.                   |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /hiveserver/hive.log                                                       | Run log file of the HiveServer process.                                             |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /hiveserver/hive-omm-*<Date>*\ ``-``\ *<PID>*-gc.log.\ *<No.>*             | GC log file of the HiveServer process.                                              |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /hiveserver/prestartDetail.log                                             | Work log file before the HiveServer startup.                                        |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /hiveserver/check-serviceDetail.log                                        | Log file that records whether the Hive service starts successfully                  |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /hiveserver/cleanupDetail.log                                              | Cleanup log file about the HiveServer uninstallation                                |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /hiveserver/startDetail.log                                                | Startup log file of the HiveServer process.                                         |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /hiveserver/stopDetail.log                                                 | Shutdown log file of the HiveServer process.                                        |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /hiveserver/localtasklog/omm\_\ *<Date>*\ \_\ *<Task ID>*.log              | Run log file of the local Hive task.                                                |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /hiveserver/localtasklog/omm\_\ *<Date>*\ \_\ *<Task ID>*-gc.log.\ *<No.>* | GC log file of the local Hive task.                                                 |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /metastore/metastore.log                                                   | Run log file of the MetaStore process.                                              |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /metastore/hive-omm-*<Date>*\ ``-``\ *<PID>*-gc.log.\ *<No.>*              | GC log file of the MetaStore process.                                               |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /metastore/postinstallDetail.log                                           | Work log file after the MetaStore installation.                                     |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /metastore/prestartDetail.log                                              | Work log file before the MetaStore startup                                          |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /metastore/cleanupDetail.log                                               | Cleanup log file of the MetaStore uninstallation                                    |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /metastore/startDetail.log                                                 | Startup log file of the MetaStore process.                                          |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /metastore/stopDetail.log                                                  | Shutdown log file of the MetaStore process.                                         |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /metastore/metastore.out                                                   | Log file that records MetaStore running environment information.                    |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /webhcat/webhcat-console.out                                               | Log file that records the normal start and stop of the WebHCat process.             |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /webhcat/webhcat-console-error.out                                         | Log file that records the start and stop exceptions of the WebHCat process.         |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /webhcat/prestartDetail.log                                                | Work log file before the WebHCat startup.                                           |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /webhcat/cleanupDetail.log                                                 | Cleanup logs generated during WebHCat uninstallation or before WebHCat installation |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /webhcat/hive-omm-<*Date*>-<PID>-gc.log.<*No*.>                            | GC log file of the WebHCat process.                                                 |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | /webhcat/webhcat.log                                                       | Run log file of the WebHCat process                                                 |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | Audit log             | hive-audit.log                                                             | HiveServer audit log file                                                           |
   |                       |                                                                            |                                                                                     |
   |                       | hive-rangeraudit.log                                                       |                                                                                     |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | metastore-audit.log                                                        | MetaStore audit log file.                                                           |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | webhcat-audit.log                                                          | WebHCat audit log file.                                                             |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   |                       | jetty-<Date>.request.log                                                   | Request logs of the jetty service.                                                  |
   +-----------------------+----------------------------------------------------------------------------+-------------------------------------------------------------------------------------+

Log Levels
----------

:ref:`Table 2 <mrs_01_0976__t91045e1a946a46b4bac39028af62f3ad>` describes the log levels supported by Hive.

Levels of run logs are ERROR, WARN, INFO, and DEBUG from the highest to the lowest priority. Run logs of equal or higher levels are recorded. The higher the specified log level, the fewer the logs recorded.

.. _mrs_01_0976__t91045e1a946a46b4bac39028af62f3ad:

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

#. Go to the **All Configurations** page of the Yarn service by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.
#. On the menu bar on the left, select the log menu of the target role.
#. Select a desired log level and save the configuration.

   .. note::

      The Hive log level takes effect immediately after being configured. You do not need to restart the service.

Log Formats
-----------

The following table lists the Hive log formats:

.. table:: **Table 3** Log formats

   +-----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Log Type  | Format                                                                                                                                                              | Example                                                                                                                                                                                                                                                                             |
   +===========+=====================================================================================================================================================================+=====================================================================================================================================================================================================================================================================================+
   | Run log   | <yyyy-MM-dd HH:mm:ss,SSS>|<LogLevel>|<Thread that generates the log>|<Message in the log>|<Location of the log event>                                               | 2014-11-05 09:45:01,242 \| INFO \| main \| Starting hive metastore on port 21088 \| org.apache.hadoop.hive.metastore.HiveMetaStore.main(HiveMetaStore.java:5198)                                                                                                                    |
   +-----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Audit log | <yyyy-MM-dd HH:mm:ss,SSS>|<LogLevel>|<Thread that generates the log>|<User Name><User IP><Time><Operation><Resource><Result><Detail >|< Location of the log event > | 2018-12-24 12:16:25,319 \| INFO \| HiveServer2-Handler-Pool: Thread-185 \| UserName=hive UserIP=10.153.2.204 Time=2018/12/24 12:16:25 Operation=CloseSession Result=SUCCESS Detail= \| org.apache.hive.service.cli.thrift.ThriftCLIService.logAuditEvent(ThriftCLIService.java:434) |
   +-----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
