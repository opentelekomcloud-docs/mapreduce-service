:original_name: mrs_01_24161.html

.. _mrs_01_24161:

IoTDB Log Overview
==================

**Description**

Log Description
---------------

**Log paths**: The default paths of IoTDB logs are **/var/log/Bigdata/iotdb/iotdbserver** (for storing run logs) and **/var/log/Bigdata/audit/iotdb/iotdbserver** (for storing audit logs).

**Log archive rule**: The automatic compression and archiving function of IoTDB is enabled. By default, when the size of a log file exceeds 20 MB (which is adjustable), the log file is automatically compressed. The naming rule of the compressed log file is as follows: <*Original log file name*>-<*yyyymmdd*>.\ *ID*.\ **log.gz**. A maximum of 10 latest compressed files are reserved. The number of compressed files and compression threshold can be configured.

.. table:: **Table 1** IoTDB log list

   +-----------+----------------------------------------------------+----------------------------------------------------+
   | Type      | Name                                               | Description                                        |
   +===========+====================================================+====================================================+
   | Run logs  | log-all.log                                        | IoTDB service log.                                 |
   +-----------+----------------------------------------------------+----------------------------------------------------+
   |           | log-error.log                                      | IoTDB service error log.                           |
   +-----------+----------------------------------------------------+----------------------------------------------------+
   |           | log-measure.log                                    | IoTDB service monitoring log.                      |
   +-----------+----------------------------------------------------+----------------------------------------------------+
   |           | log-query-debug.log                                | IoTDB query debug log.                             |
   +-----------+----------------------------------------------------+----------------------------------------------------+
   |           | log-query-frequency.log                            | IoTDB query frequency log.                         |
   +-----------+----------------------------------------------------+----------------------------------------------------+
   |           | log-sync.log                                       | IoTDB synchronization log.                         |
   +-----------+----------------------------------------------------+----------------------------------------------------+
   |           | log-slow-sql.log                                   | IoTDB slow SQL log.                                |
   +-----------+----------------------------------------------------+----------------------------------------------------+
   |           | server.out                                         | Log that records IoTDB service startup exceptions. |
   +-----------+----------------------------------------------------+----------------------------------------------------+
   |           | postinstall.log                                    | IoTDB process startup log.                         |
   +-----------+----------------------------------------------------+----------------------------------------------------+
   |           | prestart.log                                       | Log that records IoTDB process startup exceptions. |
   +-----------+----------------------------------------------------+----------------------------------------------------+
   |           | service-healthcheck.log                            | IoTDB database initialization log.                 |
   +-----------+----------------------------------------------------+----------------------------------------------------+
   |           | start.log                                          | IoTDBServer service startup log.                   |
   +-----------+----------------------------------------------------+----------------------------------------------------+
   |           | stop.log                                           | IoTDBServer service stop log.                      |
   +-----------+----------------------------------------------------+----------------------------------------------------+
   |           | IoTDBServer-omm-<timestamp>-<pid>-gc.log.0.current | IoTDBServer service GC log.                        |
   +-----------+----------------------------------------------------+----------------------------------------------------+
   | Audit log | log_audit.log                                      | IoTDB audit log.                                   |
   +-----------+----------------------------------------------------+----------------------------------------------------+

**Log levels**

:ref:`Table 2 <mrs_01_24161__table135218393114>` describes the log levels supported by IoTDB.

Levels of logs are ERROR, WARN, INFO, and DEBUG from the highest to the lowest priority. Run logs of equal or higher levels are recorded. The higher the specified log level, the fewer the logs recorded.

.. _mrs_01_24161__table135218393114:

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

#. Go to the **All Configurations** page of the IoTDB service by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.
#. In the navigation tree on the left, select **Log** corresponding to the role to be modified.
#. Select a desired log level and save the configuration.

.. note::

   The IoTDB log level takes effect 60 seconds after being configured. You do not need to restart the service.

Log Formats
-----------

The following table lists the IoTDB log formats:

.. table:: **Table 3** Log formats

   +-----------+-----------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type      | Format                                                                                                                            | Example                                                                                                                                                                                                                    |
   +===========+===================================================================================================================================+============================================================================================================================================================================================================================+
   | Run log   | <*yyyy-MM-dd HH:mm:ss,SSS*> \| *Log level* \| [*Thread name*] \| *Log information* \| *Log printing class* (*File*:*Line number*) | 2021-06-08 10:08:41,221 \| ERROR \| [main] \| Client failed to open SaslClientTransport to interact with a server during session initiation: \| org.apache.iotdb.rpc.sasl.TFastSaslTransport (TFastSaslTransport.java:257) |
   +-----------+-----------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Audit log | <*yyyy-MM-dd HH:mm:ss,SSS*> \| *Log level* \| [*Thread name*] \| *Log information* \| *Log printing class* (*File*:*Line number*) | 2021-06-08 11:03:49,365 \| INFO \| [ClusterClient-1] \| Session-1 is closing \| IoTDB_AUDIT_LOGGER (TSServiceImpl.java:326)                                                                                                |
   +-----------+-----------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
