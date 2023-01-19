:original_name: mrs_01_24146.html

.. _mrs_01_24146:

Configuring a ClickHouse Data Source
====================================

Scenarios
---------

-  Currently, HetuEngine supports the interconnection with the ClickHouse data source in the cluster of MRS 3.1.1 or later.
-  The HetuEngine cluster in security mode supports the interconnection with the ClickHouse data source in the cluster of MRS 3.1.1 or later in security mode.
-  The HetuEngine cluster in normal mode supports the interconnection with the ClickHouse data source in the cluster of MRS 3.1.1 or later in normal mode.
-  In the ClickHouse data source, tables with the same name but in different cases, for example, **cktable** (lowercase), **CKTABLE** (uppercase), and **CKtable** (uppercase and lowercase), cannot co-exist in the same schema or database. Otherwise, tables in the schema or database cannot be used by HetuEngine.

Prerequisites
-------------

You have created a HetuEngine administrator by referring to :ref:`Creating a HetuEngine User <mrs_01_1714>`.

Procedure
---------

#. Log in to FusionInsight Manager as a HetuEngine administrator and choose **Cluster** > **Services** > **HetuEngine**. The **HetuEngine** service page is displayed.
#. In the **Basic Information** area on the **Dashboard** tab page, click the link next to **HSConsole WebUI**. The HSConsole page is displayed.
#. Choose **Data Source**.
#. Click **Add Data Source**. On the **Add Data Source** page that is displayed, configure parameters.

   a. Configure parameters in the **Basic Configuration** area. For details about the parameters, see :ref:`Table 1 <mrs_01_24146__en-us_topic_0000001219350589_table1019212591518>`.

      .. _mrs_01_24146__en-us_topic_0000001219350589_table1019212591518:

      .. table:: **Table 1** Basic Information

         +-----------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | Parameter             | Description                                                                                                    | Example Value         |
         +=======================+================================================================================================================+=======================+
         | Name                  | Name of the data source to be connected.                                                                       | clickhouse_1          |
         |                       |                                                                                                                |                       |
         |                       | The value can contain only letters, digits, and underscores (_) and must start with a letter.                  |                       |
         +-----------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | Data Source Type      | Type of the data source to be connected. Choose **JDBC** > **ClickHouse**.                                     | ClickHouse            |
         +-----------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | Description           | Description of the data source.                                                                                | ``-``                 |
         |                       |                                                                                                                |                       |
         |                       | The value can contain only letters, digits, commas (,), periods (.), underscores (_), spaces, and line breaks. |                       |
         +-----------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+

   b. Configure parameters in the **ClickHouse Configuration** area. For details, see :ref:`Table 2 <mrs_01_24146__en-us_topic_0000001219350589_table17193559125115>`.

      .. _mrs_01_24146__en-us_topic_0000001219350589_table17193559125115:

      .. table:: **Table 2** ClickHouse Configuration

         +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
         | Parameter                        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Example Value                                                                                                                                   |
         +==================================+===============================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+=================================================================================================================================================+
         | Driver                           | The default value is **clickhouse**.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | clickhouse                                                                                                                                      |
         +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
         | JDBC URL                         | JDBC URL of the ClickHouse data source.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | **jdbc:clickhouse://10.162.156.243:21426**, **jdbc:clickhouse://10.162.156.243:21425**, or **jdbc:clickhouse://[fec0::d916:8:5:164:200]:21426** |
         |                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                                                                                                 |
         |                                  | -  If the ClickHouse data source uses IPv4, the format is **jdbc:clickhouse://<host>:<port>**.                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                                                                                 |
         |                                  | -  If the ClickHouse data source uses IPv6, the format is **jdbc:clickhouse://[<host>]:<port>**.                                                                                                                                                                                                                                                                                                                                                                                                                                              |                                                                                                                                                 |
         |                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                                                                                                 |
         |                                  | -  To obtain the value of **<host>**, log in to Manager of the cluster where the ClickHouse data source is located, choose **Cluster** > **Services** > **ClickHouse** > **Instance**, and view the ClickHouseBalancer service IP address.                                                                                                                                                                                                                                                                                                    |                                                                                                                                                 |
         |                                  | -  To obtain the value of **<port>**, log in to Manager of the cluster where the ClickHouse data source is located, and choose **Cluster** > **Services** > **ClickHouse** > **Configurations** > **All Configurations**. If the ClickHouse data source is in security mode, check the HTTPS port number of the ClickHouseBalancer instance, that is, the value of **lb_https_port**. If the ClickHouse data source is in normal mode, check the HTTP port number of the ClickHouseBalancer instance, that is, the value of **lb_http_port**. |                                                                                                                                                 |
         +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
         | Username                         | Username used for connecting to the ClickHouse data source.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Change the value based on the username being connected with the data source.                                                                    |
         +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
         | Password                         | User password used for connecting to the ClickHouse data source.                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Change the value based on the user password for connecting to the data source.                                                                  |
         +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
         | Case-sensitive Table/Schema Name | Whether to support case-sensitive names or schemas of the data source.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | ``-``                                                                                                                                           |
         |                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                                                                                                 |
         |                                  | HetuEngine supports case-sensitive names or schemas of the data source.                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |                                                                                                                                                 |
         |                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                                                                                                 |
         |                                  | -  **No**: If multiple table names exist in the same schema of a data source, for example, **cktable** (lowercase), **CKTABLE** (uppercase), and **CKtable** (lowercase and uppercase), only **cktable** (lowercase) can be used by HetuEngine.                                                                                                                                                                                                                                                                                               |                                                                                                                                                 |
         |                                  | -  **Yes**: Only one table name can exist in the same schema of the data source, for example, **cktable** (lowercase), **CKTABLE** (uppercase), or **CKtable** (lowercase and uppercase). Otherwise, all tables in the schema cannot be used by HetuEngine.                                                                                                                                                                                                                                                                                   |                                                                                                                                                 |
         +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+

   c. (Optional) Customize the configuration.

      You can click **Add** to add custom configuration parameters. Configure custom parameters of the ClickHouse data source. For details, see :ref:`Table 3 <mrs_01_24146__en-us_topic_0000001219350589_table188672024123816>`.

      .. _mrs_01_24146__en-us_topic_0000001219350589_table188672024123816:

      .. table:: **Table 3** Custom parameters of the ClickHouse data source

         +------------------------------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | Parameter                                | Description                                                                                                    | Example Value         |
         +==========================================+================================================================================================================+=======================+
         | use-connection-pool                      | Whether to use the JDBC connection pool.                                                                       | true                  |
         +------------------------------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | jdbc.connection.pool.maxTotal            | Maximum number of connections in the JDBC connection pool.                                                     | 8                     |
         +------------------------------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | jdbc.connection.pool.maxIdle             | Maximum number of idle connections in the JDBC connection pool.                                                | 8                     |
         +------------------------------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | jdbc.connection.pool.minIdle             | Minimum number of idle connections in the JDBC connection pool.                                                | 0                     |
         +------------------------------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | jdbc.connection.pool.testOnBorrow        | Whether to check the connection validity when using a connection obtained from the JDBC connection pool.       | false                 |
         +------------------------------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | jdbc.pushdown-enabled                    | Whether to enable the pushdown function.                                                                       | true                  |
         |                                          |                                                                                                                |                       |
         |                                          | Default value: **true**                                                                                        |                       |
         +------------------------------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | jdbc.pushdown-module                     | Pushdown type.                                                                                                 | ``-``                 |
         |                                          |                                                                                                                |                       |
         |                                          | -  **DEFAULT**: No operator is pushed down.                                                                    |                       |
         |                                          | -  **BASE_PUSHDOWN**: Only operators such as Filter, Aggregation, Limit, TopN, and Projection are pushed down. |                       |
         |                                          | -  **FULL_PUSHDOWN**: All supported operators are pushed down.                                                 |                       |
         +------------------------------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | clickhouse.map-string-as-varchar         | Whether to convert the ClickHouse data source of the String and FixedString types to the Varchar type.         | true                  |
         |                                          |                                                                                                                |                       |
         |                                          | Default value: **true**                                                                                        |                       |
         +------------------------------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | clickhouse.socket-timeout                | Timeout interval for connecting to the ClickHouse data source.                                                 | 120000                |
         |                                          |                                                                                                                |                       |
         |                                          | Unit: millisecond                                                                                              |                       |
         |                                          |                                                                                                                |                       |
         |                                          | Default value: **120000**                                                                                      |                       |
         +------------------------------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+
         | case-insensitive-name-matching.cache-ttl | Timeout interval for caching case-sensitive names of schemas or tables of the data sources.                    | 1                     |
         |                                          |                                                                                                                |                       |
         |                                          | Unit: minute                                                                                                   |                       |
         |                                          |                                                                                                                |                       |
         |                                          | Default value: **1**                                                                                           |                       |
         +------------------------------------------+----------------------------------------------------------------------------------------------------------------+-----------------------+

      You can click **Delete** to delete custom configuration parameters.

   d. Click **OK**.

