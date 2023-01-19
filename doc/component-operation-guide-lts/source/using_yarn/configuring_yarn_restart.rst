:original_name: mrs_01_0865.html

.. _mrs_01_0865:

Configuring Yarn Restart
========================

Scenario
--------

The Yarn Restart feature includes ResourceManager Restart and NodeManager Restart.

-  When ResourceManager Restart is enabled, the new active ResourceManager node loads the information of the previous active ResourceManager node, and takes over container status information on all NodeManager nodes to continue service running. In this way, status information can be saved by periodically executing checkpoint operations, avoiding data loss.
-  When NodeManager Restart is enabled, NodeManager locally saves information about containers running on the node. After NodeManager is restarted, the container running progress on the node will not be lost by restoring the saved status information.

Configuration Description
-------------------------

Go to the **All Configurations** page of Yarn and enter a parameter name in the search box by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.

Configure ResourceManager Restart as follows:

.. table:: **Table 1** Parameter description of ResourceManager Restart

   +-------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------+
   | Parameter                                             | Description                                                                                                                                                                              | Default Value                                                              |
   +=======================================================+==========================================================================================================================================================================================+============================================================================+
   | yarn.resourcemanager.recovery.enabled                 | Whether to enable ResourceManager to restore the status after startup. If this parameter is set to **true**, **yarn.resourcemanager.store.class** must also be set.                      | true                                                                       |
   +-------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------+
   | yarn.resourcemanager.store.class                      | State-store class used to store the application and task statuses and certificate content.                                                                                               | org.apache.hadoop.yarn.server.resourcemanager.recovery.AsyncZKRMStateStore |
   +-------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------+
   | yarn.resourcemanager.zk-state-store.parent-path       | Directory for storing ZKRMStateStore in ZooKeeper                                                                                                                                        | /rmstore                                                                   |
   +-------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------+
   | yarn.resourcemanager.work-preserving-recovery.enabled | Whether to enable ResourceManager work serving. This configuration is used only for Yarn feature verification.                                                                           | true                                                                       |
   +-------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------+
   | yarn.resourcemanager.state-store.async.load           | Whether to apply asynchronous restoration to completed applications.                                                                                                                     | true                                                                       |
   +-------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------+
   | yarn.resourcemanager.zk-state-store.num-fetch-threads | If asynchronous restoration is enabled, increasing the number of working threads can speed up the restoration of task information stored in ZooKeeper. The value must be greater than 0. | 20                                                                         |
   +-------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------+

Configure NodeManager Restart as follows:

.. table:: **Table 2** Parameter description of NodeManager Restart

   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
   | Parameter                            | Description                                                                                                                                                                                       | Default Value                    |
   +======================================+===================================================================================================================================================================================================+==================================+
   | yarn.nodemanager.recovery.enabled    | Whether to enable the function of collecting logs upon a log collection failure when NodeManager is restarted and whether to restore the unfinished application                                   | true                             |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
   | yarn.nodemanager.recovery.dir        | Local directory used by NodeManager to store container status                                                                                                                                     | ${SRV_HOME}/tmp/yarn-nm-recovery |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
   | yarn.nodemanager.recovery.supervised | Whether NodeManager is monitored. After this parameter is enabled, NodeManager does not clear containers after exit. NodeManager assumes that it will restart and restore containers immediately. | true                             |
   +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+
