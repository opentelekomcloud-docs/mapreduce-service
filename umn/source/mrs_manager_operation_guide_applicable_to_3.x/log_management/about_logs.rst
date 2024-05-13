:original_name: admin_guide_000193.html

.. _admin_guide_000193:

About Logs
==========

Log Description
---------------

MRS cluster logs are stored in the **/var/log/Bigdata** directory. The following table lists the log types.

.. table:: **Table 1** Log types

   +-------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Log Type          | Description                                                                                                                                                                                       |
   +===================+===================================================================================================================================================================================================+
   | Installation logs | Installation logs record information about MRS Manager, cluster, and service installation to help users locate installation errors.                                                               |
   +-------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Run logs          | Run logs record the running track information, debugging information, status changes, potential problems, and error information generated during the running of services.                         |
   +-------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Audit logs        | Audit logs record information about users' activities and operation instructions, which can be used to locate fault causes in security events and determine who are responsible for these faults. |
   +-------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

The following table lists the MRS log directories.

.. table:: **Table 2** Log directories

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Directory                         | Log                                                                                                                                                                  |
   +===================================+======================================================================================================================================================================+
   | /var/log/Bigdata/audit            | Component audit log.                                                                                                                                                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/controller       | Log collecting script log.                                                                                                                                           |
   |                                   |                                                                                                                                                                      |
   |                                   | Controller process log.                                                                                                                                              |
   |                                   |                                                                                                                                                                      |
   |                                   | Controller monitoring log.                                                                                                                                           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/dbservice        | DBService log.                                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/flume            | Flume log.                                                                                                                                                           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/hbase            | HBase log.                                                                                                                                                           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/hdfs             | HDFS log.                                                                                                                                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/hive             | Hive log.                                                                                                                                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/httpd            | HTTPd log.                                                                                                                                                           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/hue              | Hue log.                                                                                                                                                             |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/kerberos         | Kerberos log.                                                                                                                                                        |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/ldapclient       | LDAP client log.                                                                                                                                                     |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/ldapserver       | LDAP server log.                                                                                                                                                     |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/loader           | Loader log.                                                                                                                                                          |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/logman           | Logman script log management log.                                                                                                                                    |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/mapreduce        | MapReduce log.                                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/nodeagent        | NodeAgent log.                                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/okerberos        | OMS Kerberos log.                                                                                                                                                    |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/oldapserver      | OMS LDAP log.                                                                                                                                                        |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/metric_agent     | Run log file of MetricAgent.                                                                                                                                         |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/omm              | **oms**: complex event processing log, alarm service log, HA log, authentication and authorization management log, and monitoring service run log of the OMM server. |
   |                                   |                                                                                                                                                                      |
   |                                   | **oma**: installation log and run log of the OMM agent.                                                                                                              |
   |                                   |                                                                                                                                                                      |
   |                                   | **core**: dump log generated when the OMM agent and the HA process are suspended.                                                                                    |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/spark2x          | Spark2x log.                                                                                                                                                         |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/sudo             | Log generated when the **sudo** command is executed by user **omm**.                                                                                                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/timestamp        | Time synchronization management log.                                                                                                                                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/tomcat           | Tomcat log.                                                                                                                                                          |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/watchdog         | Watchdog log.                                                                                                                                                        |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/yarn             | Yarn log.                                                                                                                                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/zookeeper        | ZooKeeper log.                                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/oozie            | Oozie log.                                                                                                                                                           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/kafka            | Kafka log.                                                                                                                                                           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/storm            | Storm log.                                                                                                                                                           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/upgrade          | OMS upgrade log.                                                                                                                                                     |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/update-service   | Upgrade service log.                                                                                                                                                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   After the multi-instance function is enabled, if the system administrator adds multiple HBase, Hive, and Spark service instances, the log description, log level, and log format of the newly added service instances are the same as those of the original service logs. Service instance logs are stored separately in the **/var/log/Bigdata/**\ *servicenameN* directory. The audit logs of the HBase and Hive service instances are stored in the **/var/log/Bigdata/audit/**\ *servicenameN* directory. For example, the logs of HBase1 are stored in the **/var/log/Bigdata/hbase1** and **/var/log/Bigdata/audit/hbase1** directories.

Installation Logs
-----------------