Operation Guide
---------------

-  :ref:`Table 4 <mrs_01_24146__en-us_topic_0000001219350589_table14995183764415>` lists the ClickHouse data types supported by HetuEngine.

   .. _mrs_01_24146__en-us_topic_0000001219350589_table14995183764415:

   .. table:: **Table 4** ClickHouse data types supported by HetuEngine

      +-----------------------------------------------+----------------------+---------------------------+
      | Name                                          | ClickHouse Data Type |                           |
      +===============================================+======================+===========================+
      | ClickHouse data types supported by HetuEngine | UInt8                | Decimal128(S)             |
      +-----------------------------------------------+----------------------+---------------------------+
      |                                               | UInt16               | Boolean                   |
      +-----------------------------------------------+----------------------+---------------------------+
      |                                               | UInt32               | String                    |
      +-----------------------------------------------+----------------------+---------------------------+
      |                                               | UInt64               | Fixedstring(N)            |
      +-----------------------------------------------+----------------------+---------------------------+
      |                                               | Int8                 | UUID                      |
      +-----------------------------------------------+----------------------+---------------------------+
      |                                               | Int16                | Date                      |
      +-----------------------------------------------+----------------------+---------------------------+
      |                                               | Int32                | DateTime([timezone])      |
      +-----------------------------------------------+----------------------+---------------------------+
      |                                               | Int64                | Enum                      |
      +-----------------------------------------------+----------------------+---------------------------+
      |                                               | Float32              | LowCardinality(data_type) |
      +-----------------------------------------------+----------------------+---------------------------+
      |                                               | Float64              | Nullable(typename)        |
      +-----------------------------------------------+----------------------+---------------------------+
      |                                               | Decimal(P, S)        | IPv4                      |
      +-----------------------------------------------+----------------------+---------------------------+
      |                                               | Decimal32(S)         | IPv6                      |
      +-----------------------------------------------+----------------------+---------------------------+
      |                                               | Decimal64(S)         | ``-``                     |
      +-----------------------------------------------+----------------------+---------------------------+

-  :ref:`Table 5 <mrs_01_24146__en-us_topic_0000001219350589_table7424121341219>` lists the tables and views that support the interconnection between HetuEngine and ClickHouse.

   .. _mrs_01_24146__en-us_topic_0000001219350589_table7424121341219:

   .. table:: **Table 5** Supported tables and views

      +---------------------------------------------------------------------------+-------------------------------------------------+
      | Name                                                                      | Supported Table and View                        |
      +===========================================================================+=================================================+
      | Tables that support the interconnection between HetuEngine and ClickHouse | Local table (MergeTree)                         |
      +---------------------------------------------------------------------------+-------------------------------------------------+
      |                                                                           | Replicated table (ReplicatedReplacingMergeTree) |
      +---------------------------------------------------------------------------+-------------------------------------------------+
      |                                                                           | Distributed table                               |
      +---------------------------------------------------------------------------+-------------------------------------------------+
      | Views that support the interconnection between HetuEngine and ClickHouse  | Normal view                                     |
      +---------------------------------------------------------------------------+-------------------------------------------------+
      |                                                                           | Materialized view                               |
      +---------------------------------------------------------------------------+-------------------------------------------------+
