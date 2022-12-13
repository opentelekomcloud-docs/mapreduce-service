:original_name: mrs_08_00346.html

.. _mrs_08_00346:

Job Pipeline
============

Enhanced Open Source Feature: Job Pipeline
------------------------------------------

Generally, logic code related to a service is stored in a large JAR package, which is called Fat JAR. Disadvantages of Fat JAR are as follows:

-  When service logic becomes more and more complex, the size of the Fat JAR increases.
-  Fat Jar makes coordination complex. Developers of all services are working with the same service logic. Even though the service logic can be divided into several modules, all modules are tightly coupled with each other. If the requirement needs to be changed, the entire flow diagram needs to be replanned.

Splitting of jobs is facing the following problems:

-  Data transmission between jobs can be achieved using Kafka. For example, job A transmits data to the topic A in Kafka, and then job B and job C read data from the topic A in Kafka. This solution is simple and easy to implement, but the latency is always longer than 100 ms.
-  Operators are connected using the TCP protocol. In distributed environment, operators can be scheduled to any node and upstream and downstream services cannot detect the scheduling.

**Job Pipeline**

A pipeline consists of multiple Flink jobs connected through TCP. Upstream jobs can send data to downstream jobs. The flow diagram about data transmission is called a job pipeline, as shown in :ref:`Figure 1 <mrs_08_00346__f9376509c971b4e4b99bd76fd4ce17b63>`.

.. _mrs_08_00346__f9376509c971b4e4b99bd76fd4ce17b63:

.. figure:: /_static/images/en-us_image_0000001349390637.png
   :alt: **Figure 1** Job pipeline

   **Figure 1** Job pipeline

**Job Pipeline Principles**


.. figure:: /_static/images/en-us_image_0000001349110473.png
   :alt: **Figure 2** Job pipeline principles

   **Figure 2** Job pipeline principles

-  NettySink and NettySource

   In a pipeline, upstream jobs and downstream jobs communicate with each other through Netty. The Sink operator of the upstream job works as a server and the Source operator of the downstream job works as a client. The Sink operator of the upstream job is called NettySink, and the Source operator of the downstream job is called NettySource.

-  NettyServer and NettyClient

   NettySink functions as the server of Netty. In NettySink, NettyServer achieves the function of a server. NettySource functions as the client of Netty. In NettySource, NettyClient achieves the function of a client.

-  Publisher

   The job that sends data to downstream jobs through NettySink is called a publisher.

-  Subscriber

   The job that receives data from upstream jobs through NettySource is called a subscriber.

-  RegisterServer

   RegisterServer is the third-party memory that stores the IP address, port number, and concurrency information about NettyServer.

-  The general outside-in architecture is as follows:

   -  NettySink->NettyServer->NettyServerHandler
   -  NettySource->NettyClient->NettyClientHandler

**Job Pipeline Functions**

