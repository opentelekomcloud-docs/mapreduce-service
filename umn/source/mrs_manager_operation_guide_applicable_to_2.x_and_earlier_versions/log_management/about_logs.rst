:original_name: mrs_01_1226.html

.. _mrs_01_1226:

About Logs
==========

Log Description
---------------

MRS cluster logs are stored in the **/var/log/Bigdata** directory. The following table lists the log types.

.. table:: **Table 1** Log types

   +------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type             | Description                                                                                                                                                                                       |
   +==================+===================================================================================================================================================================================================+
   | Installation log | Installation logs record information about MRS Manager, cluster, and service installation to help users locate installation errors.                                                               |
   +------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Run logs         | Run logs record the running track information, debugging information, status changes, potential problems, and error information generated during the running of services.                         |
   +------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Audit logs       | Audit logs record information about users' activities and operation instructions, which can be used to locate fault causes in security events and determine who are responsible for these faults. |
   +------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

The following table lists the MRS log directories.

.. table:: **Table 2** Log directories

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | File Directory                    | Log Content                                                                                                                                                          |
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
   | /var/log/Bigdata/httpd            | HTTPD log.                                                                                                                                                           |
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
   | /var/log/Bigdata/logman           | logman script log management log.                                                                                                                                    |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/mapreduce        | MapReduce log.                                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/nodeagent        | NodeAgent log.                                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/okerberos        | OMS Kerberos log.                                                                                                                                                    |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/oldapserver      | OMS LDAP log.                                                                                                                                                        |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/omm              | **oms**: complex event processing log, alarm service log, HA log, authentication and authorization management log, and monitoring service run log of the omm server. |
   |                                   |                                                                                                                                                                      |
   |                                   | **oma**: installation log and run log of the omm agent.                                                                                                              |
   |                                   |                                                                                                                                                                      |
   |                                   | **core**: dump log generated when the omm agent and the HA process are suspended.                                                                                    |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/spark            | Spark log.                                                                                                                                                           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/sudo             | Log generated when the **sudo** command is executed by user **omm**.                                                                                                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/timestamp        | Time synchronization management log.                                                                                                                                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/tomcat           | Tomcat log.                                                                                                                                                          |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/yarn             | Yarn log.                                                                                                                                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/zookeeper        | ZooKeeper log.                                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/kafka            | Kafka log.                                                                                                                                                           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/storm            | Storm log.                                                                                                                                                           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | /var/log/Bigdata/patch            | Patch log.                                                                                                                                                           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Run logs
--------

:ref:`Table 3 <mrs_01_1226__t6d0bc48e23fc402ba1643b1dcd9f77c4>` describes the running information recorded in run logs.

.. _mrs_01_1226__t6d0bc48e23fc402ba1643b1dcd9f77c4:

.. table:: **Table 3** Running information

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
   | Script logs                     | Records information about the script execution process.                                                                                                                   |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Resource reclamation log        | Records information about the resource reclaiming process.                                                                                                                |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Uninstallation clearing logs    | Records information about operations performed during service uninstallation, such as directory deletion and execution time                                               |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Audit logs
----------

Audit information recorded in audit logs includes MRS Manager audit information and component audit information.

