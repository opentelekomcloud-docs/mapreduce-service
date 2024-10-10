:original_name: mrs_01_24279.html

.. _mrs_01_24279:

Interconnecting Flume with OBS
==============================

This section applies to MRS 3.x or later.

Before performing the following operations, ensure that you have configured a storage-compute decoupled cluster by referring to :ref:`Configuring a Storage-Compute Decoupled Cluster (Agency) <mrs_01_0768>` or :ref:`Configuring a Storage-Compute Decoupled Cluster (AK/SK) <mrs_01_0468>`.

#. Configure an agency.

   a. Log in to the MRS console. In the navigation pane on the left, choose **Clusters** > **Active Clusters**.
   b. Click the name of a cluster to go to the cluster details page.
   c. On the **Dashboard** page, click **Synchronize** on the right of **IAM User Sync** to synchronize IAM users.
   d. Click **Manage Agency** on the right of **Agency**, select the target agency, and click **OK**.

#. .. _mrs_01_24279__li3279721151214:

   Create an OBS file system for storing data.

   a. Log in to the OBS console.
   b. In the navigation pane on the left, choose **Parallel File Systems**. On the displayed page, click **Create Parallel File System**.
   c. Enter the file system name, for example, **esdk-c-test-pfs1**, and set other parameters as required. Click **Create Now**.
   d. In the parallel file system list on the OBS console, click the created file system name to go to its details page.
   e. In the navigation pane on the left, choose **Files** and click **Create Folder** to create the **testFlumeOutput** folder.

#. Prepare the **properties.properties** file and upload it to the **/opt/flumeInput** directory.

   a. .. _mrs_01_24279__li192551317183716:

      Prepare the **properties.properties** file on the local host. Its content is as follows:

      .. code-block::

         # source
         server.sources = r1
         # channels
         server.channels = c1
         # sink
         server.sinks = obs_sink
         # ----- define net source -----
         server.sources.r1.type = seq
         server.sources.r1.spooldir = /opt/flumeInput
         # ---- define OBS sink ----
         server.sinks.obs_sink.type = hdfs
         server.sinks.obs_sink.hdfs.path = obs://esdk-c-test-pfs1/testFlumeOutput
         server.sinks.obs_sink.hdfs.filePrefix = %[localhost]
         server.sinks.obs_sink.hdfs.useLocalTimeStamp = true
         # set file size to trigger roll
         server.sinks.obs_sink.hdfs.rollSize = 0
         server.sinks.obs_sink.hdfs.rollCount = 0
         server.sinks.obs_sink.hdfs.rollInterval = 5
         #server.sinks.obs_sink.hdfs.threadsPoolSize = 30
         server.sinks.obs_sink.hdfs.fileType = DataStream
         server.sinks.obs_sink.hdfs.writeFormat = Text
         server.sinks.obs_sink.hdfs.fileCloseByEndEvent = false

         # define channel
         server.channels.c1.type = memory
         server.channels.c1.capacity = 1000
         # transaction size
         server.channels.c1.transactionCapacity = 1000
         server.channels.c1.byteCapacity = 800000
         server.channels.c1.byteCapacityBufferPercentage = 20
         server.channels.c1.keep-alive = 60
         server.sources.r1.channels = c1
         server.sinks.obs_sink.channel = c1

      .. note::

         The value of **server.sinks.obs_sink.hdfs.path** is the OBS file system created in :ref:`2 <mrs_01_24279__li3279721151214>`.

   b. Log in to the node where the Flume client is installed as user **root**.

   c. Create the **/opt/flumeInput** directory and create a customized **.txt** file in this directory.

   d. Log in to MRS Manager.

   e. Choose **Cluster** > *Name of the target cluster* > **Services** > **Flume**. On the displayed page, click **Configurations** and then **Upload File** in the **Value** column corresponding to the **flume.config.file** parameter, upload the **properties.properties** file prepared in :ref:`3.a <mrs_01_24279__li192551317183716>`, and click **Save**.

#. View the result in the OBS system.

   a. Log in to the OBS console.
   b. Click **Parallel File Systems** and go to the folder created in :ref:`2 <mrs_01_24279__li3279721151214>` to view the result.
