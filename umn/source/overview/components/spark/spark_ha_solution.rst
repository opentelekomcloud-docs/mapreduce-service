:original_name: mrs_08_00082.html

.. _mrs_08_00082:

Spark HA Solution
=================

Spark Multi-Active Instance HA Principles and Implementation Solution
---------------------------------------------------------------------

Based on existing JDBCServer in the community, multi-active-instance mode is used to achieve HA. In this mode, multiple JDBCServers coexist in the cluster and the client can randomly connect any JDBCServer to perform service operations. When one or multiple JDBCServers stop working, a client can connect to another normal JDBCServer.

Compared with active/standby HA mode, multi-active instance mode has following advantages:

-  In active/standby HA, when the active/standby switchover occurs, the unavailable period cannot be controlled by JDBCServer, but it depends on Yarn service resources.
-  In Spark, the Thrift JDBC similar to HiveServer2 provides services and users access services through Beeline and JDBC API. Therefore, the processing capability of the JDBCServer cluster depends on the single-point capability of the primary server, and the scalability is insufficient.

The multi-active instance HA mode not only can prevent service interruption caused by switchover, but also enables cluster scale-out to improve high concurrency.

-  **Implementation**

   The following figure shows the basic principle of multi-active instance HA of Spark JDBCServer.


   .. figure:: /_static/images/en-us_image_0000001349110489.png
      :alt: **Figure 1** Spark JDBCServer HA

      **Figure 1** Spark JDBCServer HA

#. When a JDBCServer is started, it registers with ZooKeeper by writing node information in a specified directory. Node information includes the instance IP address, port number, version, and serial number.
#. To connect to JDBCServer, the client must specify the namespace, which is the directory of JDBCServer instances in ZooKeeper. During the connection, a JDBCServer instance is randomly selected from the specified namespace.
#. After the connection succeeds, the client sends SQL statements to JDBCServer.
#. JDBCServer executes received SQL statements and returns results to the client.

If multi-active instance HA of Spark JDBCServer is enabled, all JDBCServer instances are independent and equivalent. When one JDBCServer instance is interrupted during upgrade, other JDBCServer instances can accept the connection request from the client.

The rules below must be followed in the multi-active instance HA of Spark JDBCServer.

-  If a JDBCServer instance exits abnormally, no other instance will take over the sessions and services running on the abnormal instance.
-  When the JDBCServer process is stopped, corresponding nodes are deleted from ZooKeeper.
-  The client randomly selects the server, which may result in uneven session allocation caused by random distribution of policy results, and finally result in load imbalance of instances.
-  After the instance enters the maintenance mode (in which no new connection requests from clients are accepted), services running on the instance may fail when the decommissioning times out.

