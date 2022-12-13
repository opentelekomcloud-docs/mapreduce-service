:original_name: mrs_01_1082.html

.. _mrs_01_1082:

Flume Client Cgroup Usage Guide
===============================

Scenario
--------

This section describes how to join and log out of a cgroup, query the cgroup status, and change the cgroup CPU threshold.

This section applies to MRS 3.\ *x* or later.

Procedure
---------

-  **Join Cgroup**

   Assume that the Flume client installation path is **/opt/FlumeClient**, and the cgroup CPU threshold is 50%. Run the following command to join a cgroup:

   **cd /opt/FlumeClient/fusioninsight-flume-1.9.0/bin**

   **./flume-manage.sh cgroup join 50**

   .. note::

      -  This command can be used to join a cgroup and change the cgroup CPU threshold.
      -  The value of the CPU threshold of a cgroup ranges from 1 to 100 x *N*. *N* indicates the number of CPU cores.

-  **Check Cgroup status**

   Assume that the Flume client installation path is **/opt/FlumeClient**. Run the following commands to query the cgroup status:

   **cd /opt/FlumeClient/fusioninsight-flume-1.9.0/bin**

   **./flume-manage.sh cgroup status**

-  **Exit Cgroup**

   Assume that the Flume client installation path is **/opt/FlumeClient**. Run the following commands to exit cgroup:

   **cd /opt/FlumeClient/fusioninsight-flume-1.9.0/bin**

   **./flume-manage.sh cgroup exit**

   .. note::

      -  After the client is installed, the default cgroup is automatically created. If the **-s** parameter is not configured during client installation, the default value **-1** is used. The default value indicates that the agent process is not restricted by the CPU usage.
      -  Joining or exiting a cgroup does not affect the agent process. Even if the agent process is not started, the joining or exiting operation can be performed successfully, and the operation will take effect after the next startup of the agent process.
      -  After the client is uninstalled, the cgroups created during the client installation are automatically deleted.