.. table:: **Table 4** Audit information of MRS Manager

   +-----------------------+------------------------+-------------------------------------------------------------+
   | Audit Log             | Operation Type         | Operation                                                   |
   +=======================+========================+=============================================================+
   | Manager audit log     | User management        | Creating a user                                             |
   |                       |                        |                                                             |
   |                       |                        | Modifying a user                                            |
   |                       |                        |                                                             |
   |                       |                        | Deleting a user                                             |
   |                       |                        |                                                             |
   |                       |                        | Creating a user group                                       |
   |                       |                        |                                                             |
   |                       |                        | Modifying a user group                                      |
   |                       |                        |                                                             |
   |                       |                        | Deleting a user group                                       |
   |                       |                        |                                                             |
   |                       |                        | Adding a role                                               |
   |                       |                        |                                                             |
   |                       |                        | Modifying a role                                            |
   |                       |                        |                                                             |
   |                       |                        | Deleting a role                                             |
   |                       |                        |                                                             |
   |                       |                        | Changing a password policy                                  |
   |                       |                        |                                                             |
   |                       |                        | Changing a password                                         |
   |                       |                        |                                                             |
   |                       |                        | Resetting a password                                        |
   |                       |                        |                                                             |
   |                       |                        | User login                                                  |
   |                       |                        |                                                             |
   |                       |                        | User logout                                                 |
   |                       |                        |                                                             |
   |                       |                        | Unlocking the screen                                        |
   |                       |                        |                                                             |
   |                       |                        | Downloading the authentication credential                   |
   |                       |                        |                                                             |
   |                       |                        | Unauthorized operation                                      |
   |                       |                        |                                                             |
   |                       |                        | Unlocking a user account                                    |
   |                       |                        |                                                             |
   |                       |                        | Locking a user account                                      |
   |                       |                        |                                                             |
   |                       |                        | Locking the screen                                          |
   |                       |                        |                                                             |
   |                       |                        | Exporting user information                                  |
   |                       |                        |                                                             |
   |                       |                        | Exporting a user group                                      |
   |                       |                        |                                                             |
   |                       |                        | Exporting a role                                            |
   +-----------------------+------------------------+-------------------------------------------------------------+
   |                       | Tenant management      | Saving the static configuration                             |
   |                       |                        |                                                             |
   |                       |                        | Adding a tenant                                             |
   |                       |                        |                                                             |
   |                       |                        | Deleting a tenant                                           |
   |                       |                        |                                                             |
   |                       |                        | Associating a service with a tenant                         |
   |                       |                        |                                                             |
   |                       |                        | Deleting a service from a tenant                            |
   |                       |                        |                                                             |
   |                       |                        | Configuring resources                                       |
   |                       |                        |                                                             |
   |                       |                        | Creating resources                                          |
   |                       |                        |                                                             |
   |                       |                        | Deleting resources                                          |
   |                       |                        |                                                             |
   |                       |                        | Adding a resource pool                                      |
   |                       |                        |                                                             |
   |                       |                        | Modifying a resource pool                                   |
   |                       |                        |                                                             |
   |                       |                        | Deleting a resource pool                                    |
   |                       |                        |                                                             |
   |                       |                        | Restoring tenant data                                       |
   +-----------------------+------------------------+-------------------------------------------------------------+
   |                       | Cluster management     | Starting a cluster                                          |
   |                       |                        |                                                             |
   |                       |                        | Stopping a cluster                                          |
   |                       |                        |                                                             |
   |                       |                        | Saving configurations                                       |
   |                       |                        |                                                             |
   |                       |                        | Synchronizing cluster configurations                        |
   |                       |                        |                                                             |
   |                       |                        | Customizing cluster monitoring indicators                   |
   |                       |                        |                                                             |
   |                       |                        | Saving monitoring thresholds                                |
   |                       |                        |                                                             |
   |                       |                        | Downloading a client configuration file                     |
   |                       |                        |                                                             |
   |                       |                        | Configuring the northbound API                              |
   |                       |                        |                                                             |
   |                       |                        | Configuring the northbound SNMP API                         |
   |                       |                        |                                                             |
   |                       |                        | Creating a threshold template                               |
   |                       |                        |                                                             |
   |                       |                        | Deleting a threshold template                               |
   |                       |                        |                                                             |
   |                       |                        | Applying a threshold template                               |
   |                       |                        |                                                             |
   |                       |                        | Saving cluster monitoring configuration data                |
   |                       |                        |                                                             |
   |                       |                        | Exporting configuration data                                |
   |                       |                        |                                                             |
   |                       |                        | Importing cluster configuration data                        |
   |                       |                        |                                                             |
   |                       |                        | Exporting an installation template                          |
   |                       |                        |                                                             |
   |                       |                        | Modifying a threshold template                              |
   |                       |                        |                                                             |
   |                       |                        | Canceling the application of a threshold template           |
   |                       |                        |                                                             |
   |                       |                        | Masking alarms                                              |
   |                       |                        |                                                             |
   |                       |                        | Sending an alarm                                            |
   |                       |                        |                                                             |
   |                       |                        | Changing the OMS database password                          |
   |                       |                        |                                                             |
   |                       |                        | Changing the component database password                    |
   |                       |                        |                                                             |
   |                       |                        | Starting the health check of a cluster                      |
   |                       |                        |                                                             |
   |                       |                        | Updating the health check configuration                     |
   |                       |                        |                                                             |
   |                       |                        | Exporting cluster health check results                      |
   |                       |                        |                                                             |
   |                       |                        | Importing a certificate file                                |
   |                       |                        |                                                             |
   |                       |                        | Deleting historical health check reports                    |
   |                       |                        |                                                             |
   |                       |                        | Exporting historical health check reports                   |
   |                       |                        |                                                             |
   |                       |                        | Customizing report monitoring indicators                    |
   |                       |                        |                                                             |
   |                       |                        | Exporting report monitoring data                            |
   |                       |                        |                                                             |
   |                       |                        | Customizing monitoring indicators for static resource pools |
   |                       |                        |                                                             |
   |                       |                        | Exporting monitoring data of a static resource pool         |
   +-----------------------+------------------------+-------------------------------------------------------------+
   |                       | Service management     | Starting a service                                          |
   |                       |                        |                                                             |
   |                       |                        | Stopping a service                                          |
   |                       |                        |                                                             |
   |                       |                        | Synchronizing service configurations                        |
   |                       |                        |                                                             |
   |                       |                        | Refreshing a service queue                                  |
   |                       |                        |                                                             |
   |                       |                        | Customizing service monitoring indicators                   |
   |                       |                        |                                                             |
   |                       |                        | Restarting a service                                        |
   |                       |                        |                                                             |
   |                       |                        | Exporting service monitoring data                           |
   |                       |                        |                                                             |
   |                       |                        | Importing service configuration data                        |
   |                       |                        |                                                             |
   |                       |                        | Starting the health check of a service                      |
   |                       |                        |                                                             |
   |                       |                        | Exporting service health check results                      |
   |                       |                        |                                                             |
   |                       |                        | Configuring the service                                     |
   |                       |                        |                                                             |
   |                       |                        | Uploading a configuration file                              |
   |                       |                        |                                                             |
   |                       |                        | Downloading a configuration file                            |
   +-----------------------+------------------------+-------------------------------------------------------------+
   |                       | Instance management    | Synchronizing instance configurations                       |
   |                       |                        |                                                             |
   |                       |                        | Commissioning an instance                                   |
   |                       |                        |                                                             |
   |                       |                        | Decommissioning an instance                                 |
   |                       |                        |                                                             |
   |                       |                        | Starting an instance                                        |
   |                       |                        |                                                             |
   |                       |                        | Stopping an instance                                        |
   |                       |                        |                                                             |
   |                       |                        | Customizing instance monitoring indicators                  |
   |                       |                        |                                                             |
   |                       |                        | Restarting an instance                                      |
   |                       |                        |                                                             |
   |                       |                        | Exporting instance monitoring data                          |
   |                       |                        |                                                             |
   |                       |                        | Importing instance configuration data                       |
   +-----------------------+------------------------+-------------------------------------------------------------+
   |                       | Host management        | Setting a node rack                                         |
   |                       |                        |                                                             |
   |                       |                        | Starting all roles                                          |
   |                       |                        |                                                             |
   |                       |                        | Stopping all roles                                          |
   |                       |                        |                                                             |
   |                       |                        | Isolating a host                                            |
   |                       |                        |                                                             |
   |                       |                        | Canceling host isolation                                    |
   |                       |                        |                                                             |
   |                       |                        | Customizing host monitoring indicators                      |
   |                       |                        |                                                             |
   |                       |                        | Exporting host monitoring data                              |
   |                       |                        |                                                             |
   |                       |                        | Starting the health check of a host                         |
   |                       |                        |                                                             |
   |                       |                        | Exporting the health check result of a host                 |
   +-----------------------+------------------------+-------------------------------------------------------------+
   |                       | Maintenance management | Exporting alarms                                            |
   |                       |                        |                                                             |
   |                       |                        | Clearing alarms                                             |
   |                       |                        |                                                             |
   |                       |                        | Exporting events                                            |
   |                       |                        |                                                             |
   |                       |                        | Clearing alarms in batches                                  |
   |                       |                        |                                                             |
   |                       |                        | Clearing alarm through SNMP                                 |
   |                       |                        |                                                             |
   |                       |                        | Adding a trap target through SNMP                           |
   |                       |                        |                                                             |
   |                       |                        | Deleting a trap target through SNMP                         |
   |                       |                        |                                                             |
   |                       |                        | Checking alarms through SNMP                                |
   |                       |                        |                                                             |
   |                       |                        | Synchronizing alarms through SNMP                           |
   |                       |                        |                                                             |
   |                       |                        | Modifying audit dump configurations                         |
   |                       |                        |                                                             |
   |                       |                        | Exporting audit logs                                        |
   |                       |                        |                                                             |
   |                       |                        | Collecting log files                                        |
   |                       |                        |                                                             |
   |                       |                        | Downloading log files                                       |
   |                       |                        |                                                             |
   |                       |                        | Uploading a file                                            |
   |                       |                        |                                                             |
   |                       |                        | Deleting an uploaded file                                   |
   |                       |                        |                                                             |
   |                       |                        | Creating a backup task                                      |
   |                       |                        |                                                             |
   |                       |                        | Executing a backup task                                     |
   |                       |                        |                                                             |
   |                       |                        | Stopping a backup task                                      |
   |                       |                        |                                                             |
   |                       |                        | Deleting a backup task                                      |
   |                       |                        |                                                             |
   |                       |                        | Modifying a backup task                                     |
   |                       |                        |                                                             |
   |                       |                        | Locking a backup task                                       |
   |                       |                        |                                                             |
   |                       |                        | Unlocking a backup task                                     |
   |                       |                        |                                                             |
   |                       |                        | Creating a restoration task                                 |
   |                       |                        |                                                             |
   |                       |                        | Executing a backup restoration task                         |
   |                       |                        |                                                             |
   |                       |                        | Stopping a restoration task                                 |
   |                       |                        |                                                             |
   |                       |                        | Retrying a restoration task                                 |
   |                       |                        |                                                             |
   |                       |                        | Deleting a restoration task                                 |
   +-----------------------+------------------------+-------------------------------------------------------------+

