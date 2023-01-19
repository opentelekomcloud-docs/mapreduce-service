:original_name: mrs_01_2009.html

.. _mrs_01_2009:

What Can I Do If the getApplicationReport Exception Is Recorded in Logs During Spark Application Execution and the Application Does Not Exit for a Long Time?
=============================================================================================================================================================

Question
--------

During Spark application execution, if the driver fails to connect to ResourceManager, the following error is reported and it does not exit for a long time. What can I do?

.. code-block::

   16/04/23 15:31:44 INFO RetryInvocationHandler: Exception while invoking getApplicationReport of class ApplicationClientProtocolPBClientImpl over 37 after 1 fail over attempts. Trying to fail over after sleeping for 44160ms.
   java.net.ConnectException: Call From vm1/192.168.39.30 to vm1:8032 failed on connection exception: java.net.ConnectException: Connection refused; For more details see:  http://wiki.apache.org/hadoop/ConnectionRefused

Answer
------

In Spark, there is a scheduled thread that listens to the status of ApplicationMaster by connecting to ResourceManager. The connection to the ResourceManager times out. As a result, the preceding error is reported and the system keeps trying to connect to the ResourceManager. In the ResourceManager, the number of retry times is limited. By default, the number of retry times is 30 and the retry interval is about 30 seconds. The preceding error is reported during each retry. The driver exits only after the number of times is exceeded.

:ref:`Table 1 <mrs_01_2009__en-us_topic_0000001219351265_t76cbd5573d354cb7846083dd9e85be25>` describes the retry-related configuration items in the ResourceManager.

.. _mrs_01_2009__en-us_topic_0000001219351265_t76cbd5573d354cb7846083dd9e85be25:

.. table:: **Table 1** Parameter description

   +------------------------------------------------+-------------------------------------------------------------+---------------+
   | Parameter                                      | Description                                                 | Default Value |
   +================================================+=============================================================+===============+
   | yarn.resourcemanager.connect.max-wait.ms       | Maximum waiting time for connecting to the ResourceManager. | 900000        |
   +------------------------------------------------+-------------------------------------------------------------+---------------+
   | yarn.resourcemanager.connect.retry-interval.ms | Interval for reconnecting to the ResourceManager.           | 30000         |
   +------------------------------------------------+-------------------------------------------------------------+---------------+

Number of retries (**yarn.resourcemanager.connect.max-wait.ms/yarn.resourcemanager.connect.retry-interval.ms**) = Maximum waiting time for connecting to the ResourceManager/Interval for reconnecting to the ResourceManager

On the Spark client, modify the **conf/yarn-site.xml** file to add and configure **yarn.resourcemanager.connect.max-wait.ms** and **yarn.resourcemanager.connect.retry-interval.ms**. In this way, the number of retry times can be changed, and the Spark application can exit in advance.