-  **URL Connection**

   -  Multi-active instance mode

      In multi-active instance mode, the client reads content from the ZooKeeper node and connects to JDBCServer. The connection strings are list below.

      -  Security mode:

         If Kinit authentication is enabled, the JDBCURL is as follows:

         .. code-block::

            jdbc:hive2://<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;saslQop=auth-conf;auth=KERBEROS;principal=spark/hadoop.<System domain name>@<System domain name>;

         .. note::

            -  In the above JDBCURL, **<zkNode_IP>:<zkNode_Port>** indicates the ZooKeeper URL. Use commas (,) to separate multiple URLs,

               Example: 192.168.81.37:2181,192.168.195.232:2181,192.168.169.84:2181.

            -  **sparkthriftserver2x** indicates the ZooKeeper directory, where a random JDBCServer instance is connected to the client.

         For example, when you use Beeline client to connect JDBCServer, run the following command:

         **sh** *CLIENT_HOME*\ **/spark/bin/beeline -u "jdbc:hive2://**\ *<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>*\ **/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;saslQop=auth-conf;auth=KERBEROS;principal=spark/hadoop.**\ *<System domain name>*\ **@**\ *<System domain name>*\ **;"**

         If Keytab authentication is enabled, the JDBCURL is as follows:

         .. code-block::

            jdbc:hive2://<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;saslQop=auth-conf;auth=KERBEROS;principal=spark/hadoop.<System domain name>@<System domain name>;user.principal=<principal_name>;user.keytab=<path_to_keytab>

         In the above URL, *<principal_name>* indicates the principal of the Kerberos user, for example, **test@**\ *<System domain name>*; *<path_to_keytab>* indicates the Keytab file path corresponding to *<principal_name>*, for example, **/opt/auth/test/user.keytab**.

      -  Common mode:

         .. code-block::

            jdbc:hive2://<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;

         For example, when you use Beeline client, in normal mode, for connection, run the following command:

         **sh** *CLIENT_HOME*\ **/spark/bin/beeline -u "jdbc:hive2://**\ *<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>*\ **/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;"**

   -  Non-multi-active instance mode

      In this mode, a client connects to a specified JDBCServer node. Compared with multi-active instance mode, the connection string in this mode does not contain **serviceDiscoveryMode** and **zooKeeperNamespace** parameters about ZooKeeper.

      For example, when you use Beeline client, in security mode, to connect JDBCServer in non-multi-active instance mode, run the following command:

      **sh** *CLIENT_HOME*\ **/spark/bin/beeline -u "jdbc:hive2://**\ *<server_IP>:<server_Port>*\ **/;user.principal=spark/hadoop.**\ *<System domain name>@<System domain name>*\ **;saslQop=auth-conf;auth=KERBEROS;principal=spark/hadoop.**\ *<System domain name>@<System domain name>*\ **;"**

      .. note::

         -  In the above command, **<server_IP>:<server_Port>** indicates the URL of the specified JDBCServer node.
         -  **CLIENT_HOME** indicates the client path.

      Except the connection method, other operations of JDBCServer API in the two modes are the same. Spark JDBCServer is another implementation of HiveServer2 in Hive. For details about how to use Spark JDBCServer, see https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients.

Spark Multi-Tenant HA
---------------------

In the JDBCServer multi-active instance solution, JDBCServer uses the Yarn-client mode, but there is only one Yarn resource queue available. To solve this resource limitation problem, the multi-tenant mode is introduced.

In multi-tenant mode, JDBCServers are bound with tenants. Each tenant corresponds to one or more JDBCServers, and a JDBCServer provides services for only one tenant. Different tenants can be configured with different Yarn queues to implement resource isolation. In addition, JDBCServer can be dynamically started as required to avoid resource waste.

-  **Implementation**

   :ref:`Figure 2 <mrs_08_00082__fd976abf162d04390bb64dc2ab6d2d226>` shows the HA solution of the multi-tenant mode.

   .. _mrs_08_00082__fd976abf162d04390bb64dc2ab6d2d226:

   .. figure:: /_static/images/en-us_image_0000001349309945.png
      :alt: **Figure 2** Multi-tenant mode of Spark JDBCServer

      **Figure 2** Multi-tenant mode of Spark JDBCServer

   #. When ProxyServer is started, it registers with ZooKeeper by writing node information in a specified directory. Node information includes the instance IP address, port number, version, and serial number.

      .. note::

         In multi-tenant mode, the JDBCServer instance refers to the ProxyServer (JDBCServer proxy).

   #. To connect to ProxyServer, the client must specify a namespace, which is the directory of the ProxyServer instance where you want to access ZooKeeper. When the client connects to the ProxyServer, a random instance under the namespace is selected for connection. For details about the URL, see :ref:`URL Connection Overview <mrs_08_00082__li4440192917386>`.
   #. After the client successfully connects to the ProxyServer, which first checks whether the JDBCServer of a tenant exists. If yes, Beeline connects the JDBCServer. If no, a new JDBCServer is started in Yarn-cluster mode. After the startup of JDBCServer, ProxyServer obtains the IP address of the JDBCServer and establishes the connection between Beeline and JDBCServer.
   #. The client sends SQL statements to ProxyServer, which forwards statements to the connected JDBCServer. JDBCServer returns the results to ProxyServer, which then returns the results to the client.

   In the multi-active instance HA mode, all instances are independent and equivalent. If one instance is interrupted during upgrade, other instances can accept the connection request from the client.

