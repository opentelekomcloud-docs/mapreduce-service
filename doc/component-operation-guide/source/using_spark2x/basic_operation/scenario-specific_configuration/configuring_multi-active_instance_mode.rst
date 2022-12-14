:original_name: mrs_01_1942.html

.. _mrs_01_1942:

Configuring Multi-active Instance Mode
======================================

Scenarios
---------

In this mode, multiple ThriftServers coexist in the cluster and the client can randomly connect any ThriftServer to perform service operations. When one or multiple ThriftServers stop working, a client can connect to another functional ThriftServer.

Configuration Description
-------------------------

Log in to Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Spark2x** > **Configurations**, click **All Configurations**, and search for and modify the following parameters.

.. table:: **Table 1** Parameter description

   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------+---------------+
   | Parameter                                       | Description                                                                                                      | Default Value |
   +=================================================+==================================================================================================================+===============+
   | spark.thriftserver.zookeeper.connection.timeout | Specifies the timeout interval of connection between ZooKeeper client and ThriftServer. The unit is millisecond. | 60000         |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------+---------------+
   | spark.thriftserver.zookeeper.session.timeout    | Specifies the timeout interval of a ZooKeeper client session. The unit is millisecond.                           | 90000         |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------+---------------+
   | spark.thriftserver.zookeeper.retry.times        | Specifies the retry times after ZooKeeper disconnection.                                                         | 3             |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------+---------------+
   | spark.yarn.queue                                | Specifies the Yarn queue where the JDBCServer service resides.                                                   | default       |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------+---------------+
