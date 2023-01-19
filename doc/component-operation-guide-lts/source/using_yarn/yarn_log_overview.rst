:original_name: mrs_01_0870.html

.. _mrs_01_0870:

Yarn Log Overview
=================

Log Description
---------------

The default paths for saving Yarn logs are as follows:

-  ResourceManager: **/var/log/Bigdata/yarn/rm** (run logs) and **/var/log/Bigdata/audit/yarn/rm** (audit logs)
-  NodeManager: **/var/log/Bigdata/yarn/nm** (run logs) and **/var/log/Bigdata/audit/yarn/nm** (audit logs)

Log archive rule: The automatic compression and archive function is enabled for Yarn logs. By default, when the size of a log file exceeds 50 MB, the log file is automatically compressed. The naming rule of the compressed log file is as follows: *<Original log file name>-<yyyy-mm-dd_hh-mm-ss>.[ID]*\ **.log.zip**. A maximum of 100 latest compressed files are retained. The number of compressed files can be configured on Manager.

**Log archive rule**:

.. table:: **Table 1** Yarn log list

   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   | Log Type              | Log File Name                                   | Description                                                                                          |
   +=======================+=================================================+======================================================================================================+
   | Run log               | hadoop-<SSH_USER>-<process_name>-<hostname>.log | Yarn component log file, which records most of the logs generated when the Yarn component is running |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | yarn-<SSH_USER>-<process_name>-<hostname>.out   | Log file that records Yarn running environment information                                           |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | <process_name>-<SSH_USER>-<DATE>-<PID>-gc.log   | Garbage collection log file                                                                          |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | yarn-haCheck.log                                | ResourceManager active/standby status detection log file                                             |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | yarn-service-check.log                          | Log file that records the health check details of the Yarn service                                   |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | yarn-start-stop.log                             | Log file that records the startup and stop of the Yarn service                                       |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | yarn-prestart.log                               | Log file that records cluster operations before the Yarn service startup                             |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | yarn-postinstall.log                            | Work log file after installation and before startup of the Yarn service                              |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | hadoop-commission.log                           | Yarn service entry log file                                                                          |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | yarn-cleanup.log                                | Log file that records the cleanup operation during uninstallation of the Yarn service                |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | yarn-refreshqueue.log                           | Yarn queue refresh log file                                                                          |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | upgradeDetail.log                               | Upgrade log file                                                                                     |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | stderr/stdin/syslog                             | Container log file of the applications running on the Yarn service                                   |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | yarn-application-check.log                      | Check log file of applications running on the Yarn service                                           |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | yarn-appsummary.log                             | Running result log file of applications running on the Yarn service                                  |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | yarn-switch-resourcemanager.log                 | Run log file that records the Yarn active/standby switchover                                         |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | ranger-yarn-plugin-enable.log                   | Log file that records the enabling of Ranger authentication for Yarn                                 |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | yarn-nodemanager-period-check.log               | Periodic check log of Yarn NodeManager                                                               |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | yarn-resourcemanager-period-check.log           | Periodic check log of Yarn ResourceManager                                                           |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | hadoop.log                                      | Hadoop client logs                                                                                   |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | env.log                                         | Environment information log file before the instance is started or stopped.                          |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   | Audit logs            | yarn-audit-<process_name>.log                   | Yarn operation audit log file                                                                        |
   |                       |                                                 |                                                                                                      |
   |                       | ranger-plugin-audit.log                         |                                                                                                      |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+
   |                       | SecurityAuth.audit                              | Yarn security audit log file                                                                         |
   +-----------------------+-------------------------------------------------+------------------------------------------------------------------------------------------------------+

Log Level
---------

:ref:`Table 2 <mrs_01_0870__en-us_topic_0000001173630946_t2815fd56171e4fc792972303da85d63c>` describes the log levels supported by Yarn, including OFF, FATAL, ERROR, WARN, INFO, and DEBUG, from high priority to low. Logs whose levels are higher than or equal to the specified level are printed. The number of printed logs decreases as the specified log level increases.

.. _mrs_01_0870__en-us_topic_0000001173630946_t2815fd56171e4fc792972303da85d63c:

.. table:: **Table 2** Log levels

   +-------+------------------------------------------------------------------------------------------+
   | Level | Description                                                                              |
   +=======+==========================================================================================+
   | FATAL | Logs of this level record critical error information about the current event processing. |
   +-------+------------------------------------------------------------------------------------------+
   | ERROR | Logs of this level record error information about the current event processing.          |
   +-------+------------------------------------------------------------------------------------------+
   | WARN  | Logs of this level record exception information about the current event processing.      |
   +-------+------------------------------------------------------------------------------------------+
   | INFO  | Logs of this level record normal running status information about the system and events. |
   +-------+------------------------------------------------------------------------------------------+
   | DEBUG | Logs of this level record the system as well as system debugging information.            |
   +-------+------------------------------------------------------------------------------------------+

To modify log levels, perform the following operations:

#. Go to the **All Configurations** page of the Yarn service by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.
#. On the menu bar on the left, select the log menu of the target role.
#. Select a desired log level.
#. Click **Save Configuration**. In the dialog box that is displayed, click **OK** to make the setting take effect.

   .. note::

      The configurations take effect immediately without the need to restart the service.

Log Format
----------

The following table lists the Yarn log formats.

.. table:: **Table 3** Log formats

   +-----------+------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Log Type  | Format                                                                                                                       | Example                                                                                                                                                                                                                                 |
   +===========+==============================================================================================================================+=========================================================================================================================================================================================================================================+
   | Run log   | <yyyy-MM-dd HH:mm:ss,SSS>|<Log Level>|<*Thread that generates the log*>|<*Message in the log*>|<*Location of the log event*> | 2014-09-26 14:18:59,109 \| INFO \| main \| Client environment:java.compiler=<NA> \| org.apache.zookeeper.Environment.logEnv(Environment.java:100)                                                                                       |
   +-----------+------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Audit log | <yyyy-MM-dd HH:mm:ss,SSS>|<Log Level>|<*Thread that generates the log*>|<*Message in the log*>|<*Location of the log event*> | 2014-09-26 14:24:43,605 \| INFO \| main-EventThread \| USER=omm OPERATION=refreshAdminAcls TARGET=AdminService RESULT=SUCCESS \| org.apache.hadoop.yarn.server.resourcemanager.RMAuditLogger$LogLevel$6.printLog(RMAuditLogger.java:91) |
   +-----------+------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
