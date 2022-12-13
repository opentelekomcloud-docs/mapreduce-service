:original_name: mrs_08_00702.html

.. _mrs_08_00702:

Relationship Between ZooKeeper and Other Components
===================================================

Relationship Between ZooKeeper and HDFS
---------------------------------------

:ref:`Figure 1 <mrs_08_00702__f4e063184638a4990ada3505cd92cf4e6>` shows the relationship between ZooKeeper and HDFS.

.. _mrs_08_00702__f4e063184638a4990ada3505cd92cf4e6:

.. figure:: /_static/images/en-us_image_0000001349190409.png
   :alt: **Figure 1** Relationship between ZooKeeper and HDFS

   **Figure 1** Relationship between ZooKeeper and HDFS

As the client of a ZooKeeper cluster, ZKFailoverController (ZKFC) monitors the status of NameNode. ZKFC is deployed only in the node where NameNode resides, and in both the active and standby HDFS NameNodes.

#. The ZKFC connects to ZooKeeper and saves information such as host names to ZooKeeper under the znode directory **/hadoop-ha**. NameNode that creates the directory first is considered as the active node, and the other is the standby node. NameNodes read the NameNode information periodically through ZooKeeper.
#. When the process of the active node ends abnormally, the standby NameNode detects changes in the **/hadoop-ha** directory through ZooKeeper, and then takes over the service of the active NameNode.

Relationship Between ZooKeeper and YARN
---------------------------------------

:ref:`Figure 2 <mrs_08_00702__fde9fecb356f3437c94d75e7544ed0cc3>` shows the relationship between ZooKeeper and YARN.

.. _mrs_08_00702__fde9fecb356f3437c94d75e7544ed0cc3:

.. figure:: /_static/images/en-us_image_0000001296750310.png
   :alt: **Figure 2** Relationship Between ZooKeeper and YARN

   **Figure 2** Relationship Between ZooKeeper and YARN

#. When the system is started, ResourceManager attempts to write state information to ZooKeeper. ResourceManager that first writes state information to ZooKeeper is selected as the active ResourceManager, and others are standby ResourceManagers. The standby ResourceManagers periodically monitor active ResourceManager election information in ZooKeeper.
#. The active ResourceManager creates the **Statestore** directory in ZooKeeper to store application information. If the active ResourceManager is faulty, the standby ResourceManager obtains application information from the **Statestore** directory and restores the data.

Relationship Between ZooKeeper and HBase
----------------------------------------

:ref:`Figure 3 <mrs_08_00702__f2b849e3767fb4026b214c0d33566684d>` shows the relationship between ZooKeeper and HBase.

.. _mrs_08_00702__f2b849e3767fb4026b214c0d33566684d:

.. figure:: /_static/images/en-us_image_0000001349390705.png
   :alt: **Figure 3** Relationship between ZooKeeper and HBase

   **Figure 3** Relationship between ZooKeeper and HBase

#. HRegionServer registers itself to ZooKeeper on Ephemeral node. ZooKeeper stores the HBase information, including the HBase metadata and HMaster addresses.
#. HMaster detects the health status of each HRegionServer using ZooKeeper, and monitors them.
#. HBase supports multiple HMaster nodes (like HDFS NameNodes). When the active HMatser is faulty, the standby HMaster obtains the state information about the entire cluster using ZooKeeper. That is, using ZooKeeper can avoid HBase SPOFs.

Relationship Between ZooKeeper and Kafka
----------------------------------------

:ref:`Figure 4 <mrs_08_00702__fig17441129145312>` shows the relationship between ZooKeeper and Kafka.

.. _mrs_08_00702__fig17441129145312:

.. figure:: /_static/images/en-us_image_0000001296590694.png
   :alt: **Figure 4** Relationship between ZooKeeper and Kafka

   **Figure 4** Relationship between ZooKeeper and Kafka

#. Broker uses ZooKeeper to register broker information and elect a partition leader.
#. The consumer uses ZooKeeper to register consumer information, including the partition list of consumer. In addition, ZooKeeper is used to discover the broker list, establish a socket connection with the partition leader, and obtain messages.
