:original_name: mrs_01_1163.html

.. _mrs_01_1163:

Example for Using the Open-Source sqoop-shell Tool (SFTP-HDFS)
==============================================================

Scenario
--------

Taking importing data from SFTP to HDFS as an example, this section introduces how to use the sqoop-shell tool to create and start Loader jobs in the interaction mode and batch mode.

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

      client.principal=hdfs/hadoop@<system domain name>

      # keytab file
      client.keytab.file=./conf/login/hdfs.keytab

   .. note::

      Log in to FusionInsight Manager and choose **System** > **Permission** > **Domain and Mutual Trust**. The value of **Local Domain** is the current system domain name.

   .. table:: **Table 1** Configuration parameters

      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
      | Configuration parameters | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Example Value                    |
      +==========================+===========================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+==================================+
      | server.url               | Floating IP address and port (21351) for Loader.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | 10.0.0.1:21351                   |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | For compatibility, multiple IP addresses and ports can be configured and need to be separated by commas (**,**). The first IP address and port must be those of Loader (21351). The others can be configured based on service requirements.                                                                                                                                                                                                                                                                                                               |                                  |
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

#. Run the following command to view the corresponding ID of the current connector:

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

   The preceding information indicates that the SFTP connector ID is 6.

#. Run the following command to create connectors and enter the specific connector information as prompted:

   **create connection -c** *connector ID*

   For example, if the connector ID is 6, run the following command:

   **create connection -c 6**

   .. code-block::

      sqoop:000> create connection -c 6
      Creating connection for connector with id 6
      Please fill following values to create new connection object
      Name: sftp14

      Connection configuration

      Sftp server IP: 10.0.0.1
      Sftp server port: 22
      Sftp user name: root
      Sftp password: ************
      Sftp public key:
      New connection was successfully created with validation status FINE and persistent id 20
      sqoop:000>

   The preceding information indicates that the connection ID is 20.

#. Based on the connection ID, run the following command to create jobs:

   **create job -x** *connection ID* **-t import**

   For example, if the connection ID is 20, run the following command:

   **create job -x 20 -t import**

   The following information is displayed:

   .. code-block::

      Creating job for connection with id 20
      Please fill following values to create new job object
      Name: sftp-hdfs-test

      File configuration

      Input path: /opt/tempfile
      File split type:
        0 : FILE
        1 : SIZE
      Choose: 0
      Filter type:
        0 : WILDCARD
        1 : REGEX
      Choose: 0
      Path filter: *
      File filter: *
      Encode type:
      Suffix name:
      Compression:

      Output configuration

      Storage type:
        0 : HDFS
        1 : HBASE_BULKLOAD
        2 : HBASE_PUTLIST
        3 : HIVE
      Choose: 0
      File type:
        0 : TEXT_FILE
        1 : SEQUENCE_FILE
        2 : BINARY_FILE
      Choose: 0
      Compression format:
        0 : NONE
        1 : DEFAULT
        2 : DEFLATE
        3 : GZIP
        4 : BZIP2
        5 : LZ4
        6 : SNAPPY
      Choose:
      Output directory: /user/loader/test
      File operate type:
        0 : OVERRIDE
        1 : RENAME
        2 : APPEND
        3 : IGNORE
        4 : ERROR
      Choose: 0

      Throttling resources

      Extractors: 2
      Extractor size:
      New job was successfully created with validation status FINE  and persistent id 85
      sqoop:000>

   The preceding information indicates that the job ID is 85.

