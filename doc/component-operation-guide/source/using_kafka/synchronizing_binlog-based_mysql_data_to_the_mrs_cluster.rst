:original_name: mrs_01_0441.html

.. _mrs_01_0441:

Synchronizing Binlog-based MySQL Data to the MRS Cluster
========================================================

This section describes how to use the Maxwell data synchronization tool to migrate offline binlog-based data to an MRS Kafka cluster.

Maxwell is an open source application that reads MySQL binlogs, converts operations, such as addition, deletion, and modification, into a JSON format, and sends them to an output end, such as a console, a file, and Kafka. For details about Maxwell, visit https://maxwells-daemon.io. Maxwell can be deployed on a MySQL server or on other servers that can communicate with MySQL.

Maxwell runs on a Linux server, including EulerOS, Ubuntu, Debian, CentOS, and OpenSUSE. Java 1.8+ must be supported.

The following provides details about data synchronization.

#. :ref:`Configuring MySQL <mrs_01_0441__section17682011252>`
#. :ref:`Installing Maxwell <mrs_01_0441__section935158131710>`
#. :ref:`Configuring Maxwell <mrs_01_0441__section897274173612>`
#. :ref:`Starting Maxwell <mrs_01_0441__section182543817211>`
#. :ref:`Verifying Maxwell <mrs_01_0441__section191261916641>`
#. :ref:`Stopping Maxwell <mrs_01_0441__section07395261236>`
#. :ref:`Format of the Maxwell Generated Data and Description of Common Fields <mrs_01_0441__section3609745132419>`

.. _mrs_01_0441__section17682011252:

Configuring MySQL
-----------------

#. Start the binlog, open the **my.cnf** file in MySQL, and check whether **server_id**, **log-bin**, and **binlog_format** are configured in the **[mysqld]** block. If they are not configured, run the following command to add configuration items and restart MySQL. If they are configured, skip this step.

   .. code-block::

      $ vi my.cnf

      [mysqld]
      server_id=1
      log-bin=master
      binlog_format=row

#. .. _mrs_01_0441__li101111736164511:

   Maxwell needs to connect to MySQL, create a database named **maxwell** for storing metadata, and access the database to be synchronized. Therefore, you are advised to create a MySQL user for Maxwell to use. Log in to MySQL as user **root** and run the following commands to create a user named **maxwell** (*XXXXXX* indicates the password and needs to be replaced with actual one).

   -  If Maxwell is deployed on a non-MySQL server, the created user **maxwell** must have a permission to remotely log in to the database. In this case, run the following command to create the user:

      **mysql> GRANT ALL on maxwell.\* to 'maxwell'@'%' identified by 'XXXXXX';**

      **mysql> GRANT SELECT, REPLICATION CLIENT, REPLICATION SLAVE on \*.\* to 'maxwell'@'%';**

   -  If Maxwell is deployed on the MySQL server, the created user **maxwell** can be configured to log in to the database only on the local host. In this case, run the following command:

      **mysql> GRANT SELECT, REPLICATION CLIENT, REPLICATION SLAVE on \*.\* to 'maxwell'@'localhost' identified by 'XXXXXX';**

      **mysql> GRANT ALL on maxwell.\* to 'maxwell'@'localhost';**

.. _mrs_01_0441__section935158131710:

Installing Maxwell
------------------

#. Download the installation package at https://github.com/zendesk/maxwell/releases and select the **maxwell-XXX.tar.gz** binary file for download. In the file name, **XXX** indicates a version number.

#. Upload the **tar.gz** package to any directory (the **/opt** directory of the Master node used as an example here).

#. Log in to the server where Maxwell is deployed and run the following command to go to the directory where the **tar.gz** package is stored.

   **cd /opt**

#. Run the following commands to decompress the **maxwell-XXX.tar.gz** package and go to the **maxwell-XXX** directory:

   **tar -zxvf maxwell-XXX.tar.gz**

   **cd maxwell-XXX**

.. _mrs_01_0441__section897274173612:

Configuring Maxwell
-------------------

If the **conf** directory exists in the **maxwell-XXX** folder, configure the **config.properties** file. For details about the configuration items, see :ref:`Table 1 <mrs_01_0441__table49411722133920>`. If the **conf** directory does not exist, change **config.properties.example** in the **maxwell-XXX** folder to **config.properties**.

.. _mrs_01_0441__table49411722133920:

