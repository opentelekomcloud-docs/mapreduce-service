:original_name: mrs_01_2098.html

.. _mrs_01_2098:

Configuring the ZooKeeper Connection
====================================

Scenarios
---------

ZooKeeper has maxClientCnxn configuration at the server side, and this configuration will verify the connections from each client IP address. But many clients can create countless unnecessary connections and consume all resources of ZooKeeper during the denial-of-service (DOS) attack. This makes other clients fail to create legitimate connections or even triggers the server breakdown.

To limit the maximum number of connections to a single ZooKeeper server, all ZooKeeper servers introduce a new configuration to check the total number of active connections before accepting any new connection requests.


.. figure:: /_static/images/en-us_image_0000001349059825.png
   :alt: **Figure 1** Connection control logic

   **Figure 1** Connection control logic

Configuration Description
-------------------------

Go to the **All Configurations** page of ZooKeeper by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`. Enter a parameter name in the search box. Configure **maxClientCnxn** and **maxCnxns** to limit the maximum number of connections on each host and the total number of connections on the ZooKeeper server.

.. table:: **Table 1** Connection policy parameters

   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                                                            | Default Value         |
   +=======================+========================================================================================================================================+=======================+
   | maxClientCnxns        | Limits the number of client connections to a ZooKeeper server in the ZooKeeper cluster. Clients are distinguished by IP address.       | 2000                  |
   |                       |                                                                                                                                        |                       |
   |                       | The configuration is the same as that in the open source version.                                                                      |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | maxCnxns              | Specifies the maximum number of client connections allowed by a single ZooKeeper server. Clients are not differentiated by IP address. | 20000                 |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

.. note::

   The ZooKeeper connection control function is based on IP addresses instead of specific users. If all connections of an IP address are occupied by few services, other mandatory services from the same IP address may fail to connect to the ZooKeeper. Therefore, ensure that only trusted applications are allowed to connect to ZooKeeper and the maximum number of connections is configured accordingly.
