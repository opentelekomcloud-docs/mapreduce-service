:original_name: mrs_01_1670.html

.. _mrs_01_1670:

Configuring the NameNode Blacklist
==================================

Scenario
--------

.. note::

   This section applies to MRS 3.\ *x* or later.

In the existing default DFSclient failover proxy provider, if a NameNode in a process is faulty, all HDFS client instances in the same process attempt to connect to the NameNode again. As a result, the application waits for a long time and timeout occurs.

When clients in the same JVM process connect to the NameNode that cannot be accessed, the system is overloaded. The NameNode blacklist is equipped with the MRS cluster to avoid this problem.

In the new Blacklisting DFSClient failover provider, the faulty NameNode is recorded in a list. The DFSClient then uses the information to prevent the client from connecting to such NameNodes again. This function is called NameNode blacklisting.

For example, there is a cluster with the following configurations:

namenode: nn1, nn2

dfs.client.failover.connection.retries: 20

Processes in a single JVM: 10 clients

In the preceding cluster, if the active **nn1** cannot be accessed, client1 will retry the connection for 20 times. Then, a failover occurs, and client1 will connect to **nn2**. In the same way, other clients also connect to **nn2** when the failover occurs after retrying the connection to **nn1** for 20 times. Such process prolongs the fault recovery of NameNode.

In this case, the NameNode blacklisting adds **nn1** to the blacklist when client1 attempts to connect to the active **nn1** which is already faulty. Therefore, other clients will avoid trying to connect to **nn1** but choose **nn2** directly.

.. note::

   If, at any time, all NameNodes are added to the blacklist, the content in the blacklist will be cleared, and the client attempts to connect to the NameNodes based on the initial NameNode list. If any fault occurs again, the NameNode is still added to the blacklist.


.. figure:: /_static/images/en-us_image_0000001296090668.jpg
   :alt: **Figure 1** NameNode blacklisting working principle

   **Figure 1** NameNode blacklisting working principle

Configuration Description
-------------------------

Go to the **All Configurations** page of HDFS and enter a parameter name in the search box by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.

.. table:: **Table 1** NameNode blacklisting parameters

   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
   | Parameter                                               | Description                                                                                             | Default Value                                                           |
   +=========================================================+=========================================================================================================+=========================================================================+
   | dfs.client.failover.proxy.provider.\ *[nameservice ID]* | Client Failover proxy provider class which creates the NameNode proxy using the authenticated protocol. | org.apache.hadoop.hdfs.server.namenode.ha.AdaptiveFailoverProxyProvider |
   |                                                         |                                                                                                         |                                                                         |
   |                                                         | Set this parameter to **org.apache.hadoop.hdfs.server.namenode.ha.BlackListingFailoverProxyProvider**.  |                                                                         |
   |                                                         |                                                                                                         |                                                                         |
   |                                                         | You can configure the observer NameNode to process read requests.                                       |                                                                         |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------+