.. table:: **Table 1** Maxwell configuration item description

   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | Parameter               | Mandatory       | Description                                                                                                                                                                                                          | Default Value   |
   +=========================+=================+======================================================================================================================================================================================================================+=================+
   | user                    | Yes             | Name of the user for connecting to MySQL, that is, the user created in :ref:`2 <mrs_01_0441__li101111736164511>`.                                                                                                    | ``-``           |
   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | password                | Yes             | Password for connecting to MySQL                                                                                                                                                                                     | ``-``           |
   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | host                    | No              | MySQL address                                                                                                                                                                                                        | localhost       |
   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | port                    | No              | MySQL port                                                                                                                                                                                                           | 3306            |
   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | log_level               | No              | Log print level. The options are as follows:                                                                                                                                                                         | info            |
   |                         |                 |                                                                                                                                                                                                                      |                 |
   |                         |                 | -  debug                                                                                                                                                                                                             |                 |
   |                         |                 | -  info                                                                                                                                                                                                              |                 |
   |                         |                 | -  warn                                                                                                                                                                                                              |                 |
   |                         |                 | -  error                                                                                                                                                                                                             |                 |
   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | output_ddl              | No              | Whether to send a DDL (modified based on definitions of the database and data table) event                                                                                                                           | false           |
   |                         |                 |                                                                                                                                                                                                                      |                 |
   |                         |                 | -  **true**: Send DDL events.                                                                                                                                                                                        |                 |
   |                         |                 | -  **false**: Do not send DDL events.                                                                                                                                                                                |                 |
   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | producer                | Yes             | Producer type. Set this parameter to **kafka**.                                                                                                                                                                      | stdout          |
   |                         |                 |                                                                                                                                                                                                                      |                 |
   |                         |                 | -  **stdout**: Log the generated events.                                                                                                                                                                             |                 |
   |                         |                 | -  **kafka**: Send the generated events to Kafka.                                                                                                                                                                    |                 |
   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | producer_partition_by   | No              | Partition policy used to ensure that data of the same type is written to the same partition of Kafka.                                                                                                                | databa          |
   |                         |                 |                                                                                                                                                                                                                      |                 |
   |                         |                 | -  **database**: Events of the same database are written to the same partition of Kafka.                                                                                                                             |                 |
   |                         |                 | -  **table**: Events of the same table are written to the same partition of Kafka.                                                                                                                                   |                 |
   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | ignore_producer_error   | No              | Specifies whether to ignore the error that the producer fails to send data.                                                                                                                                          | true            |
   |                         |                 |                                                                                                                                                                                                                      |                 |
   |                         |                 | -  **true**: The error information is logged and the error data is skipped. The program continues to run.                                                                                                            |                 |
   |                         |                 | -  **false**: The error information is logged and the program is terminated.                                                                                                                                         |                 |
   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | metrics_slf4j_interval  | No              | Interval for outputting statistics on data successfully uploaded or failed to be uploaded to Kafka in logs. The unit is second.                                                                                      | 60              |
   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | kafka.bootstrap.servers | Yes             | Address of the Kafka proxy node. The value is in the format of **HOST:PORT[,HOST:PORT]**.                                                                                                                            | ``-``           |
   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | kafka_topic             | No              | Name of the topic that is written to Kafka                                                                                                                                                                           | maxwell         |
   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | dead_letter_topic       | No              | Kafka topic used to record the primary key of the error log record when an error occurs when the record is sent                                                                                                      | ``-``           |
   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | kafka_version           | No              | Kafka producer version used by Maxwell, which cannot be configured in the **config.properties** file. You need to use the **-- kafka_version xxx** parameter to import the version number when starting the command. | ``-``           |
   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | kafka_partition_hash    | No              | Kafka topic partitioning algorithm. The value can be **default** or **murmur3**.                                                                                                                                     | default         |
   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | kafka_key_format        | No              | Key generation method of the Kafka record. The value can be **array** or **Hash**.                                                                                                                                   | Hash            |
   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | ddl_kafka_topic         | No              | Topic that is written to the DDL operation when **output_ddl** is set to **true**                                                                                                                                    | {kafka_topic}   |
   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | filter                  | No              | Used to filter databases or tables.                                                                                                                                                                                  | ``-``           |
   |                         |                 |                                                                                                                                                                                                                      |                 |
   |                         |                 | -  If only the **mydatabase** database needs to be collected, set this parameter to the following:                                                                                                                   |                 |
   |                         |                 |                                                                                                                                                                                                                      |                 |
   |                         |                 |    exclude: \*.*,include: mydatabase.\*                                                                                                                                                                              |                 |
   |                         |                 |                                                                                                                                                                                                                      |                 |
   |                         |                 | -  If only the **mydatabase.mytable** table needs to be collected, set this parameter to the following:                                                                                                              |                 |
   |                         |                 |                                                                                                                                                                                                                      |                 |
   |                         |                 |    exclude: \*.*,include: mydatabase.mytable                                                                                                                                                                         |                 |
   |                         |                 |                                                                                                                                                                                                                      |                 |
   |                         |                 | -  If only the **mytable**, **mydate_123**, and **mydate_456** tables in the **mydatabase** database need to be collected, set this parameter to the following:                                                      |                 |
   |                         |                 |                                                                                                                                                                                                                      |                 |
   |                         |                 |    exclude: \*.*,include: mydatabase.mytable, include: mydatabase./mydat\ ``_``\\d*/                                                                                                                                 |                 |
   +-------------------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+

