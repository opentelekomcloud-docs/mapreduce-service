:original_name: mrs_01_1958.html

.. _mrs_01_1958:

Configuring Whether Spark Obtains HBase Tokens
==============================================

Scenario
--------

When Spark is used to submit tasks, the driver obtains tokens from HBase by default. To access HBase, you need to configure the **jaas.conf** file for security authentication. If the **jaas.conf** file is not configured, the application will fail to run.

Therefore, perform the following operations based on whether the application involves HBase:

-  If the application does not involve HBase, you do not need to obtain the HBase tokens. In this case, set **spark.yarn.security.credentials.hbase.enabled** to **false**.

-  If the application involves HBase, set **spark.yarn.security.credentials.hbase.enabled** to **true** and configure the **jaas.conf** file on the driver as follows:

   .. code-block::

      {client}/spark/bin/spark-sql  --master yarn-client --principal {principal} --keytab {keytab} --driver-java-options "-Djava.security.auth.login.config={LocalPath}/jaas.conf"

   Specify Keytab and Principal in the **jaas.conf** file. The following is an example:

   .. code-block::

      Client {
      com.sun.security.auth.module.Krb5LoginModule required
      useKeyTab=true
      keyTab = "{LocalPath}/user.keytab"
      principal="super@<System domain name>"
      useTicketCache=false
      debug=false;
      };

Configuration
-------------

Configure the following parameter in the **spark-defaults.conf** file of the Spark client.

.. table:: **Table 1** Parameter description

   +-----------------------------------------------+----------------------------------------------+-----------------------+
   | Parameter                                     | Description                                  | Default Value         |
   +===============================================+==============================================+=======================+
   | spark.yarn.security.credentials.hbase.enabled | Indicates whether HBase obtains a token.     | false                 |
   |                                               |                                              |                       |
   |                                               | -  **true**: HBase obtains a token.          |                       |
   |                                               | -  **false**: HBase does not obtain a token. |                       |
   +-----------------------------------------------+----------------------------------------------+-----------------------+
