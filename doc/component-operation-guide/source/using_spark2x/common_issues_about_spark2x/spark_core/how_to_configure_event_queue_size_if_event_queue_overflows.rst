:original_name: mrs_01_2008.html

.. _mrs_01_2008:

How to Configure Event Queue Size If Event Queue Overflows?
===========================================================

Question
--------

How to configure the event queue size if the following Driver log information is displayed indicating that the event queue overflows?

-  Common applications

   .. code-block::

      Dropping SparkListenerEvent because no remaining room in event queue.
      This likely means one of the SparkListeners is too slow and cannot keep
      up with the rate at which tasks are being started by the scheduler.

-  Spark Streaming applications

   .. code-block::

      Dropping StreamingListenerEvent because no remaining room in event queue.
      This likely means one of the StreamingListeners is too slow and cannot keep
      up with the rate at which events are being started by the scheduler.

Answer
------

#. Stop the application. Set the configuration option **spark.event.listener.logEnable** in the Spark configuration file **spark-defaults.conf** to **true**. And set the configuration option **spark.eventQueue.size** to **1000W**. If you need to control the logging rate (in milliseconds), also change the value of the configuration option **spark.event.listener.logRate**.

   By default, the logging rate is 1000 ms, which means that one log is printed out every 1000 ms.

#. Start the application.

   The following log information is displayed, including the event consumption rate, event production rate, and **MaxSize** (maximum size of messages in the queue).

   .. code-block::

      INFO LiveListenerBus: [SparkListenerBus]:16044 events are consumed in 5000 ms.
      INFO LiveListenerBus: [SparkListenerBus]:51381 events are produced in 5000 ms, eventQueue still has 86417 events, MaxSize: 171764.

#. Change the value of the configuration option **spark.eventQueue.size** in the Spark configuration file **spark-defaults.conf** based on the **MaxSize** in the log information.

   For example, if **MaxSize** is 250000, the appropriate message queue size is 300000.