.. table:: **Table 3** Installation logs

   +------------------------------+------------------------------------------------------------------------------+
   | Installation Log             | Description                                                                  |
   +==============================+==============================================================================+
   | Configuration log            | Records information about the configuration process before the installation. |
   +------------------------------+------------------------------------------------------------------------------+
   | MRS Manager installation log | Records information about the two-node MRS Manager installation.             |
   +------------------------------+------------------------------------------------------------------------------+
   | Cluster installation log     | Records information about the cluster installation.                          |
   +------------------------------+------------------------------------------------------------------------------+

Run Logs
--------

:ref:`Table 4 <admin_guide_000193__t6d0bc48e23fc402ba1643b1dcd9f77c4>` describes the running information recorded in run logs.

.. _admin_guide_000193__t6d0bc48e23fc402ba1643b1dcd9f77c4:

.. table:: **Table 4** Running information

   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Run Log                         | Description                                                                                                                                                               |
   +=================================+===========================================================================================================================================================================+
   | Installation preparation log    | Records information about preparations for the installation, such as the detection, configuration, and feedback operation information.                                    |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Process startup log             | Records information about the commands executed during the process startup.                                                                                               |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Process startup exception log   | Records information about exceptions during process startup, such as dependent service errors and insufficient resources.                                                 |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Process run log                 | Records information about the process running track information and debugging information, such as function entries and exits as well as cross-module interface messages. |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Process running exception log   | Records errors that cause process running errors, for example, the empty input objects or encoding or decoding failure.                                                   |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Process running environment log | Records information about the process running environment, such as resource status and environment variables.                                                             |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Script log                      | Records information about the script execution process.                                                                                                                   |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Resource reclamation log        | Records information about the resource reclaiming process.                                                                                                                |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Uninstallation clearing logs    | Records information about operations performed during service uninstallation, such as directory and execution time deletion.                                              |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _admin_guide_000193__s481f1c14aca34ee788baed345970a5c0:

Audit Logs
----------

Audit information recorded in audit logs includes MRS Manager audit information and component audit information.

