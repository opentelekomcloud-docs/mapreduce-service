:original_name: mrs_01_0811.html

.. _mrs_01_0811:

Reducing the Probability of Abnormal Client Application Operation When the Network Is Not Stable
================================================================================================

Scenario
--------

Clients probably encounter running errors when the network is not stable. Users can adjust the following parameter values to improve the running efficiency.

Configuration Description
-------------------------

Go to the **All Configurations** page of HDFS and enter a parameter name in the search box by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.

.. table:: **Table 1** Parameter description

   +--------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter                                  | Description                                                                                                                                                                                           | Default Value         |
   +============================================+=======================================================================================================================================================================================================+=======================+
   | ha.health-monitor.rpc-timeout.ms           | Timeout interval during the NameNode health check performed by ZKFC. Increasing this value can prevent dual active NameNodes and reduce the probability of application running exceptions on clients. | 180,000               |
   |                                            |                                                                                                                                                                                                       |                       |
   |                                            | Unit: millisecond. Value range: 30,000 to 3,600,000                                                                                                                                                   |                       |
   +--------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | ipc.client.connect.max.retries.on.timeouts | Number of retry times when the socket connection between a server and a client times out.                                                                                                             | 45                    |
   |                                            |                                                                                                                                                                                                       |                       |
   |                                            | Value range: 1 to 256                                                                                                                                                                                 |                       |
   +--------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | ipc.client.connect.timeout                 | Timeout interval of the socket connection between a client and a server. Increasing the value of this parameter increases the timeout interval for setting up a connection.                           | 20,000                |
   |                                            |                                                                                                                                                                                                       |                       |
   |                                            | Unit: millisecond. Value range: 1 to 3,600,000                                                                                                                                                        |                       |
   +--------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
