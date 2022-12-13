:original_name: mrs_01_1081.html

.. _mrs_01_1081:

Introduction to Flume Logs
==========================

Log Description
---------------

**Log path**: The default path of Flume log files is **/var/log/Bigdata/**\ *Role name*.

-  FlumeServer: **/var/log/Bigdata/flume/flume**
-  FlumeClient: **/var/log/Bigdata/flume-client-n/flume**
-  MonitorServer: **/var/log/Bigdata/flume/monitor**

**Log archive rule**: The automatic Flume log compression function is enabled. By default, when the size of logs exceeds 50 MB , logs are automatically compressed into a log file named in the following format: *<Original log file name>-<yyyy-mm-dd_hh-mm-ss>.[ID]*\ **.log.zip**. A maximum of 20 latest compressed files are reserved. The number of compressed files can be configured on the Manager portal.

.. table:: **Table 1** Flume log list

   +----------+-------------------------------------+---------------------------------------------------------------------+
   | Type     | Name                                | Description                                                         |
   +==========+=====================================+=====================================================================+
   | Run logs | /flume/flumeServer.log              | Log file that records FlumeServer running environment information.  |
   +----------+-------------------------------------+---------------------------------------------------------------------+
   |          | /flume/install.log                  | FlumeServer installation log file                                   |
   +----------+-------------------------------------+---------------------------------------------------------------------+
   |          | /flume/flumeServer-gc.log.\ *<No.>* | GC log file of the FlumeServer process                              |
   +----------+-------------------------------------+---------------------------------------------------------------------+
   |          | /flume/prestartDvietail.log         | Work log file before the FlumeServer startup                        |
   +----------+-------------------------------------+---------------------------------------------------------------------+
   |          | /flume/startDetail.log              | Startup log file of the Flume process                               |
   +----------+-------------------------------------+---------------------------------------------------------------------+
   |          | /flume/stopDetail.log               | Shutdown log file of the Flume process                              |
   +----------+-------------------------------------+---------------------------------------------------------------------+
   |          | /monitor/monitorServer.log          | Log file that records MonitorServer running environment information |
   +----------+-------------------------------------+---------------------------------------------------------------------+
   |          | /monitor/startDetail.log            | Startup log file of the MonitorServer process                       |
   +----------+-------------------------------------+---------------------------------------------------------------------+
   |          | /monitor/stopDetail.log             | Shutdown log file of the MonitorServer process                      |
   +----------+-------------------------------------+---------------------------------------------------------------------+
   |          | function.log                        | External function invoking log file                                 |
   +----------+-------------------------------------+---------------------------------------------------------------------+

Log Level
---------

:ref:`Table 2 <mrs_01_1081__tc09b739e3eb34797a6da936a37654e97>` describes the log levels supported by Flume.

Levels of run logs are FATAL, ERROR, WARN, INFO, and DEBUG from the highest to the lowest priority. Run logs of equal or higher levels are recorded. The higher the specified log level, the fewer the logs recorded.

.. _mrs_01_1081__tc09b739e3eb34797a6da936a37654e97:

.. table:: **Table 2** Log level

   +---------+-------+------------------------------------------------------------------------------------------+
   | Type    | Level | Description                                                                              |
   +=========+=======+==========================================================================================+
   | Run log | FATAL | Logs of this level record critical error information about system running.               |
   +---------+-------+------------------------------------------------------------------------------------------+
   |         | ERROR | Logs of this level record error information about system running.                        |
   +---------+-------+------------------------------------------------------------------------------------------+
   |         | WARN  | Logs of this level record exception information about the current event processing.      |
   +---------+-------+------------------------------------------------------------------------------------------+
   |         | INFO  | Logs of this level record normal running status information about the system and events. |
   +---------+-------+------------------------------------------------------------------------------------------+
   |         | DEBUG | Logs of this level record the system information and system debugging information.       |
   +---------+-------+------------------------------------------------------------------------------------------+

To modify log levels, perform the following operations:

#. Go to the **All Configurations** page of Flume by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.
#. On the menu bar on the left, select the log menu of the target role.
#. Select a desired log level.
#. Save the configuration. In the displayed dialog box, click **OK** to make the configurations take effect.

.. note::

   The configurations take effect immediately without the need to restart the service.

Log Format
----------

The following table lists the Flume log formats.

.. table:: **Table 3** Log format

   +----------+--------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type     | Format                                                                                                                                                 | Example                                                                                                                                          |
   +==========+========================================================================================================================================================+==================================================================================================================================================+
   | Run logs | <*yyyy-MM-dd HH:mm:ss,SSS*>|<*Log level*>|<*Name of the thread that generates the log*>|<*Message in the log*>|<*Location where the log event occurs*> | 2014-12-12 11:54:57,316 \| INFO \| [main] \| log4j dynamic load is start. \| org.apache.flume.tools.LogDynamicLoad.start(LogDynamicLoad.java:59) |
   +----------+--------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   |          | <*yyyy-MM-dd HH:mm:ss,SSS*><*Username*><*User IP*><*Time*><*Operation*><*Resource*><*Result*><*Detail>*                                                | 2014-12-12 23:04:16,572 \| INFO \| [SinkRunner-PollingRunner-DefaultSinkProcessor] \| SRCIP=null OPERATION=close                                 |
   +----------+--------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
