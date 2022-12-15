:original_name: mrs_08_00141.html

.. _mrs_08_00141:

Storm Basic Principles
======================

Apache Storm is a distributed, reliable, and fault-tolerant real-time stream data processing system. In Storm, a graph-shaped data structure called topology needs to be designed first for real-time computing. The topology will be submitted to a cluster. Then a master node in the cluster distributes codes and assigns tasks to worker nodes. A topology contains two roles: spout and bolt. A spout sends messages and sends data streams in tuples. A bolt converts the data streams and performs computing and filtering operations. The bolt can randomly send data to other bolts. Tuples sent by a spout are unchangeable arrays and map to fixed key-value pairs.


.. figure:: /_static/images/en-us_image_0000001296750294.png
   :alt: **Figure 1** System architecture of Storm

   **Figure 1** System architecture of Storm

Service processing logic is encapsulated in the topology of Storm. A topology is a set of spout (data sources) and bolt (logical processing) components that are connected using Stream Groupings in DAG mode. All components (spout and bolt) in a topology are working in parallel. In a topology, you can specify the parallelism for each node. Then, Storm allocates tasks in the cluster for computing to improve system processing capabilities.


.. figure:: /_static/images/en-us_image_0000001296270862.png
   :alt: **Figure 2** Topology

   **Figure 2** Topology

Storm is applicable to real-time analysis, continuous computing, and distributed extract, transform, and load (ETL). It has the following advantages:

-  Wide applications
-  High scalability
-  Zero data loss
-  High fault tolerance
-  Easy to construct and control
-  Multi-language support

Storm is a computing platform and provides Continuous Query Language (CQL) in the service layer to facilitate service implementation. CQL has the following features:

-  Easy to use: The CQL syntax is similar to the SQL syntax. Users who have basic knowledge of SQL can easily learn CQL and use it to develop services.
-  Rich functions: In addition to basic expressions provided by SQL, CQL provides functions, such as windows, filtering, and concurrency setting, for stream processing.
-  Easy to scale: CQL provides an extension API to support increasingly complex service scenarios. Users can customize the input, output, serialization, and deserialization to meet specific service requirements.
-  Easy to debug: CQL provides detailed explanation of error codes, facilitating users to rectify faults.

For details about Storm architecture and principles, see https://storm.apache.org/.

Principle
---------

-  **Basic Concepts**

   .. table:: **Table 1** Concepts

      +------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Concept          | Description                                                                                                                                                                                                                                                                                                                                                                                                |
      +==================+============================================================================================================================================================================================================================================================================================================================================================================================================+
      | Tuple            | A tuple is an invariable key-value pair used to transfer data. Tuples are created and processed in distributed manner.                                                                                                                                                                                                                                                                                     |
      +------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Stream           | A stream is an unbounded sequence of tuples.                                                                                                                                                                                                                                                                                                                                                               |
      +------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Topology         | A topology is a real-time application running on the Storm platform. It is a Directed Acyclic Graph (DAG) composed of components. A topology can concurrently run on multiple machines. Each machine runs a part of the DAG. A topology is similar to a MapReduce job. The difference is that the topology is a resident program. Once started, the topology cannot stop unless it is manually terminated. |
      +------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Spout            | A spout is the source of tuples. For example, a spout may read data from a message queue, database, file system, or TCP connection and converts them as tuples, which are processed by the next component.                                                                                                                                                                                                 |
      +------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Bolt             | In a Topology, a bolt is a component that receives data and executes specific logic, such as filtering or converting tuples, joining or aggregating streams, and performing statistics and result persistence.                                                                                                                                                                                             |
      +------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Worker           | A Worker is a physical processing in running state in a Topology. Each Worker is a JVM process. Each Topology may be executed by multiple Workers. Each Worker executes a logic subset of the Topology.                                                                                                                                                                                                    |
      +------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Task             | A task is a spout or bolt thread of a Worker.                                                                                                                                                                                                                                                                                                                                                              |
      +------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Stream groupings | A stream grouping specifies the tuple dispatching policies. It instructs the subsequent bolt how to receive tuples. The supported policies include Shuffle Grouping, Fields Grouping, All Grouping, Global Grouping, Non Grouping, and Directed Grouping.                                                                                                                                                  |
      +------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   :ref:`Figure 3 <mrs_08_00141__fig_topo>` shows a Topology (DAG) consisting of a Spout and Bolt. In the figure, a rectangle indicates a Spout or Bolt, the node in each rectangle indicate tasks, and the lines between tasks indicate streams.

   .. _mrs_08_00141__fig_topo:

   .. figure:: /_static/images/en-us_image_0000001349110525.png
      :alt: **Figure 3** Topology

      **Figure 3** Topology

-  **Reliability**

   Storm provides three levels of data reliability:

   -  At Most Once: The processed data may be lost, but it cannot be processed repeatedly. This reliability level offers the highest throughput.
   -  At Least Once: Data may be processed repeatedly to ensure reliable data transmission. If a response is not received within the specified time, the Spout resends the data to Bolts for processing. This reliability level may slightly affect system performance.
   -  Exactly Once: Data is successfully transmitted without loss or redundancy processing. This reliability level delivers the poorest performance.

   Select the reliability level based on service requirements. For example, for the services requiring high data reliability, use Exactly Once to ensure that data is processed only once. For the services insensitive to data loss, use other levels to improve system performance.

-  **Fault Tolerance**

   Storm is a fault-tolerant system that offers high availability. :ref:`Table 2 <mrs_08_00141__table_04>` describes the fault tolerance of the Storm components.

   .. _mrs_08_00141__table_04:

   .. table:: **Table 2** Fault tolerance

      +-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Scenario          | Description                                                                                                                                                                                                                                                      |
      +===================+==================================================================================================================================================================================================================================================================+
      | Nimbus failed     | Nimbus is fail-fast and stateless. If the active Nimbus is faulty, the standby Nimbus takes over services immediately, and provide external services.                                                                                                            |
      +-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Supervisor failed | Supervisor is a background daemon of Workers. It is fail-fast and stateless. If a Supervisor is faulty, the Workers running on the node are not affected but cannot receive new tasks. The OMS can detect the fault of the Supervisor and restart the processes. |
      +-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Worker failed     | If a Worker is faulty, the Supervisor on the Worker will restart it again. If the restart fails for multiple times, Nimbus reassigns tasks to other nodes.                                                                                                       |
      +-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Node failed       | If a node is faulty, all the tasks being processed by the node time out and Nimbus will assign the tasks to another node for processing.                                                                                                                         |
      +-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Open Source Features
--------------------

-  Distributed real-time computing

   In a Storm cluster, each machine supports the running of multiple work processes and each work process can create multiple threads. Each thread can execute multiple tasks. A task indicates concurrent data processing.

-  High fault tolerance

   During message processing, if a node or a process is faulty, the message processing unit can be redeployed.

-  Reliable messages

   Data processing methods including At-Least Once, At-Most Once, and Exactly Once are supported.

-  Security mechanism

   Storm provides Kerberos-based authentication and pluggable authorization mechanisms, supports SSL Storm UI and Log Viewer UI, and supports security integration with other big data platform components (such as ZooKeeper and HDFS).

-  Flexible topology defining and deployment

   The Flux framework is used to define and deploy service topologies. If the service DAG is changed, users only need to modify YAML domain specific language (DSL), but do not need to recompile or package service code.

-  Integration with external components

   Storm supports integration with multiple external components such as Kafka, HDFS, HBase, Redis, and JDBC/RDBMS, implementing services that involve multiple data sources.
