:original_name: mrs_01_0868.html

.. _mrs_01_0868:

Configuring Users That Run Tasks
================================

Scenario
--------

Currently, YARN allows the user that starts the NodeManager to run the task submitted by all other users, or the users to run the task submitted by themselves.

Configuration Description
-------------------------

On Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Yarn** > **Configurations**. Click **All Configurations** Enter a parameter name in the search box.

.. table:: **Table 1** Parameter description

   +------------------------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------+
   | Parameter                                      | Description                               | Default Value                                                                                              |
   +================================================+===========================================+============================================================================================================+
   | yarn.nodemanager.linux-container-executor.user | Indicates the user who runs a task.       | The value is left blank by default.                                                                        |
   |                                                |                                           |                                                                                                            |
   |                                                |                                           | .. note::                                                                                                  |
   |                                                |                                           |                                                                                                            |
   |                                                |                                           |    The value is left blank by default. The user who submits a task is the actual person who runs the task. |
   +------------------------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------+
   | yarn.nodemanager.container-executor.class      | Indicates the executor who starts a task. | org.apache.hadoop.yarn.server.nodemanager.EnhancedLinuxContainerExecutor                                   |
   +------------------------------------------------+-------------------------------------------+------------------------------------------------------------------------------------------------------------+

.. note::

   -  Set **yarn.nodemanager.linux-container-executor.user** to configure the user who runs the container. This parameter is left blank by default. The user who submits the task is the person who runs the container. This parameter is valid only when **yarn.nodemanager.container-executor.class** is set to **org.apache.hadoop.yarn.server.nodemanager.EnhancedLinuxContainerExecutor**.
   -  In non-security mode, if **yarn.nodemanager.linux-container-executor.user** is set to **omm**, **yarn.nodemanager.linux-container-executor.nonsecure-mode.local-user** must also be set to **omm**.
   -  For security reasons, it is advised to retain the default values of **yarn.nodemanager.linux-container-executor.user** and **yarn.nodemanager.container-executor.class**.
