:original_name: mrs_01_24124.html

.. _mrs_01_24124:

CDL Usage Instructions
======================

CDL is a simple and efficient real-time data integration service. It captures data change events from various OLTP databases and pushes them to Kafka. The Sink Connector consumes data in topics and imports the data to the software applications of big data ecosystems. In this way, data is imported to the data lake in real time.

The CDL service contains two roles: CDLConnector and CDLService. CDLConnector is the instance for executing a data capture job, and CDLService is the instance for managing and creating a job.

You can create data synchronization and comparison tasks on the CDLService WebUI.

Data synchronization task
-------------------------

-  The CDL supports the following types of data synchronization tasks:

   .. table:: **Table 1** Data synchronization task types supported by the CDL

      +-------------+-----------------+-------------------------------------------------------------------+
      | Data source | Destination end | Description                                                       |
      +=============+=================+===================================================================+
      | MySQL       | Hudi            | This task synchronizes data from the MySQL database to Hudi.      |
      +-------------+-----------------+-------------------------------------------------------------------+
      |             | Kafka           | This task synchronizes data from the MySQL database to Kafka.     |
      +-------------+-----------------+-------------------------------------------------------------------+
      | PgSQL       | Hudi            | This task synchronizes data from the PgSQL database to Hudi.      |
      +-------------+-----------------+-------------------------------------------------------------------+
      |             | Kafka           | This task synchronizes data from the PgSQL database to Kafka.     |
      +-------------+-----------------+-------------------------------------------------------------------+
      | Hudi        | DWS             | This task synchronizes data from the Hudi database to DWS.        |
      +-------------+-----------------+-------------------------------------------------------------------+
      |             | ClickHouse      | This task synchronizes data from the Hudi database to ClickHouse. |
      +-------------+-----------------+-------------------------------------------------------------------+
      | ThirdKafka  | Hudi            | This task synchronizes data from the ThirdKafka database to Hudi. |
      +-------------+-----------------+-------------------------------------------------------------------+

