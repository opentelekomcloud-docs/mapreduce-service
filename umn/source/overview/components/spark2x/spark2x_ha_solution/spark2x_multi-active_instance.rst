:original_name: mrs_08_007103.html

.. _mrs_08_007103:

Spark2x Multi-active Instance
=============================

Background
----------

Based on existing JDBCServers in the community, multi-active-instance HA is used to achieve the high availability. In this mode, multiple JDBCServers coexist in the cluster and the client can randomly connect any JDBCServer to perform service operations. When one or multiple JDBCServers stop working, a client can connect to another normal JDBCServer.

Compared with active/standby HA, multi-active instance HA eliminates the following restrictions:

-  In active/standby HA, when the active/standby switchover occurs, the unavailable period cannot be controlled by JDBCServer, but determined by Yarn service resources.
-  In Spark, the Thrift JDBC similar to HiveServer2 provides services and users access services through Beeline and JDBC API. Therefore, the processing capability of the JDBCServer cluster depends on the single-point capability of the primary server, and the scalability is insufficient.

Multi-active instance HA not only prevents service interruption caused by switchover, but also enables cluster scale-out to secure high concurrency.

Implementation
--------------

The following figure shows the basic principle of multi-active instance HA of Spark JDBCServer.


.. figure:: /_static/images/en-us_image_0000001349309965.png
   :alt: **Figure 1** Spark JDBCServer HA

   **Figure 1** Spark JDBCServer HA

#. After JDBCServer is started, it registers with ZooKeeper by writing node information in a specified directory. Node information includes the JDBCServer instance IP, port number, version, and serial number (information of different nodes is separated by commas).

   An example is provided as follows:

   .. code-block::

      [serverUri=192.168.169.84:22550
      ;version=8.1.0.1;sequence=0000001244,serverUri=192.168.195.232:22550 ;version=8.1.0.1;sequence=0000001242,serverUri=192.168.81.37:22550 ;version=8.1.0.1;sequence=0000001243]

#. To connect to JDBCServer, the client must specify the namespace, which is the directory of JDBCServer instances in ZooKeeper. During the connection, a JDBCServer instance is randomly selected from the specified namespace. For details about URL, see :ref:`URL Connection <mrs_08_007103__s85fcf528f3e0410bb62ba828660aa83d>`.

#. After the connection succeeds, the client sends SQL statements to JDBCServer.

#. JDBCServer executes received SQL statements and sends results back to the client.

In multi-active instance HA mode, all JDBCServer instances are independent and equivalent. When one instance is interrupted during upgrade, other JDBCServer instances can accept the connection request from the client.

Following rules must be followed in the multi-active instance HA of Spark JDBCServer:

-  If a JDBCServer instance exits abnormally, no other instance will take over the sessions and services running on this abnormal instance.
-  When the JDBCServer process is stopped, corresponding nodes are deleted from ZooKeeper.
-  The client randomly selects the server, which may result in uneven session allocation, and finally result in imbalance of instance load.
-  After the instance enters the maintenance mode (in which no new connection request from the client is accepted), services still running on the instance may fail when the decommissioning times out.

.. _mrs_08_007103__s85fcf528f3e0410bb62ba828660aa83d:

URL Connection
--------------

**Multi-active instance mode**

In multi-active instance mode, the client reads content from the ZooKeeper node and connects to JDBCServer. The connection strings are as follows:

-  Security mode:

   -  If Kinit authentication is enabled, the JDBCURL is as follows:

      .. code-block::

         jdbc:hive2://<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;saslQop=auth-conf;auth=KERBEROS;principal=spark2x/hadoop.<System domain name>@<System domain name>;

      .. note::

         -  **<zkNode_IP>:<zkNode_Port>** indicates the ZooKeeper URL. Use commas (,) to separate multiple URLs,

            For example, **192.168.81.37:2181,192.168.195.232:2181,192.168.169.84:2181**.

         -  **sparkthriftserver2x** indicates the directory in ZooKeeper, where a random JDBCServer instance is connected to the client.

      For example, when you use Beeline client for connection in security mode, run the following command:

      **sh** *CLIENT_HOME*\ **/spark/bin/beeline -u "jdbc:hive2://**\ *<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>*\ **/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;saslQop=auth-conf;auth=KERBEROS;principal=spark2x/hadoop.**\ *<System domain name>*\ **@**\ *<System domain name>*\ **;"**

   -  If Keytab authentication is enabled, the JDBCURL is as follows:

      .. code-block::

         jdbc:hive2://<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;saslQop=auth-conf;auth=KERBEROS;principal=spark2x/hadoop.<System domain name>@<System domain name>;user.principal=<principal_name>;user.keytab=<path_to_keytab>

      *<principal_name>* indicates the principal of Kerberos user, for example, **test@**\ *<System domain name>*. *<path_to_keytab>* indicates the Keytab file path corresponding to *<principal_name>*, for example, **/opt/auth/test/user.keytab**.

-  Common mode:

   .. code-block::

      jdbc:hive2://<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;

   For example, when you use Beeline client for connection in common mode, run the following command:

   **sh** *CLIENT_HOME*\ **/spark/bin/beeline -u "jdbc:hive2://**\ *<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>*\ **/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;"**

**Non-multi-active instance mode**

In non-multi-active instance mode, a client connects to a specified JDBCServer node. Compared with multi-active instance mode, the connection string in non-multi-active instance mode does not contain **serviceDiscoveryMode** and **zooKeeperNamespace** parameters about ZooKeeper.

For example, when you use Beeline client to connect JDBCServer in non-multi-active instance mode, run the following command:

**sh** *CLIENT_HOME*\ **/spark/bin/beeline -u "jdbc:hive2://**\ *<server_IP>:<server_Port>*\ **/;user.principal=spark2x/hadoop.**\ *<System domain name>@<System domain name>*\ **;saslQop=auth-conf;auth=KERBEROS;principal=spark2x/hadoop.**\ *<System domain name>@<System domain name>*\ **;"**

.. note::

   -  **<server_IP>:<server_Port>** indicates the URL of the specified JDBCServer node.
   -  **CLIENT_HOME** indicates the client path.

Except the connection method, operations of JDBCServer API in multi-active instance mode and non-multi-active instance mode are the same. Spark JDBCServer is another implementation of HiveServer2 in Hive. For details about other operations, see official website of Hive at https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients.
