:original_name: mrs_01_2399.html

.. _mrs_01_2399:

ClickHouse Log Overview
=======================

Log Description
---------------

**Log path**: The default storage path of ClickHouse log files is as follows: **${BIGDATA_LOG_HOME}/clickhouse**

**Log archive rule**: The automatic ClickHouse log compression function is enabled. By default, when the size of logs exceeds 100 MB, logs are automatically compressed into a log file named in the following format: *<Original log name>*\ **.**\ *[ID]*\ **.gz**. A maximum of 10 latest compressed files are reserved by default. The number of compressed files can be configured on Manager.

.. table:: **Table 1** ClickHouse log list

   +--------------------------+---------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   | Log Type                 | Log File Name                                                                                                             | Description                                                                                                                          |
   +==========================+===========================================================================================================================+======================================================================================================================================+
   | Run logs                 | /var/log/Bigdata/clickhouse/clickhouseServer/clickhouse-server.err.log                                                    | Path of ClickHouseServer error log files.                                                                                            |
   +--------------------------+---------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   |                          | /var/log/Bigdata/clickhouse/clickhouseServer/checkService.log                                                             | Path of key ClickHouseServer run log files.                                                                                          |
   +--------------------------+---------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   |                          | /var/log/Bigdata/clickhouse/clickhouseServer/clickhouse-server.log                                                        |                                                                                                                                      |
   +--------------------------+---------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   |                          | /var/log/Bigdata/clickhouse/balance/start.log                                                                             | Path of ClickHouseBalancer startup log files.                                                                                        |
   +--------------------------+---------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   |                          | /var/log/Bigdata/clickhouse/balance/error.log                                                                             | Path of ClickHouseBalancer error log files.                                                                                          |
   +--------------------------+---------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   |                          | /var/log/Bigdata/clickhouse/balance/access_http.log                                                                       | Path of ClickHouseBalancer run log files.                                                                                            |
   +--------------------------+---------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   | Data migration logs      | /var/log/Bigdata/clickhouse/migration/*Data migration task name*/clickhouse-copier_{timestamp}_{processId}/copier.log     | Run logs generated when you use the migration tool by referring to :ref:`Using the ClickHouse Data Migration Tool <mrs_01_24053>`.   |
   +--------------------------+---------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   |                          | /var/log/Bigdata/clickhouse/migration/*Data migration task name*/clickhouse-copier_{timestamp}_{processId}/copier.err.log | Error logs generated when you use the migration tool by referring to :ref:`Using the ClickHouse Data Migration Tool <mrs_01_24053>`. |
   +--------------------------+---------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   | Audit log                | /var/log/Bigdata/audit/clickhouse/clickhouse-server.audit.log                                                             | Path of ClickHouse audit log files.                                                                                                  |
   +--------------------------+---------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   | Backup and recovery logs | /var/log/Bigdata/clickhouse/clickhouseServer/backup.log                                                                   | Path of log files generated when ClickHouse performs the backup and restoration operations on Manager.                               |
   +--------------------------+---------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+

Log Level
---------

:ref:`Table 2 <mrs_01_2399__en-us_topic_0000001219029595_tc09b739e3eb34797a6da936a37654e97>` describes the log levels supported by ClickHouse.

Levels of run logs are error, warning, trace, information, and debug from the highest to the lowest priority. Run logs of equal or higher levels are recorded. The higher the specified log level, the fewer the logs recorded.

.. _mrs_01_2399__en-us_topic_0000001219029595_tc09b739e3eb34797a6da936a37654e97:

.. table:: **Table 2** Log levels

   +----------+-------------+------------------------------------------------------------------------------------------+
   | Log Type | Level       | Description                                                                              |
   +==========+=============+==========================================================================================+
   | Run log  | error       | Logs of this level record error information about system running.                        |
   +----------+-------------+------------------------------------------------------------------------------------------+
   |          | warning     | Logs of this level record exception information about the current event processing.      |
   +----------+-------------+------------------------------------------------------------------------------------------+
   |          | trace       | Logs of this level record trace information about the current event processing.          |
   +----------+-------------+------------------------------------------------------------------------------------------+
   |          | information | Logs of this level record normal running status information about the system and events. |
   +----------+-------------+------------------------------------------------------------------------------------------+
   |          | debug       | Logs of this level record system running and debugging information.                      |
   +----------+-------------+------------------------------------------------------------------------------------------+

To modify log levels, perform the following operations:

#. Log in to FusionInsight Manager.
#. Choose **Cluster** > **Services** > **ClickHouse** > **Configurations**.
#. Select **All Configurations**.
#. On the menu bar on the left, select the log menu of the target role.
#. Select a desired log level.
#. Click **Save**. Then, click **OK**.

.. note::

   The configurations take effect immediately without the need to restart the service.

Log Format
----------

The following table lists the ClickHouse log format:

.. table:: **Table 3** Log formats

   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Log Type              | Format                                                                                                                                                 | Example                                                                                                                                                                                                                                  |
   +=======================+========================================================================================================================================================+==========================================================================================================================================================================================================================================+
   | Run log               | <*yyyy-MM-dd HH:mm:ss,SSS*>|<*Log level*>|<*Name of the thread that generates the log*>|<*Message in the log*>|<*Location where the log event occurs*> | 2021.02.23 15:26:30.691301 [ 6085 ] {} <Error> DynamicQueryHandler: Code: 516, e.displayText() = DB::Exception: default: Authentication failed: password is incorrect or there is no user with such name, Stack trace (when copying this |
   |                       |                                                                                                                                                        |                                                                                                                                                                                                                                          |
   |                       |                                                                                                                                                        | message, always include the lines below):                                                                                                                                                                                                |
   |                       |                                                                                                                                                        |                                                                                                                                                                                                                                          |
   |                       |                                                                                                                                                        | 0. Poco::Exception::Exception(std::__1::basic_string<char, std::__1::char_traits<char>, std::__1::allocator<char> > const&, int) @ 0x1250e59c                                                                                            |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
