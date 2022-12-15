:original_name: mrs_01_24184.html

.. _mrs_01_24184:

Using a ClickHouse Client
=========================

ClickHouse is a column-based database oriented to online analysis and processing. It supports SQL query and provides good query performance. The aggregation analysis and query performance based on large and wide tables is excellent, which is one order of magnitude faster than other analytical databases.

Prerequisites
-------------

You have installed the client, for example, in the **/opt/hadoopclient** directory. The client directory in the following operations is only an example. Change it to the actual installation directory. Before using the client, download and update the client configuration file, and ensure that the active management node of Manager is available.

Procedure
---------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to go to the client installation directory:

   **cd /opt/hadoopclient**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the current user. The current user must have the permission to create ClickHouse tables. If Kerberos authentication is disabled for the current cluster, skip this step.

   a. Run the following command if it is an MRS 3.1.0 cluster:

      **export CLICKHOUSE_SECURITY_ENABLED=true**

   b. **kinit** *Component service user*

      Example: **kinit clickhouseuser**

#. Run the client command of the ClickHouse component.

   Run the **clickhouse -h** command to view the command help of ClickHouse.

   The command output is as follows:

   .. code-block::

      Use one of the following commands:
      clickhouse local [args]
      clickhouse client [args]
      clickhouse benchmark [args]
      clickhouse server [args]
      clickhouse performance-test [args]
      clickhouse extract-from-config [args]
      clickhouse compressor [args]
      clickhouse format [args]
      clickhouse copier [args]
      clickhouse obfuscator [args]
      ...

   For details about how to use the command, see https://clickhouse.tech/docs/en/operations/.

   Run the **clickhouse client** command to connect to the ClickHouse serverif MRS 3.1.0 or later.

   -  Command for using SSL to log in to a ClickHouse cluster with Kerberos authentication disabled

      **clickhouse client --host** *IP address of the ClickHouse instance*\ **--user** *Username* **--password** **--port** 9440 **--secure**

      *Enter the user password.*

   -  Using SSL for login when Kerberos authentication is enabled for the current cluster:

      You must create a user on Manager because there is no default user.

      After the user authentication is successful, you do not need to carry the **--user** and **--password** parameters when logging in to the client as the authenticated user.

      **clickhouse client --host** *IP address of the ClickHouse instance* **--port** 9440 **--secure**

      The following table describes the parameters of the **clickhouse client** command.

   .. table:: **Table 1** Parameters of the **clickhouse client** command

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                                                                    |
      +===================================+================================================================================================================================================================================================================================================================================================================================================================+
      | --host                            | Host name of the server. The default value is **localhost**. You can use the host name or IP address of the node where the ClickHouse instance is located.                                                                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   | .. note::                                                                                                                                                                                                                                                                                                                                                      |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   |    You can log in to FusionInsight Manager and choose **Cluster** > **Services** > **ClickHouse** > **Instance** to obtain the service IP address of the ClickHouseServer instance.                                                                                                                                                                            |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | --port                            | Port for connection.                                                                                                                                                                                                                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   | -  If the SSL security connection is used, the default port number is **9440**, the parameter **--secure** must be carried. For details about the port number, search for the **tcp_port_secure** parameter in the ClickHouseServer instance configuration.                                                                                                    |
      |                                   | -  If non-SSL security connection is used, the default port number is **9000**, the parameter **--secure** does not need to be carried. For details about the port number, search for the **tcp_port** parameter in the ClickHouseServer instance configuration.                                                                                               |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | --user                            | Username.                                                                                                                                                                                                                                                                                                                                                      |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   | You can create the user on Manager and bind a role to the user.                                                                                                                                                                                                                                                                                                |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   | -  If Kerberos authentication is enabled for the current cluster and the user authentication is successful, you do not need to carry the **--user** and **--password** parameters when logging in to the client as the authenticated user. You must create a user with this name on Manager because there is no default user in the Kerberos cluster scenario. |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   | -  If Kerberos authentication is not enabled for the current cluster, you can specify a user and its password created on Manager when logging in to the client. If the user and password parameters are not carried, user **default** is used for login by default.                                                                                            |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   |    The user in normal mode (Kerberos authentication disabled) is the default user, or you can create an administrator using the open source capability provided by the ClickHouse community. You cannot use the users created on FusionInsight Manager.                                                                                                        |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | --password                        | Password. The default password is an empty string. This parameter is used together with the **--user** parameter. You can set a password when creating a user on Manager.                                                                                                                                                                                      |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | --query                           | Query to process when using non-interactive mode.                                                                                                                                                                                                                                                                                                              |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | --database                        | Current default database. The default value is **default**, which is the default configuration on the server.                                                                                                                                                                                                                                                  |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | --multiline                       | If this parameter is specified, multiline queries are allowed. (**Enter** only indicates line feed and does not indicate that the query statement is complete.)                                                                                                                                                                                                |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | --multiquery                      | If this parameter is specified, multiple queries separated with semicolons (;) can be processed. This parameter is valid only in non-interactive mode.                                                                                                                                                                                                         |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | --format                          | Specified default format used to output the result.                                                                                                                                                                                                                                                                                                            |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | --vertical                        | If this parameter is specified, the result is output in vertical format by default. In this format, each value is printed on a separate line, which helps to display a wide table.                                                                                                                                                                             |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | --time                            | If this parameter is specified, the query execution time is printed to **stderr** in non-interactive mode.                                                                                                                                                                                                                                                     |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | --stacktrace                      | If this parameter is specified, stack trace information will be printed when an exception occurs.                                                                                                                                                                                                                                                              |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | --config-file                     | Name of the configuration file.                                                                                                                                                                                                                                                                                                                                |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | --secure                          | If this parameter is specified, the server will be connected in SSL mode.                                                                                                                                                                                                                                                                                      |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | --history_file                    | Path of files that record command history.                                                                                                                                                                                                                                                                                                                     |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | --param_<name>                    | Query with parameters. Pass values from the client to the server. For details, see https://clickhouse.tech/docs/en/interfaces/cli/#cli-queries-with-parameters.                                                                                                                                                                                                |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
