:original_name: mrs_01_1044.html

.. _mrs_01_1044:

Kafka Performance Tuning
========================

Scenario
--------

You can modify Kafka server parameters to improve Kafka processing capabilities in specific service scenarios.

Parameter Tuning
----------------

Modify the service configuration parameters. For details, see :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`. For details about the tuning parameters, see :ref:`Table 1 <mrs_01_1044__en-us_topic_0000001173631108_td2ff03d5b464413597bebde9472f162f>`.

.. _mrs_01_1044__en-us_topic_0000001173631108_td2ff03d5b464413597bebde9472f162f:

.. table:: **Table 1** Tuning parameters

   +-----------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Default Value | Scenario                                                                                                                                                                                         |
   +===================================+===============+==================================================================================================================================================================================================+
   | num.recovery.threads.per.data.dir | 10            | During the Kafka startup process, if a large volume of data exists, you can increase the value of this parameter to accelerate the startup.                                                      |
   +-----------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | background.threads                | 10            | Specifies the number of threads processed by a broker background task. If a large volume of data exists, you can increase the value of this parameter to improve broker processing capabilities. |
   +-----------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | num.replica.fetchers              | 1             | Specifies the number of threads used when a replica requests to the Leader for data synchronization. If the value of this parameter is increased, the replica I/O concurrency increases.         |
   +-----------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | num.io.threads                    | 8             | Specifies the number of threads used by the broker to process disk I/O. It is recommended that the number of threads be greater than or equal to the number of disks.                            |
   +-----------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | KAFKA_HEAP_OPTS                   | -Xmx6G -Xms6G | Specifies the Kafka JVM heap memory setting. If the data volume on the broker is large, adjust the heap memory size.                                                                             |
   +-----------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
