:original_name: mrs_01_1164.html

.. _mrs_01_1164:

Example for Using the Open-Source sqoop-shell Tool (Oracle-HBase)
=================================================================

Scenario
--------

Taking **Importing Data from Oracle to HBase** as an example, this section introduces how to use the sqoop-shell tool to create and start Loader jobs in the interaction mode and batch mode.

Prerequisites
-------------

The Loader client has been installed and configured.

Example for the Interaction Mode
--------------------------------

#. Log in to the node where the Loader client is installed as the user who installs the client.

#. Run the following command to go to the **conf** directory of the sqoop-shell tool. For example, if the Loader client installation directory is **/opt/hadoopclient/Loader**, run the following command:

   **cd /opt/hadoopclient/Loader/loader-tools-1.99.3/sqoop-shell/conf**

#. Run the following command to configure authentication information:

   **vi client.properties**

   .. code-block::

      server.url=10.0.0.1:21351
      # simple or kerberos
      authentication.type=simple
      # true or false
      use.keytab=true

      authentication.user=
      authentication.password=

      client.principal=oracle/hadoop@<system domain name>

      # keytab file
      client.keytab.file=./conf/login/oracle.keytab

   .. note::

      Log in to FusionInsight Manager and choose **System** > **Permission** > **Domain and Mutual Trust**. The value of **Local Domain** is the current system domain name.

   .. table:: **Table 1** Configuration parameters

      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
      | Configuration parameters | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Example Value                    |
      +==========================+===========================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+==================================+
      | server.url               | Floating IP address and port (21351) for Loader.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | 10.0.0.1:21351                   |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | For compatibility, multiple IP addresses and ports can be configured and need to be separated by **commas (,)**. The first IP address and port must be those of Loader (21351). The others can be configured based on service requirements.                                                                                                                                                                                                                                                                                                               |                                  |
      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
      | authentication.type      | Login authentication mode.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | kerberos                         |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | -  **kerberos** indicates that the security mode is used and Kerberos authentication is performed. Kerberos authentication provides two authentication modes: the password mode and the keytab file mode.                                                                                                                                                                                                                                                                                                                                                 |                                  |
      |                          | -  **simple** indicates that the normal mode is used and Kerberos authentication is not performed.                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                  |
      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
      | authentication.user      | User for login when the normal mode or password authentication is used.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | bar                              |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | In the keytab login mode, this parameter does not need to be set.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                                  |
      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
      | authentication.password  | User password for login when the password authentication mode is used.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | 43B80E33A96DF3D203ABBDFD1050C041 |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | In the normal mode or keytab login mode, this parameter does not need to be set.                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |                                  |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | The password needs to be encrypted. The encryption method is described as follows:                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                  |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | a. Go to the directory where **encrypt_tool** is located. For example, if the Loader client installation directory is **/opt/hadoopclient/Loader**, run the following command:                                                                                                                                                                                                                                                                                                                                                                            |                                  |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          |    **cd /opt/hadoopclient/Loader/loader-tools-1.99.3**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |                                  |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | b. Run the following command to encrypt the non-encrypted password:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |                                  |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          |    **./encrypt_tool** *Unencrypted password*                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |                                  |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          |    The obtained encrypted password is used as the value of **authentication.password**.                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                  |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          |    .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |                                  |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          |       If a non-encrypted password contains special characters, the special characters must be escaped. For example, the dollar sign ($) is a special character and can be escaped using single quotation marks ('), for example, **'1q2w#e$r'**. If a non-encrypted password contains single quotation marks, use double quotation marks to escape the single quotation marks. If a non-encrypted password contains double quotation marks, use backslashes (\\) to escape the double quotation marks. For details, see the shell escape character rules. |                                  |
      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
      | use.keytab               | Whether to use the keytab mode to log in.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | true                             |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | -  **true** indicates using the keytab file to log in.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |                                  |
      |                          | -  **false** indicates using the password to log in.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |                                  |
      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
      | client.principal         | User principal for accessing the Loader service when the keytab authentication mode is used.                                                                                                                                                                                                                                                                                                                                                                                                                                                              | loader/hadoop                    |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | In the normal mode or password login mode, this parameter does not need to be set.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                  |
      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
      | client.keytab.file       | Directory where the used keytab file is located when the keytab authentication mode is used.                                                                                                                                                                                                                                                                                                                                                                                                                                                              | /opt/client/conf/loader.keytab   |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | In the normal mode or password login mode, this parameter does not need to be set.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                  |
      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+

#. Run the following command to go to the interaction mode:

   **source /opt/hadoopclient/bigdata_env**

   **cd /opt/hadoopclient/Loader/loader-tools-1.99.3/sqoop-shell**

   **./sqoop2-shell**

   The preceding commands obtain authentication information by reading the configuration file.

   Alternatively, you can also use the password or Kerberos authentication.

   Run the following command to authenticate login using the password mode:

   **./sqoop2-shell -uk false -u username -p encryptedPassword**

   Run the following command to authenticate login using the Kerberos mode:

   **./sqoop2-shell -uk true -k user.keytab -s userPrincipal**

   .. code-block::

      Welcome to sqoop client
      Use the username and password authentication mode
      Authentication success.
      Sqoop Shell: Type 'help' or '\h' for help.

      sqoop:000>

5. Run the following command to view the corresponding ID of the current connector:

   **show connector**

   The following information is displayed:

   .. code-block::

      +----+----------------------------+----------------+----------------------------------------------------------------------+
      | Id |            Name            |    Version     |                                Class                                 |
      +----+----------------------------+----------------+----------------------------------------------------------------------+
      | 1  | generic-jdbc-connector     | XXX            | org.apache.sqoop.connector.jdbc.GenericJdbcConnector                 |
      | 2  | ftp-connector              | XXX            | org.apache.sqoop.connector.ftp.FtpConnector                          |
      | 3  | hdfs-connector             | XXX            | org.apache.sqoop.connector.hdfs.HdfsConnector                        |
      | 4  | oracle-connector           | XXX            | org.apache.sqoop.connector.oracle.OracleConnector                    |
      | 5  | mysql-fastpath-connector   | XXX            | org.apache.sqoop.connector.mysql.MySqlConnector                      |
      | 6  | sftp-connector             | XXX            | org.apache.sqoop.connector.sftp.SftpConnector                        |
      | 7  | oracle-partition-connector | XXX            | org.apache.sqoop.connector.oracle.partition.OraclePartitionConnector |
      +----+----------------------------+----------------+----------------------------------------------------------------------+

   The preceding information indicates that the Oracle connector ID is 4.

6. Run the following command to create connectors and enter the specific connector information as prompted:

   **create connection -c** *connector ID*

   For example, if the connector ID is 4, run the following command:

   **create connection -c 4**

   .. code-block::

      sqoop:000> create connection -c 4
      Creating connection for connector with id 4
      Please fill following values to create new connection object
      Name: oracle14

      Oracle connection configuration

      JDBC connection string: jdbc:oracle:thin:@189.120.84.106:1521:orcl
      Username: oracledba
      Password: **********
      JDBC connection properties:
      There are currently 0 values in the map:
      entry#
      New connection was successfully created with validation status FINE and persistent id 3
      sqoop:000>

   The preceding information indicates that the connection ID is 3.

7. Based on the connection ID, run the following command to create jobs:

   **create job -x** *connection ID* **-t import** **--trans** *absolute path of job-config*\ **/oracle-hbase.json**

   For example, if the connection ID is 3, run the following command:

   **create job -x 3 -t import** **--trans /opt/hadoopclient/Loader/loader-tools-1.99.3/loader-tool/job-config/oracle-hbase.json**

   The following information is displayed:

   .. code-block::

      sqoop:000> create job -x 3 -t import --trans /opt/hadoopclient/Loader/loader-tools-1.99.3/loader-tool/job-config/oracle-to-hbase.json
      Creating job for connection with id 3
      Please fill following values to create new job object
      Name: run

      Database target

      Table name: test
      Columns:
      Conditions:
      Data split method:
        0 : ROWID
        1 : PARTITION
      Choose:
      Table Partitions:
      Data split allocation method:
        0 : ROUNDROBIN
        1 : SEQUENTIAL
        2 : RANDOM
      Choose:
      JDBC fetch size:

      Output configuration

      Storage type:
        0 : HDFS
        1 : HBASE_BULKLOAD
        2 : HBASE_PUTLIST
        3 : HIVE
        4 : SPARK
      Choose: 1
      HBase instance: HBase
      Clear data before import : false

      Throttling resources

      Extractors: 10
      Extractor size:
      New job was successfully created with validation status FINE  and persistent id 7
      sqoop:000>

   The preceding information indicates that the job ID is 7.

8. Run the following command to start the job:

   **start job -j** *job ID* **-s**

   For example, if the job ID is 7, run the following command:

   **start job -j 7 -s**

   Displaying the **SUCCEEDED** information indicates that the job is started successfully.

   .. code-block::

      Submission details
      Job ID: 7
      Server URL: https://10.0.0.0:21351/loader/
      Created by: admintest
      Creation date: 2019-12-04 16:37:34 CST
      Lastly updated by: admintest
      2019-12-04 16:37:34 CST: BOOTING  - Progress is not available
      2019-12-04 16:37:42 CST: BOOTING  - 0.00 %
      2019-12-04 16:37:42 CST: BOOTING  - 0.00 %
      2019-12-04 16:37:57 CST: RUNNING  - 0.00 %
      2019-12-04 16:38:12 CST: RUNNING  - 45.00 %
      2019-12-04 16:38:12 CST: RUNNING  - 45.00 %
      2019-12-04 16:38:27 CST: SUCCEEDED

Example for the Batch Mode
--------------------------

#. Log in to the node where the Loader client is installed as the user who installs the client.

#. Run the following command to go to the **conf** directory of the sqoop-shell tool. For example, if the Loader client installation directory is **/opt/hadoopclient/Loader**, run the following command:

   **cd /opt/hadoopclient/Loader/loader-tools-1.99.3/sqoop-shell/conf**

#. Run the following command to configure authentication information:

   **vi client.properties**

   .. code-block::

      server.url=10.0.0.1:21351
      # simple or kerberos
      authentication.type=simple
      # true or false
      use.keytab=true

      authentication.user=
      authentication.password=

      client.principal=hdfs/hadoop.@<system domain name>@<system domain name>

      # keytab file
      client.keytab.file=./conf/login/hdfs.keytab

   .. table:: **Table 2** Configuration parameters

      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
      | Configuration parameters | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Example Value                    |
      +==========================+===========================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+==================================+
      | server.url               | Floating IP address and port (21351) for Loader.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | 10.0.0.1:21351                   |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | For compatibility, multiple IP addresses and ports can be configured and need to be separated by **commas (,)**. The first IP address and port must be those of Loader (21351). The others can be configured based on service requirements.                                                                                                                                                                                                                                                                                                               |                                  |
      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
      | authentication.type      | Login authentication mode.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | kerberos                         |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | -  **kerberos** indicates that the security mode is used and Kerberos authentication is performed. Kerberos authentication provides two authentication modes: the password mode and the keytab file mode.                                                                                                                                                                                                                                                                                                                                                 |                                  |
      |                          | -  **simple** indicates that the normal mode is used and Kerberos authentication is not performed.                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                  |
      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
      | authentication.user      | User for login when the normal mode or password authentication is used.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | bar                              |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | In the keytab login mode, this parameter does not need to be set.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                                  |
      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
      | authentication.password  | User password for login when the password authentication mode is used.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | 43B80E33A96DF3D203ABBDFD1050C041 |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | In the normal mode or keytab login mode, this parameter does not need to be set.                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |                                  |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | The password needs to be encrypted. The encryption method is described as follows:                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                  |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | a. Go to the directory where **encrypt_tool** is located. For example, if the Loader client installation directory is **/opt/hadoopclient/Loader**, run the following command:                                                                                                                                                                                                                                                                                                                                                                            |                                  |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          |    **cd /opt/hadoopclient/Loader/loader-tools-1.99.3**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |                                  |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | b. Run the following command to encrypt the non-encrypted password:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |                                  |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          |    **./encrypt_tool** *Unencrypted password*                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |                                  |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          |    The obtained encrypted password is used as the value of **authentication.password**.                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                  |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          |    .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |                                  |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          |       If a non-encrypted password contains special characters, the special characters must be escaped. For example, the dollar sign ($) is a special character and can be escaped using single quotation marks ('), for example, **'1q2w#e$r'**. If a non-encrypted password contains single quotation marks, use double quotation marks to escape the single quotation marks. If a non-encrypted password contains double quotation marks, use backslashes (\\) to escape the double quotation marks. For details, see the shell escape character rules. |                                  |
      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
      | use.keytab               | Whether to use the keytab mode to log in.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | true                             |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | -  **true** indicates using the keytab file to log in.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |                                  |
      |                          | -  **false** indicates using the password to log in.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |                                  |
      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
      | client.principal         | User principal for accessing the Loader service when the keytab authentication mode is used.                                                                                                                                                                                                                                                                                                                                                                                                                                                              | loader/hadoop                    |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | In the normal mode or password login mode, this parameter does not need to be set.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                  |
      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
      | client.keytab.file       | Directory where the used keytab file is located when the keytab authentication mode is used.                                                                                                                                                                                                                                                                                                                                                                                                                                                              | /opt/client/conf/loader.keytab   |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | In the normal mode or password login mode, this parameter does not need to be set.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                  |
      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+

#. Run the following command to go to the directory where the **sqoop2-shell** script is located and create a text file in the directory, such as **batchCommand.sh**:

   **cd /opt/hadoopclient/Loader/loader-tools-1.99.3/sqoop-shell**

   **vi batchCommand.sh**

   An example of **batchCommand.sh** is displayed as follows:

   .. code-block::

      View parameters
      create connection -c 4 --help

      // Create a connector
      create connection -c 4 -name oracle-connection --connector-connection-oracleServerIp 10.0.0.1 --connector-connection-oracleServerPort 22 --connector-connection-oracleUser root --connector-connection-oraclePassword xxxxx

      Create a job
      create job -t import -x 3 --connector-file-inputPath /opt/tempfile --connector-file-fileFilter * --framework-output-outputDirectory /user/loader/1 --framework-output-storageType HBase --framework-throttling-extractorSize 120 --framework-output-fileType TEXT_FILE --connector-file-splitType FILE -name test

      Start a job
      start job -j 7 -s

   xxxxx is the password for the connector.

#. Run the following command and the sqoop-shell tool will run the preceding commands in sequence:

   **./sqoop2-shell batchCommand.sh**

   The commands above authenticate login by reading configuration files. Alternatively, you can attach the authentication information to the command, that is, use the password mode or Kerberos mode to authenticate login.

   Run the following command to authenticate login using the password mode:

   **./sqoop2-shell -uk false -u username -p encryptedPassword batchCommand.sh**

   Run the following command to authenticate login using the Kerberos mode:

   **./sqoop2-shell -uk true -k user.keytab -s userPrincipal batchCommand.sh**

   Displaying the **SUCCEEDED** information indicates that the job is started successfully.

   .. code-block::

      Welcome to sqoop client
      Use the username and password authentication mode
      Authentication success.
      sqoop:000> create connection -c 4 --help
      usage: Show connection viparameters:
          --connector-connection-oraclePassword <arg>
          --connector-connection-oracleServerIp <arg>
          --connector-connection-oracleServerPort <arg>
          --connector-connection-oracleUser <arg>
          --framework-security-maxConnections <arg>
          --name <arg>
      ===> FINE
      sqoop:000> create connection -c 4 -name oracle-connection --connector-connection-oracleServerIp 10.0.0.1 --connector-connection-oracleServerPort 22 --connector-connection-oracleUser root --connector-connection-oraclePassword xxxxx
      Creating connection for connector with id 4
      New connection was successfully created with validation status FINE and persistent id 3
      ===> FINE
      sqoop:000> create job -t import -x 3 --connector-file-inputPath /opt/tempfile --connector-file-fileFilter * --framework-output-outputDirectory /user/loader/1 --framework-output-storageType HDFS --framework-throttling-extractorSize 120 --framework-output-fileType TEXT_FILE --connector-file-splitType FILE -name test
      Creating job for connection with id 3
      New job was successfully created with validation status FINE  and persistent id 7
      ===> FINE
      Submission details
      Job ID: 7
      Server URL: https://10.0.0.0:21351/loader/
      Created by: admintest
      Creation date: 2019-12-04 16:37:34 CST
      Lastly updated by: admintest
      2019-12-04 16:37:34 CST: BOOTING  - Progress is not available
      2019-12-04 16:37:42 CST: BOOTING  - 0.00 %
      2019-12-04 16:37:42 CST: BOOTING  - 0.00 %
      2019-12-04 16:37:57 CST: RUNNING  - 0.00 %
      2019-12-04 16:38:12 CST: RUNNING  - 45.00 %
      2019-12-04 16:38:12 CST: RUNNING  - 45.00 %
      2019-12-04 16:38:27 CST: SUCCEEDED

#. In the batch mode, the **-c** parameter can be used to attach a command. sqoop-shell can execute only the attached command at a time.

   Run the following command to create a connection:

   **./sqoop2-shell -c "create connection -c 4 -name oracle-connection --connector-connection-oracleServerIp 10.0.0.1 --connector-connection-oracleServerPort 22 --connector-connection-oracleUser root --connector-connection-oraclePassword xxxxx"**

   You can also use the password mode or Kerberos mode to attach the authentication information to the command.

   Run the following command to authenticate login using the password mode:

   **./sqoop2-shell -uk false -u username -p encryptedPassword -c "create connection -c 4 -name oracle-connection --connector-connection-oracleerverIp 10.0.0.1 --connector-connection-oracleServerPort 22 --connector-connection-oracleUser root --connector-connection-oraclePassword xxxxx"**

   Run the following command to authenticate login using the Kerberos mode:

   **./sqoop2-shell -uk true -k user.keytab -s userPrincipal -c "create connection -c 4 -name oracle-connection --connector-connection-oracleServerIp 10.0.0.1 --connector-connection-oracleServerPort 22 --connector-connection-oracleUser root --connector-connection-oraclePassword xxxxx"**

   Displaying the **FINE** information indicates the connection is created successfully.

   .. code-block::

      Welcome to sqoop client
      Use the username and password authentication mode
      Authentication success.
      sqoop:000> create connection -c 4 -name oracle-connection --connector-connection-oracleServerIp 10.0.0.1 --connector-connection-oracleServerPort 22 --connector-connection-oracleUser root --connector-connection-oraclePassword xxxxx
      Creating connection for connector with id 4
      New connection was successfully created with validation status FINE and persistent id 3
      ===> FINE
