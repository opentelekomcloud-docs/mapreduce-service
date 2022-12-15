:original_name: mrs_08_00703.html

.. _mrs_08_00703:

ZooKeeper Enhanced Open Source Features
=======================================

Enhanced Log
------------

In security mode, an ephemeral node is deleted as long as the session that created the node expires. Ephemeral node deletion is recorded in audit logs so that ephemeral node status can be obtained.

Usernames must be added to audit logs for all operations performed on ZooKeeper clients.

On the ZooKeeper client, create a znode, of which the Kerberos principal is **zkcli/hadoop.**\ *<System domain name>*\ **@**\ *<System domain name>*.

For example, open the **<ZOO_LOG_DIR>/zookeeper_audit.log** file. The file content is as follows:

.. code-block::

   2016-12-28 14:17:10,505 | INFO  | CommitProcWorkThread-4 | session=0x12000007553b4903?user=10.177.223.78,zkcli/hadoop.hadoop.com@HADOOP.COM?ip=10.177.223.78?operation=create znode?target=ZooKeeperServer?znode=/test1?result=success
   2016-12-28 14:17:10,530 | INFO  | CommitProcWorkThread-4 | session=0x12000007553b4903?user=10.177.223.78,zkcli/hadoop.hadoop.com@HADOOP.COM?ip=10.177.223.78?operation=create znode?target=ZooKeeperServer?znode=/test2?result=success
   2016-12-28 14:17:10,550 | INFO  | CommitProcWorkThread-4 | session=0x12000007553b4903?user=10.177.223.78,zkcli/hadoop.hadoop.com@HADOOP.COM?ip=10.177.223.78?operation=create znode?target=ZooKeeperServer?znode=/test3?result=success
   2016-12-28 14:17:10,570 | INFO  | CommitProcWorkThread-4 | session=0x12000007553b4903?user=10.177.223.78,zkcli/hadoop.hadoop.com@HADOOP.COM?ip=10.177.223.78?operation=create znode?target=ZooKeeperServer?znode=/test4?result=success
   2016-12-28 14:17:10,592 | INFO  | CommitProcWorkThread-4 | session=0x12000007553b4903?user=10.177.223.78,zkcli/hadoop.hadoop.com@HADOOP.COM?ip=10.177.223.78?operation=create znode?target=ZooKeeperServer?znode=/test5?result=success
   2016-12-28 14:17:10,613 | INFO  | CommitProcWorkThread-4 | session=0x12000007553b4903?user=10.177.223.78,zkcli/hadoop.hadoop.com@HADOOP.COM?ip=10.177.223.78?operation=create znode?target=ZooKeeperServer?znode=/test6?result=success
   2016-12-28 14:17:10,633 | INFO  | CommitProcWorkThread-4 | session=0x12000007553b4903?user=10.177.223.78,zkcli/hadoop.hadoop.com@HADOOP.COM?ip=10.177.223.78?operation=create znode?target=ZooKeeperServer?znode=/test7?result=success

The content shows that logs of the ZooKeeper client user **zkcli/hadoop.hadoop.com@HADOOP.COM** are added to the audit log.

**User details in ZooKeeper**

In ZooKeeper, different authentication schemes use different credentials as users. Based on the authentication provider requirement, any parameter can be considered as users.

Example:

-  **SAMLAuthenticationProvider** uses the client principal as a user.
-  **X509AuthenticationProvider** uses the user client certificate as a user.
-  **IAuthenticationProvider** uses the client IP address as a user.
-  A username can be obtained from the custom authentication provider by implementing the **org.apache.zookeeper.server.auth.ExtAuthenticationProvider.getUserName(String)** method. If the method is not implemented, getting the username from the authentication provider instance will be skipped.

Enhanced Open Source Feature: ZooKeeper SSL Communication (Netty Connection)
----------------------------------------------------------------------------

The ZooKeeper design contains the Nio package and does not support SSL later than version 3.5. To solve this problem, Netty is added to ZooKeeper. Therefore, if you need to use SSL, enable Netty and set the following parameters on the server and client:

The open source server supports only plain text passwords, which may cause security problems. Therefore, such text passwords are no longer used on the server.