.. table:: **Table 5** Component audit information

   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   | Audit Log             | Operation Type                             | Operation                                                                                      |
   +=======================+============================================+================================================================================================+
   | DBService audit log   | Maintenance management                     | Performing backup restoration operations                                                       |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   | HBase audit log       | Data definition language (DDL) statement   | Creating a table                                                                               |
   |                       |                                            |                                                                                                |
   |                       |                                            | Deleting a table                                                                               |
   |                       |                                            |                                                                                                |
   |                       |                                            | Modifying a table                                                                              |
   |                       |                                            |                                                                                                |
   |                       |                                            | Adding a column family                                                                         |
   |                       |                                            |                                                                                                |
   |                       |                                            | Modifying a column family                                                                      |
   |                       |                                            |                                                                                                |
   |                       |                                            | Deleting a column family                                                                       |
   |                       |                                            |                                                                                                |
   |                       |                                            | Enabling a table                                                                               |
   |                       |                                            |                                                                                                |
   |                       |                                            | Disabling a table                                                                              |
   |                       |                                            |                                                                                                |
   |                       |                                            | Modify the user information                                                                    |
   |                       |                                            |                                                                                                |
   |                       |                                            | Changing a password                                                                            |
   |                       |                                            |                                                                                                |
   |                       |                                            | User login                                                                                     |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   |                       | Data manipulation language (DML) statement | Putting data (to the **hbase:meta**, **\_ctmeta\_**, and **hbase:acl** tables)                 |
   |                       |                                            |                                                                                                |
   |                       |                                            | Deleting data (from the **hbase:meta**, **\_ctmeta\_**, and **hbase:acl** tables)              |
   |                       |                                            |                                                                                                |
   |                       |                                            | Checking and putting data (to the **hbase:meta**, **\_ctmeta\_**, and **hbase:acl** tables)    |
   |                       |                                            |                                                                                                |
   |                       |                                            | Checking and deleting data (from the **hbase:meta**, **\_ctmeta\_**, and **hbase:acl** tables) |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   |                       | Permission control                         | Assigning permissions to a user                                                                |
   |                       |                                            |                                                                                                |
   |                       |                                            | Canceling permission assigning                                                                 |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   | Hive audit logs       | Metadata operation                         | Defining metadata, such as creating databases and tables                                       |
   |                       |                                            |                                                                                                |
   |                       |                                            | Deleting metadata, such as deleting databases and tables                                       |
   |                       |                                            |                                                                                                |
   |                       |                                            | Modifying metadata, such as adding columns and renaming tables                                 |
   |                       |                                            |                                                                                                |
   |                       |                                            | Importing and exporting metadata                                                               |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   |                       | Data maintenance                           | Loading data to a table                                                                        |
   |                       |                                            |                                                                                                |
   |                       |                                            | Inserting data into a table                                                                    |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   |                       | Permissions management                     | Creating or deleting roles                                                                     |
   |                       |                                            |                                                                                                |
   |                       |                                            | Granting/Reclaiming roles                                                                      |
   |                       |                                            |                                                                                                |
   |                       |                                            | Granting/Reclaiming permissions                                                                |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   | HDFS audit log        | Permissions management                     | Managing permissions on files or folders                                                       |
   |                       |                                            |                                                                                                |
   |                       |                                            | Managing permissions on owner information files or folders                                     |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   |                       | File operation                             | Creating a folder                                                                              |
   |                       |                                            |                                                                                                |
   |                       |                                            | Creating a file                                                                                |
   |                       |                                            |                                                                                                |
   |                       |                                            | Opening a file                                                                                 |
   |                       |                                            |                                                                                                |
   |                       |                                            | Appending file content                                                                         |
   |                       |                                            |                                                                                                |
   |                       |                                            | Changing a file name                                                                           |
   |                       |                                            |                                                                                                |
   |                       |                                            | Deleting a file or folder                                                                      |
   |                       |                                            |                                                                                                |
   |                       |                                            | Setting time property of a file                                                                |
   |                       |                                            |                                                                                                |
   |                       |                                            | Setting the number of file copies                                                              |
   |                       |                                            |                                                                                                |
   |                       |                                            | Merging files                                                                                  |
   |                       |                                            |                                                                                                |
   |                       |                                            | Checking the file system                                                                       |
   |                       |                                            |                                                                                                |
   |                       |                                            | File links                                                                                     |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   | MapReduce audit log   | Application running                        | Starting a Container request                                                                   |
   |                       |                                            |                                                                                                |
   |                       |                                            | Stopping a Container request                                                                   |
   |                       |                                            |                                                                                                |
   |                       |                                            | After Container request is completed, the status of the request is displayed as succeeded.     |
   |                       |                                            |                                                                                                |
   |                       |                                            | After Container request is completed, the status of the request is displayed as failed.        |
   |                       |                                            |                                                                                                |
   |                       |                                            | After Container request is completed, the status of the request is displayed as suspended.     |
   |                       |                                            |                                                                                                |
   |                       |                                            | Submitting a task                                                                              |
   |                       |                                            |                                                                                                |
   |                       |                                            | Ending a task                                                                                  |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   | LdapServer audit log  | Maintenance management                     | Adding an operating system user                                                                |
   |                       |                                            |                                                                                                |
   |                       |                                            | Adding a user group                                                                            |
   |                       |                                            |                                                                                                |
   |                       |                                            | Adding a user to user group                                                                    |
   |                       |                                            |                                                                                                |
   |                       |                                            | Deleting a user                                                                                |
   |                       |                                            |                                                                                                |
   |                       |                                            | Deleting a group                                                                               |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   | KrbServer audit log   | Maintenance management                     | Changing the password of a Kerberos account                                                    |
   |                       |                                            |                                                                                                |
   |                       |                                            | Adding a Kerberos account                                                                      |
   |                       |                                            |                                                                                                |
   |                       |                                            | Deleting a Kerberos account                                                                    |
   |                       |                                            |                                                                                                |
   |                       |                                            | Authenticating a user                                                                          |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   | Loader audit log      | Security management                        | User login                                                                                     |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   |                       | Metadata management                        | Querying connector information                                                                 |
   |                       |                                            |                                                                                                |
   |                       |                                            | Querying a framework                                                                           |
   |                       |                                            |                                                                                                |
   |                       |                                            | Querying step information                                                                      |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   |                       | Managing data source connections           | Querying a data source connection                                                              |
   |                       |                                            |                                                                                                |
   |                       |                                            | Adding a data source connection                                                                |
   |                       |                                            |                                                                                                |
   |                       |                                            | Updating a data source connection                                                              |
   |                       |                                            |                                                                                                |
   |                       |                                            | Deleting a data source connection                                                              |
   |                       |                                            |                                                                                                |
   |                       |                                            | Activating a data source connection                                                            |
   |                       |                                            |                                                                                                |
   |                       |                                            | Disabling a data source connection                                                             |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   |                       | Job management                             | Querying a job                                                                                 |
   |                       |                                            |                                                                                                |
   |                       |                                            | Creating a Job                                                                                 |
   |                       |                                            |                                                                                                |
   |                       |                                            | Updating a Job                                                                                 |
   |                       |                                            |                                                                                                |
   |                       |                                            | Deleting a job                                                                                 |
   |                       |                                            |                                                                                                |
   |                       |                                            | Activating a job                                                                               |
   |                       |                                            |                                                                                                |
   |                       |                                            | Disabling a job                                                                                |
   |                       |                                            |                                                                                                |
   |                       |                                            | Querying all execution records of a job                                                        |
   |                       |                                            |                                                                                                |
   |                       |                                            | Querying the latest execution record of a job                                                  |
   |                       |                                            |                                                                                                |
   |                       |                                            | Submitting a job                                                                               |
   |                       |                                            |                                                                                                |
   |                       |                                            | Stopping a job                                                                                 |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   | Hue audit log         | Service startup                            | Starting Hue                                                                                   |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   |                       | User operation                             | User login                                                                                     |
   |                       |                                            |                                                                                                |
   |                       |                                            | User logout                                                                                    |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   |                       | Task operation                             | Creating a job                                                                                 |
   |                       |                                            |                                                                                                |
   |                       |                                            | Modifying a job                                                                                |
   |                       |                                            |                                                                                                |
   |                       |                                            | Deleting a job                                                                                 |
   |                       |                                            |                                                                                                |
   |                       |                                            | Submitting a task                                                                              |
   |                       |                                            |                                                                                                |
   |                       |                                            | Saving a task                                                                                  |
   |                       |                                            |                                                                                                |
   |                       |                                            | Updating the status of a task                                                                  |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   | ZooKeeper audit log   | Permissions management                     | Setting the access permission to Znode                                                         |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   |                       | Znode operation                            | Creating a Znode                                                                               |
   |                       |                                            |                                                                                                |
   |                       |                                            | Deleting a Znode                                                                               |
   |                       |                                            |                                                                                                |
   |                       |                                            | Configuring Znode data                                                                         |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   | Storm audit log       | Nimbus                                     | Submitting a topology                                                                          |
   |                       |                                            |                                                                                                |
   |                       |                                            | Stopping a topology                                                                            |
   |                       |                                            |                                                                                                |
   |                       |                                            | Reallocating a topology                                                                        |
   |                       |                                            |                                                                                                |
   |                       |                                            | Deactivating a topology                                                                        |
   |                       |                                            |                                                                                                |
   |                       |                                            | Activating a topology                                                                          |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+
   |                       | UI                                         | Stopping a topology                                                                            |
   |                       |                                            |                                                                                                |
   |                       |                                            | Reallocating a topology                                                                        |
   |                       |                                            |                                                                                                |
   |                       |                                            | Deactivating a topology                                                                        |
   |                       |                                            |                                                                                                |
   |                       |                                            | Activating a topology                                                                          |
   +-----------------------+--------------------------------------------+------------------------------------------------------------------------------------------------+

