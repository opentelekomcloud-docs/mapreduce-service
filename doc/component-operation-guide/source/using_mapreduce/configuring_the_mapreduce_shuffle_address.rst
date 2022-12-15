:original_name: mrs_01_0840.html

.. _mrs_01_0840:

Configuring the MapReduce Shuffle Address
=========================================

Scenario
--------

When the MapReduce shuffle service is started, it attempts to bind an IP address based on local host. If the MapReduce shuffle service is required to connect to a specific IP address, no configuration is available. The following description allows you to configure a connection to a specific IP address.

Configuration
-------------

To bind a specific IP address to the MapReduce shuffle service, set the following parameters in the **mapred-site.xml** configuration file of the node where the NodeManager instance resides:

.. table:: **Table 1** Parameter description

   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter                 | Description                                                                                                                                                                                                             | Default Value         |
   +===========================+=========================================================================================================================================================================================================================+=======================+
   | mapreduce.shuffle.address | Indicates the specified address to run the shuffle service. The format is *IP:PORT*. The default value is empty. If this parameter is left empty, the local host IP address is bound. The default port number is 13562. | ``-``                 |
   |                           |                                                                                                                                                                                                                         |                       |
   |                           | .. note::                                                                                                                                                                                                               |                       |
   |                           |                                                                                                                                                                                                                         |                       |
   |                           |    If the value of *PORT* is different from that of **mapreduce.shuffle.port**, the **mapreduce.shuffle.port** value does not take effect.                                                                              |                       |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
