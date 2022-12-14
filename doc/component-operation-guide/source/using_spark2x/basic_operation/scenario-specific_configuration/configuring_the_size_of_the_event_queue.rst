:original_name: mrs_01_1945.html

.. _mrs_01_1945:

Configuring the Size of the Event Queue
=======================================

Scenarios
---------

Functions such as UI, EventLog, and dynamic resource scheduling in Spark are implemented through event transfer. Events include SparkListenerJobStart and SparkListenerJobEnd, which record each important process.

Each event is saved to a queue after it occurs. When creating a SparkContext object, Driver starts a thread to obtain an event from the queue in sequence and sends the event to each Listener. Each Listener processes the event after detecting the event.

Therefore, when the queuing speed is faster than the read speed, the queue overflows. As a result, the overflow event is lost, affecting the UI, EventLog, and dynamic resource scheduling functions. Therefore, a configuration item is added for more flexible use. You can set a proper value based on the memory size of the driver.

Configuration Description
-------------------------

**Navigation path for setting parameters:**

Before executing an application, modify the Spark service configuration. On Manager, choose **Cluster > *Name of the desired cluster* > Service** > **Spark2x** > **Configuration** and click **All Configurations**. Enter a parameter name in the search box.

.. table:: **Table 1** Parameter description

   +-------------------------------------------------+----------------------------------------------------------------------------------------------------+---------------+
   | Parameter                                       | Description                                                                                        | Default Value |
   +=================================================+====================================================================================================+===============+
   | spark.scheduler.listenerbus.eventqueue.capacity | Specifies the size of the event queue. Configure this parameter based on the memory of the driver. | 1000000       |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------+---------------+

.. note::

   If the following information is displayed in the Driver log, the queue overflows.

   #. Common application:

      .. code-block::

         Dropping SparkListenerEvent because no remaining room in event queue.
         This likely means one of the SparkListeners is too slow and cannot keep
         up with the rate at which tasks are being started by the scheduler.

   #. Spark Streaming application:

      .. code-block::

         Dropping StreamingListenerEvent because no remaining room in event queue.
         This likely means one of the StreamingListeners is too slow and cannot keep
         up with the rate at which events are being started by the scheduler.
