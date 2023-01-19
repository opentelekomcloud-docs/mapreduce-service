:original_name: mrs_01_1672.html

.. _mrs_01_1672:

Optimizing HDFS NameNode RPC QoS
================================

Scenarios
---------

Several finished Hadoop clusters are faulty because the NameNode is overloaded and unresponsive.

Such problem is caused by the initial design of Hadoop: In Hadoop, the NameNode functions as an independent part and in its namespace coordinates various HDFS operations, including obtaining the data block location, listing directories, and creating files. The NameNode receives HDFS operations, regards them as RPC calls, and places them in the FIFO call queue for read threads to process. Requests in FIFO call queue are served first-in first-out. However, users who perform more I/O operations are served more time than those performing fewer I/O operations. In this case, the FIFO is unfair and causes the delay.


.. figure:: /_static/images/en-us_image_0000001295740212.png
   :alt: **Figure 1** NameNode request processing based on the FIFO call queue

   **Figure 1** NameNode request processing based on the FIFO call queue

The unfair problem and delaying mentioned before can be improved by replacing the FIFO queue with a new type of queue called FairCallQueue. In this way, FAIR queues assign incoming RPC calls to multiple queues based on the scale of the caller's call. The scheduling module tracks the latest calls and assigns a higher priority to users with a smaller number of calls.


.. figure:: /_static/images/en-us_image_0000001296060016.png
   :alt: **Figure 2** NameNode request processing based on FAIRCallQueue

   **Figure 2** NameNode request processing based on FAIRCallQueue

Configuration Description
-------------------------

-  FairCallQueue ensures quality of service (QoS) by internally adjusting the order in which RPCs are invoked.

   This queue consists of the following parts:

   #. DecayRpcScheduler: used to provide priority values from 0 to N (the value 0 indicates the highest priority).
   #. Multi-level queues (located in the FairCallQueue): used to ensure that queues are invoked in order of priority.
   #. Multi-channel converters (provided with Weighted Round Robin Multiplexer): used to provide logic control for queue selection.

   After the FairCallQueue is configured, the control module determines the sub-queue to which the received invoking is allocated. The current scheduling module is DecayRpcScheduler, which only continuously tracks the priority numbers of various calls and periodically reduces these numbers.

   Go to the **All Configurations** page of HDFS and enter a parameter name in the search box by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.

   .. table:: **Table 1** FairCallQueue parameters

      +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
      | Parameter                     | Description                                                                                                                              | Default Value                            |
      +===============================+==========================================================================================================================================+==========================================+
      | ipc.\ *<port>*.callqueue.impl | Specifies the queue implementation class. You need to run the **org.apache.hadoop.ipc.FairCallQueue** command to enable the QoS feature. | java.util.concurrent.LinkedBlockingQueue |
      +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+

-  RPC BackOff

   Backoff is one of the FairCallQueue functions. It requires the client to retry operations (such as creating, deleting, and opening a file) after a period of time. When the backoff occurs, the RCP server throws RetriableException. The FairCallQueue performs backoff in either of the following cases:

   -  The queue is full, that is, there are many client calls in the queue.
   -  The queue response time is longer than the threshold time (specified by the **ipc.<port>.decay-scheduler.backoff.responsetime.thresholds** parameter).

   .. table:: **Table 2** RPC Backoff configuration

      +----------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------+
      | Parameter                                                      | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Default Value           |
      +================================================================+==============================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+=========================+
      | ipc.\ *<port>*.backoff.enable                                  | Specifies whether to enable the backoff. When the current application contains a large number of user callings, the RPC request is blocked if the connection limit of the operating system is not reached. Alternatively, when the RPC or NameNode is heavily loaded, some explicit exceptions can be thrown back to the client based on certain policies. The client can understand these exceptions and perform exponential rollback, which is another implementation of the RetryInvocationHandler class. | false                   |
      +----------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------+
      | ipc.\ *<port>*.decay-scheduler.backoff.responsetime.enable     | Indicate whether to enable the backoff based on the average queue response time.                                                                                                                                                                                                                                                                                                                                                                                                                             | false                   |
      +----------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------+
      | ipc.\ *<port>*.decay-scheduler.backoff.responsetime.thresholds | Configure the response time threshold for each queue. The response time threshold must match the number of priorities (the value of **ipc.<port> .faircallqueue.priority-levels**). Unit: millisecond                                                                                                                                                                                                                                                                                                        | 10000,20000,30000,40000 |
      +----------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------+

.. note::

   -  **<port>** indicates the RPC port configured on the NameNode.
   -  The backoff function based on the response time takes effect only when **ipc.<port> .backoff.enable** is set to **true**.
