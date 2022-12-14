:original_name: mrs_01_2018.html

.. _mrs_01_2018:

Why Do the Executors Fail to Register Shuffle Services During the Shuffle of a Large Amount of Data?
====================================================================================================

Question
--------

When more than 50 terabytes of data is shuffled, some executors fail to register shuffle services due to timeout. The shuffle tasks then fail. Why? The error log is as follows:

.. code-block::

   2016-10-19 01:33:34,030 | WARN | ContainersLauncher #14 | Exception from container-launch with container ID: container_e1452_1476801295027_2003_01_004512 and exit code: 1 | LinuxContainerExecutor.java:397
   ExitCodeException exitCode=1:
   at org.apache.hadoop.util.Shell.runCommand(Shell.java:561)
   at org.apache.hadoop.util.Shell.run(Shell.java:472)
   at org.apache.hadoop.util.Shell$ShellCommandExecutor.execute(Shell.java:738)
   at org.apache.hadoop.yarn.server.nodemanager.LinuxContainerExecutor.launchContainer(LinuxContainerExecutor.java:381)
   at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:312)
   at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:88)
   at java.util.concurrent.FutureTask.run(FutureTask.java:266)
   at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
   at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
   at java.lang.Thread.run(Thread.java:745)
   2016-10-19 01:33:34,031 | INFO | ContainersLauncher #14 | Exception from container-launch. | ContainerExecutor.java:300
   2016-10-19 01:33:34,031 | INFO | ContainersLauncher #14 | Container id: container_e1452_1476801295027_2003_01_004512 | ContainerExecutor.java:300
   2016-10-19 01:33:34,031 | INFO | ContainersLauncher #14 | Exit code: 1 | ContainerExecutor.java:300
   2016-10-19 01:33:34,031 | INFO | ContainersLauncher #14 | Stack trace: ExitCodeException exitCode=1: | ContainerExecutor.java:300

Answer
------

The imported data exceeds 50 TB, which exceeds the shuffle processing capability. The shuffle may fail to respond to the registration request of an executor in a timely manner due to the heavy load.

The timeout interval for an executor to register the shuffle service is 5 seconds. The maximum number of retries is 3. This parameter is not configurable.

You are advised to increase the number of task retry times and the number of allowed executor failure times.

Configure the following parameters in the **spark-defaults.conf** file on the client: If **spark.yarn.max.executor.failures** does not exist, manually add it.

.. table:: **Table 1** Parameter Description

   +----------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------+
   | Parameter                        | Description                                                                                           | Default Value                        |
   +==================================+=======================================================================================================+======================================+
   | spark.task.maxFailures           | Specifies task retry times.                                                                           | 4                                    |
   +----------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------+
   | spark.yarn.max.executor.failures | Specifies executor failure attempt times.                                                             | numExecutors \* 2, with minimum of 3 |
   |                                  |                                                                                                       |                                      |
   |                                  | Set **spark.dynamicAllocation.enabled** to **false**, to disable the dynamic allocation of executors. |                                      |
   +----------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------+
   |                                  | Specifies executor failure attempt times.                                                             | 3                                    |
   |                                  |                                                                                                       |                                      |
   |                                  | Set **spark.dynamicAllocation.enabled** to **true**, to enable the dynamic allocation of executors.   |                                      |
   +----------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------+
