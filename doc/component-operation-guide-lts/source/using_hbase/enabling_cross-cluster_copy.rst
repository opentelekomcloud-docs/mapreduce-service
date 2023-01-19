:original_name: mrs_01_0502.html

.. _mrs_01_0502:

Enabling Cross-Cluster Copy
===========================

Scenario
--------

DistCp is used to copy the data stored on HDFS from a cluster to another cluster. DistCp depends on the cross-cluster copy function, which is disabled by default. This function needs to be enabled in both clusters.

This section describes how to enable cross-cluster copy.

Impact on the System
--------------------

Yarn needs to be restarted to enable the cross-cluster copy function and cannot be accessed during the restart.

Prerequisites
-------------

The **hadoop.rpc.protection** parameter of the two HDFS clusters must be set to the same data transmission mode, which can be **privacy** (encryption enabled) or **authentication** (encryption disabled).

.. note::

   Go to the **All Configurations** page by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>` and search for **hadoop.rpc.protection**.

Procedure
---------

#. Go to the **All Configurations** page of the Yarn service. For details, see :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.

   .. note::

      If the **Components** tab is not displayed on the cluster details page, complete IAM user synchronization first. (In the **Dashboard** area of the cluster details page, click **Click to synchronize** on the right of **IAM User Sync** to synchronize IAM users.)

#. In the navigation pane, choose **Yarn** > **Distcp**.

#. Set **haclusterX.remotenn1** of **dfs.namenode.rpc-address** to the service IP address and RPC port number of one NameNode instance of the peer cluster, and set **haclusterX.remotenn2** to the service IP address and RPC port number of the other NameNode instance of the peer cluster. Enter a value in the *IP address:port* format.

   .. note::

      For MRS 1.9.2 or later, log in to the MRS console, click the cluster name, and choose **Components** > **HDFS** > **Instances** to obtain the service IP address of the NameNode instance.

      You can also log in to FusionInsight Manager, and choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS** > **Instance** to obtain the service IP address of the NameNode instance.

   **dfs.namenode.rpc-address.haclusterX.remotenn1** and **dfs.namenode.rpc-address.haclusterX.remotenn2** do not distinguish active and standby NameNode instances. The default NameNode RPC port is 9820 and cannot be modified on MRS Manager.

   For example, **10.1.1.1:9820** and **10.1.1.2:9820**.

#. Save the configuration. On the **Dashboard** tab page, and choose **More** > **Restart Service** to restart the Yarn service.

   **Operation succeeded** is displayed. Click **Finish**. The Yarn service is started successfully.

#. Log in to the other cluster and repeat the preceding operations.