-  Usage Constraints:

   -  If CDL is required, the value of **log.cleanup.policy** of Kafka must be **delete**.

   -  The CDL service has been installed in the MRS cluster.

   -  CDL can capture incremental data only from non-system tables, but not from built-in databases of databases such as MySQL, and PostgreSQL.

   -  .. _mrs_01_24124__li268123915168:

      Binary logging (enabled by default) and GTID have been enabled for the MySQL database. CDL cannot fetch tables whose names contain special characters such as the dollar sign ($) character.

      **To check whether binary logging is enabled for the MySQL database:**

      Use a tool (Navicat is used in this example) or CLI to connect to the MySQL database and run the **show variables like 'log_%'** command to view the configuration.

      For example, in Navicat, choose **File** > **New Query** to create a query, enter the following SQL statement, and click **Run**. If **log_bin** is displayed as **ON** in the result, the function is enabled successfully.

      **show variables like 'log_%'**

      |image1|

      **If the bin log function of the MySQL database is not enabled, perform the following operations:**

      Modify the MySQL configuration file **my.cnf** (**my.ini** for Windows) as follows:

      .. code-block::

         server-id         = 223344
         log_bin           = mysql-bin
         binlog_format     = ROW
         binlog_row_image  = FULL
         expire_logs_days  = 10

      After the modification, restart MySQL for the configurations to take effect.

      **To check whether GTID is enabled for the MySQL database:**

      Run the **show global variables like '%gtid%'** command to check whether GTID is enabled. For details, see the official documentation of the corresponding MySQL version. (For details about how to enable the function in MySQL 8.x, see https://dev.mysql.com/doc/refman/8.0/en/replication-mode-change-online-enable-gtids.html.)

      |image2|

      **Set user permissions:**

      To execute MySQL tasks, users must have the **SELECT**, **RELOAD**, **SHOW DATABASES**, **REPLICATION SLAVE** and **REPLICATION CLIENT** permissions.

      Run the following command to grant the permissions:

      **GRANT SELECT, RELOAD, SHOW DATABASES, REPLICATION SLAVE, REPLICATION CLIENT ON \*.\* TO** '*Username*' **IDENTIFIED BY** '*Password*';

      Run the following command to update the permissions:

      **FLUSH PRIVILEGES;**

   -  .. _mrs_01_24124__li1868193914169:

      The write-ahead log policy is modified for the PostgreSQL database.

      .. note::

         -  The user for connecting to the PostgreSQL database must have the replication permission, the CREATE permission on the database, and is the owner of tables.

         -  CDL cannot fetch tables whose names contain special characters such as the dollar sign ($) character.

         -  For PostgreSQL databases, you must have the permission to set the **statement_timeout** and **lock_timeout** parameters and the permission to query and delete slots and publications.

         -  You are advised to set **max_wal_senders** to 1.5 or 2 times the value of **Slot**.

         -  If the replication identifier of a PostgreSQL table is **default**, enable the full field completion function in the following scenarios:

            -  Scenario 1:

               When the **delete** operation is performed on the source database, a **delete** event contains only the primary key information. In this case, for the **delete** data written to Hudi, only the primary key has values, and the values of other service fields are **null**.

            -  Scenario 2:

               When the size of a single piece of data in the database exceeds 8 KB (including 8 KB), an **update** event contains only changed fields. In this case, the values of some fields in the Hudi data are **\__debezium_unavailable_value**.

            The related commands are as follows:

            -  Command for querying the replication identifier of a PostgreSQL table:

               **SELECT CASE relreplident WHEN 'd' THEN 'default' WHEN 'n' THEN 'nothing' WHEN 'f' THEN 'full' WHEN 'i' THEN 'index' END AS replica_identity FROM pg_class WHERE oid = '**\ *tablename*\ **'::regclass;**

            -  Command for enabling the full field completion function for a table:

               **ALTER TABLE** *tablename* **REPLICA IDENTITY FULL;**

      #. Modify **wal_level = logical** in the database configuration file **postgresql.conf** (which is stored in the **data** folder in the PostgreSQL installation directory by default).

         .. code-block::

            #------------------------------------------------
            #WRITE-AHEAD LOG
            #------------------------------------------------

            # - Settings -
            wal_level = logical         # minimal, replica, or logical
                                    # (change requires restart)
            #fsync = on             #flush data to disk for crash safety
            ...

      #. Restart the database service.

         .. code-block::

            # Stop
            pg_ctl stop
            # Start
            pg_ctl start

   -  .. _mrs_01_24124__li6127144552014:

      Prerequisites for the DWS database

      Before a synchronization task is started, both the source and target tables exist and have the same table structure. The value of **ads_last_update_date** in the DWS table is the current system time.

   -  .. _mrs_01_24124__li347115587209:

      Prerequisites for ThirdPartyKafka

      The upper-layer source supports openGauss and OGG. Kafka topics at the source end can be consumed by Kafka in the MRS cluster.

   -  Prerequisites for ClickHouse

      You have the permissions to operate ClickHouse. For details, see :ref:`ClickHouse User and Permission Management <mrs_01_24057>`.

Data Types and Mapping Supported by CDL Synchronization Tasks
-------------------------------------------------------------

This section describes the data types supported by CDL synchronization tasks and the mapping between data types of the source database and Spark data types.

.. table:: **Table 2** Mapping between PostgreSQL and Spark data types

   ==================== ======================
   PostgreSQL Data Type Spark (Hudi) Data Type
   ==================== ======================
   int2                 int
   int4                 int
   int8                 bigint
   numeric(p, s)        decimal[p,s]
   bool                 boolean
   char                 string
   varchar              string
   text                 string
   timestamptz          timestamp
   timestamp            timestamp
   date                 date
   json, jsonb          string
   float4               float
   float8               double
   ==================== ======================

.. table:: **Table 3** Mapping between MySQL and Spark data types

   =============== ======================
   MySQL Data Type Spark (Hudi) Data Type
   =============== ======================
   int             int
   integer         int
   bigint          bigint
   double          double
   decimal[p,s]    decimal[p,s]
   varchar         string
   char            string
   text            string
   timestamp       timestamp
   datetime        timestamp
   date            date
   json            string
   float           double
   =============== ======================

.. table:: **Table 4** Mapping between Ogg and Spark data types

   ======================== ======================
   Oracle Data Type         Spark (Hudi) Data Type
   ======================== ======================
   NUMBER(3), NUMBER(5)     bigint
   INTEGER                  decimal
   NUMBER(20)               decimal
   NUMBER                   decimal
   BINARY_DOUBLE            double
   CHAR                     string
   VARCHAR                  string
   TIMESTAMP, DATETIME      timestamp
   timestamp with time zone timestamp
   DATE                     timestamp
   ======================== ======================

.. table:: **Table 5** Mapping between Spark (Hudi) and DWS data types

   ====================== =============
   Spark (Hudi) Data Type DWS Data Type
   ====================== =============
   int                    int
   long                   bigint
   float                  float
   double                 double
   decimal[p,s]           decimal[p,s]
   boolean                boolean
   string                 varchar
   date                   date
   timestamp              timestamp
   ====================== =============

.. table:: **Table 6** Mapping between Spark (Hudi) and ClickHouse data types

   +------------------------+----------------------------------------------------------------------------------------------------+
   | Spark (Hudi) Data Type | ClickHouse Data Type                                                                               |
   +========================+====================================================================================================+
   | int                    | Int32                                                                                              |
   +------------------------+----------------------------------------------------------------------------------------------------+
   | long                   | Int64 (bigint)                                                                                     |
   +------------------------+----------------------------------------------------------------------------------------------------+
   | float                  | Float32 (float)                                                                                    |
   +------------------------+----------------------------------------------------------------------------------------------------+
   | double                 | Float64 (double)                                                                                   |
   +------------------------+----------------------------------------------------------------------------------------------------+
   | decimal[p,s]           | Decimal(P,S)                                                                                       |
   +------------------------+----------------------------------------------------------------------------------------------------+
   | boolean                | bool                                                                                               |
   +------------------------+----------------------------------------------------------------------------------------------------+
   | string                 | String (LONGTEXT, MEDIUMTEXT, TINYTEXT, TEXT, LONGBLOB, MEDIUMBLOB, TINYBLOB, BLOB, VARCHAR, CHAR) |
   +------------------------+----------------------------------------------------------------------------------------------------+
   | date                   | Date                                                                                               |
   +------------------------+----------------------------------------------------------------------------------------------------+
   | timestamp              | DateTime                                                                                           |
   +------------------------+----------------------------------------------------------------------------------------------------+

Data comparison task
--------------------

Data comparison checks the consistency between data in the source database and that in the target Hive. If the data is inconsistent, CDL can attempt to repair the inconsistent data. For detail, see :ref:`Creating a CDL Data Comparison Job <mrs_01_24775>`.

.. |image1| image:: /_static/images/en-us_image_0000001532472704.png
.. |image2| image:: /_static/images/en-us_image_0000001532791924.png
