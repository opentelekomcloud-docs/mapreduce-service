:original_name: mrs_01_1162.html

.. _mrs_01_1162:

Open Source sqoop-shell Tool Usage Guide
========================================

Overview
--------

Sqoop-shell is a shell tool of Loader. All its functions are implemented by executing the **sqoop2-shell** script.

The sqoop-shell tool provides the following functions:

-  Creating and updating connectors
-  Creating and updating jobs
-  Deleting connectors and jobs
-  Starting jobs in the synchronous or asynchronous mode.
-  Stopping jobs
-  Viewing job status
-  Viewing historical execution records of jobs
-  Cloning connectors and jobs
-  Creating and updating conversion steps
-  Specifying line and field separators

The sqoop-shell tool supports the following modes:

-  Interaction mode

   Users execute the **sqoop2-shell** script without parameters to go to the particular interaction window of Loader. After the contents of the script are input, the tool returns the relevant information to the interaction window.

-  Batch mode

   The **sqoop2-shell** script has a file name as a parameter and multiple commands are stored in lines in the file. The sqoop-shell tool runs all commands in the file in sequence by executing the script. Alternatively, users can execute the **sqoop2-shell** script, to the end of which a command is attached with the **-c** parameter as the bridge. In this case, the sqoop-shell tool runs one command each time.

The sqoop-shell implements functions of Loader by running the commands in :ref:`Table 1 <mrs_01_1162__en-us_topic_0000001173789536_t377ae098b7e243328537c0bfbe54a211>`.

.. _mrs_01_1162__en-us_topic_0000001173789536_t377ae098b7e243328537c0bfbe54a211:

.. table:: **Table 1** Command list

   +-----------------------------------+-------------------------------------------------------------------------+
   | Command                           | Description                                                             |
   +===================================+=========================================================================+
   | exit                              | Exists the interaction mode.                                            |
   |                                   |                                                                         |
   |                                   | This command is supported only in the interaction mode.                 |
   +-----------------------------------+-------------------------------------------------------------------------+
   | history                           | Views the executed commands.                                            |
   |                                   |                                                                         |
   |                                   | This command is supported only in the interaction mode.                 |
   +-----------------------------------+-------------------------------------------------------------------------+
   | help                              | Views the tool help information.                                        |
   +-----------------------------------+-------------------------------------------------------------------------+
   | set                               | Sets server attributes.                                                 |
   +-----------------------------------+-------------------------------------------------------------------------+
   | show                              | Displays service attributes and all the metadata information of Loader. |
   +-----------------------------------+-------------------------------------------------------------------------+
   | create                            | Creates connectors and jobs.                                            |
   +-----------------------------------+-------------------------------------------------------------------------+
   | update                            | Updates connectors and jobs.                                            |
   +-----------------------------------+-------------------------------------------------------------------------+
   | delete                            | Deletes connectors and jobs.                                            |
   +-----------------------------------+-------------------------------------------------------------------------+
   | clone                             | Clones connectors and jobs.                                             |
   +-----------------------------------+-------------------------------------------------------------------------+
   | start                             | Starts jobs.                                                            |
   +-----------------------------------+-------------------------------------------------------------------------+
   | stop                              | Stops jobs.                                                             |
   +-----------------------------------+-------------------------------------------------------------------------+
   | status                            | Views job status.                                                       |
   +-----------------------------------+-------------------------------------------------------------------------+

Commands
--------

-  The sqoop2-shell tool provides two methods to obtain login authentication information. The first method is to obtain login authentication information from the configuration file. For details about the configuration items, see :ref:`Example for Using the Open-Source sqoop-shell Tool (SFTP-HDFS) <mrs_01_1163>` and :ref:`Example for Using the Open-Source sqoop-shell Tool (Oracle-HBase) <mrs_01_1164>`. The second one is to obtain the authentication information by using parameters. Two modes are available in the second method: password mode and Kerberos authentication mode.

-  Command for accessing the interaction mode

   Execute the **sqoop2-shell** script without parameters to go to the sqoop tool window and run the commands one by one.

   Run the following command to obtain the authentication information by reading the configuration file:

   **./sqoop2-shell**

   Run the following command to authenticate login using the password mode:

   **./sqoop2-shell -uk false -u username -p encryptedPassword**

   Run the following command to authenticate login using the Kerberos mode:

   **./sqoop2-shell -uk true -k user.keytab -s userPrincipal**

   The following information is displayed:

   .. code-block::

      Welcome to sqoop client
      Use the username and password authentication mode
      Authentication success.
      Sqoop Shell: Type 'help' or '\h' for help.

      sqoop:000>

