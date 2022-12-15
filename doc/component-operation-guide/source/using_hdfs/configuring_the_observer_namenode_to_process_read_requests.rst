:original_name: mrs_01_1681.html

.. _mrs_01_1681:

Configuring the Observer NameNode to Process Read Requests
==========================================================

Scenario
--------

In an HDFS cluster configured with HA, the active NameNode processes all client requests, and the standby NameNode reserves the latest metadata and block location information. However, in this architecture, the active NameNode is the bottleneck of client request processing. This bottleneck is more obvious in clusters with a large number of requests.

To address this issue, a new NameNode is introduced: an observer NameNode. Similar to the standby NameNode, the observer NameNode also reserves the latest metadata information and block location information. In addition, the observer NameNode can process read requests from clients in the same way as the active NameNode. In typical HDFS clusters with many read requests, the observer NameNode can be used to process read requests, reducing the active NameNode load and improving the cluster capability of processing requests.

.. note::

   This section applies to MRS 3.\ *x* or later.

Impact on the System
--------------------

-  The active NameNode load can be reduced and the capability of HDFS cluster processing requests can be improved, which is especially obvious for large clusters.
-  The client application configuration needs to be updated.

Prerequisites
-------------

-  The HDFS cluster has been installed, the active and standby NameNodes are running properly, and the HDFS service is normal.
-  The **${BIGDATA_DATA_HOME}/namenode** partition has been created on the node where the observer NameNode is to be installed.

Procedure
---------

The following steps describe how to configure the observer NameNode of a hacluster and enable it to process read requests. If there are multiple pairs of NameServices in the cluster and they are all in use, perform the following steps to configure the observer NameNode for each pair.

#. Log in to FusionInsight Manager.
#. Choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS** > **NameService Management**.
#. Click **Add** next to **hacluster**.
#. On the **Add NameNode** page, set **NameNode type** to **Observer** and click **Next**.
#. On the **Assign Role** page, select the planned host, add the observer NameNode, and click **Next**.

   .. note::

      A maximum of five observer NameNodes can be added to each pair of NameServices.

#. On the configuration page, configure the storage directory and port number of the NameNode as planned and click **Next**.
#. Confirm the information, click **Submit**, and wait until the installation of the observer NameNode is complete.

8. Restart the upper-layer components that depend on HDFS, update the client application configuration, and restart the client application.
