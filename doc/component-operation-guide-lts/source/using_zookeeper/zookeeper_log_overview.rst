:original_name: mrs_01_2106.html

.. _mrs_01_2106:

ZooKeeper Log Overview
======================

Log Description
---------------

**Log path**: **/var/log/Bigdata/zookeeper/quorumpeer** (Run log), **/var/log/Bigdata/audit/zookeeper/quorumpeer** (Audit log)

**Log archive rule**: The automatic ZooKeeper log compression function is enabled. By default, when the size of logs exceeds 30 MB, logs are automatically compressed into a log file. A maximum of 20 compressed file can be reserved. The number of compressed files can be configured on Manager.

.. table:: **Table 1** ZooKeeper log list

   +-----------+----------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | Log Type  | Log File Name                                      | Description                                                                                               |
   +===========+====================================================+===========================================================================================================+
   | Run logs  | zookeeper-<SSH_USER>-<process_name>-<hostname>.log | ZooKeeper system log file, which records most of the logs generated when the ZooKeeper system is running. |
   +-----------+----------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   |           | check-serviceDetail.log                            | Log that records whether the ZooKeeper service starts successfully.                                       |
   +-----------+----------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   |           | zookeeper-<SSH_USER>-<DATA>-<PID>-gc.log           | ZooKeeper garbage collection log file                                                                     |
   +-----------+----------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   |           | instanceHealthDetail.log                           | Log that records the health check details of ZooKeeper instance                                           |
   +-----------+----------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   |           | zookeeper-omm-server-<hostname>.out                | Log indicating that ZooKeeper unexpectedly quits                                                          |
   +-----------+----------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   |           | zk-err-<zkpid>.log                                 | ZooKeeper fatal error log                                                                                 |
   +-----------+----------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   |           | java_pid<zkpid>.hprof                              | ZooKeeper memory overflow log                                                                             |
   +-----------+----------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   |           | funcDetail.log                                     | ZooKeeper instance startup log                                                                            |
   +-----------+----------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   |           | zookeeper-period-check.log                         | Health check log of the ZooKeeper instance                                                                |
   +-----------+----------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | Audit Log | zk-audit-quorumpeer.log                            | ZooKeeper operation audit log                                                                             |
   +-----------+----------------------------------------------------+-----------------------------------------------------------------------------------------------------------+

Log levels
----------

:ref:`Table 2 <mrs_01_2106__en-us_topic_0000001219029649_tbae56afd6a3d4eb5b6260b7d0fd10cbf>` describes the log levels supported by ZooKeeper. The priorities of log levels are FATAL, ERROR, WARN, INFO, and DEBUG in descending order. Logs whose levels are higher than or equal to the specified level are printed. The number of printed logs decreases as the specified log level increases.

.. _mrs_01_2106__en-us_topic_0000001219029649_tbae56afd6a3d4eb5b6260b7d0fd10cbf:

.. table:: **Table 2** Log levels

   +-------+-------------------------------------------------------------------------------------------------------------------------+
   | Level | Description                                                                                                             |
   +=======+=========================================================================================================================+
   | FATAL | Logs of this level record fatal error information about the current event processing that may result in a system crash. |
   +-------+-------------------------------------------------------------------------------------------------------------------------+
   | ERROR | Error information about the current event processing, which indicates that system running is abnormal.                  |
   +-------+-------------------------------------------------------------------------------------------------------------------------+
   | WARN  | Abnormal information about the current event processing. These abnormalities will not result in system faults.          |
   +-------+-------------------------------------------------------------------------------------------------------------------------+
   | INFO  | Logs of this level record normal running status information about the system and events.                                |
   +-------+-------------------------------------------------------------------------------------------------------------------------+
   | DEBUG | Logs of this level record the system information and system debugging information.                                      |
   +-------+-------------------------------------------------------------------------------------------------------------------------+

To modify log levels, perform the following operations:

#. Go to the **All Configurations** page of the ZooKeeper service by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.
#. On the menu bar on the left, select the log menu of the target role.
#. Select a desired log level.
#. Click **Save**. In the displayed dialog box, click **OK** to make the configuration take effect.

   .. note::

      The configurations take effect immediately without the need to restart the service.

Log Format
----------

The following table lists the ZooKeeper log formats.

.. table:: **Table 3** Log Format

   +-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Log Type        | Component       | Format                                                                                                                                                 | Example                                                                                                                                                                                                                                                                   |
   +=================+=================+========================================================================================================================================================+===========================================================================================================================================================================================================================================================================+
   | Run logs        | zookeeper       | <*yyyy-MM-dd HH:mm:ss,SSS*>|<*Log level*>|<*Name of the thread that generates the log*>|<*Message in the log*>|<*Location where the log event occurs*> | 2020-01-20 16:33:43,816 \| INFO \| main \| Defaulting to majority quorums \| org.apache.zookeeper.server.quorum.QuorumPeerConfig.parseProperties(QuorumPeerConfig.java:335)                                                                                               |
   |                 |                 |                                                                                                                                                        |                                                                                                                                                                                                                                                                           |
   |                 | quorumpeer      |                                                                                                                                                        |                                                                                                                                                                                                                                                                           |
   +-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Audit logs      | zookeeper       | <*yyyy-MM-dd HH:mm:ss,SSS*>|<*Log level*>|<*Name of the thread that generates the log*>|<*Message in the log*>|<*Location where the log event occurs*> | 2020-01-20 16:33:54,313 \| INFO \| CommitProcessor:13 \| session=0xd4b0679daea0000 ip=10.177.112.145 operation=create znode target=ZooKeeperServer znode=/zk-write-test-2 result=success \| org.apache.zookeeper.ZKAuditLogger$LogLevel$5.printLog(ZKAuditLogger.java:70) |
   |                 |                 |                                                                                                                                                        |                                                                                                                                                                                                                                                                           |
   |                 | quorumpeer      |                                                                                                                                                        |                                                                                                                                                                                                                                                                           |
   +-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
