:original_name: mrs_01_2101.html

.. _mrs_01_2101:

Configuring the Port Range Bound to the Client
==============================================

Scenarios
---------

When the ZooKeeper client is started, it is bound to a random port. In most cases, you want to bind the ZooKeeper client to a specific port. For example, for the client connection whitelist based on the IP address and port number, users can configure the port range bound to the client so that the same port range can be configured in the connection whitelist.

Configuration Description
-------------------------

Set **zookeeper.client.bind.port.range** to *<startPort:endPort>* to ensure that the client is always bound to a port in the specified port range. For example, if **zookeeper.client.bind.port.range** is set to **65510:65512**, the client can be bound only to port **65510**, **65511**, or **65512**.

To set **zookeeper.client.bind.port.range** to *<startPort:endPort>*, set **Dzookeeper.client.bind.port.range** to *<startPort:endPort>* when starting the ZooKeeper client.

.. table:: **Table 1** Parameter description

   +----------------------------------+----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+
   | Parameter                        | System Parameter                 | Description                                                                                                                                                                                                                                                                                                                           | Default Value   |
   +==================================+==================================+=======================================================================================================================================================================================================================================================================================================================================+=================+
   | zookeeper.client.bind.port.range | zookeeper.client.bind.port.range | This parameter is optional. Range of ports that can be used by the client during binding. The format is startPort:endPort (including startPort and endPort). The values of startPort and endPort range from 1024 to 65535, and the value of endPort must be greater than that of startPort. For example, 50000:50050 and 50100:50200. | ``-``           |
   |                                  |                                  |                                                                                                                                                                                                                                                                                                                                       |                 |
   |                                  |                                  | The client can be successfully connected only when at least two ports are available. If no port is available in the configured port range, the client fails to connect to the server. If the configured value is invalid, the value is ignored, the error is recorded, and the client will be bound to a random port.                 |                 |
   +----------------------------------+----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+

Procedure
---------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to switch to the client installation directory:

   **cd** **/opt/client**

#. Run the following command to edit the **component_env** file:

   **vi ZooKeeper/component_env**

   Add the **zookeeper.client.bind.port.range** parameter and its value.

   Normal mode:

   .. code-block::

      export ZOOKEEPER_HOME="/opt/client/ZooKeeper/zookeeper"
      PATH_NEW=`echo $PATH | sed "s|:$ZOOKEEPER_HOME/bin||g" | sed "s|$ZOOKEEPER_HOME/bin:||g"`
      export PATH="$ZOOKEEPER_HOME/bin:$PATH_NEW"
      # default heap for zookeeper client
      export ZK_CLIENT_HEAP="256"
      export CLIENT_JVMFLAGS="-Xmx${ZK_CLIENT_HEAP}m"
      export CLIENT_JVMFLAGS="$CLIENT_JVMFLAGS -Dzookeeper.root.logger=WARN,CONSOLE -Dzookeeper.request.timeout=120000 -Dzookeeper.client.bind.port.range=<startPort:endPort>" # Add a parameter.

   Security mode:

   .. code-block::

      if [ "$HADOOP_SECURITY_AUTHENTICATION" = "kerberos" ]; then
          default_realm=`cat $KRB5_CONFIG |grep default_realm|awk -F"=" '{gsub(" ","");print $2}'|tr 'A-Z' 'a-z'`
          export ZOO_SERVER_PRINCIPAL="zookeeper/hadoop.${default_realm}"
          export CLIENT_JVMFLAGS=" ${CLIENT_JVMFLAGS} -Djava.security.krb5.conf=$KRB5_CONFIG -Dzookeeper.client.bind.port.range=<startPort:endPort>"  # Add a parameter.

4. Run the **:wq** command to save execution.
5. Restart the client for the settings to take effect.
