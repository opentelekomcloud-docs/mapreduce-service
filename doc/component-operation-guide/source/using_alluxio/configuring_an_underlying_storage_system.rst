:original_name: mrs_01_0759.html

.. _mrs_01_0759:

Configuring an Underlying Storage System
========================================

If you want to use a unified client API and a global namespace to access persistent storage systems including HDFS and OBS to separate computing from storage, you can configure the underlying storage system of Alluxio on MRS Manager. After a cluster is created, the default underlying storage address is **hdfs://hacluster/**, that is, the HDFS root directory is mapped to Alluxio.

Prerequisites
-------------

-  Alluxio has been installed in a cluster.
-  The password of user **admin** has been obtained. The password of user **admin** is specified by the user during MRS cluster creation.

Configuring HDFS as the Underlying File System of Alluxio
---------------------------------------------------------

.. note::

   Security clusters with Kerberos authentication enabled do not support this function.

#. Go to the **All Configurations** page of Alluxio. See :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.

#. In the left pane, choose **Alluxio** > **Under Stores**, and modify the value of **alluxio.master.mount.table.root.ufs** to **hdfs://hacluster**\ */XXX/*.

   For example, if you want to use *HDFS root directory*\ **/alluxio/** as the root directory of Alluxio, modify the value of **alluxio.master.mount.table.root.ufs** to **hdfs://hacluster/alluxio/**.

#. Click **Save Configuration**. In the displayed dialog box, select **Restart the affected services or instances**.

#. Click **OK** to restart Alluxio.