-  Command for entering the batch mode

   Two methods are available for accessing the batch mode.

   1. Execute the **sqoop2-shell** script, in which a file name is used as a parameter and multiple commands are stored in lines in this file. The sqoop-shell tool runs all commands in the file in sequence. The script must be stored in the home directory of the current user, for example, **/root/batchCommand.sh**.

   Run the following command to authenticate login by reading configuration files:

   **./sqoop2-shell** */root/batchCommand.sh*

   Run the following command to authenticate login using the password mode:

   **./sqoop2-shell -uk false -u username -p encryptedPassword** */root/batchCommand.sh*

   Run the following command to authenticate login using the Kerberos mode:

   **./sqoop2-shell -uk true -k user.keytab -s userPrincipal** */root/batchCommand.sh*

   *batchCommand.sh* is the user-defined name of the text file.

   2. Execute the **sqoop2-shell** script, to the end of which a command is attached with the -c parameter as the bridge. The sqoop-shell tool will execute the command.

   Run the following command to authenticate login by reading configuration files:

   **./sqoop2-shell** *-c expression*

   Run the following command to authenticate login using the password mode:

   **./sqoop2-shell -uk false -u username -p encryptedPassword** *-c expression*

   Run the following command to authenticate login using the Kerberos mode:

   **./sqoop2-shell -uk true -k user.keytab -s userPrincipal** *-c expression*

   *expression* is the attached statement, whose format is the same as that in the text file in the first method.

-  Exit command

   This command is used for exiting the interaction mode and supported only in the interaction mode.

   Example:

   .. code-block::

      Welcome to sqoop client
      Use the username and password authentication mode
      Authentication success.
      Sqoop Shell: Type 'help' or '\h' for help.

      sqoop:000> exit
      10-5-211-9:/opt/hadoopclient/Loader/loader-tools-1.99.3/sqoop-shell#

-  History command

   This command is used for viewing the executed commands and supported only in the interaction mode.

   Example:

   .. code-block::

      sqoop:000> history
         0  show connector
         1  create connection -c 4
         2  show connections;
         3  show connection;
         4  show connection -a;
         5  show connections;
         6  show connection;
         7  show connection -x 53;
         8  show connection -x 52;
         9  show connection -x 2
        10  show connection -x 53;
        11  show connection
        12  show connection -x 53
        13  create job -x 53 -t import
        14  show connector
        15  create connection -c 5
        16  show connection -x 54
        17  exit
        18  show connector
        19  create connection -c 5
        20  exit
        21  show connector
        22  create connection -c 6
        23  create job -x 20 -t import
        24  start job -j 85 -s
        25  \x
        26  exit
        27  history
      sqoop:000>

-  Help command

   This command is used for viewing the tool help information.

   Example:

   .. code-block::

      sqoop:000> help
      For information about Sqoop, visit: http://sqoop.apache.org/docs/1.99.3/index.html

      Available commands:
        exit    (\x  ) Exit the shell
        history (\H  ) Display, manage and recall edit-line history
        help    (\h  ) Display this help message
        set     (\st ) Set server or option Info
        show    (\sh ) Show server, connector, framework, connection, job, submission or option Info
        create  (\cr ) Create connection or job Info
        delete  (\d  ) Delete connection or job Info
        update  (\up ) Update connection or job Info
        clone   (\cl ) Clone connection or job Info
        start   (\sta) Start job
        stop    (\stp) Stop job
        status  (\stu) Status job

      For help on a specific command type: help command

      sqoop:000>

-  Set command

   The set command is used for setting attributes of clients and servers and supports the following attributes:

   -  **server** indicates setting the connection attributes for servers.

      .. note::

         When attribute -u is set, attributes -h, -p, and -w can be ignored.

   -  **option** indicates setting the client attributes.

      .. note::

         **option** can be set by key values. For example, **set option --name verbose --value true**.

      +----------------+--------------+--------------------------------------------------------------------+
      | Attribute Type | Subattribute | Description                                                        |
      +================+==============+====================================================================+
      | server         | -h,--host    | Service IP address.                                                |
      +----------------+--------------+--------------------------------------------------------------------+
      |                | -p,--port    | Service Port                                                       |
      +----------------+--------------+--------------------------------------------------------------------+
      |                | -w,--webapp  | Tomcat application name.                                           |
      +----------------+--------------+--------------------------------------------------------------------+
      |                | -u,--url     | Sqoop service URL.                                                 |
      +----------------+--------------+--------------------------------------------------------------------+
      | option         | verbose      | Redundancy mode, which indicates that more information is printed. |
      +----------------+--------------+--------------------------------------------------------------------+
      |                | poll-timeout | Sets the polling timeout duration.                                 |
      +----------------+--------------+--------------------------------------------------------------------+

   Example:

   .. code-block::

      set option --name verbose --value false
      set server --host 10.0.0.1 --port 21351 --webapp loader

