:original_name: mrs_08_00083.html

.. _mrs_08_00083:

Relationship Among Spark, HDFS, and Yarn
========================================

Relationship Between Spark and HDFS
-----------------------------------

Data computed by Spark comes from multiple data sources, such as local files and HDFS. Most data computed by Spark comes from the HDFS. The HDFS can read data in large scale for parallel computing. After being computed, data can be stored in the HDFS.

Spark involves Driver and Executor. Driver schedules tasks and Executor runs tasks.

:ref:`Figure 1 <mrs_08_00083__fa4b797ba877b48a9887616253937f2ff>` shows the process of reading a file.

.. _mrs_08_00083__fa4b797ba877b48a9887616253937f2ff:

.. figure:: /_static/images/en-us_image_0000001296270798.png
   :alt: **Figure 1** File reading process

   **Figure 1** File reading process

The file reading process is as follows:

#. Driver interconnects with the HDFS to obtain the information of File A.
#. The HDFS returns the detailed block information about this file.
#. Driver sets a parallel degree based on the block data amount, and creates multiple tasks to read the blocks of this file.
#. Executor runs the tasks and reads the detailed blocks as part of the Resilient Distributed Dataset (RDD).

:ref:`Figure 2 <mrs_08_00083__fd0c7d400d05a40c1b12b1a5f9921b09a>` shows the process of writing data to a file.

.. _mrs_08_00083__fd0c7d400d05a40c1b12b1a5f9921b09a:

.. figure:: /_static/images/en-us_image_0000001349390629.png
   :alt: **Figure 2** File writing process

   **Figure 2** File writing process

The file writing process is as follows:

#. .. _mrs_08_00083__la0d49754431847d9ba121414f074589b:

   Driver creates a directory where the file is to be written.

#. Based on the RDD distribution status, the number of tasks related to data writing is computed, and these tasks are sent to Executor.

#. Executor runs these tasks, and writes the RDD data to the directory created in :ref:`1 <mrs_08_00083__la0d49754431847d9ba121414f074589b>`.

Relationship Between Spark and Yarn
-----------------------------------

The Spark computing and scheduling can be implemented using Yarn mode. Spark enjoys the computing resources provided by Yarn clusters and runs tasks in a distributed way. Spark on Yarn has two modes: Yarn-cluster and Yarn-client.

-  Yarn-cluster mode

   :ref:`Figure 3 <mrs_08_00083__ffe758bc524de483aa66394ea1cb6cb62>` shows the running framework of Spark on Yarn-cluster.

   .. _mrs_08_00083__ffe758bc524de483aa66394ea1cb6cb62:

   .. figure:: /_static/images/en-us_image_0000001296590618.png
      :alt: **Figure 3** Spark on Yarn-cluster operation framework

      **Figure 3** Spark on Yarn-cluster operation framework

   Spark on Yarn-cluster implementation process:

   #. The client generates the application information, and then sends the information to ResourceManager.

   #. ResourceManager allocates the first container (ApplicationMaster) to SparkApplication and starts driver on the container.

   #. ApplicationMaster applies for resources from ResourceManager to run the container.

      ResourceManager allocates the container to ApplicationMaster, which communicates with NodeManager, and starts the executor in the obtained container. After the executor is started, it registers with the driver and applies for tasks.

   #. The driver allocates tasks to the executor.

   #. The executor runs tasks and reports the operating status to the driver.

-  Yarn-client mode

   :ref:`Figure 4 <mrs_08_00083__f6c6ae283e91d48c98c7d7a2a59379989>` shows the running framework of Spark on Yarn-cluster.

   .. _mrs_08_00083__f6c6ae283e91d48c98c7d7a2a59379989:

   .. figure:: /_static/images/en-us_image_0000001296430766.png
      :alt: **Figure 4** Spark on Yarn-client operation framework

      **Figure 4** Spark on Yarn-client operation framework

   Spark on Yarn-client implementation process:

   .. note::

      In Yarn-client mode, Driver is deployed on the client and started on the client. In Yarn-client mode, the client of the earlier version is incompatible. You are advised to use the Yarn-cluster mode.

   #. The client sends the Spark application request to ResourceManager, then ResourceManager returns the results. The results include information such as Application ID and the maximum and minimum available resources. The client packages all information required to start ApplicationMaster, and sends the information to ResourceManager.

   #. After receiving the request, ResourceManager finds a proper node for ApplicationMaster and starts it on this node. ApplicationMaster is a role in Yarn, and the process name in Spark is ExecutorLauncher.

   #. Based on the resource requirements of each task, ApplicationMaster can apply for a series of Containers to run tasks from ResourceManager.

   #. After receiving the newly allocated container list (from ResourceManager), ApplicationMaster sends information to the related NodeManagers to start the containers.

      ResourceManager allocates the containers to ApplicationMaster, which communicates with the related NodeManagers, and starts the executors in the obtained containers. After the executors are started, it registers with drivers and applies for tasks.

      .. note::

         Running containers are not suspended and resources are not released.

   #. The drivers allocate tasks to the executors. The executor executes tasks and reports the operating status to the driver.
