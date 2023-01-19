:original_name: mrs_01_2071.html

.. _mrs_01_2071:

Log Overview
============

Log Description
---------------

**Log path**: The default save path of Tez logs is **/var/log/Bigdata/tez/**\ *role name*.

TezUI: **/var/log/Bigdata/tez/tezui** (run logs) and **/var/log/Bigdata/audit/tez/tezui** (audit logs)

**Log archive rule**: The automatic compression and archiving function of Tez is enabled. By default, when the size of a log file exceeds 20 MB (which is adjustable), the log file is automatically compressed. The naming rule of the compressed log file is as follows: <*Original log file name*>-<*yyyy-mm-dd_hh-mm-ss*>.[*ID*].\ **log.zip** A maximum of 20 latest compressed files are retained. The number of compressed files and compression threshold can be configured.

.. table:: **Table 1** Tez log list

   +-----------+-----------------------------------+---------------------------------------------------------------------+
   | Log Type  | Name                              | Description                                                         |
   +===========+===================================+=====================================================================+
   | Run log   | tezui.out                         | Log file that records TezUI running environment information         |
   +-----------+-----------------------------------+---------------------------------------------------------------------+
   |           | tezui.log                         | Run log of the TezUI process                                        |
   +-----------+-----------------------------------+---------------------------------------------------------------------+
   |           | tezui-omm-<*Date*>-gc.log.<*No.*> | GC log of the TezUI process                                         |
   +-----------+-----------------------------------+---------------------------------------------------------------------+
   |           | prestartDetail.log                | Work logs generated before the TezUI is started                     |
   +-----------+-----------------------------------+---------------------------------------------------------------------+
   |           | check-serviceDetail.log           | Log file that records whether the TezUI service starts successfully |
   +-----------+-----------------------------------+---------------------------------------------------------------------+
   |           | postinstallDetail.log             | Work logs after the TezUI is installed                              |
   +-----------+-----------------------------------+---------------------------------------------------------------------+
   |           | startDetail.log                   | Startup log of the TezUI process                                    |
   +-----------+-----------------------------------+---------------------------------------------------------------------+
   |           | stopDetail.log                    | Stop log of the TezUI process                                       |
   +-----------+-----------------------------------+---------------------------------------------------------------------+
   | Audit log | tezui-audit.log                   | TezUI audit log                                                     |
   +-----------+-----------------------------------+---------------------------------------------------------------------+

Log Level
---------

:ref:`Table 2 <mrs_01_2071__en-us_topic_0000001173789436_t91045e1a946a46b4bac39028af62f3ad>` describes the log levels supported by TezUI.

Levels of run logs are ERROR, WARN, INFO, and DEBUG from the highest to the lowest priority. Run logs of equal or higher levels are recorded. The higher the specified log level, the fewer the logs recorded.

.. _mrs_01_2071__en-us_topic_0000001173789436_t91045e1a946a46b4bac39028af62f3ad:

.. table:: **Table 2** Log levels

   +-------+------------------------------------------------------------------------------------------+
   | Level | Description                                                                              |
   +=======+==========================================================================================+
   | ERROR | Logs of this level record error information about system running.                        |
   +-------+------------------------------------------------------------------------------------------+
   | WARN  | Exception information about the current event processing                                 |
   +-------+------------------------------------------------------------------------------------------+
   | INFO  | Logs of this level record normal running status information about the system and events. |
   +-------+------------------------------------------------------------------------------------------+
   | DEBUG | Logs of this level record the system information and system debugging information.       |
   +-------+------------------------------------------------------------------------------------------+

To modify log levels, perform the following operations:

#. Log in to Manager.
#. Choose **Cluster** > **Service** > **Tez** > **Configuration**.
#. Select **All Configurations**.
#. In the navigation pane, choose **TezUI** > **Log**.
#. Select a desired log level.
#. Click **Save**. In the dialog box that is displayed, click **OK** to save the configuration.
#. Click **Instance**, select the **TezUI** role, choose **More** > **Restart Instance**, enter the user password, and click **OK** in the dialog box that is displayed.
#. Wait until the instance is restarted for the configuration to take effect.

Log Format
----------

The following table lists the Tez log formats.

.. table:: **Table 3** Log formats

   +------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Log Type   | Format                                                                                                                                                              | Example                                                                                                                                                                                                                                                                             |
   +============+=====================================================================================================================================================================+=====================================================================================================================================================================================================================================================================================+
   | Run log    | <yyyy-MM-dd HH:mm:ss,SSS>|<LogLevel>|<Thread that generates the log>|<Message in the log>|<Location of the log event>                                               | 2020-07-31 11:44:21,378 \| INFO \| TezUI-health-check \| Start health check \| com.XXX.tez.HealthCheck.run(HealthCheck.java:30)                                                                                                                                                     |
   +------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Audit logs | <yyyy-MM-dd HH:mm:ss,SSS>|<LogLevel>|<Thread that generates the log>|<User Name><User IP><Time><Operation><Resource><Result><Detail >|< Location of the log event > | 2018-12-24 12:16:25,319 \| INFO \| HiveServer2-Handler-Pool: Thread-185 \| UserName=hive UserIP=10.153.2.204 Time=2018/12/24 12:16:25 Operation=CloseSession Result=SUCCESS Detail= \| org.apache.hive.service.cli.thrift.ThriftCLIService.logAuditEvent(ThriftCLIService.java:434) |
   +------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
