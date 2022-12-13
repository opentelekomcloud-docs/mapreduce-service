:original_name: mrs_08_00513.html

.. _mrs_08_00513:

Relationship Between YARN and Other Components
==============================================

Relationship Between YARN and Spark
-----------------------------------

The Spark computing and scheduling can be implemented using YARN mode. Spark enjoys the compute resources provided by YARN clusters and runs tasks in a distributed way. Spark on YARN has two modes: YARN-cluster and YARN-client.

-  YARN Cluster mode

   :ref:`Figure 1 <mrs_08_00513__f4a05be79f46946c490c811dadbff1ab5>` describes the operation framework.

   .. _mrs_08_00513__f4a05be79f46946c490c811dadbff1ab5:

   .. figure:: /_static/images/en-us_image_0000001349110449.png
      :alt: **Figure 1** Spark on YARN-cluster operation framework

      **Figure 1** Spark on YARN-cluster operation framework

   Spark on YARN-cluster implementation process:

   #. The client generates the application information, and then sends the information to ResourceManager.

   #. ResourceManager allocates the first container (ApplicationMaster) to SparkApplication and starts the driver on the container.

   #. ApplicationMaster applies for resources from ResourceManager to run the container.

      ResourceManager allocates the containers to ApplicationMaster, which communicates with the related NodeManagers and starts the executor in the obtained container. After the executor is started, it registers with drivers and applies for tasks.

   #. Drivers allocate tasks to the executors.

   #. Executors run tasks and report the operating status to Drivers.

-  YARN Client mode

   :ref:`Figure 2 <mrs_08_00513__f262883214bcd497c9b530206e64b0395>` describes the operation framework.

   .. _mrs_08_00513__f262883214bcd497c9b530206e64b0395:

   .. figure:: /_static/images/en-us_image_0000001296750218.png
      :alt: **Figure 2** Spark on YARN-client operation framework

      **Figure 2** Spark on YARN-client operation framework

   Spark on YARN-client implementation process:

   .. note::

      In YARN-client mode, the driver is deployed and started on the client. In YARN-client mode, the client of an earlier version is incompatible. You are advised to use the YARN-cluster mode.

   #. The client sends the Spark application request to ResourceManager, then ResourceManager returns the results. The results include information such as Application ID and the maximum and minimum available resources. The client packages all information required to start ApplicationMaster, and sends the information to ResourceManager.

   #. After receiving the request, ResourceManager finds a proper node for ApplicationMaster and starts it on this node. ApplicationMaster is a role in YARN, and the process name in Spark is ExecutorLauncher.

   #. Based on the resource requirements of each task, ApplicationMaster can apply for a series of containers to run tasks from ResourceManager.

   #. After receiving the newly allocated container list (from ResourceManager), ApplicationMaster sends information to the related NodeManagers to start the containers.

      ResourceManager allocates the containers to ApplicationMaster, which communicates with the related NodeManagers and starts the executor in the obtained container. After the executor is started, it registers with drivers and applies for tasks.

      .. note::

         Running containers are not suspended and resources are not released.

   #. Drivers allocate tasks to the executors. Executors run tasks and report the operating status to Drivers.

Relationship Between YARN and MapReduce
---------------------------------------

MapReduce is a computing framework running on YARN, which is used for batch processing. MRv1 is implemented based on MapReduce in Hadoop 1.0, which is composed of programming models (new and old programming APIs), running environment (JobTracker and TaskTracker), and data processing engine (MapTask and ReduceTask). This framework is still weak in scalability, fault tolerance (JobTracker SPOF), and compatibility with multiple frameworks. (Currently, only the MapReduce computing framework is supported.) MRv2 is implemented based on MapReduce in Hadoop 2.0. The source code reuses MRv1 programming models and data processing engine implementation, and the running environment is composed of ResourceManager and ApplicationMaster. ResourceManager is a brand new resource manager system, and ApplicationMaster is responsible for cutting MapReduce job data, assigning tasks, applying for resources, scheduling tasks, and tolerating faults.

Relationship Between YARN and ZooKeeper
---------------------------------------

:ref:`Figure 3 <mrs_08_00513__fdf7cc662abc147c6b9ea58bc752662cd>` shows the relationship between ZooKeeper and YARN.

.. _mrs_08_00513__fdf7cc662abc147c6b9ea58bc752662cd:

.. figure:: /_static/images/en-us_image_0000001349309905.png
   :alt: **Figure 3** Relationship Between ZooKeeper and YARN

   **Figure 3** Relationship Between ZooKeeper and YARN

#. When the system is started, ResourceManager attempts to write state information to ZooKeeper. ResourceManager that first writes state information to ZooKeeper is selected as the active ResourceManager, and others are standby ResourceManagers. The standby ResourceManagers periodically monitor active ResourceManager election information in ZooKeeper.
#. The active ResourceManager creates the **Statestore** directory in ZooKeeper to store application information. If the active ResourceManager is faulty, the standby ResourceManager obtains application information from the **Statestore** directory and restores the data.

Relationship Between YARN and Tez
---------------------------------

The Hive on Tez job information requires the TimeLine Server capability of YARN so that Hive tasks can display the current and historical status of applications, facilitating storage and retrieval.
