:original_name: mrs_01_2099.html

.. _mrs_01_2099:

Configuring ZooKeeper Response Timeout Interval
===============================================

Scenarios
---------

The ZooKeeper client uses the FIFO queue to send a request to the server and waits for a response from the server. The client maintains the FIFO queue until it acknowledges the server's response to the request. The client waits indefinitely before acknowledging the response from the server. If the client cannot receive a response due to a server or network fault, the client enters the suspended state. Therefore, to avoid infinite waiting time, the client needs to associate with the ACK response timeout.


.. figure:: /_static/images/en-us_image_0000001296219696.png
   :alt: **Figure 1** Request timeout logic

   **Figure 1** Request timeout logic

Configuration Description
-------------------------

Change the value of **zookeeper.request.timeout** based on the network latency. If the packet loss duration is greater than the default value **120000 ms**, set this parameter to a larger value. To set **zookeeper.request.timeout** to *X*, set **Dzookeeper.request.timeout** to *X* when starting the ZooKeeper client.

.. table:: **Table 1** Response timeout duration parameters

   +---------------------------+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | Parameter                 | System Parameter          | Description                                                                                                                                                                                                          | Default Value |
   +===========================+===========================+======================================================================================================================================================================================================================+===============+
   | zookeeper.request.timeout | zookeeper.request.timeout | If no response is received from the server within the configured time, terminate the request that is not responded with **org.apache.zookeeper.KeeperException.ConnectionLossException** and exit. Unit: millisecond | 120000        |
   +---------------------------+---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+

Procedure
---------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to switch to the client installation directory:

   **cd** **/opt/client**

#. Run the following command to edit the **component_env** file:

   **vi ZooKeeper/component_env**

   Change the value of **zookeeper.request.timeout**.

   .. code-block::

      -Dzookeeper.request.timeout=120000

#. Run the **:wq** command to save execution.

#. Restart the client for the settings to take effect.