MRS audit logs are stored in the database. You can view and export audit logs on the **Audit** page.

The following table lists the directories to store component audit logs. Audit log files of some components are stored in **/var/log/Bigdata/audit**, such as HDFS, HBase, MapReduce, Hive, Hue, Yarn, Storm, and ZooKeeper. The component audit logs are automatically compressed and backed up to **/var/log/Bigdata/audit/bk** at 03: 00 every day. A maximum of latest 90 compressed backup files are retained, and the backup time cannot be changed.

Audit log files of other components are stored in the component log directory.

.. table:: **Table 6** Directory for storing component audit logs

   +-----------------------------------+-------------------------------------------------------------------------+
   | Component                         | Audit Log Directory                                                     |
   +===================================+=========================================================================+
   | DBService                         | /var/log/Bigdata/audit/dbservice/dbservice_audit.log                    |
   +-----------------------------------+-------------------------------------------------------------------------+
   | HDFS                              | /var/log/Bigdata/audit/hdfs/nn/hdfs-audit-namenode.log                  |
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
   | MapReduce                         | /var/log/Bigdata/audit/mapreduce/jobhistory/mapred-audit-jobhistory.log |
   +-----------------------------------+-------------------------------------------------------------------------+
   | Hive                              | /var/log/Bigdata/audit/hive/hiveserver/hive-audit.log                   |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/hive/metastore/metastore-audit.log               |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/hive/webhcat/webhcat-audit.log                   |
   +-----------------------------------+-------------------------------------------------------------------------+
   | Loader                            | /var/log/Bigdata/loader/audit/default.audit                             |
   +-----------------------------------+-------------------------------------------------------------------------+
   | Hue                               | /var/log/Bigdata/audit/hue/hue-audits.log                               |
   +-----------------------------------+-------------------------------------------------------------------------+
   | ZooKeeper                         | /var/log/Bigdata/audit/zookeeper/quorumpeer/zk-audit-quorumpeer.log     |
   +-----------------------------------+-------------------------------------------------------------------------+
   | Spark                             | /var/log/Bigdata/audit/spark/jdbcserver/jdbcserver-audit.log            |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/spark/jobhistory/jobhistory-audit.log            |
   +-----------------------------------+-------------------------------------------------------------------------+
   | Yarn                              | /var/log/Bigdata/audit/yarn/rm/yarn-audit-resourcemanager.log           |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/yarn/nm/yarn-audit-nodemanager.log               |
   +-----------------------------------+-------------------------------------------------------------------------+
   | Storm                             | /var/log/Bigdata/audit/storm/nimbus/audit.log                           |
   |                                   |                                                                         |
   |                                   | /var/log/Bigdata/audit/storm/ui/audit.log                               |
   +-----------------------------------+-------------------------------------------------------------------------+