.. table:: **Table 5** Audit information of MRS Manager

   +-----------------------------------+--------------------------------------------------------------------+
   | Operation Type                    | Operation                                                          |
   +===================================+====================================================================+
   | User management                   | Creating a user.                                                   |
   |                                   |                                                                    |
   |                                   | Modifying a user.                                                  |
   |                                   |                                                                    |
   |                                   | Deleting a user.                                                   |
   |                                   |                                                                    |
   |                                   | Creating a user group.                                             |
   |                                   |                                                                    |
   |                                   | Modifying a user group.                                            |
   |                                   |                                                                    |
   |                                   | Deleting a group.                                                  |
   |                                   |                                                                    |
   |                                   | Adding a role.                                                     |
   |                                   |                                                                    |
   |                                   | Changing the user's roles.                                         |
   |                                   |                                                                    |
   |                                   | Deleting a role.                                                   |
   |                                   |                                                                    |
   |                                   | Changing a password policy.                                        |
   |                                   |                                                                    |
   |                                   | Changing a password.                                               |
   |                                   |                                                                    |
   |                                   | Resetting a password.                                              |
   |                                   |                                                                    |
   |                                   | Logging in.                                                        |
   |                                   |                                                                    |
   |                                   | Logging out.                                                       |
   |                                   |                                                                    |
   |                                   | Unlocking the screen.                                              |
   |                                   |                                                                    |
   |                                   | Downloading the authentication credential.                         |
   |                                   |                                                                    |
   |                                   | Unauthorized operation.                                            |
   |                                   |                                                                    |
   |                                   | Unlocking a user account.                                          |
   |                                   |                                                                    |
   |                                   | Locking a user account.                                            |
   |                                   |                                                                    |
   |                                   | Locking the screen.                                                |
   |                                   |                                                                    |
   |                                   | Exporting a user.                                                  |
   |                                   |                                                                    |
   |                                   | Exporting a user group.                                            |
   |                                   |                                                                    |
   |                                   | Exporting a role.                                                  |
   +-----------------------------------+--------------------------------------------------------------------+
   | Cluster management                | Starting a cluster.                                                |
   |                                   |                                                                    |
   |                                   | Stopping a cluster.                                                |
   |                                   |                                                                    |
   |                                   | Restarting a cluster.                                              |
   |                                   |                                                                    |
   |                                   | Performing a rolling restart of a cluster.                         |
   |                                   |                                                                    |
   |                                   | Restarting all expired instances.                                  |
   |                                   |                                                                    |
   |                                   | Saving configurations.                                             |
   |                                   |                                                                    |
   |                                   | Synchronizing cluster configurations.                              |
   |                                   |                                                                    |
   |                                   | Customizing cluster monitoring metrics.                            |
   |                                   |                                                                    |
   |                                   | Configuring monitoring dumping.                                    |
   |                                   |                                                                    |
   |                                   | Saving monitoring thresholds.                                      |
   |                                   |                                                                    |
   |                                   | Downloading a client configuration file.                           |
   |                                   |                                                                    |
   |                                   | Configuring the northbound Syslog interface.                       |
   |                                   |                                                                    |
   |                                   | Configuring the northbound SNMP interface.                         |
   |                                   |                                                                    |
   |                                   | Clearing alarms using SNMP.                                        |
   |                                   |                                                                    |
   |                                   | Adding a trap target using SNMP.                                   |
   |                                   |                                                                    |
   |                                   | Deleting a trap target using SNMP.                                 |
   |                                   |                                                                    |
   |                                   | Checking alarms using SNMP.                                        |
   |                                   |                                                                    |
   |                                   | Synchronizing alarms using SNMP.                                   |
   |                                   |                                                                    |
   |                                   | Creating a threshold template.                                     |
   |                                   |                                                                    |
   |                                   | Deleting a threshold template.                                     |
   |                                   |                                                                    |
   |                                   | Applying a threshold template.                                     |
   |                                   |                                                                    |
   |                                   | Saving cluster monitoring configurations.                          |
   |                                   |                                                                    |
   |                                   | Exporting configurations.                                          |
   |                                   |                                                                    |
   |                                   | Importing cluster configurations.                                  |
   |                                   |                                                                    |
   |                                   | Exporting an installation template.                                |
   |                                   |                                                                    |
   |                                   | Modifying a threshold template.                                    |
   |                                   |                                                                    |
   |                                   | Canceling the application of a threshold template.                 |
   |                                   |                                                                    |
   |                                   | Masking an alarm.                                                  |
   |                                   |                                                                    |
   |                                   | Sending an alarm.                                                  |
   |                                   |                                                                    |
   |                                   | Changing the OMS database password.                                |
   |                                   |                                                                    |
   |                                   | Resetting the component database password.                         |
   |                                   |                                                                    |
   |                                   | Restarting OMM and Controller.                                     |
   |                                   |                                                                    |
   |                                   | Starting the health check of a cluster.                            |
   |                                   |                                                                    |
   |                                   | Importing a certificate file.                                      |
   |                                   |                                                                    |
   |                                   | Configuring SSO information.                                       |
   |                                   |                                                                    |
   |                                   | Deleting historical health check reports.                          |
   |                                   |                                                                    |
   |                                   | Modifying cluster properties.                                      |
   |                                   |                                                                    |
   |                                   | Running maintenance commands in synchronous mode.                  |
   |                                   |                                                                    |
   |                                   | Running maintenance commands in asynchronous mode.                 |
   |                                   |                                                                    |
   |                                   | Customizing report monitoring metrics.                             |
   |                                   |                                                                    |
   |                                   | Exporting report monitoring data.                                  |
   |                                   |                                                                    |
   |                                   | Runing a command in asynchronous mode using SNMP.                  |
   |                                   |                                                                    |
   |                                   | Restarting the Web service.                                        |
   |                                   |                                                                    |
   |                                   | Customizing monitoring metrics for static resource pools.          |
   |                                   |                                                                    |
   |                                   | Exporting monitoring data of a static resource pool.               |
   |                                   |                                                                    |
   |                                   | Customizing dashboard monitoring metrics.                          |
   |                                   |                                                                    |
   |                                   | Stopping a task.                                                   |
   |                                   |                                                                    |
   |                                   | Restoring configurations.                                          |
   |                                   |                                                                    |
   |                                   | Modifying domain and mutual trust configurations.                  |
   |                                   |                                                                    |
   |                                   | Modifying system parameters.                                       |
   |                                   |                                                                    |
   |                                   | Making a cluster enter the maintenance mode.                       |
   |                                   |                                                                    |
   |                                   | Making a cluster exit the maintenance mode.                        |
   |                                   |                                                                    |
   |                                   | Making OMS enter the maintenance mode.                             |
   |                                   |                                                                    |
   |                                   | Making OMS exit the maintenance mode.                              |
   |                                   |                                                                    |
   |                                   | Making services in a cluster exit the maintenance mode in batches. |
   |                                   |                                                                    |
   |                                   | Modifying OMS configurations.                                      |
   |                                   |                                                                    |
   |                                   | Enabling threshold alarms.                                         |
   |                                   |                                                                    |
   |                                   | Synchronizing all cluster configurations.                          |
   +-----------------------------------+--------------------------------------------------------------------+
   | Service management                | Starting a service.                                                |
   |                                   |                                                                    |
   |                                   | Stopping a service.                                                |
   |                                   |                                                                    |
   |                                   | Synchronizing service configurations.                              |
   |                                   |                                                                    |
   |                                   | Refreshing a service queue.                                        |
   |                                   |                                                                    |
   |                                   | Customizing service monitoring metrics.                            |
   |                                   |                                                                    |
   |                                   | Restarting a service.                                              |
   |                                   |                                                                    |
   |                                   | Performing a rolling service restart.                              |
   |                                   |                                                                    |
   |                                   | Exporting service monitoring data.                                 |
   |                                   |                                                                    |
   |                                   | Importing service configuration data.                              |
   |                                   |                                                                    |
   |                                   | Starting the health check of a service.                            |
   |                                   |                                                                    |
   |                                   | Configuring a service.                                             |
   |                                   |                                                                    |
   |                                   | Uploading a configuration file.                                    |
   |                                   |                                                                    |
   |                                   | Downloading a configuration file.                                  |
   |                                   |                                                                    |
   |                                   | Synchronizing instance configurations.                             |
   |                                   |                                                                    |
   |                                   | Commissioning an instance.                                         |
   |                                   |                                                                    |
   |                                   | Decommissioning an instance.                                       |
   |                                   |                                                                    |
   |                                   | Starting an instance.                                              |
   |                                   |                                                                    |
   |                                   | Stopping an instance.                                              |
   |                                   |                                                                    |
   |                                   | Customizing instance monitoring metrics.                           |
   |                                   |                                                                    |
   |                                   | Restarting an instance.                                            |
   |                                   |                                                                    |
   |                                   | Performing a rolling restart of an instance.                       |
   |                                   |                                                                    |
   |                                   | Exporting instance monitoring data.                                |
   |                                   |                                                                    |
   |                                   | Importing instance configuration data.                             |
   |                                   |                                                                    |
   |                                   | Creating an instance group.                                        |
   |                                   |                                                                    |
   |                                   | Modifying an instance group.                                       |
   |                                   |                                                                    |
   |                                   | Deleting an instance group.                                        |
   |                                   |                                                                    |
   |                                   | Moving an instance to another instance group.                      |
   |                                   |                                                                    |
   |                                   | Making a service enter the maintenance mode.                       |
   |                                   |                                                                    |
   |                                   | Making a service exit the maintenance mode.                        |
   |                                   |                                                                    |
   |                                   | Changing the name of a service.                                    |
   |                                   |                                                                    |
   |                                   | Modifying service association.                                     |
   |                                   |                                                                    |
   |                                   | Downloading monitoring data.                                       |
   |                                   |                                                                    |
   |                                   | Masking alarms.                                                    |
   |                                   |                                                                    |
   |                                   | Unmasking alarms.                                                  |
   |                                   |                                                                    |
   |                                   | Exporting report data of a service.                                |
   |                                   |                                                                    |
   |                                   | Adding custom parameters for a report.                             |
   |                                   |                                                                    |
   |                                   | Modifying custom parameters of a report.                           |
   |                                   |                                                                    |
   |                                   | Deleting custom parameters of a report.                            |
   |                                   |                                                                    |
   |                                   | Switching over control nodes.                                      |
   |                                   |                                                                    |
   |                                   | Adding a mount table.                                              |
   |                                   |                                                                    |
   |                                   | Modifying a mount table.                                           |
   +-----------------------------------+--------------------------------------------------------------------+
   | Host management                   | Setting a node rack.                                               |
   |                                   |                                                                    |
   |                                   | Starting all roles.                                                |
   |                                   |                                                                    |
   |                                   | Stopping all roles.                                                |
   |                                   |                                                                    |
   |                                   | Isolating a host.                                                  |
   |                                   |                                                                    |
   |                                   | Canceling isolation of a host.                                     |
   |                                   |                                                                    |
   |                                   | Customizing host monitoring metrics.                               |
   |                                   |                                                                    |
   |                                   | Exporting host monitoring data.                                    |
   |                                   |                                                                    |
   |                                   | Making a host enter the maintenance mode.                          |
   |                                   |                                                                    |
   |                                   | Making a host exit the maintenance mode.                           |
   |                                   |                                                                    |
   |                                   | Exporting basic host information.                                  |
   |                                   |                                                                    |
   |                                   | Exporting host distribution report data.                           |
   |                                   |                                                                    |
   |                                   | Exporting host trend report data.                                  |
   |                                   |                                                                    |
   |                                   | Exporting host cluster report data.                                |
   |                                   |                                                                    |
   |                                   | Exporting report data of a service.                                |
   |                                   |                                                                    |
   |                                   | Customizing host cluster monitoring metrics.                       |
   |                                   |                                                                    |
   |                                   | Customizing host cluster trend monitoring metrics.                 |
   +-----------------------------------+--------------------------------------------------------------------+
   | Alarm management                  | Exporting alarms.                                                  |
   |                                   |                                                                    |
   |                                   | Clearing alarms.                                                   |
   |                                   |                                                                    |
   |                                   | Exporting events.                                                  |
   |                                   |                                                                    |
   |                                   | Clearing alarms in batches.                                        |
   +-----------------------------------+--------------------------------------------------------------------+
   | Log collection                    | Collecting log files.                                              |
   |                                   |                                                                    |
   |                                   | Downloading log files.                                             |
   |                                   |                                                                    |
   |                                   | Collecting service stack information.                              |
   |                                   |                                                                    |
   |                                   | Collecting instance stack information.                             |
   |                                   |                                                                    |
   |                                   | Preparing service stack information.                               |
   |                                   |                                                                    |
   |                                   | Preparing instance stack information.                              |
   |                                   |                                                                    |
   |                                   | Clearing service stack information.                                |
   |                                   |                                                                    |
   |                                   | Clearing instance stack information.                               |
   +-----------------------------------+--------------------------------------------------------------------+
   | Audit log management              | Modifying audit dumping configurations.                            |
   |                                   |                                                                    |
   |                                   | Exporting audit logs.                                              |
   +-----------------------------------+--------------------------------------------------------------------+
   | Data backup and restoration       | Creating a backup task.                                            |
   |                                   |                                                                    |
   |                                   | Executing a backup task.                                           |
   |                                   |                                                                    |
   |                                   | Executing backup tasks in batches.                                 |
   |                                   |                                                                    |
   |                                   | Stopping a backup task.                                            |
   |                                   |                                                                    |
   |                                   | Deleting a backup task.                                            |
   |                                   |                                                                    |
   |                                   | Modifying a backup task.                                           |
   |                                   |                                                                    |
   |                                   | Locking a backup task.                                             |
   |                                   |                                                                    |
   |                                   | Unlocking a backup task.                                           |
   |                                   |                                                                    |
   |                                   | Creating a restoration task.                                       |
   |                                   |                                                                    |
   |                                   | Executing a restoration task.                                      |
   |                                   |                                                                    |
   |                                   | Stopping a restoration task.                                       |
   |                                   |                                                                    |
   |                                   | Retrying a restoration task.                                       |
   |                                   |                                                                    |
   |                                   | Deleting a restoration task.                                       |
   +-----------------------------------+--------------------------------------------------------------------+
   | Multi-tenant management           | Saving static configurations.                                      |
   |                                   |                                                                    |
   |                                   | Adding a tenant.                                                   |
   |                                   |                                                                    |
   |                                   | Deleting a tenant.                                                 |
   |                                   |                                                                    |
   |                                   | Associating a service with a tenant.                               |
   |                                   |                                                                    |
   |                                   | Deleting a service from a tenant.                                  |
   |                                   |                                                                    |
   |                                   | Configuring resources.                                             |
   |                                   |                                                                    |
   |                                   | Creating a resource.                                               |
   |                                   |                                                                    |
   |                                   | Deleting a resource.                                               |
   |                                   |                                                                    |
   |                                   | Adding a resource pool.                                            |
   |                                   |                                                                    |
   |                                   | Modifying a resource pool.                                         |
   |                                   |                                                                    |
   |                                   | Deleting a resource pool.                                          |
   |                                   |                                                                    |
   |                                   | Restoring tenant data.                                             |
   |                                   |                                                                    |
   |                                   | Modifying global configurations of a tenant.                       |
   |                                   |                                                                    |
   |                                   | Modifying queue configurations of a capacity scheduler.            |
   |                                   |                                                                    |
   |                                   | Modifying queue configurations of a super scheduler.               |
   |                                   |                                                                    |
   |                                   | Modifying resource distribution of a capacity scheduler.           |
   |                                   |                                                                    |
   |                                   | Clearing resource distribution of a capacity scheduler.            |
   |                                   |                                                                    |
   |                                   | Modifying resource distribution of a super scheduler.              |
   |                                   |                                                                    |
   |                                   | Clearing resource distribution of a super scheduler.               |
   |                                   |                                                                    |
   |                                   | Adding a resource catalog.                                         |
   |                                   |                                                                    |
   |                                   | Modifying a resource catalog.                                      |
   |                                   |                                                                    |
   |                                   | Deleting a resource catalog.                                       |
   |                                   |                                                                    |
   |                                   | Customizing tenant monitoring metrics.                             |
   +-----------------------------------+--------------------------------------------------------------------+
   | Health check                      | Starting the health check of a cluster.                            |
   |                                   |                                                                    |
   |                                   | Starting the health check of a service.                            |
   |                                   |                                                                    |
   |                                   | Starting the health check of a host.                               |
   |                                   |                                                                    |
   |                                   | Starting the health check of OMS.                                  |
   |                                   |                                                                    |
   |                                   | Starting the system health check.                                  |
   |                                   |                                                                    |
   |                                   | Updating the health check configurations.                          |
   |                                   |                                                                    |
   |                                   | Exporting health check reports.                                    |
   |                                   |                                                                    |
   |                                   | Exporting health check results of a cluster.                       |
   |                                   |                                                                    |
   |                                   | Exporting health check results of a service.                       |
   |                                   |                                                                    |
   |                                   | Exporting health check results of a host.                          |
   |                                   |                                                                    |
   |                                   | Deleting historical health check reports.                          |
   |                                   |                                                                    |
   |                                   | Exporting historical health check reports.                         |
   |                                   |                                                                    |
   |                                   | Downloading a health check report.                                 |
   +-----------------------------------+--------------------------------------------------------------------+