.. _mrs_01_0441__section182543817211:

Starting Maxwell
----------------

#. Log in to the server where Maxwell is deployed.

#. Run the following command to go to the Maxwell installation directory:

   **cd /opt/maxwell-1.21.0/**

   .. note::

      For the first time to use Maxwell, you are advised to change **log_level** in **conf/config.properties** to **debug** (debug level) so that you can check whether data can be obtained from MySQL and sent to Kafka after startup. After the entire process is debugged, change **log_level** to **info**, and then restart Maxwell for the modification to take effect.

      # log level [debug \| info \| warn \| error]

      log_level=debug

#. Run the following commands to start Maxwell:

   **source /opt/client/bigdata_env**

   **bin/Maxwell**

   **bin/maxwell --user='maxwell' --password='XXXXXX' --host='127.0.0.1' \\**

   **--producer=kafka --kafka.bootstrap.servers=kafkahost:9092 --kafka_topic=Maxwell**

   In the preceding commands, **user**, **password**, and **host** indicate the username, password, and IP address of MySQL, respectively. You can configure the three parameters by modifying configurations of the configuration items or using the preceding commands. **kafkahost** indicates the IP address of the Core node in the streaming cluster.

   If information similar to the following appears, Maxwell has started successfully:

   .. code-block::

      Success to start Maxwell [78092].

.. _mrs_01_0441__section191261916641:

Verifying Maxwell
-----------------

#. Log in to the server where Maxwell is deployed.

#. View the logs. If the log file does not contain an ERROR log and the following information is displayed, the connection between Maxwell and MySQL is normal:

   .. code-block::

      BinlogConnectorLifecycleListener - Binlog connected.

#. Log in to the MySQL database and update, create, or delete test data. The following provides operation statement examples for your reference.

   .. code-block::

      --Creating a database
      create database test;
      --Creating a table
      create table test.e (
        id int(10) not null primary key auto_increment,
        m double,
        c timestamp(6),
        comment varchar(255) charset 'latin1'
      );
      -- Adding a record
      insert into test.e set m = 4.2341, c = now(3), comment = 'I am a creature of light.';
      --Updating a record
      update test.e set m = 5.444, c = now(3) where id = 1;
      --Deleting a record
      delete from test.e where id = 1;
      --Modifying a table
      alter table test.e add column torvalds bigint unsigned after m;
      --Deleting a table
      drop table test.e;
      -- Deleting a database
      drop database test;

#. Check the Maxwell logs. If no WARN/ERROR is displayed, Maxwell is installed and configured properly.

   To check whether the data is successfully uploaded, set **log_level** in the **config.properties** file to **debug**. When the data is successfully uploaded, the following JSON data is printed immediately. For details about the fields, see :ref:`Format of the Maxwell Generated Data and Description of Common Fields <mrs_01_0441__section3609745132419>`.

   .. code-block::

      {"database":"test","table":"e","type":"insert","ts":1541150929,"xid":60556,"commit":true,"data":{"id":1,"m":4.2341,"c":"2018-11-02 09:28:49.297000","comment":"I am a creature of light."}}
      ......

   .. note::

      After the entire process is debugged, you can change the value of **log_level** in the **config.properties** file to **info** to reduce the number of logs to be printed and restart Maxwell for the modification to take effect.

      .. code-block::

         # log level [debug | info | warn | error]
         log_level=info

.. _mrs_01_0441__section07395261236:

Stopping Maxwell
----------------

#. Log in to the server where Maxwell is deployed.

#. Run the command to obtain the Maxwell process ID (PID). The second field in the command output is PID.

   **ps -ef \| grep Maxwell \| grep -v grep**

#. Run the following command to forcibly stop the Maxwell process:

   **kill -9 PID**

.. _mrs_01_0441__section3609745132419:

Format of the Maxwell Generated Data and Description of Common Fields
---------------------------------------------------------------------

The data generated by Maxwell is in JSON format. The common fields are described as follows:

-  **type**: operation type. The options are **database-create**, **database-drop**, **table-create**, **table-drop**, **table-alter**, **insert**, **update**, and **delete**.
-  **database**: name of the database to be operated
-  **ts**: operation time, which is a 13-digit timestamp
-  **table**: name of the table to be operated
-  **data**: content after data is added, deleted, or modified
-  **old**: content before data is modified or schema definition before a table is modified
-  **sql**: SQL statement for DDL operations
-  **def**: schema definition for table creation and modification
-  **xid**: unique ID of an object
-  **commit**: check whether such operations as data addition, deletion, and modification have been submitted.
