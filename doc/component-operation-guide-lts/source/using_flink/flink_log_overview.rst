:original_name: mrs_01_0596.html

.. _mrs_01_0596:

Flink Log Overview
==================

Log Description
---------------

**Log path:**

-  Run logs of a Flink job: **${BIGDATA_DATA_HOME}/hadoop/data${i}/nm/containerlogs/application_${appid}/container_{$contid}**

   .. note::

      The logs of executing tasks are stored in the preceding path. After the execution is complete, the Yarn configuration determines whether these logs are gathered to the HDFS directory.

-  FlinkResource run logs: **/var/log/Bigdata/flink/flinkResource**
-  FlinkServer run logs: **/var/log/Bigdata/flink/flinkserver**
-  FlinkServer audit logs: **/var/log/Bigdata/audit/flink/flinkserver**

**Log archive rules:**

#. FlinkResource run logs:

   -  By default, service logs are backed up each time when the log size reaches 20 MB. A maximum of 20 logs can be reserved without being compressed.
   -  You can set the log size and number of compressed logs on the Manager page or modify the corresponding configuration items in **log4j-cli.properties**, **log4j.properties**, and **log4j-session.properties** in **/opt/client/Flink/flink/conf/** on the client. **/opt/client** is the client installation directory.

   .. table:: **Table 1** FlinkResource log list

      ====================== ================ ========================
      Type                   Name             Description
      ====================== ================ ========================
      FlinkResource run logs checkService.log Health check log
      \                      kinit.log        Initialization log
      \                      postinstall.log  Service installation log
      \                      prestart.log     Prestart script log
      \                      start.log        Startup log
      ====================== ================ ========================

#. FlinkServer service logs and audit logs

   -  By default, FlinkServer service logs and audit logs are backed up each time when the log size reaches 100 MB. The service logs are stored for a maximum of 30 days, and audit logs are stored for a maximum of 90 days.
   -  You can set the log size and number of compressed logs on the Manager page or modify the corresponding configuration items in **log4j-cli.properties**, **log4j.properties**, and **log4j-session.properties** in **/opt/client/Flink/flink/conf/** on the client. **/opt/client** is the client installation directory.

   .. table:: **Table 2** FlinkServer log list

      +------------------------+----------------------------------------------+---------------------------------------------------------------+
      | Type                   | Name                                         | Description                                                   |
      +========================+==============================================+===============================================================+
      | FlinkServer run logs   | checkService.log                             | Health check log                                              |
      +------------------------+----------------------------------------------+---------------------------------------------------------------+
      |                        | cleanup.log                                  | Cleanup log file for instance installation and uninstallation |
      +------------------------+----------------------------------------------+---------------------------------------------------------------+
      |                        | flink-omm-client-*IP*.log                    | Job startup log                                               |
      +------------------------+----------------------------------------------+---------------------------------------------------------------+
      |                        | flinkserver\_\ *yyyymmdd-x*.log.gz           | Service archive log                                           |
      +------------------------+----------------------------------------------+---------------------------------------------------------------+
      |                        | flinkserver.log                              | Service log                                                   |
      +------------------------+----------------------------------------------+---------------------------------------------------------------+
      |                        | flinkserver---*pidxxxx*-gc.log.\ *x*.current | GC log                                                        |
      +------------------------+----------------------------------------------+---------------------------------------------------------------+
      |                        | kinit.log                                    | Initialization log                                            |
      +------------------------+----------------------------------------------+---------------------------------------------------------------+
      |                        | postinstall.log                              | Service installation log                                      |
      +------------------------+----------------------------------------------+---------------------------------------------------------------+
      |                        | prestart.log                                 | Prestart script log                                           |
      +------------------------+----------------------------------------------+---------------------------------------------------------------+
      |                        | start.log                                    | Startup log                                                   |
      +------------------------+----------------------------------------------+---------------------------------------------------------------+
      |                        | stop.log                                     | Stop log                                                      |
      +------------------------+----------------------------------------------+---------------------------------------------------------------+
      | FlinkServer audit logs | flinkserver_audit\_\ *yyyymmdd-x*.log.gz     | Audit archive log                                             |
      +------------------------+----------------------------------------------+---------------------------------------------------------------+
      |                        | flinkserver_audit.log                        | Audit log                                                     |
      +------------------------+----------------------------------------------+---------------------------------------------------------------+

Log Level
---------

:ref:`Table 3 <mrs_01_0596__en-us_topic_0000001219029139_table63318572917>` describes the log levels supported by Flink. The priorities of log levels are ERROR, WARN, INFO, and DEBUG in descending order. Logs whose levels are higher than or equal to the specified level are printed. The number of printed logs decreases as the specified log level increases.

.. _mrs_01_0596__en-us_topic_0000001219029139_table63318572917:

.. table:: **Table 3** Log levels

   ===== =============================================================
   Level Description
   ===== =============================================================
   ERROR Error information about the current event processing
   WARN  Exception information about the current event processing
   INFO  Normal running status information about the system and events
   DEBUG System information and system debugging information
   ===== =============================================================

To modify log levels, perform the following steps:

#. Go to the **All Configurations** page of Flink by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.
#. On the menu bar on the left, select the log menu of the target role.
#. Select a desired log level.
#. Save the configuration. In the displayed dialog box, click **OK** to make the configurations take effect.

.. note::

   -  After the configuration is complete, you do not need to restart the service. Download the client again for the configuration to take effect.
   -  You can also change the configuration items corresponding to the log level in **log4j-cli.properties**, **log4j.properties**, and **log4j-session.properties** in **/opt/client/Flink/flink/conf/** on the client. **/opt/client** is the client installation directory.
   -  When a job is submitted using a client, a log file is generated in the **log** folder on the client. The default umask value is **0022**. Therefore, the default log permission is **644**. To change the file permission, you need to change the umask value. For example, to change the umask value of user **omm**:

      -  Add **umask 0026** to the end of the **/home/omm/.baskrc** file.
      -  Run the **source /home/omm/.baskrc** command to make the file permission take effect.

Log Format
----------

.. table:: **Table 4** Log formats

   +---------+--------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type    | Format                                                                                                                                                 | Example                                                                                                                                                                                                                             |
   +=========+========================================================================================================================================================+=====================================================================================================================================================================================================================================+
   | Run log | <*yyyy-MM-dd HH:mm:ss,SSS*>|<*Log level*>|<*Name of the thread that generates the log*>|<*Message in the log*>|<*Location where the log event occurs*> | 2019-06-27 21:30:31,778 \| INFO \| [flink-akka.actor.default-dispatcher-3] \| TaskManager container_e10_1498290698388_0004_02_000007 has started. \| org.apache.flink.yarn.YarnFlinkResourceManager (FlinkResourceManager.java:368) |
   +---------+--------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