.. table:: **Table 6** Component audit information

   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   | Audit Log             | Operation Type                              | Operation                                                                                       |
   +=======================+=============================================+=================================================================================================+
   | ClickHouse audit log  | Maintenance management                      | Granting permissions.                                                                           |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Revoking permissions.                                                                           |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Recording authentication and login information.                                                 |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | Service operations                          | Creating databases or tables.                                                                   |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Inserting, deleting, querying, and migrating data.                                              |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   | DBService audit log   | Maintenance management                      | Performing backup restoration operations.                                                       |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   | HBase audit log       | Data definition language (DDL) statements   | Creating a table.                                                                               |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Deleting a table.                                                                               |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Modifying a table.                                                                              |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Adding a column family.                                                                         |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Modifying a column family.                                                                      |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Deleting a column family.                                                                       |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Enabling a table.                                                                               |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Disabling a table.                                                                              |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Modifying user information.                                                                     |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Changing a password.                                                                            |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Logging in.                                                                                     |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | Data manipulation language (DML) statements | Putting data (to the **hbase:meta**, **\_ctmeta\_**, and **hbase:acl** tables).                 |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Deleting data (from the **hbase:meta**, **\_ctmeta\_**, and **hbase:acl** tables).              |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Checking and putting data (to the **hbase:meta**, **\_ctmeta\_**, and **hbase:acl** tables).    |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Checking and deleting data (from the **hbase:meta**, **\_ctmeta\_**, and **hbase:acl** tables). |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | Permission control                          | Assigning permissions to a user.                                                                |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Canceling permission assigning.                                                                 |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   | HDFS audit log        | Permission management                       | Managing access permissions on files or folders.                                                |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Managing the owner information of files or folders.                                             |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | File operations                             | Creating a folder.                                                                              |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Creating a file.                                                                                |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Opening a file.                                                                                 |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Appending file content.                                                                         |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Changing a file name.                                                                           |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Deleting a file or folder.                                                                      |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Setting time property of a file.                                                                |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Setting the number of file copies.                                                              |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Merging files.                                                                                  |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Checking the file system.                                                                       |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Linking to a file.                                                                              |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   | Hive audit log        | Metadata operations                         | Defining metadata, such as creating databases and tables.                                       |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Deleting metadata, such as deleting databases and tables.                                       |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Modifying metadata, such as adding columns and renaming tables.                                 |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Importing and exporting metadata.                                                               |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | Data maintenance                            | Loading data to a table.                                                                        |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Inserting data into a table.                                                                    |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | Permission management                       | Creating or deleting a role.                                                                    |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Granting/Reclaiming roles.                                                                      |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Granting/Reclaiming permissions.                                                                |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   | Hue audit log         | Service startup                             | Starting Hue.                                                                                   |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | User operations                             | Logging in.                                                                                     |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Logging out.                                                                                    |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | Task operations                             | Creating a task.                                                                                |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Modifying a task.                                                                               |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Deleting a task.                                                                                |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Submitting a task.                                                                              |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Saving a task.                                                                                  |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Updating the status of a task.                                                                  |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   | KrbServer audit log   | Maintenance management                      | Changing the password of a Kerberos account.                                                    |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Adding a Kerberos account.                                                                      |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Deleting a Kerberos account.                                                                    |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Authenticating users.                                                                           |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   | LdapServer audit log  | Maintenance management                      | Adding an OS user.                                                                              |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Adding a user group.                                                                            |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Adding a user to a user group.                                                                  |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Deleting a user.                                                                                |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Deleting a group.                                                                               |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   | Loader audit log      | Security management                         | Logging in.                                                                                     |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | Metadata management                         | Querying connector information.                                                                 |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Querying a framework.                                                                           |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Querying step information.                                                                      |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | Data source connection management           | Querying a data source connection.                                                              |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Adding a data source connection.                                                                |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Updating a data source connection.                                                              |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Deleting a data source connection.                                                              |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Activating a data source connection.                                                            |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Disabling a data source connection.                                                             |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | Job management                              | Querying a job.                                                                                 |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Creating a job.                                                                                 |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Updating a job.                                                                                 |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Deleting a job.                                                                                 |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Activating a job.                                                                               |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Disabling a job.                                                                                |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Querying all execution records of a job.                                                        |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Querying the latest execution record of a job.                                                  |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Submitting a job.                                                                               |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Stopping a job.                                                                                 |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   | MapReduce audit log   | Application running                         | Starting a container request.                                                                   |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Stopping a container request.                                                                   |
   |                       |                                             |                                                                                                 |
   |                       |                                             | After a container request is complete, the status of the request becomes successful.            |
   |                       |                                             |                                                                                                 |
   |                       |                                             | After a container request is complete, the status of the request becomes failed.                |
   |                       |                                             |                                                                                                 |
   |                       |                                             | After a container request is complete, the status of the request becomes suspended.             |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Submitting a task.                                                                              |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Ending a task.                                                                                  |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   | Oozie audit log       | Task management                             | Submitting a task.                                                                              |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Starting a task.                                                                                |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Killing a task.                                                                                 |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Suspending a task.                                                                              |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Resuming a task.                                                                                |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Running a task again.                                                                           |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   | Spark2x audit log     | Metadata operations                         | Defining metadata, such as creating databases and tables.                                       |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Deleting metadata, such as deleting databases and tables.                                       |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Modifying metadata, such as adding columns and renaming tables.                                 |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Importing and exporting metadata.                                                               |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | Data maintenance                            | Loading data to a table.                                                                        |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Inserting data into a table.                                                                    |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   | Storm audit log       | Nimbus operations                           | Submitting a topology.                                                                          |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Stopping a topology.                                                                            |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Reallocating a topology.                                                                        |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Deactivating a topology.                                                                        |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Activating a topology.                                                                          |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | UI operations                               | Stopping a topology.                                                                            |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Reallocating a topology.                                                                        |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Deactivating a topology.                                                                        |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Activating a topology.                                                                          |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   | Yarn audit log        | Job submission                              | Submitting a job to a queue.                                                                    |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   | ZooKeeper audit log   | Permission management                       | Setting access permissions to Znode.                                                            |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+
   |                       | Znode operations                            | Creating Znodes.                                                                                |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Deleting Znodes.                                                                                |
   |                       |                                             |                                                                                                 |
   |                       |                                             | Configuring Znode data.                                                                         |
   +-----------------------+---------------------------------------------+-------------------------------------------------------------------------------------------------+