-  .. _mrs_08_00082__li4440192917386:

   **URL Connection Overview**

   -  Multi-tenant mode

      In multi-tenant mode, the client reads content from the ZooKeeper node and connects to ProxyServer. The connection strings are list below.

      -  Security mode:

         If Kinit authentication is enabled, the client URL is as follows:

         .. code-block::

            jdbc:hive2://<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;saslQop=auth-conf;auth=KERBEROS;principal=spark/hadoop.<System domain name>@<System domain name>;

         .. note::

            -  In the above URL, **<zkNode_IP>:<zkNode_Port>** indicates the ZooKeeper URL. Use commas (,) to separate multiple URLs,

               Example: **192.168.81.37:2181,192.168.195.232:2181,192.168.169.84:2181**.

            -  **sparkthriftserver2x** indicates the ZooKeeper directory, where a random JDBCServer instance is connected to the client.

         For example, when you use Beeline client for connection, run the following command:

         **sh** *CLIENT_HOME*\ **/spark/bin/beeline -u "jdbc:hive2://**\ *<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>*\ **/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;saslQop=auth-conf;auth=KERBEROS;principal=spark/hadoop.**\ *<System domain name>*\ **@**\ *<System domain name>*\ **;"**

         If Keytab authentication is enabled, the URL is as follows:

         .. code-block::

            jdbc:hive2://<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;saslQop=auth-conf;auth=KERBEROS;principal=spark/hadoop.<System domain name>@<System domain name>;user.principal=<principal_name>;user.keytab=<path_to_keytab>

         In the above URL, *<principal_name>* indicates the principal of the Kerberos user, for example, **test@**\ *<System domain name>*; *<path_to_keytab>* indicates the Keytab file path corresponding to *<principal_name>*, for example, **/opt/auth/test/user.keytab**.

      -  Common mode:

         .. code-block::

            jdbc:hive2://<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;

         For example, run the following command when you use Beeline client for connection in normal mode:

         **sh** *CLIENT_HOME*\ **/spark/bin/beeline -u "jdbc:hive2://**\ *<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>*\ **/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;"**

   -  Non-multi-tenant mode

      In non-multi-tenant mode, a client connects to a specified JDBCServer node. Compared with multi-tenant instance mode, the connection string in this mode does not contain **serviceDiscoveryMode** and **zooKeeperNamespace** parameters about ZooKeeper.

      For example, when you use Beeline client to connect JDBCServer in non-multi-tenant instance mode, run the following command:

      **sh** *CLIENT_HOME*\ **/spark/bin/beeline -u "jdbc:hive2://**\ *<server_IP>:<server_Port>*\ **/;user.principal=spark/hadoop.**\ *<System domain name>@<System domain name>*\ **;saslQop=auth-conf;auth=KERBEROS;principal=spark/hadoop.**\ *<System domain name>@<System domain name>*\ **;"**

      .. note::

         -  In the above command, **<server_IP>:<server_Port>** indicates the URL of the specified JDBCServer node.
         -  **CLIENT_HOME** indicates the client path.

      Except the connection method, other operations of JDBCServer API in multi-tenant mode and non-multi-tenant mode are the same. Spark JDBCServer is another implementation of HiveServer2 in Hive. For details about how to use Spark JDBCServer, go to the official Hive website at https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients.

      **Specifying a Tenant**

      Generally, the client submitted by a user connects to the default JDBCServer of the tenant to which the user belongs. If you want to connect the client to the JDBCServer of a specified tenant, add the **--hiveconf mapreduce.job.queuename** parameter.

      If you use Beeline client for connection, run the following command (**aaa** is the tenant name):

      **beeline --hiveconf mapreduce.job.queuename=aaa -u 'jdbc:hive2://192.168.39.30:2181,192.168.40.210:2181,192.168.215.97:2181;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;saslQop=auth-conf;auth=KERBEROS;principal=spark/hadoop.\ <System domain name>\ @\ <System domain name>;'**
