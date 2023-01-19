:original_name: mrs_01_1567.html

.. _mrs_01_1567:

Blob
====

Scenarios
---------

The Blob server on the JobManager node is used to receive JAR files uploaded by users on the client, send JAR files to TaskManager, and transfer log files. Flink provides some items for configuring the Blob server. You can configure them in the **flink-conf.yaml** configuration file.

Configuration Description
-------------------------

Users can configure the port, SSL, retry times, and concurrency.

.. table:: **Table 1** Parameters

   +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------+-----------+
   | Parameter                              | Description                                                                                                                                                    | Default Value  | Mandatory |
   +========================================+================================================================================================================================================================+================+===========+
   | blob.server.port                       | Blob server port                                                                                                                                               | 32456 to 32520 | No        |
   +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------+-----------+
   | blob.service.ssl.enabled               | Indicates whether to enable the encryption for the blob transmission channel. This parameter is valid only when the global switch **security.ssl** is enabled. | true           | Yes       |
   +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------+-----------+
   | blob.fetch.retries                     | Number of times that TaskManager tries to download blob files from JobManager.                                                                                 | 50             | No        |
   +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------+-----------+
   | blob.fetch.num-concurrent              | Number of concurrent tasks for downloading blob files supported by JobManager.                                                                                 | 50             | No        |
   +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------+-----------+
   | blob.fetch.backlog                     | Number of blob files, such as **.jar** files, to be downloaded in the queue supported by JobManager. The unit is count.                                        | 1000           | No        |
   +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------+-----------+
   | library-cache-manager.cleanup.interval | Interval at which JobManager deletes the JAR files stored on the HDFS when the user cancels the Flink job. The unit is second.                                 | 3600           | No        |
   +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------+-----------+
