:original_name: mrs_01_1288.html

.. _mrs_01_1288:

Interconnecting Flink with OBS
==============================

Before performing the following operations, ensure that you have configured a storage-compute decoupled cluster by referring to :ref:`Configuring a Storage-Compute Decoupled Cluster (Agency) <mrs_01_0768>` or :ref:`Configuring a Storage-Compute Decoupled Cluster (AK/SK) <mrs_01_0468>`.

#. Log in to the Flink client installation node as the client installation user.

#. Run the following command to initialize environment variables:

   **source ${client_home}/bigdata_env**

#. Configure the Flink client properly. For details, see :ref:`Installing a Client (Version 3.x or Later) <mrs_01_0090>`.

#. For a security cluster, run the following command to perform user authentication. If Kerberos authentication is not enabled for the current cluster, you do not need to run this command.

   **kinit** *Username*

#. Explicitly add the OBS file system to be accessed in the Flink command line.

   **./bin/flink run --xxx ./config/FlinkCheckpointJavaExample.jar --chkPath** **obs://**\ *Name of the OBS parallel file system*

.. note::

   Flink jobs are running on Yarn. Before configuring Flink to interconnect with the OBS file system, ensure that the interconnection between Yarn and the OBS file system is normal.
