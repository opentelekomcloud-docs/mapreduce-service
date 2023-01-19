:original_name: mrs_01_1158.html

.. _mrs_01_1158:

loader-tool Usage Example
=========================

Scenario
--------

loader-tool can be used to create, update, query, and delete a connector or job by using a job template or setting parameters.

This section describes how to use loader-tool in the job template mode. The job of importing data from the SFTP server to HDFS is used as an example.

Prerequisites
-------------

The Loader client has been installed and configured.

Procedure
---------

#. Log in to the node where the client is located as the user who installs the client.

#. Run the following command to go to the directory where loader-tool is located on the Loader client. For example, if the Loader client installation directory is **/opt/hadoopclient/Loader**, run the following command:

   **cd /opt/hadoopclient/Loader/loader-tools-1.99.3/loader-tool/**

#. Run the following command to modify the existing job template. For example, if the job template **sftp-to-hdfs.xml** already exists in the **/opt/hadoopclient/Loader/loader-tools-1.99.3/loader-tool/job-config/**, run the following command:

   **vi /opt/hadoopclient/Loader/loader-tools-1.99.3/loader-tool/job-config/sftp-to-hdfs.xml**

   .. code-block::

      <root>
      <!-- Database connection information -->
      <sqoop.connection name="vt_sftp_test" type="sftp-connector">
      <connection.sftpServerIp>10.96.26.111</connection.sftpServerIp>
      <connection.sftpServerPort>22</connection.sftpServerPort>
      <connection.sftpUser>root</connection.sftpUser>
      <connection.sftpPassword>d2NjX2NyeXB0ATQxNDU1MzVGNDM0MjQzOzMzMzkzOTMwMzI0NTM5MzQzOTM1Mzk0NTMwMzIzNTM4NDEzNzQ2MzIzNjQyMzMzMDM4MzMzNzQ1MzYzODQxMzQ7OzMyMzUzMDMwO0EzMTUzM0ExNTAyNDhENzE3QTRBRTlCQkRBQzlFRkFEOzYyOEE4NTlDODc2MkMyNzU7NTc0MzQzNUY0MzUyNTk1MDU0NUY0NDQ1NDY0MTU1NEM1NDVGNDQ0RjRENDE0OTRFOzMwOzMxMzQzNTM2MzMzMTMyMzgzMzMzMzIzNzMwOw</connection.sftpPassword>
      </sqoop.connection>

      <!--Job name, globally unique.-->
      <sqoop.job name="Sftp.to.Hdfs" type="IMPORT" queue="default" priority="NORMAL">
      <data.source connectionName="vt_sftp_test" connectionType="sftp-connector">
      <file.inputPath>/opt/houjt/hive/all</file.inputPath>
      <file.splitType>FILE</file.splitType>
      <file.filterType>WILDCARD</file.filterType>
      <file.pathFilter>*</file.pathFilter>
      <file.fileFilter>*</file.fileFilter>
      <file.encodeType>GBK</file.encodeType>
      <file.suffixName></file.suffixName>
      <file.isCompressive>FALSE</file.isCompressive>
      </data.source>

      <hadoop.source storageType="HDFS" >
      <output.outputDirectory>/user/loader/sftp-to-hdfs</output.outputDirectory>
      <output.fileOprType>OVERRIDE</output.fileOprType>
      <throttling.extractors>3</throttling.extractors>
      <output.fileType>TEXT_FILE</output.fileType>
      </hadoop.source>

      <sqoop.job.trans.file></sqoop.job.trans.file>
      </sqoop.job>
      </root>

   .. note::

      Each Loader job needs to be associated with a connector. Connectors are used to read data from external data sources when data is imported to a cluster and used to write data into external data sources when data is exported from the cluster. In the preceding example, an SFTP data source connector is configured. To configure an SFTP and FTP data source connector, a password needs to be set and encrypted. The password encryption method is described as follows:

      a. Run the following command to go to the **loader-tools-1.99.3** directory. For example, if the Loader client installation directory is **/opt/hadoopclient/Loader**, run the following command:

         **cd /opt/hadoopclient/Loader/loader-tools-1.99.3**

      b. Run the following command to encrypt the non-encrypted password:

         **./encrypt_tool** *Unencrypted password*

#. Run the following command to go to the directory where loader-tool is located:

   **cd /opt/hadoopclient/Loader/loader-tools-1.99.3/loader-tool**

#. Run the following command to use the lt-ucc tool to create a connector:

   **./bin/lt-ucc -l /opt/hadoopclient/Loader/loader-tools-1.99.3/loader-tool/job-config/login-info.xml -w /opt/hadoopclient/Loader/loader-tools-1.99.3/loader-tool/job-config/sftp-to-hdfs.xml -a create**

   If no error is reported and the following information is displayed, the connector creation task is submitted successfully:

   .. code-block::

      User login success. begin to execute task.

#. Run the following command to use the lt-ucj tool to create a job:

   **./bin/lt-ucj -l /opt/hadoopclient/Loader/loader-tools-1.99.3/loader-tool/job-config/login-info.xml -w /opt/hadoopclient/Loader/loader-tools-1.99.3/loader-tool/job-config/sftp-to-hdfs.xml -a create**

   If no error is reported and the following information is displayed, the job creation task is submitted successfully:

   .. code-block::

      User login success. begin to execute task.

#. Run the following command to use the lt-ctl tool to submit the job:

   **./bin/lt-ctl -l /opt/hadoopclient/Loader/loader-tools-1.99.3/loader-tool/job-config/login-info.xml -n Sftp.to.Hdfs -a start**

   If the following information is displayed, the job is submitted successfully:

   .. code-block::

      Start job success.

#. Run the following command to view the job status:

   **./bin/lt-ctl -l /opt/hadoopclient/Loader/loader-tools-1.99.3/loader-tool/job-config/login-info.xml -n Sftp.to.Hdfs -a status**

   .. code-block::

      Job:Sftp.to.Hdfs
      Status:RUNNING
      Progress: 0.0
