:original_name: mrs_01_1056.html

.. _mrs_01_1056:

HBase Log Overview
==================

Log Description
---------------

**Log path**: The default storage path of HBase logs is **/var/log/Bigdata/hbase/**\ *Role name*.

-  HMaster: **/var/log/Bigdata/hbase/hm** (run logs) and **/var/log/Bigdata/audit/hbase/hm** (audit logs)
-  RegionServer: **/var/log/Bigdata/hbase/rs** (run logs) and **/var/log/Bigdata/audit/hbase/rs** (audit logs)
-  ThriftServer: **/var/log/Bigdata/hbase/ts2** (run logs, **ts2** is the instance name) and **/var/log/Bigdata/audit/hbase/ts2** (audit logs, **ts2** is the instance name)

**Log archive rule**: The automatic log compression and archiving function of HBase is enabled. By default, when the size of a log file exceeds 30 MB, the log file is automatically compressed. The naming rule of a compressed log file is as follows: <*Original log name*>-<*yyyy-mm-dd_hh-mm-ss*>.[*ID*].\ **log.zip** A maximum of 20 latest compressed files are reserved. The number of compressed files can be configured on the Manager portal.

.. table:: **Table 1** HBase log list

   +------------+------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   | Type       | Name                                           | Description                                                                                                                   |
   +============+================================================+===============================================================================================================================+
   | Run logs   | hbase-<SSH_USER>-<process_name>-<hostname>.log | HBase system log that records the startup time, startup parameters, and most logs generated when the HBase system is running. |
   +------------+------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   |            | hbase-<SSH_USER>-<process_name>-<hostname>.out | Log that records the HBase running environment information.                                                                   |
   +------------+------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   |            | <process_name>-<SSH_USER>-<DATE>-<PID>-gc.log  | Log that records HBase junk collections.                                                                                      |
   +------------+------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   |            | checkServiceDetail.log                         | Log that records whether the HBase service starts successfully.                                                               |
   +------------+------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   |            | hbase.log                                      | Log generated when the HBase service health check script and some alarm check scripts are executed.                           |
   +------------+------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   |            | sendAlarm.log                                  | Log that records alarms reported after execution of HBase alarm check scripts.                                                |
   +------------+------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   |            | hbase-haCheck.log                              | Log that records the active and standby status of HMaster                                                                     |
   +------------+------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   |            | stop.log                                       | Log that records the startup and stop processes of HBase.                                                                     |
   +------------+------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   | Audit logs | hbase-audit-<process_name>.log                 | Log that records HBase security audit.                                                                                        |
   +------------+------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+

Log Level
---------

:ref:`Table 2 <mrs_01_1056__tbb25f33f364f4d2d8e14cd48d9f8dd0b>` describes the log levels supported by HBase. The priorities of log levels are FATAL, ERROR, WARN, INFO, and DEBUG in descending order. Logs whose levels are higher than or equal to the specified level are printed. The number of printed logs decreases as the specified log level increases.

.. _mrs_01_1056__tbb25f33f364f4d2d8e14cd48d9f8dd0b:

.. table:: **Table 2** Log levels

   +-------+------------------------------------------------------------------------------------------------------------------------------------------+
   | Level | Description                                                                                                                              |
   +=======+==========================================================================================================================================+
   | FATAL | Logs of this level record fatal error information about the current event processing that may result in a system crash.                  |
   +-------+------------------------------------------------------------------------------------------------------------------------------------------+
   | ERROR | Logs of this level record error information about the current event processing, which indicates that system running is abnormal.         |
   +-------+------------------------------------------------------------------------------------------------------------------------------------------+
   | WARN  | Logs of this level record abnormal information about the current event processing. These abnormalities will not result in system faults. |
   +-------+------------------------------------------------------------------------------------------------------------------------------------------+
   | INFO  | Logs of this level record normal running status information about the system and events.                                                 |
   +-------+------------------------------------------------------------------------------------------------------------------------------------------+
   | DEBUG | Logs of this level record the system information and system debugging information.                                                       |
   +-------+------------------------------------------------------------------------------------------------------------------------------------------+

To modify log levels, perform the following operations:

#. Go to the **All Configurations** page of the HBase service. For details, see :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.
#. On the left menu bar, select the log menu of the target role.
#. Select a desired log level.
#. Save the configuration. In the displayed dialog box, click **OK** to make the configurations take effect.

   .. note::

      The configurations take effect immediately without the need to restart the service.

Log Formats
-----------

The following table lists the HBase log formats.

.. table:: **Table 3** Log formats

   +------------+--------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type       | Component    | Format                                                                                                                       | Example                                                                                                                                                                                                              |
   +============+==============+==============================================================================================================================+======================================================================================================================================================================================================================+
   | Run logs   | HMaster      | <yyyy-MM-dd HH:mm:ss,SSS>|<Log Level>|<*Thread that generates the log*>|<*Message in the log*>|<*Location of the log event*> | 2020-01-19 16:04:53,558 \| INFO \| main \| env:HBASE_THRIFT_OPTS= \| org.apache.hadoop.hbase.util.ServerCommandLine.logProcessInfo(ServerCommandLine.java:113)                                                       |
   +------------+--------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |            | RegionServer | <yyyy-MM-dd HH:mm:ss,SSS>|<Log Level>|<*Thread that generates the log*>|<*Message in the log*>|<*Location of the log event*> | 2020-01-19 16:05:18,589 \| INFO \| regionserver16020-SendThread(linux-k6da:2181) \| Client will use GSSAPI as SASL mechanism. \| org.apache.zookeeper.client.ZooKeeperSaslClient$1.run(ZooKeeperSaslClient.java:285) |
   +------------+--------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |            | ThriftServer | <yyyy-MM-dd HH:mm:ss,SSS>|<Log Level>|<*Thread that generates the log*>|<*Message in the log*>|<*Location of the log event*> | 2020-02-16 09:42:55,371 \| INFO \| main \| loaded properties from hadoop-metrics2.properties \| org.apache.hadoop.metrics2.impl.MetricsConfig.loadFirst(MetricsConfig.java:111)                                      |
   +------------+--------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Audit logs | HMaster      | <yyyy-MM-dd HH:mm:ss,SSS>|<Log Level>|<*Thread that generates the log*>|<*Message in the log*>|<*Location of the log event*> | 2020-02-16 09:42:40,934 \| INFO \| master:linux-k6da:16000 \| Master: [master:linux-k6da:16000] start operation called. \| org.apache.hadoop.hbase.master.HMaster.run(HMaster.java:581)                              |
   +------------+--------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |            | RegionServer | <yyyy-MM-dd HH:mm:ss,SSS>|<Log Level>|<*Thread that generates the log*>|<*Message in the log*>|<*Location of the log event*> | 2020-02-16 09:42:51,063 \| INFO \| main \| RegionServer: [regionserver16020] start operation called. \| org.apache.hadoop.hbase.regionserver.HRegionServer.startRegionServer(HRegionServer.java:2396)                |
   +------------+--------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |            | ThriftServer | <yyyy-MM-dd HH:mm:ss,SSS>|<Log Level>|<*Thread that generates the log*>|<*Message in the log*>|<*Location of the log event*> | 2020-02-16 09:42:55,512 \| INFO \| main \| thrift2 server start operation called. \| org.apache.hadoop.hbase.thrift2.ThriftServer.main(ThriftServer.java:421)                                                        |
   +------------+--------------+------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
