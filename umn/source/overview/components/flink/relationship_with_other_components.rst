:original_name: mrs_08_00343.html

.. _mrs_08_00343:

Relationship with Other Components
==================================

Relationship between Flink and Yarn
-----------------------------------

Flink supports Yarn-based cluster management mode. In this mode, Flink serves as an application of Yarn and runs on Yarn.

:ref:`Figure 1 <mrs_08_00343__f8d08e179442e449abad5d92b707fe130>` shows how Flink interacts with Yarn.

.. _mrs_08_00343__f8d08e179442e449abad5d92b707fe130:

.. figure:: /_static/images/en-us_image_0000001349390773.png
   :alt: **Figure 1** Flink interaction with Yarn

   **Figure 1** Flink interaction with Yarn

#. The Flink YARN Client first checks whether there are sufficient resources for starting the Yarn cluster. If yes, the Flink Yarn client uploads JAR packages and configuration files to HDFS.
#. Flink Yarn client communicates with Yarn ResourceManager to request a container for starting ApplicationMaster. After all Yarn NodeManagers finish downloading the JAR package and configuration files, the ApplicationMaster is started.
#. During the startup, the ApplicationMaster interacts with the Yarn ResourceManager to request the container for starting a TaskManager. After the container is ready, the TaskManager process is started.
#. In the Flink Yarn cluster, the ApplicationMaster and Flink JobManager are running in the same container. The ApplicationMaster informs each TaskManager of the RPC address of the JobManager. After TaskManagers are started successfully, they register with the JobManager.
#. After all TaskManagers have registered with the JobManager successfully, Flink starts up in the Yarn cluster. Then, the Flink Yarn client can submit Flink jobs to the JobManager, and Flink can perform mapping, scheduling, and computing for the jobs.