MRS Manager audit logs are stored in the database. You can view and export the audit logs on the **Audit** page.

The following table lists the directories to store component audit logs. Audit log files of some components are stored in **/var/log/Bigdata/audit**, such as HDFS, HBase, MapReduce, Hive, Hue, Yarn, Storm, and ZooKeeper. The component audit logs are automatically compressed and backed up to **/var/log/Bigdata/audit/bk** at 03: 00 every day. A maximum of latest 90 compressed backup files are retained, and the backup time cannot be changed. For details about how to configure the number of reserved audit log files, see :ref:`Configuring the Number of Local Audit Log Backups <admin_guide_000196>`.

Audit log files of other components are stored in the component log directory.

.. table:: **Table 7** Directories for storing component audit logs

   +-----------------------------------+-------------------------------------------------------------------------+
   | Component                         | Audit Log Directory                                                     |
   +===================================+=========================================================================+
   | DBService                         | /var/log/Bigdata/audit/dbservice/dbservice_audit.log                    |
   +-----------------------------------+-------------------------------------------------------------------------+
   | HBase                             | /var/log/Bigdata/audit/hbase/hm/hbase-audit-hmaster.log                 |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/hbase/hm/hbase-ranger-audit-hmaster.log          |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/hbase/rs/hbase-audit-regionserver.log            |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/hbase/rs/hbase-ranger-audit-regionserver.log     |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/hbase/rt/hbase-audit-restserver.log              |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/hbase/ts/hbase-audit-thriftserver.log            |
   +-----------------------------------+-------------------------------------------------------------------------+
   | HDFS                              | /var/log/Bigdata/audit/hdfs/nn/hdfs-audit-namenode.log                  |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/hdfs/nn/ranger-plugin-audit.log                  |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/hdfs/dn/hdfs-audit-datanode.log                  |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/hdfs/jn/hdfs-audit-journalnode.log               |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/hdfs/zkfc/hdfs-audit-zkfc.log                    |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/hdfs/httpfs/hdfs-audit-httpfs.log                |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/hdfs/router/hdfs-audit-router.log                |
   +-----------------------------------+-------------------------------------------------------------------------+
   | Hive                              | /var/log/Bigdata/audit/hive/hiveserver/hive-audit.log                   |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/hive/hiveserver/hive-rangeraudit.log             |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/hive/metastore/metastore-audit.log               |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/hive/webhcat/webhcat-audit.log                   |
   +-----------------------------------+-------------------------------------------------------------------------+
   | Hue                               | /var/log/Bigdata/audit/hue/hue-audits.log                               |
   +-----------------------------------+-------------------------------------------------------------------------+
   | Kafka                             | /var/log/Bigdata/audit/kafka/audit.log                                  |
   +-----------------------------------+-------------------------------------------------------------------------+
   | Loader                            | /var/log/Bigdata/loader/audit/default.audit                             |
   +-----------------------------------+-------------------------------------------------------------------------+
   | MapReduce                         | /var/log/Bigdata/audit/mapreduce/jobhistory/mapred-audit-jobhistory.log |
   +-----------------------------------+-------------------------------------------------------------------------+
   | Oozie                             | /var/log/Bigdata/audit/oozie/oozie-audit.log                            |
   +-----------------------------------+-------------------------------------------------------------------------+
   | Spark2x                           | /var/log/Bigdata/audit/spark2x/jdbcserver/jdbcserver-audit.log          |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/spark2x/jdbcserver/ranger-audit.log              |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/spark2x/jobhistory/jobhistory-audit.log          |
   +-----------------------------------+-------------------------------------------------------------------------+
   | Storm                             | /var/log/Bigdata/audit/storm/logviewer/audit.log                        |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/storm/nimbus/audit.log                           |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/storm/supervisor/audit.log                       |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/storm/ui/audit.log                               |
   +-----------------------------------+-------------------------------------------------------------------------+
   | Yarn                              | /var/log/Bigdata/audit/yarn/rm/yarn-audit-resourcemanager.log           |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/yarn/rm/ranger-plugin-audit.log                  |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/yarn/nm/yarn-audit-nodemanager.log               |
   +-----------------------------------+-------------------------------------------------------------------------+
   | ZooKeeper                         | /var/log/Bigdata/audit/zookeeper/quorumpeer/zk-audit-quorumpeer.log     |
   +-----------------------------------+-------------------------------------------------------------------------+
