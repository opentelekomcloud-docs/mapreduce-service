:original_name: mrs_08_00342.html

.. _mrs_08_00342:

Flink HA Solution
=================


Flink HA Solution
-----------------

A Flink cluster has only one JobManager. This has the risks of single point of failures (SPOFs). There are three modes of Flink: Flink On Yarn, Flink Standalone, and Flink Local. Flink On Yarn and Flink Standalone modes are based on clusters and Flink Local mode is based on a single node. Flink On Yarn and Flink Standalone provide an HA mechanism. With such a mechanism, you can recover the JobManager from failures and thereby eliminate SPOF risks. This section describes the HA mechanism of the Flink On Yarn.

Flink supports the HA mode and job exception recovery that highly depend on ZooKeeper. If you want to enable the two functions, configure ZooKeeper in the **flink-conf.yaml** file in advance as follows:

.. code-block::

   high-availability: zookeeper
   high-availability.zookeeper.quorum:  ZooKeeper IP address:2181
   high-availability.storageDir: hdfs:///flink/recovery

**Flink On Yarn**

Flink JobManager and Yarn ApplicationMaster are in the same process. Yarn ResourceManager monitors ApplicationMaster. If ApplicationMaster is abnormal, Yarn restarts it and restores all JobManager metadata from HDFS. During the recovery, existing tasks cannot run and new tasks cannot be submitted. ZooKeeper stores JobManager metadata, such as information about jobs, to be used by the new JobManager. A TaskManager failure is listened and processed by the DeathWatch mechanism of Akka on JobManager. When a TaskManager fails, a container is requested again from Yarn and a TaskManager is created.

For more information about the HA solution of Flink on Yarn, visit `https://hadoop.apache.org/docs/r3.1.1/hadoop-yarn/hadoop-yarn-site/ResourceManagerHA.html <http://hadoop.apache.org/docs/r3.1.1/hadoop-yarn/hadoop-yarn-site/ResourceManagerHA.html>`__.

For details about how to set **yarn-site.xml**, visit https://ci.apache.org/projects/flink/flink-docs-release-1.12/ops/jobmanager_high_availability.html.

**Standalone**

In the standalone mode, multiple JobManagers can be started and ZooKeeper elects one as the leader JobManager. In this mode, there is a leader JobManager and multiple standby JobManagers. If the leader JobManager fails, a standby JobManager takes over the leadership. :ref:`Figure 1 <mrs_08_00342__f5525c98e300e4d9b946da5d43305371c>` shows the process of a leader/standby JobManager switchover.

.. _mrs_08_00342__f5525c98e300e4d9b946da5d43305371c:

.. figure:: /_static/images/en-us_image_0000001296270790.png
   :alt: **Figure 1** Switchover process

   **Figure 1** Switchover process

**Restoring TaskManager**

A TaskManager failure is listened and processed by the DeathWatch mechanism of Akka on JobManager. If the TaskManager fails, the JobManager creates a TaskManager and migrates services to the created TaskManager.

**Restoring JobManager**

Flink JobManager and Yarn ApplicationMaster are in the same process. Yarn ResourceManager monitors ApplicationMaster. If ApplicationMaster is abnormal, Yarn restarts it and restores all JobManager metadata from HDFS. During the recovery, existing tasks cannot run and new tasks cannot be submitted.

**Restoring Jobs**

If you want to restore jobs, ensure that the startup policy is configured in Flink configuration files. Supported restart policies are **fixed-delay**, **failure-rate**, and **none**. Jobs can be restored only when the policy is configured to **fixed-delay** or **failure-rate**. If the restart policy is configured to **none** and checkpoint is configured for jobs, the restart policy is automatically configured to **fixed-delay** and the value of **restart-strategy.fixed-delay.attempts** (which specifies the number of retry times) is configured to **Integer.MAX_VALUE**.

For details about the three strategies, visit https://ci.apache.org/projects/flink/flink-docs-release-1.12/dev/task_failure_recovery.html. The following is an example of the restart policy configuration:

.. code-block::

   restart-strategy: fixed-delay
   restart-strategy.fixed-delay.attempts: 3
   restart-strategy.fixed-delay.delay: 10 s

Jobs will be restored in the following scenarios:

-  If a JobManager fails, all its jobs are stopped, and will be recovered after another JobManager is created and running.
-  If a TaskManager fails, all tasks on the TaskManager are stopped, and will be started until there are available resources.
-  When a task of a job fails, the job is restarted.

   .. note::

      For details about how to configure the restart policy of a job, visit https://ci.apache.org/projects/flink/flink-docs-release-1.12/ops/jobmanager_high_availability.html.