-  **show** command

   This command is used for displaying information, such as variable information and storage metadata information.

   +----------------+--------------+-------------------------------------------------------------------+
   | Attribute Type | Subattribute | Description                                                       |
   +================+==============+===================================================================+
   | server         | -a,--all     | Displays all server attributes.                                   |
   +----------------+--------------+-------------------------------------------------------------------+
   |                | -p,--port    | Displays the service port.                                        |
   +----------------+--------------+-------------------------------------------------------------------+
   |                | -w,--webapp  | Displays the Tomcat application name.                             |
   +----------------+--------------+-------------------------------------------------------------------+
   |                | -h,--host    | Displays the service IP address.                                  |
   +----------------+--------------+-------------------------------------------------------------------+
   | option         | -name        | Displays the attributes of the specified name.                    |
   +----------------+--------------+-------------------------------------------------------------------+
   | connector      | -a,--all     | Displays information about all connection types.                  |
   +----------------+--------------+-------------------------------------------------------------------+
   |                | -c,--cid     | Displays information about the connection type of a specified ID. |
   +----------------+--------------+-------------------------------------------------------------------+
   | framework      | None.        | Displays metadata information about frameworks.                   |
   +----------------+--------------+-------------------------------------------------------------------+
   | connection     | -a,--all     | Displays all connection attributes.                               |
   +----------------+--------------+-------------------------------------------------------------------+
   |                | -x,--xid     | Displays the attributes of a specified connection.                |
   +----------------+--------------+-------------------------------------------------------------------+
   |                | -n,--name    | Displays the connection attributes of a specified name.           |
   +----------------+--------------+-------------------------------------------------------------------+
   | job            | -a,--all     | Displays information about all jobs.                              |
   +----------------+--------------+-------------------------------------------------------------------+
   |                | -j,--jid     | Displays job information about a specified ID.                    |
   +----------------+--------------+-------------------------------------------------------------------+
   |                | -n,--name    | Displays job information about a specified name.                  |
   +----------------+--------------+-------------------------------------------------------------------+
   | submission     | -j,--jid     | Displays the submission record of a specified job.                |
   +----------------+--------------+-------------------------------------------------------------------+
   |                | -d,--detail  | Displays details.                                                 |
   +----------------+--------------+-------------------------------------------------------------------+

   Example:

   .. code-block::

      show server -all
      show option --name verbose
      show connector -all
      show framework
      show connection -all
      show connection -n sftp-example
      show job -all
      show job -j 1
      show submission --jid 1
      show submission --jid 1 -d

-  Create command

   This command is used for creating connectors and jobs.

   +-----------------------+-----------------------+---------------------------------------------------+
   | Attribute Type        | Subattribute          | Description                                       |
   +=======================+=======================+===================================================+
   | connection            | -c,--cid              | Specifies the ID of a connector type.             |
   +-----------------------+-----------------------+---------------------------------------------------+
   |                       | -cn,--cname           | Specifies the name of a specified connector type. |
   +-----------------------+-----------------------+---------------------------------------------------+
   | job                   | -x,--xid              | Specifies the connector ID.                       |
   +-----------------------+-----------------------+---------------------------------------------------+
   |                       | -xn,--xname           | Specifies the connector name.                     |
   +-----------------------+-----------------------+---------------------------------------------------+
   |                       | -t,--type             | Specifies the job type.                           |
   |                       |                       |                                                   |
   |                       |                       | Possible values:                                  |
   |                       |                       |                                                   |
   |                       |                       | -  import                                         |
   |                       |                       | -  export                                         |
   +-----------------------+-----------------------+---------------------------------------------------+

   -  In the interaction mode, enter the attribute values one by one as prompted.

      Example for creating connectors:

      .. code-block::

         create connection -c 1
         create connection -cn example

      Example for creating jobs:

      .. code-block::

         create job -x 1 -t import
         create job -xn job_example -t export

   -  In the batch mode, run the following command to view the specific attribute and then set a value for the attribute:

      **create job -t import -x 1 --help**

      You can run the above command in either of the following ways:

      Save the command to a text file and attach this file to the end of the **sqoop-shell** script, and run the following command:

      **./sqoop2-shell** *batchCommand.sh*

      Attach a command with the **-c** parameter to the end of the **sqoop-shell** script and run the following command:

      **./sqoop2-shell** *-c expression*

      For details about command execution, refer to previous description in this section. The following shows two complete commands:

      Example for creating connectors:

      .. code-block::

         create connection -c 4 --connector-connection-sftpPassword xxxxx --connector-connection-sftpServerIp 10.0.0.1 --connector-connection-sftpServerPort 22 --connector-connection-sftpUser root--name testConnection

      Example for creating jobs:

      .. code-block::

         create job -t import -x 1 --connector-file-inputPath /opt/tempfile --connector-file-fileFilter * --framework-output-outputDirectory /user/loader/1 --framework-output-storageType HDFS --framework-throttling-extractorSize 120 --framework-output-fileType TEXT_FILE --connector-file-splitType FILE -queue default -priority low -name newJob

   -  In the batch mode, you can attach a statement using the **-c** parameter as the bridge.

      Example for creating connectors:

      .. code-block::

         ./sqoop2-shell -c "create connection -c 4 --connector-connection-sftpPassword xxxxx --connector-connection-sftpServerIp 10.0.0.1 --connector-connection-sftpServerPort 22 --connector-connection-sftpUser root--name testConnection"

