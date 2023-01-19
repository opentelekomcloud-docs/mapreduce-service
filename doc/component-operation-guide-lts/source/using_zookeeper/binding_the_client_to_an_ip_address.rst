:original_name: mrs_01_2100.html

.. _mrs_01_2100:

Binding the Client to an IP Address
===================================

Scenarios
---------

To prevent multiple IP nodes, bind the current ZooKeeper client to any available IP address. The data flow layer, management layer, and other network layers in the production environment have different IP address ranges. Bind the ZooKeeper client to the IP address at the data flow layer. This helps locate the failure scenario where the data IP address is unreachable.

Configuration Description
-------------------------

Configure **zookeeper.client.bind.address** to ensure that the client is always bound to the specified IP address. To set **zookeeper.client.bind.address** to *X*, set **-Dzookeeper.client.bind.address** to *X* when starting the ZooKeeper client.

.. table:: **Table 1** Parameter description

   +-------------------------------+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | Parameter                     | System Parameter              | Description                                                                                                                                           | Default Value |
   +===============================+===============================+=======================================================================================================================================================+===============+
   | zookeeper.client.bind.address | zookeeper.client.bind.address | Optional. IP address or host name bound to the ZooKeeper client. By default, the ZooKeeper client is bound to any available IP address in the system. | ``-``         |
   +-------------------------------+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+

Procedure
---------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to switch to the client installation directory:

   **cd** **/opt/client**

#. Run the following command to edit the **component_env** file:

   **vi ZooKeeper/component_env**

   Add the **zookeeper.client.bind.address** parameter and its value.

   Normal mode:

   .. code-block::

      export ZOOKEEPER_HOME="/opt/client/ZooKeeper/zookeeper"
      PATH_NEW=`echo $PATH | sed "s|:$ZOOKEEPER_HOME/bin||g" | sed "s|$ZOOKEEPER_HOME/bin:||g"`
      export PATH="$ZOOKEEPER_HOME/bin:$PATH_NEW"
      # default heap for zookeeper client
      export ZK_CLIENT_HEAP="256"
      export CLIENT_JVMFLAGS="-Xmx${ZK_CLIENT_HEAP}m"
      export CLIENT_JVMFLAGS="$CLIENT_JVMFLAGS -Dzookeeper.root.logger=WARN,CONSOLE -Dzookeeper.request.timeout=120000 -Dzookeeper.client.bind.address=X" #Add a parameter. X indicates the configured IP address.

   Security mode:

   .. code-block::

      if [ "$HADOOP_SECURITY_AUTHENTICATION" = "kerberos" ]; then
          default_realm=`cat $KRB5_CONFIG |grep default_realm|awk -F"=" '{gsub(" ","");print $2}'|tr 'A-Z' 'a-z'`
          export ZOO_SERVER_PRINCIPAL="zookeeper/hadoop.${default_realm}"
          export CLIENT_JVMFLAGS=" ${CLIENT_JVMFLAGS} -Djava.security.krb5.conf=$KRB5_CONFIG -Dzookeeper.kin -Dzookeeper.client.bind.address=X" #Add a parameter. X indicates the configured IP address.

4. Run the **:wq** command to save execution.
5. Restart the client for the settings to take effect.
