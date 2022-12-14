:original_name: mrs_01_1665.html

.. _mrs_01_1665:

Configuring NFS
===============

Scenario
--------

.. note::

   This section applies to MRS 3.\ *x* or later.

Before deploying a cluster, you can deploy a Network File System (NFS) server based on requirements to store NameNode metadata to enhance data reliability.

If the NFS server has been deployed and NFS services are configured, you can follow operations in this section to configure NFS on the cluster. These operations are optional.

Procedure
---------

#. Check the permission of the shared NFS directories on the NFS server to ensure that the server can access NameNode in the MRS cluster.

#. .. _mrs_01_1665__lff3e9b51a9354f89ab59a1c515495818:

   Log in to the active NameNode as user **root**.

#. Run the following commands to create a directory and assign it write permissions:

   **mkdir** **${BIGDATA_DATA_HOME}/namenode-nfs**

   **chown omm:wheel** **${BIGDATA_DATA_HOME}/namenode-nfs**

   **chmod 750** **${BIGDATA_DATA_HOME}/namenode-nfs**

#. .. _mrs_01_1665__lbb64192db9814446b3744fcbf6326d7b:

   Run the following command to mount the NFS to the active NameNode:

   **mount -t nfs -o rsize=8192,wsize=8192,soft,nolock,timeo=3,intr** *IP address of the NFS server*:*Shared directory* **${BIGDATA_DATA_HOME}/namenode-nfs**

   For example, if the IP address of the NFS server is **192.168.0.11** and the shared directory is **/opt/Hadoop/NameNode**, run the following command:

   **mount -t nfs -o rsize=8192,wsize=8192,soft,nolock,timeo=3,intr 192.168.0.11:/opt/Hadoop/NameNode** **${BIGDATA_DATA_HOME}/namenode-nfs**

#. Perform :ref:`2 <mrs_01_1665__lff3e9b51a9354f89ab59a1c515495818>` to :ref:`4 <mrs_01_1665__lbb64192db9814446b3744fcbf6326d7b>` on the standby NameNode.

   .. note::

      The names of the shared directories (for example, **/opt/Hadoop/NameNode**) created on the NFS server by the active and standby NameNodes must be different.

#. Log in to FusionInsight Manager, and choose **Cluster** > *Name of the desired cluster* > **Service** > **HDFS** > **Configuration** > **All Configurations**.

#. In the search box, search for **dfs.namenode.name.dir**, add **${BIGDATA_DATA_HOME}/namenode-nfs** to **Value**, and click **Save**. Separate paths with commas (,).

#. Click **OK**. On the **Dashboard** tab page, choose **More** > **Restart Service** to restart the service.