-  **update** command

   This command is used for updating connectors and jobs.

   +-----------------------+-----------------------+---------------------------------------------------------------+
   | Attribute Type        | Subattribute          | Description                                                   |
   +=======================+=======================+===============================================================+
   | connection            | -x,--xid              | Specifies the connector ID.                                   |
   |                       |                       |                                                               |
   |                       |                       | .. note::                                                     |
   |                       |                       |                                                               |
   |                       |                       |    When the connectors are updated, the password must be set. |
   +-----------------------+-----------------------+---------------------------------------------------------------+
   | job                   | -j,--jid              | Specifies the job ID.                                         |
   +-----------------------+-----------------------+---------------------------------------------------------------+

   -  Interaction mode

      Example for updating connectors:

      .. code-block::

         update connection --xid 1

      Example for updating jobs:

      .. code-block::

         update job --jid 1

   -  Batch mode

      Example for updating connectors:

      .. code-block::

         update connection -x 6 --connector-connection-sftpServerPort 21 - --name sfp_130--connector-connection-sftpPassword xxxx

      Example for updating jobs:

      .. code-block::

         update job -jid 1 -name sftp2hdfs --connector-file-fileFilter *.txt

-  **delete** command

   This command is used for deleting connectors and jobs.

   ============== ============ =============================
   Attribute Type Subattribute Description
   ============== ============ =============================
   connection     -x,--xid     Specifies the connector ID.
   \              -n,--name    Specifies the connector name.
   job            -j,--jid     Specifies the job ID.
   \              -n,--name    Specifies the job name.
   ============== ============ =============================

   Example:

   .. code-block::

      delete connection -x 1
      delete connection --name abc
      delete job -j 1
      delete job -n qwerty

-  **clone** command

   This command is used for cloning connectors and jobs.

   +-----------------------+-----------------------+------------------------------------------------------------------------------------+
   | Attribute Type        | Subattribute          | Description                                                                        |
   +=======================+=======================+====================================================================================+
   | connection            | -x,--xid              | Specifies the connector ID.                                                        |
   |                       |                       |                                                                                    |
   |                       |                       | .. note::                                                                          |
   |                       |                       |                                                                                    |
   |                       |                       |    The password and connector name must be entered when the connectors are cloned. |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------+
   | job                   | -j,--jid              | Specifies the job ID.                                                              |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------+

   Example:

   .. code-block::

      clone job -j 1

-  **start** command

   This command is used for starting jobs.

   +----------------+------------------+-------------------------------------------------------+
   | Attribute Type | Subattribute     | Description                                           |
   +================+==================+=======================================================+
   | job            | -j,--jid         | Specifies the job ID.                                 |
   +----------------+------------------+-------------------------------------------------------+
   |                | -n,--name        | Specifies the job name.                               |
   +----------------+------------------+-------------------------------------------------------+
   |                | -s,--synchronous | Whether to start jobs in the synchronous mode or not. |
   +----------------+------------------+-------------------------------------------------------+

   Example for starting jobs in the asynchronous mode:

   .. code-block::

      start job -j 1
      start job -n abc

   Example for starting jobs in the synchronous mode:

   .. code-block::

      start job -j 1 -s
      start job --name abc --synchronous

