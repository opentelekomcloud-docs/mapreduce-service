:original_name: mrs_08_007105.html

.. _mrs_08_007105:

Relationship Between Spark2x and Other Components
=================================================

Relationship Between Spark and HDFS
-----------------------------------

Data computed by Spark comes from multiple data sources, such as local files and HDFS. Most data comes from HDFS which can read data in large scale for parallel computing After being computed, data can be stored in HDFS.

Spark involves Driver and Executor. Driver schedules tasks and Executor runs tasks.

:ref:`Figure 1 <mrs_08_007105__f685f281350dc4fd3b98d846f3e41143d>` describes the file reading process.

.. _mrs_08_007105__f685f281350dc4fd3b98d846f3e41143d:

.. figure:: /_static/images/en-us_image_0000001349110517.png
   :alt: **Figure 1** File reading process

   **Figure 1** File reading process

The file reading process is as follows:

#. Driver interconnects with HDFS to obtain the information of File A.
#. The HDFS returns the detailed block information about this file.
#. Driver sets a parallel degree based on the block data amount, and creates multiple tasks to read the blocks of this file.
#. Executor runs the tasks and reads the detailed blocks as part of the Resilient Distributed Dataset (RDD).

:ref:`Figure 2 <mrs_08_007105__f18154e3da87f42c5976570cd262f7ec1>` describes the file writing process.

.. _mrs_08_007105__f18154e3da87f42c5976570cd262f7ec1:

.. figure:: /_static/images/en-us_image_0000001349309973.png
   :alt: **Figure 2** File writing process

   **Figure 2** File writing process

The file writing process is as follows:

#. .. _mrs_08_007105__l4c0b15c64e104bfb9f02ae2489ed59ce:

   Driver creates a directory where the file is to be written.

#. Based on the RDD distribution status, the number of tasks related to data writing is computed, and these tasks are sent to Executor.

#. Executor runs these tasks, and writes the RDD data to the directory created in :ref:`1 <mrs_08_007105__l4c0b15c64e104bfb9f02ae2489ed59ce>`.

Relationship with Yarn
----------------------

The Spark computing and scheduling can be implemented using Yarn mode. Spark enjoys the computing resources provided by Yarn clusters and runs tasks in a distributed way. Spark on Yarn has two modes: Yarn-cluster and Yarn-client.

-  Yarn-cluster mode

   :ref:`Figure 3 <mrs_08_007105__f0c19aec9e28a4f2fbdd56db1a318f641>` describes the operation framework.

   .. _mrs_08_007105__f0c19aec9e28a4f2fbdd56db1a318f641:

   .. figure:: /_static/images/en-us_image_0000001296270854.png
      :alt: **Figure 3** Spark on Yarn-cluster operation framework

      **Figure 3** Spark on Yarn-cluster operation framework

   Spark on Yarn-cluster implementation process:

   #. The client generates the application information, and then sends the information to ResourceManager.

   #. ResourceManager allocates the first container (ApplicationMaster) to SparkApplication and starts the driver on the container.

   #. ApplicationMaster applies for resources from ResourceManager to run the container.

      ResourceManager allocates the containers to ApplicationMaster, which communicates with the related NodeManagers and starts the executor in the obtained container. After the executor is started, it registers with drivers and applies for tasks.

   #. Drivers allocate tasks to the executors.

   #. Executors run tasks and report the operating status to Drivers.

-  Yarn-client mode

   :ref:`Figure 4 <mrs_08_007105__f627f617b8382474ba78da7751a10219a>` describes the operation framework.

   .. _mrs_08_007105__f627f617b8382474ba78da7751a10219a:

   .. figure:: /_static/images/en-us_image_0000001349390685.png
      :alt: **Figure 4** Spark on Yarn-client operation framework

      **Figure 4** Spark on Yarn-client operation framework

   Spark on Yarn-client implementation process:

   .. note::

      In Yarn-client mode, the Driver is deployed and started on the client. In Yarn-client mode, the client of an earlier version is incompatible. The Yarn-cluster mode is recommended.

   #. The client sends the Spark application request to ResourceManager, and packages all information required to start ApplicationMaster and sends the information to ResourceManager. ResourceManager then returns the results to the client. The results include information such as ApplicationId, and the upper limit as well as lower limit of available resources. After receiving the request, ResourceManager finds a proper node for ApplicationMaster and starts it on this node. ApplicationMaster is a role in Yarn, and the process name in Spark is ExecutorLauncher.

   #. Based on the resource requirements of each task, ApplicationMaster can apply for a series of containers to run tasks from ResourceManager.

   #. After receiving the newly allocated container list (from ResourceManager), ApplicationMaster sends information to the related NodeManagers to start the containers.

      ResourceManager allocates the containers to ApplicationMaster, which communicates with the related NodeManagers and starts the executor in the obtained container. After the executor is started, it registers with drivers and applies for tasks.

      .. note::

         Running Containers will not be suspended to release resources.

   #. Drivers allocate tasks to the executors. Executors run tasks and report the operating status to Drivers.