-  **NettySink**

   NettySink consists of the following major modules:

   -  RichParallelSinkFunction

      NettySink inherits RichParallelSinkFunction and attributes of Sink operators. The RichParallelSinkFunction API implements following functions:

      -  Starts the NettySink operator.
      -  Runs the NettySink operator and receives data from the upstream operator.
      -  Cancels the running of NettySink operators.

      Following information can be obtained using the attribute of RichParallelSinkFunction:

      -  subtaskIndex about the concurrency of each NettySink operator.
      -  Concurrency of the NettySink operator.

   -  RegisterServerHandler

      RegisterServerHandler interacts with the component of RegisterServer and defines following APIs:

      -  **start();**: Starts the RegisterServerHandler and establishes a contact with the third-party RegisterServer.
      -  **createTopicNode();**: Creates a topic node.
      -  **register();**: Registers information such as the IP address, port number, and concurrency to the topic node.
      -  **deleteTopicNode();**: Deletes a topic node.
      -  **unregister();**: Deletes registration information.
      -  **query();**: Queries registration information.
      -  **isExist();**: Verifies that a specific piece of information exists.
      -  **shutdown();**: Disables the RegisterServerHandler and disconnects from the third-party RegisterServer.

      .. note::

         -  RegisterServerHandler API enables ZooKeeper to work as the handler of RegisterServer. You can customize your handler as required. Information is stored in ZooKeeper in the following form:

            .. code-block::

               Namespace
               |---Topic-1
                 |---parallel-1
                 |---parallel-2
                 |....
                 |---parallel-n
               |---Topic-2
                 |---parallel-1
                 |---parallel-2
                 |....
                 |---parallel-m
               |...

         -  Information about NameSpace can be obtained from the following parameters of the **flink-conf.yaml** file:

            .. code-block::

               nettyconnector.registerserver.topic.storage: /flink/nettyconnector

         -  The simple authentication and security layer (SASL) authentication between ZookeeperRegisterServerHandler and ZooKeeper is implemented through the Flink framework.

         -  Ensure that each job has a unique topic. Otherwise, the subscription relationship may be unclear.

         -  When calling **shutdown()**, ZookeeperRegisterServerHandler deletes the registration information about the current concurrency, and then attempts to delete the topic node. If the topic node is not empty, deletion will be canceled, because not all concurrency has exited.

   -  NettyServer

      NettyServer is the core of the NettySink operator, whose main function is to create a NettyServer and receive connection requests from NettyClient. Use NettyServerHandler to send data received from upstream operators of a same job. The port number and subnet of NettyServer needs to be configured in the **flink-conf.yaml** file.

      -  Port range

         .. code-block::

            nettyconnector.sinkserver.port.range: 28444-28943

      -  Subnet

         .. code-block::

            nettyconnector.sinkserver.subnet: 10.162.222.123/24

         .. note::

            The **nettyconnector.sinkserver.subnet** parameter is set to the subnet (service IP address) of the Flink client by default. If the client and TaskManager are not in the same subnet, an error may occur. Therefore, you need to manually set this parameter to the subnet (service IP address) of TaskManager.

   -  NettyServerHandler

      The handler enables the interaction between NettySink and subscribers. After NettySink receives messages, the handler sends these messages out. To ensure data transmission security, this channel is encrypted using SSL. The **nettyconnector.ssl.enabled** configures whether to enable SSL encryption. The SSL encryption is enabled only when **nettyconnector.ssl.enabled** is set to **true**.

-  **NettySource**

   NettySource consists of the following major modules:

   -  RichParallelSourceFunction

      NettySource inherits RichParallelSinkFunction and attributes of Source operators. The RichParallelSourceFunction API implements following functions:

      -  Starts the NettySink operator.
      -  Runs the NettySink operator, receives data from subscribers, and injects the data to jobs.
      -  Cancels the running of Source operators.

      Following information can be obtained using the attribute of RichParallelSourceFunction:

      -  subtaskIndex about the concurrency of each NettySource operator.
      -  Concurrency of the NettySource operator.

      When the NettySource operator enters the running stage, the NettyClient status is monitored. Once abnormality occurs, NettyClient is restarted and reconnected to NettyServer, preventing data confusion.

   -  RegisterServerHandler

      RegisterServerHandler of NettySource has similar function as the RegisterServerHandler of NettySink. It obtains the IP address, port number, and information of concurrent operators of each subscribed job obtained in the NettySource operator.

   -  NettyClient

      NettyClient establishes a connection with NettyServer and uses NettyClientHandler to receive data. Each NettySource operator must have a unique name (specified by the user). NettyServer determines whether each client comes from different NettySources based on unique names. When a connection is established between NettyClient and NettyServer, NettyClient is registered with NettyServer and the NettySource name of NettyClient is transferred to NettyServer.

   -  NettyClientHandler

      The NettyClientHandler enables the interaction with publishers and other operators of the job. When messages are received, NettyClientHandler transfers these messages to the job. To ensure secure data transmission, SSL encryption is enabled for the communication with NettySink. The SSL encryption is enabled only when SSL is enabled and **nettyconnector.ssl.enabled** is set to **true**.

The relationship between the jobs may be many-to-many. The concurrency between each NettySink and NettySource operator is one-to-many, as shown in :ref:`Figure 3 <mrs_08_00346__f06f4b6e5263b4e2780ee1688783def5f>`.

.. _mrs_08_00346__f06f4b6e5263b4e2780ee1688783def5f:

.. figure:: /_static/images/en-us_image_0000001349190345.png
   :alt: **Figure 3** Relationship diagram

   **Figure 3** Relationship diagram
