:original_name: mrs_01_1843.html

.. _mrs_01_1843:

Oozie Log Overview
==================

Log Description
---------------

**Log path**: The default storage paths of Oozie log files are as follows:

-  Run log: **/var/log/Bigdata/oozie**
-  Audit log: **/var/log/Bigdata/audit/oozie**

**Log archiving rule**: Oozie logs are classified into run logs, script logs, and audit logs. The maximum size of a run log file is 20 MB, and a maximum of 20 run log files can be reserved. The maximum size of an audit log file is 20 MB, and a maximum of 20 audit log files can be reserved.

.. note::

   A compressed log file is generated for **oozie.log** every hour. 720 compressed files (log files of one month) are retained by default.

.. table:: **Table 1** Oozie log list

   +-------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   | Log Type    | Log File Name                        | Description                                                                                                         |
   +=============+======================================+=====================================================================================================================+
   | Run log     | jetty.log                            | Oozie built-in jetty server log file, which is used to process the request and response information of OozieServlet |
   +-------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   |             | jetty.out                            | Oozie process startup log file                                                                                      |
   +-------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   |             | oozie_db_temp.log                    | Oozie database connection log                                                                                       |
   +-------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   |             | oozie-instrumentation.log            | Oozie dashboard log file, which records the Oozie running status and configuration information of each component    |
   +-------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   |             | oozie-jpa.log                        | openJPa run log file                                                                                                |
   +-------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   |             | oozie.log                            | Oozie run log file                                                                                                  |
   +-------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   |             | oozie-<SSH_USER>-<DATE>-<PID>-gc.log | Log file that records the garbage collection of the Oozie service                                                   |
   +-------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   |             | oozie-ops.log                        | Oozie operation log file                                                                                            |
   +-------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   |             | check-serviceDetail.log              | Oozie health check logs                                                                                             |
   +-------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   |             | oozie-error.log                      | Oozie running error logs                                                                                            |
   +-------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   |             | threadDump-<DATE>.log                | Log file that records stack information when the service process exits normally                                     |
   +-------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   | Script logs | postinstallDetail.log                | Work log file generated after the installation and before the startup                                               |
   +-------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   |             | prestartDetail.log                   | Pre-startup log file                                                                                                |
   +-------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   |             | startDetail.log                      | Service startup log file                                                                                            |
   +-------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   |             | stopDetail.log                       | Service stop log file                                                                                               |
   +-------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   |             | upload-sharelib.log                  | Operation logs uploaded by **sharelib**                                                                             |
   +-------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   | Audit log   | oozie-audit.log                      | Audit log                                                                                                           |
   +-------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------+

Log Level
---------

:ref:`Table 2 <mrs_01_1843__tf6a4761259f54fb3b310d3e79035d06a>` describes the log levels provided by Oozie.

The priorities of log levels are ERROR, WARN, INFO, and DEBUG in descending order. Logs whose levels are higher than or equal to the set level are printed. The number of printed logs decreases as the configured log level increases.

.. _mrs_01_1843__tf6a4761259f54fb3b310d3e79035d06a:

.. table:: **Table 2** Log levels

   +-------+-----------------------------------------------------------------------------------------------------------+
   | Level | Description                                                                                               |
   +=======+===========================================================================================================+
   | ERROR | Logs of this level record abnormal information about events that cause process exceptions.                |
   +-------+-----------------------------------------------------------------------------------------------------------+
   | WARN  | Logs of this level record exception information about the current event processing.                       |
   +-------+-----------------------------------------------------------------------------------------------------------+
   | INFO  | Logs of this level record normal running status information about the system and events.                  |
   +-------+-----------------------------------------------------------------------------------------------------------+
   | DEBUG | Logs of this level record system information and information about database underlying data transmission. |
   +-------+-----------------------------------------------------------------------------------------------------------+

To modify log levels, perform the following operations:

#. Log in to FusionInsight Manager.
#. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Oozie** > **Configurations**.
#. Select **All Configurations**.
#. On the menu bar on the left, select the log menu of the target role.
#. Select a desired log level.
#. Click **Save**, and then click **OK**. The settings take effect after the processing is complete.

Log Formats
-----------

The following table lists the Oozie log formats.

.. table:: **Table 3** Log formats

   +-------------+-----------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Log Type    | Format                                                                                                                | Example                                                                                                                                                                                                                                                                                          |
   +=============+=======================================================================================================================+==================================================================================================================================================================================================================================================================================================+
   | Run log     | *<yyyy-MM-dd HH:mm:ss,SSS><Log level><Location where the log event occurs><Log level><Message in the log>*            | 2015-05-29 21:01:45,268 INFO StatusTransitService$StatusTransitRunnable:539 - USER[-] GROUP[-] Released lock for [org.apache.oozie.service.StatusTransitService]                                                                                                                                 |
   +-------------+-----------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Script logs | *<yyyy-MM-dd HH:mm:ss,SSS><Host name > <Log level > <Message in the log>*                                             | 2015-06-01 17:18:03 001 suse11-192-168-0-111 oozie INFO Running oozie service check script                                                                                                                                                                                                       |
   +-------------+-----------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Audit log   | *<yyyy-MM-dd HH:mm:ss,SSS>|<Log Level>|< Thread name \| \| Message in the log \| Location where the log event occurs* | 2015-06-01 22:38:41,323 \| INFO \| http-bio-21003-exec-8 \| IP [192.168.0.111] USER [null], GROUP [null], APP [null], JOBID [null], OPERATION [null], PARAMETER [null], RESULT [SUCCESS], HTTPCODE [200], ERRORCODE [null], ERRORMESSAGE [null] \| org.apache.oozie.util.XLog.log(XLog.java:539) |
   +-------------+-----------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
