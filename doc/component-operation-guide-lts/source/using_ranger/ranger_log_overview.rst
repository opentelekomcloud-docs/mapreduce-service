:original_name: mrs_01_1865.html

.. _mrs_01_1865:

Ranger Log Overview
===================

Log Description
---------------

**Log path**: The default storage path of Ranger logs is **/var/log/Bigdata/ranger/**\ *Role name*.

-  RangerAdmin: /var/log/Bigdata/ranger/rangeradmin (run logs)
-  TagSync: /var/log/Bigdata/ranger/tagsync (run logs)
-  UserSync: /var/log/Bigdata/ranger/usersync (run logs)

**Log archive rule**: The automatic compression and archive function is enabled for Ranger logs. By default, when the size of a log file exceeds 20 MB, the log file is automatically compressed. The naming rule of the compressed log file is as follows: *<Original log file name>-<yyyy-mm-dd_hh-mm-ss>.[ID]*\ **.log.zip**. A maximum of 20 compressed file are retained.

.. table:: **Table 1** HDFS log list

   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   | Type                     | Name                              | Description                                                         |
   +==========================+===================================+=====================================================================+
   | RangerAdmin run log file | access_log.\ *<DATE>*.log         | Tomcat access log                                                   |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | catalina.out                      | Tomcat service run log                                              |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | gc-worker.log                     | RangerAdmin garbage collection (GC) log                             |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | postinstallDetail.log             | Work log generated after an instance is started before installation |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | prestartDetail.log                | Log that records preparations before instance startup               |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | ranger-admin-*<hostname>*.log     | RangerAdmin run log                                                 |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | ranger_admin_sql-*<hostname>*.log | RangerAdmin log used to retrieve DBService                          |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | startDetail.log                   | Instance startup log                                                |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   | TagSync run log          | cleanupDetail.log                 | Instance clearing log                                               |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | gc-worker.log                     | GC log file of an instance                                          |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | postinstallDetail.log             | Work log generated after an instance is started before installation |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | prestartDetail.log                | Log that records preparations before instance startup               |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | ranger-tagsync-*<hostname>*.log   | TagSync run log                                                     |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | startDetail.log                   | Instance startup log                                                |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | tagsync.out                       | TagSync run log                                                     |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   | UserSync run log         | auth.log                          | UnixAuth service run log                                            |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | cleanupDetail.log                 | Instance clearing log                                               |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | gc-worker.log                     | GC log file of an instance                                          |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | postinstallDetail.log             | Work log generated after an instance is started before installation |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | prestartDetail.log                | Log that records preparations before instance startup               |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | ranger-usersync-*<hostname>*.log  | UserSync run log                                                    |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+
   |                          | startDetail.log                   | Instance startup log                                                |
   +--------------------------+-----------------------------------+---------------------------------------------------------------------+

Log Levels
----------

:ref:`Table 2 <mrs_01_1865__en-us_topic_0000001219148931_t9a69df8da9a84f41bb6fd3e008d7a3b8>` describes the log levels provided by HDFS. The priorities of log levels are FATAL, ERROR, WARN, INFO, and DEBUG in descending order. Logs whose levels are higher than or equal to the specified level are printed. The number of printed logs decreases as the specified log level increases.

.. _mrs_01_1865__en-us_topic_0000001219148931_t9a69df8da9a84f41bb6fd3e008d7a3b8:

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

#. Log in to FusionInsight Manager.
#. Choose **Cluster** > **Services** > **Ranger** > **Configurations**.
#. Select **All Configurations**.
#. On the menu bar on the left, select the log menu of the target role.
#. Select a desired log level.
#. Click **Save**. In the displayed dialog box, click **OK** to make the configuration take effect.

   .. note::

      The configurations take effect immediately without the need to restart the service.

Log Formats
-----------

The following table lists the Ranger log formats.

.. table:: **Table 3** Log formats

   +---------+--------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type    | Format                                                                                                                                                 | Example Value                                                                                                                                        |
   +=========+========================================================================================================================================================+======================================================================================================================================================+
   | Run log | <*yyyy-MM-dd HH:mm:ss,SSS*>|<*Log level*>|<*Name of the thread that generates the log*>|<*Message in the log*>|<*Location where the log event occurs*> | 2020-04-29 20:09:28,543 \| INFO \| http-bio-21401-exec-56 \| Request comes from API call, skip cas filter. \| CasAuthenticationFilterWrapper.java:25 |
   +---------+--------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
