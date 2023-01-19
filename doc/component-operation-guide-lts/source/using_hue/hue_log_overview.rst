:original_name: mrs_01_0147.html

.. _mrs_01_0147:

Hue Log Overview
================

Log Description
---------------

**Log paths**: The default paths of Hue logs are **/var/log/Bigdata/hue** (for storing run logs) and **/var/log/Bigdata/audit/hue** (for storing audit logs).

**Log archive rules**: The automatic compression and archiving function of the Hue logs is enabled. By default, when the size of a log file (**access.log**, **error.log**, **runcpserver.log**, or **hue-audits.log**) exceeds 5 MB, logs are automatically compressed. A maximum of 20 latest compressed files are reserved. The number of compressed files and compression threshold can be configured.

.. table:: **Table 1** Hue log list

   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   | Type      | Log File Name             | Description                                                                               |
   +===========+===========================+===========================================================================================+
   | Run log   | access.log                | Access log file                                                                           |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | error.log                 | Error log file                                                                            |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | gsdb_check.log            | Log file of the GaussDB check information                                                 |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | kt_renewer.log            | Log file of Kerberos authentication                                                       |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | kt_renewer.out.log        | Log file of the abnormal Kerberos authentication logs                                     |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | runcpserver.log           | Log file of operation records                                                             |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | runcpserver.out.log       | Log file of process running exceptions                                                    |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | supervisor.log            | Log file of process startup                                                               |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | supervisor.out.log        | Log file of process startup exceptions                                                    |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | dbDetail.log              | Log file of database initialization                                                       |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | initSecurityDetail.log    | Download initialization log file of the Keytab file                                       |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | postinstallDetail.log     | Work log file generated after the Hue service is installed                                |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | prestartDetail.log        | Prestart log file                                                                         |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | statusDetail.log          | Log file of the Hue health status                                                         |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | startDetail.log           | Startup log                                                                               |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | get-hue-ha.log            | Log file of the Hue HA status                                                             |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | hue-ha-status.log         | Log file of the Hue HA status monitoring                                                  |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | get-hue-health.log        | Log file of the Hue health status                                                         |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | hue-health-check.log      | Log file of the Hue health check                                                          |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | hue-refresh-config.log    | Log file of the Hue configuration update                                                  |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | hue-script-log.log        | Log file of the Hue operations on the Manager console                                     |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | hue-service-check.log     | Log file of the Hue service status monitoring                                             |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | db_pwd.log                | Log that records the changes of the password for Hue to connect to the DBService database |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | modifyDBPwd\_\ *Date*.log | ``-``                                                                                     |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   |           | watch_config_update.log   | Parameter update log file                                                                 |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+
   | Audit log | hue-audits.log            | Audit log file                                                                            |
   +-----------+---------------------------+-------------------------------------------------------------------------------------------+

Log Level
---------

:ref:`Table 2 <mrs_01_0147__en-us_topic_0000001173789706_t85cf40d58c61438a8876c531c55d9f44>` describes the log levels supported by Hue.

Levels of logs are ERROR, WARN, INFO, and DEBUG from the highest to the lowest priority. Run logs of equal or higher levels are recorded. The higher the specified log level, the fewer the logs recorded.

.. _mrs_01_0147__en-us_topic_0000001173789706_t85cf40d58c61438a8876c531c55d9f44:

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

#. Go to the **All Configurations** page of the Hue service by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.
#. In the navigation tree on the left, select **Log** corresponding to the role to be modified.
#. Select the log level to be changed on the right.
#. Save the configuration. In the displayed dialog box, click **OK** to make the configurations take effect.
#. Restart the service or instance whose configuration has expired for the configuration to take effect.

Log Format
----------

The following table lists the Hue log formats:

.. table:: **Table 3** Log formats

   +-----------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type      | Format                                                                                                                                           | Example                                                                                                                                                                                                                                 |
   +===========+==================================================================================================================================================+=========================================================================================================================================================================================================================================+
   | Run log   | <*dd-MM-yy HH:mm:ss,SSS*><*Location where the log event occurs*><*Log level*><*Message in the log*>                                              | [03/Nov/2014 11:57:19 ] middleware \| INFO \| Unloading MimeTypeJSFileFixStreamingMiddleware.                                                                                                                                           |
   +-----------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |           | <*Log level*><*Time format*><*yyyy-MM-dd HH:mm:ss,SSS*><*Location where the log event occurs*><*Message in the log*>                             | INFO : CST 2014-11-06 11:22:52 hue-ha-status.sh : update 4 <= 15:myHostName=10.0.0.250 ACTIVE=10.0.0.250                                                                                                                                |
   +-----------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Audit log | *<UserName><yyyy-MM-dd HH:mm:ss,SSS>< Audit operation description> <Resource parameter> <URL> <Whether to allow> <Audit operation> <IP address>* | {"username": "admin", "eventTime": "2014-11-06 10:28:34", "operationText": "Successful login for user: admin", "service": "accounts", "url": "/accounts/login/", "allowed": true, "operation": "USER_LOGIN", "ipAddress": "10.0.0.250"} |
   +-----------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
