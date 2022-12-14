:original_name: mrs_01_2031.html

.. _mrs_01_2031:

Why Does 16 Terabytes of Text Data Fails to Be Converted into 4 Terabytes of Parquet Data?
==========================================================================================

Question
--------

When the default configuration is used, 16 terabytes of text data fails to be converted into 4 terabytes of parquet data, and the error information below is displayed. Why?

.. code-block::

   Job aborted due to stage failure: Task 2866 in stage 11.0 failed 4 times, most recent failure: Lost task 2866.6 in stage 11.0 (TID 54863, linux-161, 2): java.io.IOException: Failed to connect to /10.16.1.11:23124
   at org.apache.spark.network.client.TransportClientFactory.createClient(TransportClientFactory.java:214)
   at org.apache.spark.network.client.TransportClientFactory.createClient(TransportClientFactory.java:167)
   at org.apache.spark.network.netty.NettyBlockTransferService$$anon$1.createAndStart(NettyBlockTransferService.scala:92)

:ref:`Table 1 <mrs_01_2031__t11c6ce9d45ea4d69a81893e1f90f35cc>` lists the default configuration.

.. _mrs_01_2031__t11c6ce9d45ea4d69a81893e1f90f35cc:

.. table:: **Table 1** Parameter Description

   +------------------------------------+---------------------------------------------------------------------------------------------+---------------+
   | Parameter                          | Description                                                                                 | Default Value |
   +====================================+=============================================================================================+===============+
   | spark.sql.shuffle.partitions       | Number of shuffle data blocks during the shuffle operation.                                 | 200           |
   +------------------------------------+---------------------------------------------------------------------------------------------+---------------+
   | spark.shuffle.sasl.timeout         | Timeout interval of SASL authentication for the shuffle operation. Unit: second             | 120s          |
   +------------------------------------+---------------------------------------------------------------------------------------------+---------------+
   | spark.shuffle.io.connectionTimeout | Timeout interval for connecting to a remote node during the shuffle operation. Unit: second | 120s          |
   +------------------------------------+---------------------------------------------------------------------------------------------+---------------+
   | spark.network.timeout              | Timeout interval for all network connection operations. Unit: second                        | 360s          |
   +------------------------------------+---------------------------------------------------------------------------------------------+---------------+

Answer
------

The current data volume is 16 TB, but the number of partitions is only 200. As a result, each task is overloaded and the preceding problem occurs.

To solve the preceding problem, you need to adjust the parameters.

-  Increase the number of partitions to divide the task into smaller ones.
-  Increase the timeout interval during task execution.

Configure the following parameters in the **spark-defaults.conf** file on the client:

.. table:: **Table 2** Parameter Description

   +------------------------------------+---------------------------------------------------------------------------------------------+-------------------+
   | Parameter                          | Description                                                                                 | Recommended Value |
   +====================================+=============================================================================================+===================+
   | spark.sql.shuffle.partitions       | Number of shuffle data blocks during the shuffle operation.                                 | 4501              |
   +------------------------------------+---------------------------------------------------------------------------------------------+-------------------+
   | spark.shuffle.sasl.timeout         | Timeout interval of SASL authentication for the shuffle operation. Unit: second             | 2000s             |
   +------------------------------------+---------------------------------------------------------------------------------------------+-------------------+
   | spark.shuffle.io.connectionTimeout | Timeout interval for connecting to a remote node during the shuffle operation. Unit: second | 3000s             |
   +------------------------------------+---------------------------------------------------------------------------------------------+-------------------+
   | spark.network.timeout              | Timeout interval for all network connection operations. Unit: second                        | 360s              |
   +------------------------------------+---------------------------------------------------------------------------------------------+-------------------+
