:original_name: mrs_01_1744.html

.. _mrs_01_1744:

Introduction to HetuEngine Logs
===============================

Log Description
---------------

**Log paths:**

The HetuEngine logs are stored in **/var/log/Bigdata/hetuengine/** and **/var/log/Bigdata/audit/hetuengine/**.

**Log archiving rules**:

Log archiving rules use the FixedWindowRollingPolicy policy. The maximum size of a single file and the maximum number of log archive files can be configured. The rules are as follows:

-  When the size of a single file exceeds the default maximum value, a new compressed archive file is generated. The naming rule of the compressed archive log file is as follows: *<Original log name>*.\ *[ID]*.log.gz.
-  When the number of log archive files reaches the maximum value, the earliest log file is deleted.

By default, the maximum size of an audit log file is 30 MB, and the maximum number of log archive files is 20.

By default, the maximum size of a run log file is 100 MB, and the maximum number of log archive files is 20.

To change the maximum size of a single run log file or audit log file or change the maximum number of log archive files of an instance, perform the following operations:

#. Log in to Manager.
#. Choose **Cluster** > **Services** > **HetuEngine** > **Configurations** > **All Configurations**.
#. In the parameter list of log levels, search for **logback.xml** to view the current run log and audit log configurations of HSBroker, HSConsole, and HSFabric.
#. Select the configuration item to be modified and modify it.
#. Click **Save**, and then click **OK**. The configuration automatically takes effect after about 30 seconds.

.. table:: **Table 1** Log list

   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | Type                                   | Name                                                                                                                     | Description                                                                                |
   +========================================+==========================================================================================================================+============================================================================================+
   | Installation, startup and stopping log | /var/log/Bigdata/hetuengine/hsbroker/prestart.log                                                                        | HSBroker pre-processing script logs before startup                                         |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsbroker/start.log                                                                           | HSBroker Spring Boot startup logs                                                          |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsbroker/stop.log                                                                            | HSBroker stop logs                                                                         |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsbroker/postinstall.log                                                                     | HSBroker post-installation logs                                                            |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsconsole/prestart.log                                                                       | HSConsole pre-processing script logs before startup                                        |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsconsole/start.log                                                                          | HSConsole Spring Boot startup logs                                                         |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsconsole/stop.log                                                                           | HSConsole stop logs                                                                        |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsconsole/postinstall.log                                                                    | HSConsole post-installation logs                                                           |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsfabric/prestart.log                                                                        | HSFabric preprocessing script logs before startup                                          |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsfabric/start.log                                                                           | HSFabric startup logs                                                                      |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsfabric/stop.log                                                                            | HSFabric stop logs                                                                         |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsfabric/postinstall.log                                                                     | HSFabric post-installation logs                                                            |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | Run log                                | /var/log/Bigdata/hetuengine/hsbroker/hsbroker.log                                                                        | HSBroker run logs                                                                          |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsconsole/hsconsole.log                                                                      | HSConsole run logs                                                                         |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsfabric/hsfabric.log                                                                        | HSFabric run logs                                                                          |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | hdfs://hacluster/hetuserverhistory/*Tenant*/*Coordinator or worker*/application_ID/container_ID/yyyyMMdd/server.log      | Run logs of the HetuEngine compute instance                                                |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | Status check log                       | /var/log/Bigdata/hetuengine/hsbroker/service_check.log                                                                   | HSBroker health check logs                                                                 |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsbroker/service_getstate.log                                                                | HSBroker status check logs                                                                 |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/availability-check.log                                                                       | Status check logs indicating whether the HetuEngine service is available                   |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsconsole/service_getstate.log                                                               | HSConsole status check logs                                                                |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsfabric/service_getstate.log                                                                | HSFabric status check logs                                                                 |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | Audit log                              | /var/log/Bigdata/audit/hetuengine/hsbroker/hsbroker-audit.log                                                            | HSBroker audit logs                                                                        |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/audit/hetuengine/hsconsole/hsconsole-audit.log                                                          | HSConsole audit logs                                                                       |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | hdfs://hacluster/hetuserverhistory/*Tenant*/coordinator/application_ID/container_ID/yyyyMMdd/hetuserver-engine-audit.log | Audit logs of the HetuEngine compute instance                                              |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/audit/hetuengine/hsfabric/hsfabric-audit.log                                                            | HSFabric audit logs                                                                        |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | Clean log                              | /var/log/Bigdata/hetuengine/hsbroker/cleanup.log                                                                         | HSBroker cleanup script logs                                                               |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsconsole/cleanup.log                                                                        | HSConsole cleanup script logs                                                              |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsfabric/cleanup.log                                                                         | HSFabric cleanup script logs                                                               |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | Initialization log                     | /var/log/Bigdata/hetuengine/hsbroker/hetupg.log                                                                          | HSBroker metadata initialization logs                                                      |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/hsconsole/hetupg.log                                                                         | HSConsole connection metadata logs.                                                        |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   |                                        | /var/log/Bigdata/hetuengine/ranger-presto-plugin-enable.log                                                              | Operation logs generated when the Ranger plug-in is integrated into the HetuEngine kernel. |
   +----------------------------------------+--------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+

Log Level
---------

:ref:`Table 2 <mrs_01_1744__en-us_topic_0000001219351035_table589895023911>` describes the log levels provided by HetuEngine. The priorities of log levels are OFF, ERROR, WARN, INFO, and DEBUG in descending order. Logs whose levels are higher than or equal to the specified level are printed. The number of printed logs decreases as the specified log level increases.

.. _mrs_01_1744__en-us_topic_0000001219351035_table589895023911:

.. table:: **Table 2** Log levels

   +-------+------------------------------------------------------------------------------------------+
   | Level | Description                                                                              |
   +=======+==========================================================================================+
   | OFF   | Logs of this level record no logs.                                                       |
   +-------+------------------------------------------------------------------------------------------+
   | ERROR | Logs of this level record error information about the current event processing.          |
   +-------+------------------------------------------------------------------------------------------+
   | WARN  | Logs of this level record exception information about the current event processing.      |
   +-------+------------------------------------------------------------------------------------------+
   | INFO  | Logs of this level record normal running status information about the system and events. |
   +-------+------------------------------------------------------------------------------------------+
   | DEBUG | Logs of this level record the system information and system debugging information.       |
   +-------+------------------------------------------------------------------------------------------+

To change the run log or audit log level of an instance, perform the following steps:

#. Log in to FusionInsight Manager.
#. Choose **Cluster** > **Services** > **HetuEngine** > **Configurations** > **All Configurations**.
#. In the parameter list of log levels, search for **logback.xml** to view the current run log and audit log levels of HSBroker, HSConsole, and HSFabric.
#. Select a desired log level.
#. Click **Save**, and then click **OK**. The configuration automatically takes effect after about 30 seconds.

To change the HetuEngine Coordinator/Worker log level, perform the following steps:

#. Log in to FusionInsight Manager.
#. Choose **Cluster** > **Services** > **HetuEngine** > **Configurations** > **All Configurations**.
#. In the parameter list of log levels, search for **log.properties** to view the current log levels.
#. Select a desired log level.
#. Click **Save**, and then click **OK**. Wait until the operation is successful.
#. Choose **Cluster** > **Services** > **HetuEngine** > **Instance**, click the HSBroker instance in the role list, and choose **More** > **Restart Instance**.
#. After the HSBroker instance is restarted, choose **Cluster** > **Services** > **HetuEngine**. On the overview page, click the link next to **HSConsole WebUI** to go to the compute instance page.
#. Select a compute instance and click **Stop**. After the instance is stopped, click **Start** to restart it.
