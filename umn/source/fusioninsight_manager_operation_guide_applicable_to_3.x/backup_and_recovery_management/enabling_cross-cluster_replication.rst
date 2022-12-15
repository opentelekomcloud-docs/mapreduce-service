:original_name: admin_guide_000200.html

.. _admin_guide_000200:

Enabling Cross-Cluster Replication
==================================

Scenario
--------

DistCp is used to replicate the data stored in HDFS from a cluster to another cluster. DistCp depends on the cross-cluster replication function, which is disabled by default. You need to enable it for both clusters.

This section describes how to modify parameters on FusionInsight Manager to enable the cross-cluster replication function. After this function is enabled, you can create a backup task for backing up data to the remote HDFS (RemoteHDFS).

Impact on the System
--------------------

Yarn needs to be restarted to enable the cross-cluster replication function and cannot be accessed during restart.

Prerequisites
-------------

-  The **hadoop.rpc.protection** parameter of HDFS in the two clusters for data replication must use the same data transmission mode. The default value is **privacy**, indicating encrypted transmission. The value **authentication** indicates that transmission is not encrypted.
-  For clusters in security mode, you need to configure mutual trust between clusters.

Procedure
---------

#. Log in to FusionInsight Manager of one of the two clusters.

#. .. _admin_guide_000200__en-us_topic_0046736761_li45131484:

   Choose **Cluster** > ****Name of the desired cluster** > Services** > **Yarn** > **Configurations**, and click **All Configurations**.

#. In the navigation pane, choose **Yarn** > **Distcp**.

#. Modify **dfs.namenode.rpc-address**, set **haclusterX.remotenn1** to the service IP address and RPC port of one NameNode instance of the peer cluster, and set **haclusterX.remotenn2** to the service IP address and RPC port number of the other NameNode instance of the peer cluster.

   **haclusterX.remotenn1** and **haclusterX.remotenn2** do not distinguish active and standby NameNodes. The default NameNode RPC port is 8020 and cannot be modified on Manager.

   Examples of modified parameter values: **10.1.1.1:8020** and **10.1.1.2:8020**.

   .. note::

      -  If data of the current cluster needs to be backed up to the HDFS of multiple clusters, you can configure the corresponding NameNode RPC addresses to haclusterX1, haclusterX2, haclusterX3, and haclusterX4.

#. Click **Save**. In the confirmation dialog box, click **OK**.

#. .. _admin_guide_000200__en-us_topic_0046736761_li8920825:

   Restart the Yarn service.

#. Log in to FusionInsight Manager of the other cluster and repeat :ref:`2 <admin_guide_000200__en-us_topic_0046736761_li45131484>` to :ref:`6 <admin_guide_000200__en-us_topic_0046736761_li8920825>`.
