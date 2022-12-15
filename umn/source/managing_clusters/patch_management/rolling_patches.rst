:original_name: mrs_01_0431.html

.. _mrs_01_0431:

Rolling Patches
===============

The rolling patch function indicates that patches are installed or uninstalled for one or more services in a cluster by performing a rolling service restart (restarting services or instances in batches), without interrupting the services or within a minimized service interruption interval. Services in a cluster are divided into the following three types based on whether they support rolling patch:

-  Services supporting rolling patch installation or uninstallation: All businesses or part of them (varying depending on different services) of the services are not interrupted during patch installation or uninstallation.
-  Services not supporting rolling patch installation or uninstallation: Businesses of the services are interrupted during patch installation or uninstallation.
-  Services with some roles supporting rolling patch installation or uninstallation: Some businesses of the services are not interrupted during patch installation or uninstallation.

.. note::

   In **MRS 3.x**, you cannot perform operations in this section on the management console.

:ref:`Table 1 <mrs_01_0431__table054720341161>` provides services and instances that support or do not support rolling restart in the MRS cluster.

.. _mrs_01_0431__table054720341161:

.. table:: **Table 1** Services and instances that support or do not support rolling restart

   ========= ================ ==================================
   Service   Instance         Whether to Support Rolling Restart
   ========= ================ ==================================
   HDFS      NameNode         Yes
   \         Zkfc
   \         JournalNode
   \         HttpFS
   \         DataNode
   Yarn      ResourceManager  Yes
   \         NodeManager
   Hive      MetaStore        Yes
   \         WebHCat
   \         HiveServer
   MapReduce JobHistoryServer Yes
   HBase     HMaster          Yes
   \         RegionServer
   \         ThriftServer
   \         RESTServer
   Spark     JobHistory       Yes
   \         JDBCServer
   \         SparkResource    No
   Hue       Hue              No
   Tez       TezUI            No
   Loader    Sqoop            No
   Zookeeper Quorumpeer       Yes
   Kafka     Broker           Yes
   \         MirrorMaker      No
   Flume     Flume            Yes
   \         MonitorServer
   Storm     Nimbus           Yes
   \         UI
   \         Supervisor
   \         LogViewer
   ========= ================ ==================================

Installing a Patch
------------------

#. Log in to the MRS console.
#. Choose **Clusters** > **Active Clusters** and click the name of the cluster to be queried to enter the page displaying the cluster's basic information.
#. On the **Patches** page, click **Install** in the **Operation** column.
#. On the **Warning** page, enable or disable **Rolling Patch**.

   .. note::

      -  Enabling the rolling patch installation function: Services are not stopped before patch installation, and rolling service restart is performed after the patch installation. This minimizes the impact on cluster services but takes more time than common patch installation.
      -  Disabling the rolling patch uninstallation function: All services are stopped before patch uninstallation, and all services are restarted after the patch uninstallation. This temporarily interrupts the cluster and the services but takes less time than rolling patch uninstallation.
      -  The rolling patch installation function is not available in clusters with less than two Master nodes and three Core nodes.

#. Click **Yes** to install the target patch.
#. View the patch installation progress.

   a. Access MRS Manager. For details, see :ref:`Accessing MRS Manager MRS 2.1.0 or Earlier) <mrs_01_0102>`.
   b. Choose **System** > **Manage Patch**. On the **Manage Patch** page, you can view the patch installation progress.

   .. note::

      For the isolated host nodes in the cluster, follow instructions in :ref:`Restoring Patches for the Isolated Hosts <mrs_01_0412>` to restore the patch.

Uninstalling a Patch
--------------------

#. Log in to the MRS console.
#. Choose **Clusters** > **Active Clusters** and click the name of the cluster to be queried to enter the page displaying the cluster's basic information.
#. On the **Patches** page, click **Uninstall** in the **Operation** column.
#. On the **Warning** page, enable or disable **Rolling Patch**.

   .. note::

      -  Enabling the rolling patch uninstallation function: Services are not stopped before patch uninstallation, and rolling service restart is performed after the patch uninstallation. This minimizes the impact on cluster services but takes more time than common patch uninstallation.
      -  Disabling the rolling patch uninstallation function: All services are stopped before patch uninstallation, and all services are restarted after the patch uninstallation. This temporarily interrupts the cluster and the services but takes less time than rolling patch uninstallation.
      -  Only patches that are installed in rolling mode can be uninstalled in the same mode.

#. Click **Yes** to uninstall the target patch.
#. View the patch uninstallation progress.

   a. Access MRS Manager. For details, see :ref:`Accessing MRS Manager MRS 2.1.0 or Earlier) <mrs_01_0102>`.
   b. Choose **System** > **Manage Patch**. On the **Manage Patch** page, you can view the patch uninstallation progress.

   .. note::

      For the isolated host nodes in the cluster, follow instructions in :ref:`Restoring Patches for the Isolated Hosts <mrs_01_0412>` to restore the patch.