-  **stop** command

   This command is used for stopping jobs.

   ============== ============ =======================
   Attribute Type Subattribute Description
   ============== ============ =======================
   job            -j,--jid     Specifies the job ID.
   \              -n,--name    Specifies the job name.
   ============== ============ =======================

   Example:

   .. code-block::

      stop job -j 1
      stop job -n abc

-  Status command

   This command is used for viewing job status.

   ============== ============ =====================
   Attribute Type Subattribute Description
   ============== ============ =====================
   job            -j,--jid     Specifies the job ID.
   ============== ============ =====================

   When **-s** parameter is attached to the command, the result only contains the enumerated value of job status.

   Example:

   .. code-block::

      status job -j 1
      status job -j 1 -s

Extended Attributes of Create Command
-------------------------------------

For the scenario in which HDFS exchanges data with the SFTP server or RDB, MRS extends the create command attributes on the basis of the open source sqoop-shell tool, so as to specify line and field separators and conversion steps when jobs are created.

.. table:: **Table 2** Extended Attributes of Create Command

   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Property                    | Description                                                                                                                                                                                                                                                                                                                   |
   +=============================+===============================================================================================================================================================================================================================================================================================================================+
   | fields-terminated-by        | Default field separator.                                                                                                                                                                                                                                                                                                      |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | lines-terminated-by         | Default line separator.                                                                                                                                                                                                                                                                                                       |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | input-fields-terminated-by  | Inputs the step field separator. If the step field separator is not specified, the value equals to **fields-terminated-by** by default.                                                                                                                                                                                       |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | input-lines-terminated-by   | Inputs the step line separator. If the step line separator is not specified, the value equals to **lines-terminated-by** by default.                                                                                                                                                                                          |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | output-fields-terminated-by | Outputs the step field separator. If the step field separator is not specified, the value equals to **fields-terminated-by** by default.                                                                                                                                                                                      |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | output-lines-terminated-by  | Outputs the step line separator. If the step line separator is not specified, the value equals to **lines-terminated-by** by default.                                                                                                                                                                                         |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | trans                       | Specifies the conversion steps. The value is the directory where the conversion step file is located. When the relative directory of file is specified, the file is by default stored in the directory where the **sqoop2-shell** script is located. When the attribute is set, the other extended attributes can be ignored. |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Interconnecting Sqoop1 with MRS
-------------------------------

#. Download the open source Sqoop from http://www.apache.org/dyn/closer.lua/sqoo:p/1.4.7.

#. Save the downloaded **sqoop-1.4.7.bin__hadoop-2.6.0.tar.gz** package to the **/opt/sqoop** directory on the Master node in the MRS cluster and decompress the package.

   **tar zxvf sqoop-1.4.7.bin__hadoop-2.6.0.tar.gz**

#. Go to the directory where the package is decompressed and modify the configuration.

   **cd /opt/sqoop/sqoop-1.4.7.bin__hadoop-2.6.0/conf**

   **cp sqoop-env-template.sh sqoop-env.sh**

   **vi sqoop-env.sh**

   Add the following configurations:

   export HADOOP_COMMON_HOME=/opt/client/HDFS/hadoop

   export HADOOP_MAPRED_HOME=/opt/client/HDFS/hadoop

   export HIVE_HOME=/opt/Bigdata/MRS_1.9.X/install/FusionInsight-Hive-3.1.0/hive (Enter the actual path.)

   export HIVE_CONF_DIR=/opt/client/Hive/config

   export HCAT_HOME=/opt/client/Hive/HCatalog

4. Add the system variable **SQOOP_HOME** to **PATH**.

   **vi /etc/profile**

   Add the following information:

   export SQOOP_HOME=/opt/sqoop/sqoop-1.4.7.bin__hadoop-2.6.0

   export PATH=$PATH:$SQOOP_HOME/bin

5. Run the following command to copy the **jline-2.12.jar** file to the **lib** file.

   **cp /opt/share/jline-2.12/jline-2.12.jar /opt/sqoop/sqoop-1.4.7.bin__hadoop-2.6.0/lib**

6. Run the following command to add the following configuration to the file.

   **vim $JAVA_HOME/jre/lib/security/java.policy**

   permission javax.management.MBeanTrustPermission "register";

7. Run the following command to interconnect sqoop1 with MRS.

   **source /etc/profile**
