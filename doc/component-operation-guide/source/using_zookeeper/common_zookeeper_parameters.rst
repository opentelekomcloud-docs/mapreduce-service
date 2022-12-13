:original_name: mrs_01_2094.html

.. _mrs_01_2094:

Common ZooKeeper Parameters
===========================

**Navigation path for setting parameters:**

Go to the **All Configurations** page of ZooKeeper by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`. Enter a parameter name in the search box.

.. table:: **Table 1** Parameters

   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | Parameter             | Description                                                                                                                                                                                   | Default Value |
   +=======================+===============================================================================================================================================================================================+===============+
   | skipACL               | Specifies whether to skip the permission check of the ZooKeeper node.                                                                                                                         | no            |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | maxClientCnxns        | Specifies the maximum number of connections of ZooKeeper. It is recommended this parameter is set to a larger value in scenarios with a large number of connections.                          | 2000          |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | LOG_LEVEL             | Specifies the log level. This parameter can be set to **DEBUG** during commissioning.                                                                                                         | INFO          |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | acl.compare.shortName | Specifies whether to perform ACL authentication only by principal username when the Znode ACL authentication type is SASL.                                                                    | true          |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | synclimit             | Specifies the interval of synchronization between the follower and leader (unit: tick). If the leader does not respond within the specified time range, the connection cannot be established. | 15            |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | tickTime              | Specifies the duration of a tick (in milliseconds). It is the basic time unit used by ZooKeeper, which defines heartbeat and timeout durations.                                               | 4000          |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+

.. note::

   The ZooKeeper internal time is determined by **ticktime** and **synclimit**. To increase the ZooKeeper internal timeout interval, increase the timeout interval for the client to connect to ZooKeeper.
