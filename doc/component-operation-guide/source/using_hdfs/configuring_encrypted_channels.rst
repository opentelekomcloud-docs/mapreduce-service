:original_name: mrs_01_0810.html

.. _mrs_01_0810:

Configuring Encrypted Channels
==============================

Scenario
--------

Encrypted channel is an encryption protocol of remote procedure call (RPC) in HDFS. When a user invokes RPC, the user's login name will be transmitted to RPC through RPC head. Then RPC uses Simple Authentication and Security Layer (SASL) to determine an authorization protocol (Kerberos and DIGEST-MD5) to complete RPC authorization. When users deploy security clusters, they need to use encrypted channels and configure the following parameters. For details about the secure Hadoop RPC, visit https://hadoop.apache.org/docs/r3.1.1/hadoop-project-dist/hadoop-common/SecureMode.html#Data_Encryption_on_RPC.

Configuration Description
-------------------------

Go to the **All Configurations** page of HDFS and enter a parameter name in the search box by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.

.. table:: **Table 1** Parameter description

   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------+
   | Parameter             | Description                                                                                                                                                                                                              | Default Value                  |
   +=======================+==========================================================================================================================================================================================================================+================================+
   | hadoop.rpc.protection | .. important::                                                                                                                                                                                                           | -  Security mode: privacy      |
   |                       |                                                                                                                                                                                                                          | -  Normal mode: authentication |
   |                       |    NOTICE:                                                                                                                                                                                                               |                                |
   |                       |                                                                                                                                                                                                                          |                                |
   |                       |    -  The setting takes effect only after the service is restarted. Rolling restart is not supported.                                                                                                                    |                                |
   |                       |    -  After the setting, you need to download the client configuration again. Otherwise, the HDFS cannot provide the read and write services.                                                                            |                                |
   |                       |                                                                                                                                                                                                                          |                                |
   |                       | Whether the RPC channels of each module in Hadoop are encrypted. The channels include:                                                                                                                                   |                                |
   |                       |                                                                                                                                                                                                                          |                                |
   |                       | -  RPC channels for clients to access HDFS                                                                                                                                                                               |                                |
   |                       | -  RPC channels between modules in HDFS, for example, RPC channels between DataNode and NameNode                                                                                                                         |                                |
   |                       | -  RPC channels for clients to access Yarn                                                                                                                                                                               |                                |
   |                       | -  RPC channels between NodeManager and ResourceManager                                                                                                                                                                  |                                |
   |                       | -  RPC channels for Spark to access Yarn and HDFS                                                                                                                                                                        |                                |
   |                       | -  RPC channels for MapReduce to access Yarn and HDFS                                                                                                                                                                    |                                |
   |                       | -  RPC channels for HBase to access HDFS                                                                                                                                                                                 |                                |
   |                       |                                                                                                                                                                                                                          |                                |
   |                       | .. note::                                                                                                                                                                                                                |                                |
   |                       |                                                                                                                                                                                                                          |                                |
   |                       |    You can set this parameter on the HDFS component configuration page. The parameter setting takes effect globally, that is, the setting of whether the RPC channel is encrypted takes effect on all modules in Hadoop. |                                |
   |                       |                                                                                                                                                                                                                          |                                |
   |                       | There are three encryption modes.                                                                                                                                                                                        |                                |
   |                       |                                                                                                                                                                                                                          |                                |
   |                       | -  **authentication**: This is the default value in normal mode. In this mode, data is directly transmitted without encryption after being authenticated. This mode ensures performance but has security risks.          |                                |
   |                       | -  **integrity**: Data is transmitted without encryption or authentication. To ensure data security, exercise caution when using this mode.                                                                              |                                |
   |                       | -  **privacy**: This is the default value in security mode, indicating that data is transmitted after authentication and encryption. This mode reduces the performance.                                                  |                                |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------+
