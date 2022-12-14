:original_name: mrs_01_1940.html

.. _mrs_01_1940:

Configuring the Client and Server
=================================

This section describes how to configure SparkSQL permission management functions (client configuration is similar to server configuration). To enable table permission, add following configurations on the client and server:

-  **spark-defaults.conf** configuration file

   .. table:: **Table 1** Parameter description (1)

      +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Parameter                       | Description                                                                                                                                                                           | Default Value |
      +=================================+=======================================================================================================================================================================================+===============+
      | spark.sql.authorization.enabled | Specifies whether to enable permission authentication of the datasource statement. It is recommended that the parameter value be set to **true** to enable permission authentication. | true          |
      +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+

-  **hive-site.xml** configuration file

   .. table:: **Table 2** Parameter description (2)

      +------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
      | Parameter                                            | Description                                                                                                                                           | Default Value                                                           |
      +======================================================+=======================================================================================================================================================+=========================================================================+
      | hive.metastore.uris                                  | Specifies the MetaStore service address of the Hive component, for example, **thrift://10.10.169.84:21088,thrift://10.10.81.37:21088**.               | ``-``                                                                   |
      +------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
      | hive.metastore.sasl.enabled                          | Specifies whether the MetaStore service uses SASL to improve security. The table permission function must be enabled.                                 | true                                                                    |
      +------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
      | hive.metastore.kerberos.principal                    | Specifies the principal of the MetaStore service in the Hive component, for example, **hive/hadoop.**\ <*system domain name*>@<*system domain name*>. | hive-metastore/_HOST@EXAMPLE.COM                                        |
      +------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
      | hive.metastore.thrift.sasl.qop                       | After the SparkSQL permission management function is enabled, set the parameter to **auth-conf**.                                                     | auth-conf                                                               |
      +------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
      | hive.metastore.token.signature                       | Specifies the token identifier of the MetaStore service, which is set to **HiveServer2ImpersonationToken**.                                           | HiveServer2ImpersonationToken                                           |
      +------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
      | hive.security.authenticator.manager                  | Specifies the manager authenticated by the Hive client, which is set to **org.apache.hadoop.hive.ql.security.SessionStateUserGroupAuthenticator**.    | org.apache.hadoop.hive.ql.security.SessionStateUserMSGroupAuthenticator |
      +------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
      | hive.security.authorization.enabled                  | Specifies whether to enable client authentication, which is set to **true**.                                                                          | true                                                                    |
      +------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
      | hive.security.authorization.createtable.owner.grants | Specifies which permissions are granted to the owner who creates the table, which is set to **ALL**.                                                  | ALL                                                                     |
      +------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+

-  **core-site.xml** configuration file of the MetaStore service

   .. table:: **Table 3** Parameter description (3)

      +-------------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------+
      | Parameter                     | Description                                                                                                              | Default Value |
      +===============================+==========================================================================================================================+===============+
      | hadoop.proxyuser.spark.hosts  | Specifies the hosts from which Spark users can be masqueraded, which is set to **\***, indicating all hosts.             | ``-``         |
      +-------------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------+
      | hadoop.proxyuser.spark.groups | Specifies the user groups from which Spark users can be masqueraded, which is set to **\***, indicating all user groups. | ``-``         |
      +-------------------------------+--------------------------------------------------------------------------------------------------------------------------+---------------+
