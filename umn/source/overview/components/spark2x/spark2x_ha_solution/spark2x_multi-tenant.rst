:original_name: mrs_08_007104.html

.. _mrs_08_007104:

Spark2x Multi-tenant
====================

Background
----------

In the JDBCServer multi-active instance mode, JDBCServer implements the Yarn-client mode but only one Yarn resource queue is available. To solve the resource limitation problem, the multi-tenant mode is introduced.

In multi-tenant mode, JDBCServers are bound with tenants. Each tenant corresponds to one or more JDBCServers, and a JDBCServer provides services for only one tenant. Different tenants can be configured with different Yarn queues to implement resource isolation. In addition, JDBCServer can be dynamically started as required to avoid resource waste.

Implementation
--------------

:ref:`Figure 1 <mrs_08_007104__fd976abf162d04390bb64dc2ab6d2d226>` shows the HA solution of the multi-tenant mode.

.. _mrs_08_007104__fd976abf162d04390bb64dc2ab6d2d226:

.. figure:: /_static/images/en-us_image_0000001349309933.png
   :alt: **Figure 1** Multi-tenant mode of Spark JDBCServer

   **Figure 1** Multi-tenant mode of Spark JDBCServer

#. When ProxyServer is started, it registers with ZooKeeper by writing node information in a specified directory. Node information includes the instance IP, port number, version, and serial number (information of different nodes is separated by commas).

   .. note::

      In multi-tenant mode, the JDBCServer instance on MRS page indicates ProxyServer, the JDBCServer agent.

   An example is provided as follows:

   .. code-block::

      serverUri=192.168.169.84:22550
      ;version=8.1.0.1;sequence=0000001244,serverUri=192.168.195.232:22550
      ;version=8.1.0.1;sequence=0000001242,serverUri=192.168.81.37:22550
      ;version=8.1.0.1;sequence=0000001243,

#. To connect to ProxyServer, the client must specify a namespace, which is the directory of the ProxyServer instance that you want to access in ZooKeeper. When the client connects to ProxyServer, an instance under Namespace is randomly selected for connection. For details about the URL, see :ref:`URL Connection <mrs_08_007104__s554f2fdef78b47bda50abc0b84bbbd5a>`.

#. After the client successfully connects to ProxyServer, ProxyServer checks whether the JDBCServer of a tenant exists. If yes, Beeline connects the JDBCServer. If no, a new JDBCServer is started in Yarn-cluster mode. After the startup of JDBCServer, ProxyServer obtains the IP address of the JDBCServer and establishes the connection between Beeline and JDBCServer.

#. The client sends SQL statements to ProxyServer, which then forwards statements to the connected JDBCServer. JDBCServer returns the results to ProxyServer, which then returns the results to the client.

In multi-tenant HA mode, all ProxyServer instances are independent and equivalent. If one instance is interrupted during upgrade, other instances can accept the connection request from the client.

.. _mrs_08_007104__s554f2fdef78b47bda50abc0b84bbbd5a:

URL Connection
--------------

**Multi-tenant mode**

In multi-tenant mode, the client reads content from the ZooKeeper node and connects to ProxyServer. The connection strings are as follows:

-  Security mode:

   -  If Kinit authentication is enabled, the client URL is as follows:

      .. code-block::

         jdbc:hive2://<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;saslQop=auth-conf;auth=KERBEROS;principal=spark2x/hadoop.<System domain name>@<System domain name>;

      .. note::

         -  **<zkNode_IP>:<zkNode_Port>** indicates the ZooKeeper URL. Use commas (,) to separate multiple URLs,

            For example, **192.168.81.37:2181,192.168.195.232:2181,192.168.169.84:2181**.

         -  **sparkthriftserver2x** indicates the ZooKeeper directory, where a random JDBCServer instance is connected to the client.

      For example, when you use Beeline client for connection in security mode, run the following command:

      **sh** *CLIENT_HOME*\ **/spark/bin/beeline -u "jdbc:hive2://**\ *<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>*\ **/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;saslQop=auth-conf;auth=KERBEROS;principal=spark2x/hadoop.**\ *<System domain name>*\ **@**\ *<System domain name>*\ **;"**

   -  If Keytab authentication is enabled, the URL is as follows:

      .. code-block::

         jdbc:hive2://<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;saslQop=auth-conf;auth=KERBEROS;principal=spark2x/hadoop.<System domain name>@<System domain name>;user.principal=<principal_name>;user.keytab=<path_to_keytab>

      *<principal_name>* indicates the principal of Kerberos user, for example, **test@**\ *<System domain name>*. *<path_to_keytab>* indicates the Keytab file path corresponding to *<principal_name>*, for example, **/opt/auth/test/user.keytab**.

-  Common mode:

   .. code-block::

      jdbc:hive2://<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;

   For example, when you use Beeline client for connection in common mode, run the following command:

   **sh** *CLIENT_HOME*\ **/spark/bin/beeline -u "jdbc:hive2://**\ *<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>*\ **/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;"**

**Non-multi-tenant mode**

In non-multi-tenant mode, a client connects to a specified JDBCServer node. Compared with multi-active instance mode, the connection string in non-multi-active instance mode does not contain **serviceDiscoveryMode** and **zooKeeperNamespace** parameters about ZooKeeper.

For example, when you use Beeline client to connect JDBCServer in non-multi-tenant instance mode, run the following command:

**sh** *CLIENT_HOME*\ **/spark/bin/beeline -u "jdbc:hive2://**\ *<server_IP>:<server_Port>*\ **/;user.principal=spark/hadoop.**\ *<System domain name>@<System domain name>*\ **;saslQop=auth-conf;auth=KERBEROS;principal=spark/hadoop.**\ *<System domain name>@<System domain name>*\ **;"**

.. note::

   -  **<server_IP>:<server_Port>** indicates the URL of the specified JDBCServer node.
   -  **CLIENT_HOME** indicates the client path.

Except the connection method, other operations of JDBCServer API in multi-tenant mode and non-multi-tenant mode are the same. Spark JDBCServer is another implementation of HiveServer2 in Hive. For details about other operations, see official website of Hive at https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients.

**Specifying a Tenant**

Generally, the client submitted by a user connects to the default JDBCServer of the tenant to which the user belongs. If you want to connect the client to the JDBCServer of a specified tenant, add the **--hiveconf mapreduce.job.queuename** parameter.

Command for connecting Beeline is as follows (**aaa** indicates the tenant name):

**beeline --hiveconf mapreduce.job.queuename=aaa -u 'jdbc:hive2://192.168.39.30:2181,192.168.40.210:2181,192.168.215.97:2181;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;saslQop=auth-conf;auth=KERBEROS;principal=spark2x/hadoop.\ <System domain name>\ @\ <System domain name>;'**