-  Client

   #. Set **-Dzookeeper.client.secure** in the **zkCli.sh/zkEnv.sh** file to **true** to use secure communication on the client. Then, the client can connect to the secureClientPort on the server.
   #. Set the following parameters in the **zkCli.sh/zkEnv.sh** file to configure the client environment:

      +-------------------------------------+---------------------------------------------------------------------------------------------------+
      | Parameter                           | Description                                                                                       |
      +=====================================+===================================================================================================+
      | -Dzookeeper.clientCnxnSocket        | Used for Netty communication between clients.                                                     |
      |                                     |                                                                                                   |
      |                                     | Default value: **org.apache.zookeeper.ClientCnxnSocketNetty**                                     |
      +-------------------------------------+---------------------------------------------------------------------------------------------------+
      | -Dzookeeper.ssl.keyStore.location   | Indicates the path for storing the keystore file.                                                 |
      +-------------------------------------+---------------------------------------------------------------------------------------------------+
      | -Dzookeeper.ssl.keyStore.password   | Encrypts a password.                                                                              |
      +-------------------------------------+---------------------------------------------------------------------------------------------------+
      | -Dzookeeper.ssl.trustStore.location | Indicates the path for storing the truststore file.                                               |
      +-------------------------------------+---------------------------------------------------------------------------------------------------+
      | -Dzookeeper.ssl.trustStore.password | Encrypts a password.                                                                              |
      +-------------------------------------+---------------------------------------------------------------------------------------------------+
      | -Dzookeeper.config.crypt.class      | Decrypts an encrypted password.                                                                   |
      +-------------------------------------+---------------------------------------------------------------------------------------------------+
      | -Dzookeeper.ssl.password.encrypted  | Default value: **false**                                                                          |
      |                                     |                                                                                                   |
      |                                     | If the keystore and truststore passwords are encrypted, set this parameter to **true**.           |
      +-------------------------------------+---------------------------------------------------------------------------------------------------+
      | -Dzookeeper.ssl.enabled.protocols   | Defines the SSL protocols to be enabled for the SSL context.                                      |
      +-------------------------------------+---------------------------------------------------------------------------------------------------+
      | -Dzookeeper.ssl.exclude.cipher.ext  | Defines the list of passwords separated by a comma which should be excluded from the SSL context. |
      +-------------------------------------+---------------------------------------------------------------------------------------------------+

      .. note::

         The preceding parameters must be set in the **zkCli.sh/zk.Env.sh** file.

-  Server

   #. Set **secureClientPort** to **3381** in the **zoo.cfg** file.
   #. Set **zookeeper.serverCnxnFactory** to **org.apache.zookeeper.server.NettyServerCnxnFactory** in the **zoo.cfg** file on the server.
   #. Set the following parameters in the **zoo.cfg** file (in the **zookeeper/conf/zoo.cfg** path) to configure the server environment:

      +-----------------------------------+---------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                       |
      +===================================+===================================================================================================+
      | ssl.keyStore.location             | Path for storing the **keystore.jks** file                                                        |
      +-----------------------------------+---------------------------------------------------------------------------------------------------+
      | ssl.keyStore.password             | Encrypts a password.                                                                              |
      +-----------------------------------+---------------------------------------------------------------------------------------------------+
      | ssl.trustStore.location           | Indicates the path for storing the truststore file.                                               |
      +-----------------------------------+---------------------------------------------------------------------------------------------------+
      | ssl.trustStore.password           | Encrypts a password.                                                                              |
      +-----------------------------------+---------------------------------------------------------------------------------------------------+
      | config.crypt.class                | Decrypts an encrypted password.                                                                   |
      +-----------------------------------+---------------------------------------------------------------------------------------------------+
      | ssl.keyStore.password.encrypted   | Default value: **false**                                                                          |
      |                                   |                                                                                                   |
      |                                   | If this parameter is set to **true**, the encrypted password can be used.                         |
      +-----------------------------------+---------------------------------------------------------------------------------------------------+
      | ssl.trustStore.password.encrypted | Default value: **false**                                                                          |
      |                                   |                                                                                                   |
      |                                   | If this parameter is set to **true**, the encrypted password can be used.                         |
      +-----------------------------------+---------------------------------------------------------------------------------------------------+
      | ssl.enabled.protocols             | Defines the SSL protocols to be enabled for the SSL context.                                      |
      +-----------------------------------+---------------------------------------------------------------------------------------------------+
      | ssl.exclude.cipher.ext            | Defines the list of passwords separated by a comma which should be excluded from the SSL context. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------+

   #. Start ZKserver and connect the security client to the security port.

-  Credential

   The credential used between client and server in ZooKeeper is **X509AuthenticationProvider**. This credential is initialized using the server certificates specified and trusted by the following parameters:

   -  zookeeper.ssl.keyStore.location
   -  zookeeper.ssl.keyStore.password
   -  zookeeper.ssl.trustStore.location
   -  zookeeper.ssl.trustStore.password

   .. note::

      If you do not want to use default mechanism of ZooKeeper, then it can be configured with different trust mechanisms as needed.
