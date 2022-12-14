:original_name: mrs_01_0789.html

.. _mrs_01_0789:

DBService Log Overview
======================

Log Description
---------------

**Log path**: The default storage path of DBService log files is **/var/log/Bigdata/dbservice**.

-  GaussDB: **/var/log/Bigdata/dbservice/DB** (GaussDB run log directory), **/var/log/Bigdata/dbservice/scriptlog/gaussdbinstall.log** (GaussDB installation log), and **/var/log/gaussdbuninstall.log** (GaussDB uninstallation log).

-  HA: **/var/log/Bigdata/dbservice/ha/runlog** (HA run log directory) and **/var/log/Bigdata/dbservice/ha/scriptlog** (HA script log directory)

-  DBServer: **/var/log/Bigdata/dbservice/healthCheck** (Directory of service and process health check logs)

   **/var/log/Bigdata/dbservice/scriptlog** (run log directory), **/var/log/Bigdata/audit/dbservice/** (audit log directory)

Log archive rule: The automatic DBService log compression function is enabled. By default, when the size of logs exceeds 1 MB, logs are automatically compressed into a log file named in the following format: *<Original log file name>-[No.]*\ **.gz**. A maximum of 20 latest compressed files are reserved.

.. note::

   Log archive rules cannot be modified.

.. table:: **Table 1** DBService log list

   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   | Type                  | Log File Name              | Description                                                                                                                       |
   +=======================+============================+===================================================================================================================================+
   | DBServer run log      | dbservice_serviceCheck.log | Run log file of the service check script                                                                                          |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | dbservice_processCheck.log | Run log file of the process check script                                                                                          |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | backup.log                 | Run logs of backup and restoration operations (The DBService backup and restoration operations need to be performed.)             |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | checkHaStatus.log          | Log file of HA check records                                                                                                      |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | cleanupDBService.log       | Uninstallation log file (You need to uninstall DBService logs.)                                                                   |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | componentUserManager.log   | Log file that records the adding and deleting operations on the database by users                                                 |
   |                       |                            |                                                                                                                                   |
   |                       |                            | (Services that depend on DBService need to be added.)                                                                             |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | install.log                | Installation log file                                                                                                             |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | preStartDBService.log      | Pre-startup log file                                                                                                              |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | start_dbserver.log         | DBServer startup operation log file (DBService needs to be started.)                                                              |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | stop_dbserver.log          | DBServer stop operation log file (DBService needs to be stopped.)                                                                 |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | status_dbserver.log        | Log file of the DBServer status check (You need to execute the **$DBSERVICE_HOME/sbin/status-dbserver.sh** script.)               |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | modifyPassword.log         | Run log file of changing the DBService password script. (You need to execute the **$DBSERVICE_HOME/sbin/modifyDBPwd.sh** script.) |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | modifyDBPwd_yyyy-mm-dd.log | Run log file that records the DBService password change tool                                                                      |
   |                       |                            |                                                                                                                                   |
   |                       |                            | (You need to execute the **$DBSERVICE_HOME/sbin/modifyDBPwd.sh** script.)                                                         |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | dbserver_switchover.log    | Log for DBServer to execute the active/standby switchover script (the active/standby switchover needs to be performed)            |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   | GaussDB run log       | gaussdb.log                | Log file that records database running information                                                                                |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | gs_ctl-current.log         | Log file that records operations performed by using the **gs_ctl** tool                                                           |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | gs_guc-current.log         | Log file that records operations, mainly parameter modification performed by using the **gs_guc** tool                            |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | gaussdbinstall.log         | GaussDB installation log file                                                                                                     |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | gaussdbuninstall.log       | GaussDB uninstallation log file                                                                                                   |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   | HA script run log     | floatip_ha.log             | Log file that records the script of floating IP addresses                                                                         |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | gaussDB_ha.log             | Log file that records the script of GaussDB resources                                                                             |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | ha_monitor.log             | Log file that records the HA process monitoring information                                                                       |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | send_alarm.log             | Alarm sending log file                                                                                                            |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |                       | ha.log                     | HA run log file                                                                                                                   |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   | DBService audit log   | dbservice_audit.log        | Audit log file that records DBService operations, such as backup and restoration operations                                       |
   +-----------------------+----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+

Log Format
----------

The following table lists the DBService log formats.

.. table:: **Table 2** Log format

   +-----------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type      | Format                                                                                                                                                                      | Example                                                                                                                                              |
   +===========+=============================================================================================================================================================================+======================================================================================================================================================+
   | Run log   | [<*yyyy-MM-dd HH:mm:ss*>] <*Log level*>: [< *Name of the script that generates the log*: *Line number* >]: < *Message in the log*>                                          | [2020-12-19 15:56:42] INFO [postinstall.sh:653] Is cloud flag is false. (main)                                                                       |
   +-----------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Audit log | [<*yyyy-MM-dd HH:mm:ss,SSS*>] UserName:<*Username*> UserIP:<*User IP address*> Operation:<*Operation content*> Result:<*Operation results*> Detail:<*Detailed information*> | [2020-05-26 22:00:23] UserName:omm UserIP:192.168.10.21 Operation:DBService data backup Result: SUCCESS Detail: DBService data backup is successful. |
   +-----------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