#. Run the following command to start the job:

   **start job -j** *job ID* **-s**

   For example, if the job ID is 85, run the following command:

   **start job -j 85 -s**

   Displaying the **SUCCEEDED** information indicates that the job is started successfully.

   .. code-block::

      Submission details
      Job ID: 85
      Server URL: https://10.0.0.0:21351/loader/
      Created by: admin
      Creation date: 2016-07-20 16:25:38 GMT+08:00
      Lastly updated by: admin
      2016-07-20 16:25:38 GMT+08:00: BOOTING  - Progress is not available
      2016-07-20 16:25:46 GMT+08:00: BOOTING  - 0.00 %
      2016-07-20 16:25:53 GMT+08:00: BOOTING  - 0.00 %
      2016-07-20 16:26:08 GMT+08:00: RUNNING  - 90.00 %
      2016-07-20 16:26:08 GMT+08:00: RUNNING  - 90.00 %
      2016-07-20 16:26:27 GMT+08:00: SUCCEEDED

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

      client.principal=hdfs/hadoop@<system domain name>

      # keytab file
      client.keytab.file=./conf/login/hdfs.keytab

   .. table:: **Table 2** Configuration parameters

      +--------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
      | Configuration parameters | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Example Value                    |
      +==========================+===========================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+==================================+
      | server.url               | Floating IP address and port (21351) for Loader.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | 10.0.0.1:21351                   |
      |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                  |
      |                          | For compatibility, multiple IP addresses and ports can be configured and need to be separated by commas (**,**). The first IP address and port must be those of Loader (21351). The others can be configured based on service requirements.                                                                                                                                                                                                                                                                                                               |                                  |
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
      create connection -c 6 --help

      // Create a connector
      create connection -c 6 -name sftp-connection --connector-connection-sftpServerIp 10.0.0.1 --connector-connection-sftpServerPort 22 --connector-connection-sftpUser root --connector-connection-sftpPassword xxxxx

      Create a job
      create job -t import -x 20 --connector-file-inputPath /opt/tempfile --connector-file-fileFilter * --framework-output-outputDirectory /user/loader/1 --framework-output-storageType HDFS --framework-throttling-extractorSize 120 --framework-output-fileType TEXT_FILE --connector-file-splitType FILE -name test

      Start a job
      start job -j 85 -s

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
      sqoop:000> create connection -c 6 --help
      usage: Show connection parameters:
          --connector-connection-sftpPassword <arg>
          --connector-connection-sftpServerIp <arg>
          --connector-connection-sftpServerPort <arg>
          --connector-connection-sftpUser <arg>
          --framework-security-maxConnections <arg>
          --name <arg>
      ===> FINE
      sqoop:000> create connection -c 6 -name sftp-connection --connector-connection-sftpServerIp 10.0.0.1 --connector-connection-sftpServerPort 22 --connector-connection-sftpUser root --connector-connection-sftpPassword xxxxx
      Creating connection for connector with id 6
      New connection was successfully created with validation status FINE and persistent id 20
      ===> FINE
      sqoop:000> create job -t import -x 20 --connector-file-inputPath /opt/tempfile --connector-file-fileFilter * --framework-output-outputDirectory /user/loader/1 --framework-output-storageType HDFS --framework-throttling-extractorSize 120 --framework-output-fileType TEXT_FILE --connector-file-splitType FILE -name test
      Creating job for connection with id 20
      New job was successfully created with validation status FINE  and persistent id 85
      ===> FINE

      Submission details
      Job ID: 85
      Server URL: https://10.0.0.0:21351/loader/
      Created by: admin
      Creation date: 2016-07-20 16:25:38 GMT+08:00
      Lastly updated by: admin
      2016-07-20 16:25:38 GMT+08:00: BOOTING  - Progress is not available
      2016-07-20 16:25:46 GMT+08:00: BOOTING  - 0.00 %
      2016-07-20 16:25:53 GMT+08:00: BOOTING  - 0.00 %
      2016-07-20 16:26:08 GMT+08:00: RUNNING  - 90.00 %
      2016-07-20 16:26:08 GMT+08:00: RUNNING  - 90.00 %
      2016-07-20 16:26:27 GMT+08:00: SUCCEEDED

#. In the batch mode, the **-c** parameter can be used to attach a command. sqoop-shell can execute only the attached command at a time.

   Run the following command to create a connection:

   **./sqoop2-shell -c "create connection -c 6 -name sftp-connection --connector-connection-sftpServerIp 10.0.0.1 --connector-connection-sftpServerPort 22 --connector-connection-sftpUser root --connector-connection-sftpPassword xxxxx"**

   You can also use the password mode or Kerberos mode to attach the authentication information to the command.

   Run the following command to authenticate login using the password mode:

   **./sqoop2-shell -uk false -u username -p encryptedPassword -c "create connection -c 6 -name sftp-connection --connector-connection-sftpServerIp 10.0.0.1 --connector-connection-sftpServerPort 22 --connector-connection-sftpUser root --connector-connection-sftpPassword xxxxx"**

   Run the following command to authenticate login using the Kerberos mode:

   **./sqoop2-shell -uk true -k user.keytab -s userPrincipal -c "create connection -c 6 -name sftp-connection --connector-connection-sftpServerIp 10.0.0.1 --connector-connection-sftpServerPort 22 --connector-connection-sftpUser root --connector-connection-sftpPassword xxxxx"**

   Displaying the **FINE** information indicates the connection is created successfully.

   .. code-block::

      Welcome to sqoop client
      Use the username and password authentication mode
      Authentication success.
      sqoop:000> create connection -c 6 -name sftp-connection --connector-connection-sftpServerIp 10.0.0.1 --connector-connection-sftpServerPort 22 --connector-connection-sftpUser root --connector-connection-sftpPassword xxxxx
      Creating connection for connector with id 6
      New connection was successfully created with validation status FINE and persistent id 20
      ===> FINE
